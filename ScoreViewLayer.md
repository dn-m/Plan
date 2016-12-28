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

	func render(_ pageModel: PageModel)
}
```

## Pseudo-implementation

```Swift
final class ScoreViewLayer {
	
	// MARK: - Initializers

	init()

	// MARK: - Instance Methods

	func render(_ pageModel: PageModel)	
}

final class PageModel {
    let systems: [SystemModel]
    let structure: ScoreStructureModel
}

final class SystemModel {
	
}
```
