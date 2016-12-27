# Abstract Musical Model

The current implementation of the `Abstract Musical Model` separates `Measure` values and a sequence of events organized hierarchically.

```Swift
final class AbstractMusicModel {
	let measures: [Measure]
	let events: [ContextualizedEventTree]
}
```

## Goals

Prefer to avoid too constricting of hierarchical organizations

## Possible changes



Currently, the only structural information of a work is modeled as a sequence of `Measure`.

First of all, this constricts the music supported to being metrical in nature, without mutilating the concept of a `Measure`.

