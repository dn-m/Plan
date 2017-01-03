# Rhythm

## Basic types

Whether or not a potential event is "tied"-over from the previous context, or whether it is a new instance of `T`.

```Swift
enum ContinuationOrInstance <T> {
    case continuation
    case instance(T)
}
```

Whether or not an `instance` is a "rest" or an actual "sounding" event.

```Swift
enum AbsenceOrEvent <T> {
    case absence
    case event(T)
}
```

A `MetricalContext` nests the `AbsenceOrEvent` within the `ContinuationOrInstance`.

In other words, it can be a `.continuation` | (`.absence` | `.event`). This models a metrical context by making it logically impossible to have a "rest" that is "tied"-into.

```Swift
typealias MetricalContext <T> = ContinuationOrInstance<AbsenceOrEvent<T>>
```

A `MetricalValue <T>` wraps up a value of type `T` with a `MetricalDuration`.

```Swift
struct MetricalValue <T> {
    let context: T
    let metricalDuration: MetricalDuration
}
```

A `MetricalLeaf <T>` specializes a `MetricalValue` by providing `MetricalContext` as its payload. That is, a `MetricalContext` (i.e., `.continuation` | (`.absence` | `.event`)) is wrapped up with a `MetricalDuration`.

```Swift
typealias MetricalLeaf <T> = MetricalValue<MetricalContext<T>>
```

A `RhythmTree <T>` is a hierarchical organization of these `MetricalLeaf` values.

```Swift
typealias RhythmTree <T> = Tree<MetricalLeaf<T>>
```
