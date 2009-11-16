Files
=====

As a rule, files should contain a *single* logical compilation unit.  By "logical"
I mean a class, trait or object.  One exception to this guideline is for classes
or traits which have companion objects.  Companion objects should be grouped
with their corresponding class or trait in the same file.  These files should
be named according to the class, trait or object they contain::
    
    package com.novell.coolness
    
    class Inbox { ... }
    
    // companion object
    object Inbox { ... }
    
These compilation units should be placed within a file named ``Inbox.scala``
within the ``com/novell/coolness`` directory.  In short, the Java file naming
and positioning conventions should be preferred, despite the fact that Scala
allows for greater flexibility in this regard.

.. toctree::

   multi_unit_files
