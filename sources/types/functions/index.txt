Functions
---------

Function types should be declared with a space between the parameter type, the
arrow and the return type::
    
    def foo(f: Int => String) = ...
    
    def bar(f: (Boolean, Double) => List[String]) = ...
    
Parentheses should be omitted wherever possible (e.g. methods of arity-1, such
as ``Int => String``).

.. toctree::

   arity_1
