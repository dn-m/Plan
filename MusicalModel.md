# Musical Model

## Elements

The most basic musical attributes, from `Pitch` to `Articulation` to `DynamicMarking` to `OSCMessage` values.

Some abbreviated examples:

```Swift
struct Pitch {
    let value: Float
}

struct Articulation: OptionSetType {
    let accent: ...
    let staccato: ...
    let tenuto: ...
    ...
}

struct DynamicMarking {

    enum Element {
        case p,f,o,m,s,z
    }

    let elements: [Element]
}

struct OSCMessage {
    let addressPattern: String
    let arguments: [String]
}
```

These can be contextualized with the performer and instrument to which these elements apply:

```Swift
struct Event {
    let performerIdentifier: String
    let instrumentIdentifier: String
    let elements: [Any] // defined above
}
```



## Rhythm Model

The elements above will need to be contextualized within some temporal model. Commonly in western notated music, we use a hierarchical division of time often called _rhythm_.

### Rhythm in abstract

We can call the most basic element of _rhythm_ a `MetricalDuration`, with an abbreviated example:

```Swift
struct MetricalDuration {
    let beats: Int
    let subdivision: Int
}
```

To put this in this in a richer abstract representation, we need to extend certain rhythms to make compound rhythmical events. We can either provide a "tie" to the previous event, or provide a new _something_.

```Swift
enum TieOrNote <T> {
    case extending
    case note(T)
}
```

### Placing events in durational context

In the most abstract contexts, we don't need to know if there are rests or proper events. In the more practical example of notated music, we can either do something at given metrical duration offset, or not:

```Swift
enum RestOrEvent <T> {
    case rest
    case event(T)
}
```

> Both `RestOrEvent<T>` and `TieOrNote<T>` are essentially the `Optional` monad. 
>
> We can discuss the desirability of using more domain-specific definitions of these types or the (initial) elegance of `T?`.

We can wrap all of this together:

```Swift
struct ContextualizedMetricalDuration <T> {
    let metricalDuration: MetricalDuration
    let value: T
}
```

In a more concretely musical context, we may instantiate one of these as:

```Swift
let eighth = MetricalDuration(1,8)
let middleC = Pitch(60)

let durationalEvent = ContextualizedMetricalDuration {
    metricalDuration: eighth,
    value: TieOrNote.note(EventOrRest.event(middleC))
}
```

> This is, of course, getting pretty verbose. However, the composer-user would not be writing this code directly, but instead of through a higher-efficiency language.

### Rhythm trees

Now, let's contextualize the durational events in richer context.

We will use this definition of a `Tree`:

```Swift
enum Tree <T> {
    case leaf(T)
    indirect case branch([Tree])
}
```

We will specialize this a bit as:

```Swift
typealias RhythmTree<T> = Tree<ContextualizedMetricalDuration<RestOrEvent<T>>
```

That is, each `leaf` node will hold a `ContextualizedMetricalDuration`, which will in turn hold onto (tie, (rest | event)) structures.
