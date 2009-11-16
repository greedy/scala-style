Currying
~~~~~~~~

In general, you should only curry functions if there is a good reason to do so.
Curried functions have a more verbose declaration and invocation syntax and are
harder for less-experienced Scala developers to understand.  When you do declare
a curried function, you should take advantage of Scala's syntactic sugar involving
multiple groups of parentheses::
    
    // right!
    def add(a: Int)(b: Int) = a + b
    
    // wrong!
    def add(a: Int) = { b: Int => a + b }
    
Scala will compile both of these declarations into the same result.  However,
the former is slightly easier to read than the latter.

