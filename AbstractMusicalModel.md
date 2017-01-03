# Abstract Musical Model

The current implementation of the `Abstract Musical Model` separates `Measure` values and a sequence of events organized hierarchically.

```Swift
final class Event {
	
	// Any collection of musical elements (`Pitch`, `Dynamic`, `Articulation`, `OSCMessage`, etc.)
	let elements: [Any]

	//
	let identifierPath: [IdentifierPath]
}

// Ensure that an `Event` can be used as a `Key` value in a `Dictionary`.
extension Event: Hashable {
	var hashValue: Int {
		return ObjectIdentifier(self).hashValue
	}
}

final class MetricalEventTree {
	
	// Performer -> Instrument -> Voice
	let identifierPath: [IdentifierPath]

	// Internal representation of rhythm
	private let rhythmTree: RhythmTree<Event>
}


final class AbstractMusicModel {

	// Model of measures, etc.
	let structure: [Structure]

	// Rhythmical representations of `Event` objects
	let rhythms: [RhythmTree<Event>]

	let articulations: [Event: Articulation]
	let dynamics: [Event: Dynamic]
	let spanners: [Event: (SpannerType, Event)] // ?
	// etc...
}
```
