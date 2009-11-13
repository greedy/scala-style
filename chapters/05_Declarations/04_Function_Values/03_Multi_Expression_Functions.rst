Multi-Expression Functions
~~~~~~~~~~~~~~~~~~~~~~~~~~

Most function values are less trivial than the examples given above.  Many contain
more than one expression.  In such cases, it is often more readable to split the
function value across multiple lines.  When this happens, only style (1) should
be used.  Style (4) becomes extremely difficult to follow when enclosed in large
amounts of code.  The declaration itself should loosely follow the declaration
style for methods, with the opening brace on the same line as the assignment or
invocation, while the closing brace is on its own line immediately following the
last line of the function.  Parameters should be on the same line as the opening
brace, as should the "arrow" (``=>``)::
    
    val f1 = { (a: Int, b: Int) =>
      a + b
    }
    
As noted earlier, function values should leverage type inference whenever
possible.

