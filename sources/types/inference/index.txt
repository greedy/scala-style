Inference
---------

Use type inference as much as possible.  You should almost never annotate the type
of a ``val`` field as their type will be immediately evident in their value::
    
    val name = "Daniel"
    
However, type inference has a way of coming back to haunt you when used on
non-trivial methods which are part of the public interface.  Just for the sake
of safety, you should annotate all public methods in your class.

.. toctree::

   function_values
   void_methods
