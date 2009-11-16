Operators
---------

Symbolic methods (operators) should *always* be invoked using infix notation with
spaces separated the target, the operator and the parameter::
    
    // right!
    "daniel" + " " + "Spiewak"
    
    // wrong!
    "daniel"+" "+"spiewak"
    
For the most part, this idiom follows Java and Haskell syntactic conventions.

Operators which take more than one parameter (they do exist!) should still be
invoked using infix notation, delimited by spaces::
    
    foo ** (bar, baz)
    
Such operators are fairly rare, however, and should be avoided during API design.

