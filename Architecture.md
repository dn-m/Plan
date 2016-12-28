# Architecture

## `ScoreModelLayer`

The `ScoreModelLayer` encapsulates abstract information of a work of music, as well as user-initiated modifications to it.

A performer may interact with the semantic construction of a score in three ways:

- **Filter** out attributes of any part
- Add a number of different types of **annotations**
- Redefine the **ordering** of parts

The `ScoreModelLayer` stores these modifications, presents an updated model of the score model when needed, and writes the updates to disk.

The only logical product of the model layer is a `ScoreModelSegment`, which is an abstract representation of the graphical objects comprising a `System`'s-worth of music. The objects contained within the `ScoreModelSegment` are knowledgeable of "musical time", but not their horizontal placement.

## Organizational diagram

<img src="img/ScoreModelLayer.png" alt="ScoreModelLayer" style="width: 20px;"/>

## API and psuedo-implementation

```Swift

final class ScoreModelLayer {

    // MARK: - Nested Types

    /// Abstract representation of graphical objects of a System's worth of music.
    /// Extends the ScoreModel with a model of managing Spanner type objects over System-breaks.
    /// Objects contained herein are organized in "time", not in horizontal space.
    /// This is the only public product of the `ScoreModelLayer`.
    struct ScoreModelSegment {

    	init(scoreModel: ScoreModel, range: ScoreRange) {
    		...
    	}

    	func filtered(with filters: FilterState) -> ScoreModelSegment {
    		...
    	}

    	/// - returns: Copy of self with annotations merged
        func annotated(with annotations: AnnotationModel) -> ScoreModelSegment {
            ...
        }
    }

    /// Abstract representation of graphical objects comprising a full score.
    /// This model has no knowledge of system breaks.
    /// Objects contained herein are organized in "time", not in horizontal space.
    private class ScoreModel {

        init(_ abstractMusicalModel: AbstractMusicalModel) {
            ...
        }

		/// - returns: Subset of `self` in a given range.
        func segment(in range: ScoreRange) -> ScoreModelSegment {
        	...
        }

        /// - returns: Subset of `self` in a given range, with the given `annotations` merged.
        func segment(in range: ScoreRange, annotations: AnnotationModel, filters: FilterModel) 
        	-> ScoreModelSegment 
        {
            return segment(in: range)
            	.annotated(with: annotations)
            	.filtered(with: filters)
        }
    }

    /// Protocol abstracting implementation for FilterModel, AnnotationModel, and OrderingModel.
    private protocol UserStateModel {
    	associatedtype Element
    	var backingModel: UserStateBackingModel<Element> { get }
    	func add(_ element: T)
    	func remove(_ element: T)
    }

    /// Data structure holding overlapping ranges of filters (hide c for a:b in (t0,t1)).
    private struct FilterModel: UserStateModel {
        let backingModel: ...
    }

    /// Data structure holding annotations (bowings, fingerings, cue links).
    private struct AnnotationModel: UserStateModel {
        let backingModel: ...
    }

	/// Data structure holding score-order selections.
    private struct OrderingModel: UserStateModel {
    	let backingModel: ...
    }

    /// Reads and writes persisting user state from/to disk on background thread.
    /// Files: filters.xxx, annotations.xxx, orderings.xxx
    private struct DataStore {
        func writeToFilterDataStore() { }
        func readFromFilterDataStore() { }
        func writeToAnnotationDataStore() { }
        func readFromAnnotationDataStore() { }
        func writeToOrderingDataStore() { }
        func readFromOrderingDataStore() { }
    }

    // MARK: - Instance Properties

    private var filters: FilterModel
    private var annotations: AnnotationModel
    private var orderings: OrderingModel
    private let dataStore: DataStore

    private let scoreModel: ScoreModel 

    // MARK: - Initializers

    init(abstractMusicalModel: AbstractMusicalModel) {
        self.scoreModel = ScoreModel(abstractMusicalModel)
    }

    // MARK: - Instance Methods

    func scoreModelSegment(in range: ScoreRange) -> ScoreModelSegment {
        return scoreModel.segment(in: range, annotations: annotations, filters: filters)
    }

    // MARK: - Modifying Model

    func add(_ filter: Filter) {
        filters.add(filter)
        writeToFilterDataStore()
    }

    func remove(_ filter: Filter) { 
        filters.remove(filter)
        writeToFilterDataStore()
    }

    func add(_ annotation: Annotation) { 
        annotations.add(annotation)
        writeToAnnotationDataStore()
    }

    func remove(_ annotation: Annotation) { 
        annotations.remove(annotation)
        writeToAnnotationDataStore()
    }

    func add(_ ordering: Ordering) { 
        annotations.add(annotation)
        writeToOrderingDataStore()
    }

    func remove(_ ordering: Ordering) { 
        annotations.remove(ordering)
        writeToOrderingDataStore()
    }
}
```

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