# Architecture

## Example API

```Swift
struct ScoreModel {
	// ...
}
```

```Swift
struct AnnotatedScoreModel {
	
	final class ScoreAnnotationState {
		var data: [String: String]
	}

	let scoreModel: ScoreModel
	let state: ScoreAnnotationState

	func update(...) { }
}

```

```Swift
struct ScoreModelSegment {
	// Subset of ScoreModel
	// Manages spanners abstractly
}
```

```Swift
struct RenderableScoreModelSegment {
	// System model
}
```

```Swift
class ViewController {

	// Reference to score model with added annotations
	// "Model" in our MVC
	let annotatedScoreModel: AnnotatedScoreModel

	// "View" in our MVC
	let view: View

	// MARK: - UI
	func didMakeScoreAnnotation(_ annotation: AnnotationType) {
		annotatedScoreModel.update(...)
		updatePersistentAnnotationState()
	}

	// MARK: - Rendering
	func makeScoreSegments(in range: ScoreRange) -> [ScoreSegment] { }

	// MARK: - Data access layer
	func updatePersistentAnnotationState() { }
}
```

![Architecture](img/architecture.png)

---

## Input

Several input methods are to be developed.

### dn-m language

For the purposes of authoring scores efficiently, a language is to be developed.

**TODO**: dn-m language definition page

### MusicXML conversion

For the purposes of translating previously authored scores into the dn-m environment, the [MusicXML](https://github.com/dn-m/MusicXML) framework will convert the abstract musical information from `MusicXML` files to the native `dn-m` `Abstract Musical Model` representation.

---

## Static Model

Before being represented graphically, the musical information of a score will go through several internal representations.

### Abstract Musical Model

The abstract musical model will hold abstract definitions of musical events, agnostic of graphical representation.

The current implementation (which can be revised considerably) looks like this:

```Swift
final class AbstractMusicModel {
	let measures: [Measure]
	let events: [ContextualizedEventTree]
}
```

### Intermediate Representations

Depending on the specific types of information, there may be different intermediate representations to appropriately prepare them for score organization.

### Score Model

The Score Model is modeled as a single (lazy) stream

Agnostic to:
- Horizontal / vertical dimensions
- Score order
- Splitting up of Spanner types

---

## Dynamic Generated Representational Model

### User Configuration

A performer-user can configure the score representation in two ways.

#### Dimensional

Scale the concrete dimensions of the score to be bigger or smaller

#### Semantic

Filter out attributes of any performers' part.

### Score Model Segment

A subsequence of the contents of the Score Model, taking into consideration system breaks, and therefore the splitting up of `Spanner` types.
