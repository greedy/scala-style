---
title: Main
layout: default
permalink: index.html
---

# Scala Style Guide

In lieu of an official style guide from EPFL, or even an unofficial guide from
a community site like Artima, this document is intended to outline some basic
Scala stylistic guidelines which should be followed with more or less fervency.
Wherever possible, this guide attempts to detail *why* a particular style is
encouraged and how it relates to other alternatives. As with all style guides,
treat this document as a list of rules to be broken. There are certainly times
when alternative styles should be preferred over the ones given here.

Generally speaking, Scala seeks to mimic Java conventions to ease interoperability.
When in doubt regarding the idiomatic way to express a particular concept, adopt
conventions and idioms from the following languages (in this order):

* Java
* [Standard ML][]
* Haskell
* C#
* OCaml
* Ruby
* Python

For example, you should use Java's naming conventions for classes and methods,
but SML's conventions for type annotation, Haskell's conventions for type
parameter naming (except upper-case rather than lower) and Ruby's conventions for
non-boolean accessor methods.  Scala really is a hybrid language!

 1. [Indentation](chapters/Indentation.html)
 1. [Naming Conventions](chapters/Naming_Conventions.html)
 1. [Types](chapters/Types.html)
 1. [Nested Blocks](chapters/Nested_Blocks.html)
 1. [Declarations](chapters/Declarations.html)
 1. [Control Structures](chapters/Control_Structures.html)
 1. [Method Invocation](chapters/Method_Invocation.html)
 1. [Files](chapters/Files.html)

[Standard ML]: http://en.wikipedia.org/wiki/Standard_ML "Standard ML"

