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

### Migrate contents

- [ ] `TreeTools`: Migrate to `Collections`, destroy
- [ ] `StringTools`: Migrate to `Collections`, destroy
- [ ] `Color`: Migrate to `GraphicsTools`, destroy
- [ ] `Duration`: Migrate to `Rhythm`, **do not destroy**
- [ ] `Graph`: Migrate to `Plot` / `PlotView`
- [ ] `GraphStructures`: Migrate to `Collections`
- [ ] `LayoutTools`: Migrate to `GraphicsTools`
- [ ] `Staff`: Split into `StaffModel` / `StaffView`, destroy
- [ ] `DocumentationTools`: Migrate to `Helper`

### Move to Archive

- [x] `300-19`: Move to `Archive`.
- [x] `FrameworkTools`: Move to `Archive`
- [x] `ScriptingTools`: Move to `Archive`
- [x] `DirectionTools`: Move to `Archive` (or destroy)

### Destroy
- [x] `CopyTools`: Destroy
- [ ] `Plot`: Destroy
- [x] `ColorMode`: Destroy
