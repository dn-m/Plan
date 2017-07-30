# SwiftPM Migration

This document outlines the process of migrating code from a Carthage-driven workflow, to one driven by Swift Package Manager.

## Structure
- Algebra
- (...) Data structures
- Destructure
- StructureWrapping
- DictionaryProtocol
- SumType
- Predicates: `Discuss`
- PatternMatching: `Discuss`
- Algorithms: `Discuss`

## Math
- Arithmetic `previously: ArithmeticTools, break into the following:`
  - Rational
  - Scaling
  - GCDDomain
  - Quadratic
  - Ranges
  - LinearRegression
  - Power
  - Random
  - StringFormatting `Discuss: name`
  - Vector2 (move to `Geometry`?)
  - ...
  
- Yet unorganized:
  - `BidirectionalCollection<SignedNumber>.closest(to:)`
  - `closer<SignedNumber>(to:a:b:)`
  - `ordered<Comparable>(_:_:)`
  - `mean<FloatingPoint>(_:_:)`
  - `mod<BinaryInteger>(_:)`
  - `mod<FloatingPoint>(_:)`
  - `BidirectionalCollection<Numeric & Additive>.mean`
  - `IntegerExtensions` (`isEven`, `isOdd`, `isPrime`, `isPowerOfTwo`, `divisible(by:)`)
- Geometry `previously: GeometryTools`

## Graphics
- Path `previously: PathTools`
- Styling: `Discuss name, previously: GraphicsTools`
- SVG
- Quartz

## MusicModel
- Articulations
- Dynamics
- Pitch
- Rhythm

## ScoreModel
- SpelledRhythm
- SpelledPitch
- PlotModel
- StaffModel
- ...

## ScoreView
- PlotView
- StaffView
- RhythmView
- ...
