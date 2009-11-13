Function Values
---------------

Scala provides a number of different syntactic options for declaring function
values.  For example, the following declarations are exactly equivalent:

1. ``val f1 = { (a: Int, b: Int) => a + b }``
2. ``val f2 = (a: Int, b: Int) => a + b``
3. ``val f3 = (_: Int) + (_: Int)``
4. ``val f4: (Int, Int) => Int = { _ + _ }``

Of these styles, (1) and (4) are to be preferred at all times.  (2) appears shorter
in this example, but whenever the function value spans multiple lines (as is
normally the case), this syntax becomes extremely unweildy.  Similarly, (3) is
concise, but obtuse.  It is difficult for the untrained eye to decipher the fact
that this is even producing a function value.

When styles (1) and (4) are used exclusively, it becomes very easy to distinguish
places in the source code where function values are used.  Both styles make use
of curly braces (``{}``), allowing those characters to be a visual cue that a
function value may be involved at some level.

Spacing
~~~~~~~

You will notice that both (1) and (4) insert spaces after the opening brace and
before the closing brace.  This extra spacing provides a bit of "breathing room"
for the contents of the function and makes it easier to distinguish from the
surrounding code.  There are *no* cases when this spacing should be omitted.

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


