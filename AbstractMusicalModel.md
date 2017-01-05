# Abstract Musical Model

A model of music, ignorant of graphical representations.

## Performance Context

### Performer

Model of a human or computer agent.

```Swift
typealias PerformerIdentifier = String
```

### Instrument

Model of an object used by a `Performer` used to _perform_ something.

```Swift
typealias InstrumentIdentifier = String
```

### Voice

Model of varyingly durational utterances of a single `Instrument`. For example, fugal keyboard material.

```Swift
typealias VoiceIdentifier = Int
```

## Musical Information

### Event

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

### Attributes

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
typealias Attribution <Attribute> = Dictionary<Event, Attribute>
```

Then, we can store these in a `Dictionary` keyed by an `AttributeIdentfier`, as:

```Swift
typealias AttributeIdentifier = String
var attributions: [AttributeIdentifier: Attribution<Any>] = [:]
```

#### Types of Attributions

As the number of possible attributes grows, so too can the number of generated mappings:

##### Musical information

```Swift
var information: [AttributeIdentifier: Attribution<Any>] = [:]
information["pitch"] = Attribution<[Pitch]>(...)
information["dynamic"] = Attribution<Dynamic>(...)
information["articulation"] = Attribution<[Articulation]>(...)
information["oscMessage"] = Attribution<[OSCMessage]>(...)
```

##### Performance context

```Swift
var performanceContext: [AttributeIdentifier: Attribution<Any>] = [:]
performanceContext["performer"] = Attribution<[PerformerIdentifier]>(...)
performanceContext["instrument"] = Attribution<[InstrumentIdentifier]>(...)
performanceContext["voice"] = Attribution<[VoiceIdentifier]>(...)
```

##### Temporal context

```Swift
var temporalContext: [AttributeIdentifier: Attribution<Any>] = [:]
temporalContext["duration"] = Attribution<[Duration]>(...)
temporalContext["offsetDuration"] = Attribution<[OffsetDuration]>(...)
```

#### Putting it together

We can enter the following: 

- "Jill" is playing `Tuba`. 
- She plays a `middle-c` with a `staccato` articulation at a `pp` dynamic.

as:

```Swift
let event = Event()

performanceContext["performer"]![event] = "Jill"
performanceContext["instrument"]![event] = "Tuba"
performanceContext["voice"]![event] = 0

information["articulation"]![event] = .staccato
information["pitch"]![event] = [Pitch(noteNumber: 60)]
information["dynamic"]![event] = Dynamic([.p, .p])
```

#### Discussion

- `Spanner` types (slur from `Event a` -> `Event b`)
- Metrical organization (rhythmical information)
- `Duration` vs `MetricalDuration`
- Consider collapsing common types (`PerformanceContext`, `TemporalContext`) into pre-fab types

### Database extraction

To reconstruct a given `Event`, we can iterate through an array of `Event` values, and then query each `Attribution` type for the existence of each `Event`.

```Swift
for event in events {
    let attributes: [Any] = information.flatMap { _, attribution in attribution[event] }
    // display attributes
}
```

A primary concern of the **dn-m** renderer is to display filtered versions of a full-score. We can very simply inject this filtration step inside this loop:

```Swift
let informationToShow: [AttributeIdentifier] = ["pitch", "articulation"]
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
let informationToShow = ["pitch", "articulation"]
let performanceContexts = [...]
for event in events {
    let attributes = information
        .lazy
        .flatMap { _, attribution in attribution[event] } // filter out non-existent attributions
        .filter { identifier, _ in informationToShow.contains(identifier) }
        .filter { _, durationSpan in durationSpan.contains(TemporalContext(event))
        .filter { _, performanceContexts in performanceContexts.contains(PerformanceContext(event)) }
    // display only desired attributes
}
```

#### Discussion:

- Is there _any_ way to preserve `Type` of attributes, or must each be deconstructed upon receipt?
- At some point, a diffing algorithm may be helpful in the updating of the graphics.
