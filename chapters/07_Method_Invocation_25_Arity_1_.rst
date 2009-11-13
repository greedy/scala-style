Arity-1
-------

Scala has a special syntax for invoking methods of arity-1 (one argument)::
    
    names.mkString(",")
    
    // is the same as
    
    names mkString ","
    
This syntax is formally known as "infix notation".  It should *only* be used for
purely-functional methods (methods with no side-effects) - such as ``mkString`` -
or methods which take functions as paramethers - such as ``foreach``::
    
    // right!
    names foreach { n => println(n) }
    names mkString ","
    optStr getOrElse "<empty>"
    
    // wrong!
    javaList add item

Higher-Order Functions
~~~~~~~~~~~~~~~~~~~~~~

As noted, methods which take functions as parameters (such as ``map`` or ``foreach``)
should be invoked using infix notation.  It is also *possible* to invoke such
methods in the following way::
    
    names.map { _.toUpperCase }     // wrong!
    
This style is *not* the accepted standard!  The reason to avoid this style is
for situations where more than one invocation must be chained together::
    
    // wrong!
    names.map { _.toUpperCase }.filter { _.length > 5 }
    
    // right!
    names map { _.toUpperCase } filter { _.length > 5 }

Both of these work, but the former exploits an extremely unintuitive wrinkle in
Scala's grammar.  The sub-expression ``{ _.toUpperCase }.filter`` when taken in
isolation looks for all the world like we are invoking the ``filter`` method on
a function value.  However, we are actually invoking ``filter`` on the result of
the ``map`` method, which takes the function value as a parameter.  This syntax
is confusing and often discouraged in Ruby, but it is shunned outright in Scala.


