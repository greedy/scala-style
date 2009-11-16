Line Wrapping
-------------

There are times when a single expression reaches a length where it becomes
unreadable to keep it confined to a single line (usually that length is anywhere
above 80 characters).  In such cases, the *preferred* approach is to simply
split the expression up into multiple expressions by assigning intermediate results
to values or by using the `pipeline operator`_.  However, this is not always a
practical solution.

When it is absolutely necessary to wrap an expression across more than one line,
each successive line should be indented two spaces from the *first*.  Also
remember that Scala requires each "wrap line" to either have an unclosed
parenthetical or to end with an infix binary function or operator in which the
right parameter is not given::
    
    val result = 1 + 2 + 3 + 4 + 5 + 6 +
      7 + 8 + 9 + 10 + 11 + 12 + 13 + 14 +
      15 + 16 + 17 + 18 + 19 + 20
      
Without this trailing operator, Scala will infer a semi-colon at the end of a
line which was intended to wrap, throwing off the compilation sometimes without
even so much as a warning.

.. _pipeline operator: http://paste.pocoo.org/show/134013/

