# Plan
Repository for planning the development of the dn-m project.

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

## Upcoming work
Quite a bit of work remains to be done. Much can be extracted and refined from this [repository](https://github.com/dn-m/Archive/tree/master/DNM-old).

### Musical model
The basic building blocks of music, designed to be notationally agnostic. 

#### Work organization
There is much room for debate and innovation in regards to the organization of the model of a work. Many notation systems couple notational aspects with the musical model at this stage. But, as a primary feature of this program is to display many different graphical representations of the same musical model, this must be decoupled.

#### Elements
Some basic elemental aspects of the musical model have been developed.
- [Pitch model](https://github.com/dn-m/Pitch)

Some basic elemental aspects of the musical model need to be developed and refined.
- Rhythm model
  - Hierarchical model, while preserving an immutable and value-type semantic
- Graphical notation model
  - This will need to be very flexible, but still structured
