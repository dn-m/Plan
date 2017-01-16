# Organizational Layers

### Application Layer

- `dn-m`

### Real-time Layer

The frameworks of this layer contain their source, and demo targets for graphical confirmation.

- `Timeline`
- `OSC`
- `AudioTools`

### User Interface Layer
- `ProgressBar`
- `ControllerElements`
- `CompoundController[View]`

### Score View Layer

The frameworks of this layer contain their source, and demo targets for graphical confirmation.

- `PlotView`
- `StaffView`

`...`

### Graphics Utilities

- `PathTools`
- `GraphicsTools`

### Score Model Layer

The frameworks of this layer contain their source and a set of unit tests.

- `PlotModel`
- `StaffModel`
- `PitchSpellingTools`

### Input Layer

- `MusicXML`
- `Language`

### Abstract Musical Model Layer

The frameworks of this layer contain their source and a set of unit tests.

- `Pitch`
- `Rhythm`
- `Dynamics`
- `Articulations`
- `EnsembleTools`

### Utility Layer

The frameworks of this layer contain their source and a set of unit tests.

- `Collections`
- `ArithmeticTools`
- `IntervalTools`
- `ParserTools`

## Frameworks needing management

- `TreeTools`: Migrate to `Collections`, destroy
- `Plot`: Destroy
- `StringTools`: Migrate to `Collections`, destroy
- `Color`: Migrate to `GraphicsTools`, destroy
- `Duration`: Migrate to `Rhythm`, **do not destroy**
- `ScriptingTools`: Move to `Archive`
- `DirectionTools`: Move to `Archive` (or destroy)
- `ColorMode`: Migrate to `GraphicsTools`
- `FrameworkTools`: Move to `Archive`
- `Graph`: Migrate to `Plot` / `PlotView`
- `GraphStructures`: Migrate to `Collections`
- `CopyTools`: Destroy
- `LayoutTools`: Migrate to `GraphicsTools`
- `Staff`: Split into `StaffModel` / `StaffView`, destroy
- `DocumentationTools`: Migrate to `Helper`
- `300-19`: Move to `Archive`.
