# Abstract Musical Model

The current implementation of the `Abstract Musical Model` separates `Measure` values and a sequence of events organized hierarchically.

```Swift
final class Event {
	let identifierPath: [IdentifierPath]

	// Any collection of musical elements (`Pitch`, `Dynamic`, `Articulation`, `OSCMessage`, etc.)
	let elements: [Any]
}

final class AbstractMusicModel {

	// Model of measures, etc.
	let structure: [Structure]

	// Rhythmical representations of `Event` objects
	let rhythms: [RhythmTree<Event>]

	let articulations: [Event: Articulation]
	let dynamics: [Event: Dynamic]
	// etc...
}
```
