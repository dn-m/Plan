# Abstract Musical Model

A model of music, ignorant of graphical representations.

## Performer

Model of a human or computer agent.

```Swift
typealias PerformerIdentifier = String
```

## Instrument

Model of an object used by a `Performer` used to _perform_ something.

```Swift
typealias InstrumentIdentifier = String
```

## Voice

Model of varyingly durational utterances of a single `Instrument`. For example, fugal keyboard material.

```Swift
typealias VoiceIdentifier = Int
```

## Event

A atomic action uttered by a single `Voice`.

```Swift
final class Event { ... }

// Ensure that an `Event` can be used as a `Key` value in a `Dictionary`.
extension Event: Hashable {
    var hashValue: Int {
        return ObjectIdentifier(self).hashValue
    }
}
```

## Attributes

An atomic `Event` may be associated with any number of `Attribute` values. 

```Swift
struct Pitch { ... }
struct Dynamic { ... }
struct DynamicSpanner { ... }
struct Articulation { ... }
struct OSCMessage { ... }
...
```

## Database

In order to relate `Attribute` values to `Event` objects, we generate a database, comprised of many `Dictionary` values.

### Database generation

Each of these relationships is stored in a `Dictionary` with (`Event`, `Attribute`) as a `(key, value)` pair. 

First, we can partially specialize, and relate these `Dictionary` types as:

```Swift
typealias Attribution<Attribute> = Dictionary<Event, Attribute>
```

Then, we can store these in a `Dictionary` keyed by an `AttributeIdentfier`, as:

```Swift
typealias AttributeIdentifier = String
var attributions: [AttributeIdentifier: Attribution<Any>] = [:]
```

As the number of possible attributes grows, so too can the number of generated mappings:

#### Musical information

```Swift
var information: [AttributeIdentifier: Attribution<Any>] = [:]
information["pitches"] = Attribution<[Pitch]>(...)
information["dynamics"] = Attribution<Dynamic>(...)
information["articulations"] = Attribution<[Articulation]>(...)
information["oscMessages"] = Attribution<[OSCMessage]>(...)
```

#### Performance context

```Swift
var performanceContexts: [AttributeIdentifier: Attribution<Any>] = [:]
performanceContexts["performers"] = Attribution<[PerformerIdentifier]>(...)
performanceContexts["instruments"] = Attribution<[InstrumentIdentifier]>(...)
performanceContexts["voices"] = Attribution<[VoiceIdentifier]>(...)
```


#### Temporal context

```Swift
var temporalContexts: [AttributeIdentifier: Attribution<Any>] = [:]
temporalContexts["duration"] = Attribution<[Duration]>(...)
temporalContexts["offsetDuration"] = Attribution<[OffsetDuration]>(...)
```

Finally, we can store all of the `Event` objects in a single `Array` as:

```Swift
let events: [Event] = [...]
```

#### Discussion

- `Spanner` types (slur from `Event a` -> `Event b`)
- Metrical organization (rhythmical information)
- `Duration` vs `MetricalDuration`…

### Database extraction

To reconstruct a given `Event`, we can iterate through the `events` array, and then query each `Attribution` type for the existence of each `Event`.

```Swift
for event in events {
    let attributes: [Any] = information.flatMap { _, attribution in attribution[event] }
    // display attributes
}
```

A primary concern of the **dn-m** renderer is to display filtered versions of a full-score. We can very simply inject this filtration step inside this loop:

```Swift
let informationToShow: [AttributeIdentifier] = ["pitches", "articulations"]
for event in events {
    let attributes = information
        .lazy
        .flatMap { _, attribution in attribution[event] }
        .filter { identifier, _ in informationToShow.contains(identifier) }
    // display only desired attributes
}
```

Further, we can perform more complex filters. For example, given a desired durational span, performance context, as well as the informational constraints, show only applicable information.

```Swift
let durationSpan: DurationSpan = ...
let informationToShow = ["pitches", "articulations"]
let performanceContexts = [...]
for event in events {
    let attributes = information
        .lazy
        .flatMap { _, attribution in attribution[event] } // filter out non-existent attributions
        .filter { identifier, _ in informationToShow.contains(identifier) }
        .filter { _, durationSpan in durationSpan.container(offsetDurations[event])
        .filter { _, performanceContexts in performanceContexts.contains(PerformanceContext(event)) }
    // display only desired attributes
}
```

#### Discussion:

- Is there _any_ way to preserve `Type` of attributes, or must each be deconstructed upon receipt?
- At some point, a diffing algorithm may be helpful in the updating of the graphics.
