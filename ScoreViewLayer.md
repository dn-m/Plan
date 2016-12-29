# `ScoreViewLayer`

The `ScoreViewLayer` renders a `PageModel` onto the screen upon request.

## Dependencies

The `ScoreViewLayer` requires the [`ScoreModelLayer`](ScoreModelLayer.md), and implicitly the `AbstractMusicalModel`.

## API

```Swift
final class ScoreViewLayer {
	
	// MARK: - Initializers

	init()

	// MARK: - Instance Methods

	func update(with userInterfaceState: UserInterfaceState)
}
```

## Pseudo-implementation

```Swift
final class ScoreViewLayer {

	private struct ScoreSelection {
		let start: ScoreBound
		let end: ScoreBound
	}

	// At first, proportionate spacing
	private struct MusicSpacingModel { }
	
	// MARK: - Initializers

	init()

	// MARK: - Instance Methods

	func render(_ pageModel: PageModel)	

		func render(_ pageModel: PageModel) {
		viewLayer.render(pageModel)
	}

	private func preparePage() {
		// Given height constrains:
		// - device dimensions
		// - user zoom state,
		// prepare Page
		prepareSystems()
		// prepare structure
		let page = PageModel(...)
		render(page)
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
			....append(scoreModelLayer.segment(in: availableScoreRange))
		}
	}
}

final class PageModel {
    let systems: [SystemModel]
    let structure: ScoreStructureModel
}

final class SystemModel {
	
}
```
