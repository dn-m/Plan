# Architecture

Notes on the architecture of **dn-m**.

![Architecture](img/architecture.png)

## Input

Several input methods are to be developed:
- dn-m language
- MusicXML conversion

## Static Model

Before being represented graphically, the musical information of a score will go through several internal representations.

### Abstract Musical Model

The abstract musical model

Agnostic to:
- Graphical representation of any kind

### Intermediate Representations

Depending on the specific types of information, there may be different intermediate representations to appropriately prepare them for score organization.

### Score Model

The Score Model is modeled as a single (lazy) stream

Agnostic to:
- Horizontal / vertical dimensions
- Score order
- Splitting up of Spanner types

## Dynamic Model

### User Configuration

A performer-user can configure the score representation in two ways.

#### Dimensional

Scale the concrete dimensions of the score to be bigger or smaller

#### Semantic

Filter out attributes of any performers' part.

### Score Model Segment

A subsequence of the contents of the Score Model, taking into consideration system breaks, and therefore the splitting up of `Spanner` types.
