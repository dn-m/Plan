# Plan
Repository for planning the development of the **dn-m** project.

## Background
**dn-m** will be a music notation renderer for the iPad, tailored to the needs of performers of contemporary music. 

## User stories

### Composers
- Composers can utilize an intelligently modelled graphical notation
  - Tablature notations
  - Electronics notations
- Composers can write in a concise textual language for rapid development of scores
- Composers can update the contents of a score, with the changes immediately accessible by a performer

### Performers
- Performers can specify exactly which musical attributes they see of their own and other player's music
  - Play from a full score
  - Display only the dynamics and rhythms of one other part
  - Display only the other players' parts, with your part memorized
  - Conduct a piece, displaying only the relevant information needed at any given time
- Performers can use built-in rehearsal tools
  - Metronomes knowledgable of the musical material
- Performers can have a more direct relationship to the activation of electronic musical elements
  - Interact with score following software

## Feature development
Quite a bit of work remains to be done. Much can be extracted and refined from this [repository](https://github.com/dn-m/Archive/tree/master/DNM-old).

### Musical model
The basic building blocks of music, designed to be notationally agnostic. 

#### Work organization
There is much room for debate and innovation in regards to the organization of the model of a work. Many notation systems couple notational aspects with the musical model at this stage. But, as a primary feature of this program is to display many different graphical representations of the same musical model, this must be decoupled.

#### Elements
Some basic elemental aspects of the musical model have been developed.
- [Pitch model](https://github.com/dn-m/Pitch)

Some basic elemental aspects of the musical model need to be developed and/or refined.
- Rhythm model
  - Hierarchical model, while preserving an immutable and value-type semantic
- [Dynamics model](https://github.com/dn-m/Dynamics/tree/master/Dynamics)
- Graphical notation model
  - This will need to be very flexible, but still structured

### Pre-notational representations
Many musical aspects may have a pipeline of intermediate, incrementally semantically rich representations.

- Pitch model
  - `Pitch` (`MIDI: 57`), (`Frequency: 440`) 
  - `SpelledPitch` (`A natural`) 
  - `StaffRepresentablePitchContext` (`A natural, half-harmonic`)
  - `StaffRepresentedPitchContext` (`A natural, half-harmonic, placed on top line of bass clef`)
- Dynamics model
  - `DynamicMarking` (`fff`)
  - `DynamicMarkingStratum` (`fff > ppp < mf — ø (sub.)`)
  - `DynamicMarkingStratumSegment` (`[[fff > (ppp)],[(fff)> ppp < mf],[(mf)— ø (sub.)]]`) 
- Rhythm model
  - Rhythm trees
  - Beaming model
  - Graphical beam representation

### Notational rendering
- Slurs
- Glyphs
- Import fonts, allow SVG conversion?

### Graphical models
- Layout
- Spanner management
- Score graphical model

## Project management
This project has been designed to be quite modular. There are many benefits to this project architecture, but it comes with inherent costs of maintainance.

We need to do certain things to ensure the health of the project.

- Testing
  - We use [Travis CI](https://travis-ci.org/dn-m/) to automatically run tests for each framework.
  - There is a strange issue with code-signing, where half of the builds fail for no logical reason.
  - We are tracking this issue [here](https://github.com/orgs/dn-m/projects/2).
  
- Documentation
  - We use [jazzy](https://github.com/realm/jazzy) to automatically generate [documentation](http://dn-m.github.io/) from source code.
  - We have scripts that merge documentation for all of the different repositories into a single site.
  - The current implementation of this is brittle and has many implicit dependencies.
  - We must refactor this to be useable by multiple developers.
  - Further, we should add a script phase to be performed after a successful `Travis CI` build on any `master` branch, to re-generate the documentation for the project.
