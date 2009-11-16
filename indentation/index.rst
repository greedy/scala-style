Indentation
===========

Indentation should follow the "2-space convention".  Thus, instead of indenting
like this::
    
    // wrong!
    class Foo {
        def bar = ...
    }
    
You should indent like this::
    
    // right!
    class Foo {
      def bar = ..
    }
    
The Scala language encourages a startling amount of nested scopes and logical
blocks (function values and such).  Do yourself a favor and don't penalize yourself
syntactically for opening up a new block.  Coming from Java, this style does take
a bit of getting used to, but it is well worth the effort.

.. toctree::

   line_wrapping
   methods_with_numerous_arguments
