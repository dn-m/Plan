```Swift
enum ContinuationOrInstance <T> {
    case continuation
    case instance(T)
}
```

```Swift
enum AbsenceOrEvent <T> {
    case absence
    case event(T)
}
```

```Swift
typealias MetricalContext <T> = ContinuationOrInstance<AbsenceOrEvent<T>>
```

```Swift
struct MetricalValue <T> {
    let context: T
    let metricalDuration: MetricalDuration
}
```

```Swift
typealias MetricalLeaf <T> = MetricalValue<MetricalContext<T>>
```

```Swift
typealias RhythmTree <T> = Tree<MetricalLeaf<T>>
```
