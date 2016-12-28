# `ScoreController`

The `ScoreController` allows the user to interact with the `ScoreModelLayer` in order to update the graphical representation of their score in the `ScoreViewLayer`.

## Dependencies

The `ScoreController` requires the `AbstractMusicalModel`, `ScoreModelLayer`, and the `ScoreViewLayer`APIs.

## Organizational diagram

**TODO**

## API

```Swift
final class ScoreController {
	
	// MARK: - Initializers

	init(abstractMusicalModel: AbstractMusicalModel)

	// MARK: - Instance Methods
}
```

## Pseudo-implementation

```Swift
final class ScoreController {
	
	// MARK: - Nested Types

	private struct DataStore {
		func writeToUserInterfaceDataStore()
		func readFromUserInterfaceDataStore()
	}

	// Given the available dimensions of the current device and the user interface 
	// state, prepare the current screen's-worth of music notation.
	private struct PageLayout {

	}

	// An extension of the `ScoreModelSegment` with positional information
	private final class SystemModel {

	}

	// At first, proportionate spacing
	private struct MusicSpacingModel {

	}

	private struct ScoreSelection {
		let start: Point
		let end: Point
	}

	// MARK: - Initializers

	init(abstractMusicalModel: AbstractMusicalModel) { 
		...
	}

	// MARK: - View Preparation

	func render(_ pageModel: PageModel) {

	}

	private func preparePage() {
		// Given height constrains:
		// - device dimensions
		// - user zoom state,
		// prepare Page
		prepareSystems()
	}

	private func prepareSystems() -> [SystemModel] {
		// Given width constraints:
		// - device dimensions
		// - user zoom state
		// - music spacing model,
		// prepare systems.
		// In the case of dynamic music spacing, a continued dialogue must occur 
		// between the `ScoreController` and the `ScoreModelLayer`.
		while accumHeight < maxHeight {
			scoreModelLayer.segment(in: availableScoreRange)
		}
	}

	// MARK: - UI

	func didMakeAnnotation(_ annotation: ScoreAnnotation)
	func didMakeFilter(_ filter: ScoreFilter)
	func didMakeOrdering(_ ordering: ScoreOrdering)

	private func didMakeSelection(start: Point, end: Point) { 
		// prepare selection type
	}

	private func scoreRange(from selection: ScoreSelection) { }
} 

struct UserInterfaceStateModel {
	// zoom
}

struct MusicSpacingModel() {
	// horizontal characteristics of spacing time in space
}

final class PageModel {
	let systems: [SystemModel]
	let structure: ScoreStructureModel
}

final class SystemModel {
	init(_ scoreModelSegment: ScoreModelSegment, userInterfaceState: UserInterfaceStateModel, musicSpacing: MusicSpacingModel)
}

// Device state
// "zoom"-level
```

