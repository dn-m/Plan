---
title: dn-m Project Style Guide
authors: Brian Heim, James Bean
created: 2017-08-21
---

dn-m Project Style Guide
========================

This document contains style recommendations for Swift source code in the dn-m project.

Source File Layout
------------------

Source files should be organized with sections in the following order:

- TODO

Naming
------

### Functions that construct objects or values

- Use `make` for a function that returns an object without side effects; this also includes factory
  methods.
- Use `create` for a function that returns an object while storing it internally or producing some
  other side effect, such as ID allocation.
- Use `add`, `insert`, etc. for a function that creates a new value internally but does not return
  it to the caller.


