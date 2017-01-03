# IRCAM Residency — Winter 2017

## Goals

### Implement `AbstractMusicalModel`

Complete implementation of basic data structures, with no complex operations.

- **Primary**:
  - [`Pitch`](https://github.com/dn-m/Pitch)
  - [`Rhythm`](https://github.com/dn-m/Rhythm)
  - [`Dynamics`](https://github.com/dn-m/Dynamics)
  - [`Articulations`](https://github.com/dn-m/Articulations)
  - `WorkModel`
    - With `Jean-Louis`: Examine storage strategies (attribute-tables with `Event`-objects as keys)
  
- **Optional**:
  - `SpannerModel`
  - `TablatureModel`

---

### Create skeleton of complete architecture

Define clear and narrow APIs between highly-modularized frameworks. 

  - `AbstractMusicalModel`
  - `ScoreModelLayer`
  - `ScoreViewLayer`
    - `ScoreRenderer`
    - `Real-time graphics`
  - `dn-m iOS` / `macOS` app targets
  
> Maintain the overhead of this abstraction with [dn-m/Helper](https://github.com/dn-m/Helper) command line tool.

- **Primary:**
  - Make contact through whole project, with compiling (though not implemented) APIs
- **Optional:**
  - Implement a basic example of a score (from abstract model to graphic representation)
  
---
  
### Basic parsing of `MusicXML`

Extract abstract (non-notational) musical elements from `MusicXML` using the [dn-m/MusicMXL](https://github.com/dn-m/MusicMXL) framework.

> `Antescofo` parser as a model.

---

### Receive OSC messages from `Antescofo`

Using the [dn-m/OSC](https://github.com/dn-m/OSC) framework, receive `OSC` messages from a running `Antescofo` instance.

- **Primary**: 
  - Just make contact.
- **Optional**: 
  - Construct model mirroring the internals of `Antescofo`.

---

### Primitive graphical representation of `ScoreModel`

#### Rhythms
With `Florent Jacquemard`: Interface to `qparse`
  
#### Traditional Staff notation

Using [dn-m/Staff](https://github.com/dn-m/Staff) framework to render `Pitch` values.
