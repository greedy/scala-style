Control Structures
==================

All control structures should be written with a space following the defining
keyword::
    
    // right!
    if (foo) bar else baz
    for (i <- 0 to 10) { ... }
    while (true) { println("Hello, World!") }
    
    // wrong!
    if(foo) bar else baz
    for(i <- 0 to 10) { ... }
    while(true) { println("Hello, World!") }
    
.. toctree::

   curly_braces
   comprehensions
   trivial_conditionals
