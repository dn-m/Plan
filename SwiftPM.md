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
  - `ordered<Comparable>(_:_:)`: `Move to dn-m/Structure`
  - `mean<FloatingPoint>(_:_:)`
  - `BidirectionalCollection<Numeric & Additive>.mean`
  - `mod<BinaryInteger>(_:)`
  - `mod<FloatingPoint>(_:)`
  - `IntegerExtensions` (`isEven`, `isOdd`, `isPrime`, `isPowerOfTwo`, `divisible(by:)`)
- Consider:
  - Factorization:
    - `GCDDomain`
    - `mod<BinaryInteger>(_:)`
    - `mod<FloatingPoint>(_:)`
    - `isPrime`
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
