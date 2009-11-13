Functions
---------

Function types should be declared with a space between the parameter type, the
arrow and the return type::
    
    def foo(f: Int => String) = ...
    
    def bar(f: (Boolean, Double) => List[String]) = ...
    
Parentheses should be omitted wherever possible (e.g. methods of arity-1, such
as ``Int => String``).

Arity-1
~~~~~~~

Scala has a special syntax for declaring types for functions of arity-1.  For
example::
    
    def map[B](f: A => B) = ...
    
Specifically, the parentheses may be omitted from the parameter type.  Thus, we
did *not* declare ``f`` to be of type "``(A) => B``, as this would have been
needlessly verbose.  Consider the more extreme example::
    
    // wrong!
    def foo(f: (Int) => (String) => (Boolean) => Double) = ...
    
    // right!
    def foo(f: Int => String => Boolean => Double) = ...
    
By omitting the parentheses, we have saved six whole characters and dramatically
improved the readability of the type expression.


