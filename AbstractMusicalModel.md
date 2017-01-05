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

#### Structural information

```Swift
attributions["performers"] = Attribution<[PerformerIdentifier]>(...)
attributions["instruments"] = Attribution<[InstrumentIdentifier]>(...)
attributions["voices"] = Attribution<[VoiceIdentifier]>(...)
```

#### Musical information

```Swift
attributions["pitches"] = Attribution<[Pitch]>(...)
attributions["dynamics"] = Attribution<Dynamic>(...)
attributions["articulations"] = Attribution<[Articulation]>(...)
attributions["oscMessages"] = Attribution<[OSCMessage]>(...)
```

#### Temporal information

```Swift
attributions["duration"] = Attribution<[Duration]>(...)
attributions["offsetDuration"] = Attribution<[OffsetDuration]>(...)
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
    let attributes: [Any] = attributions.flatMap { _, attribution in attribution[event] }
    // display attributes
}
```

A primary concern of the **dn-m** renderer is to display filtered versions of a full-score. We can very simply inject this filtration step inside this loop:

```Swift
let attributesToShow: [AttributeIdentifier] = ["pitches", "articulations"]
for event in events {
    let attributes = attributions
        .lazy
        .filter { identifier, _ in attributesToShow.contains(identifier) }
        .flatMap { _, attribution in attribution[event] }
    // display only desired attributes
}
```

Further, we can perform more complex filters:

```Swift
let timeSpanRange
```


#### Discussion:

- Is there _any_ way to preserve `Type` of attributes, or must each be deconstructed upon receipt?
