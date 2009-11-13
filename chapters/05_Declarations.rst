Declarations
============

All class/object/trait members should be declared interleaved with newlines.
The only exceptions to this rule are ``var`` and ``val``.  These may be declared
without the intervening newline, but only if none of the fields hava scaladoc
and if all of the fields have simple (max of 20-ish chars, one line) definitions::
    
    class Foo {
      val bar = 42
      val baz = "Daniel"
      
      def doSomething() { ... }
      
      def add(x: Int, y: Int) = x + y
    }
    
Fields should *precede* methods in a scope.  The only exception is if the ``val``
has a block definition (more than one expression) and performs opertions which
may be deemed "method-like" (e.g. computing the length of a ``List``).  In such
cases, the non-trivial ``val`` may be declared at a later point in the file as
logical member ordering would dictate.  This rule *only* applies to ``val`` and
``lazy val``!  It becomes very difficult to track changing aliases if ``var``
declarations are strewn throughout class file.


Methods
-------

Methods should be declared according to the following pattern::
    
    def foo(bar: Baz): Bin = expr
    
The only exceptions to this rule are methods which return ``Unit``.  Such methods
should use Scala's syntactic sugar to avoid accidentally confusing return types::
    
    def foo(bar: Baz) {       // return type is Unit
      expr
    }
    
Modifiers
~~~~~~~~~

Method modifiers should be given in the following order (when each is applicable):

#. Annotations, *each on their own line*
#. Override modifier (``override``)
#. Access modifier (``protected``, ``private``)
#. Final modifier (``final``)
#. ``def``

::
    
    @Transaction
    @throws(classOf[IOException])
    override protected final def foo() { 
      ...
    }
    
Body
~~~~

When a method body comprises a single expression which is less than 30 (or so)
characters, it should be given on a single line with the method::
    
    def add(a: Int, b: Int) = a + b
    
When the method body is a single expression *longer* than 30 (or so) characters
but still shorter than 70 (or so) characters, it should be given on the following
line, indented two spaces::
    
    def sum(ls: List[String]) =
      (ls map { _.toInt }).foldLeft(0) { _ + _ }
      
The distinction between these two cases is somewhat artificial.  Generally
speaking, you should choose whichever style is more readable on a case-by-case
basis.  For example, your method declaration may be very long, while the expression
body may be quite short.  In such a case, it may be more readable to put the
expression on the next line rather than making the declaration line unreadably
long.

When the body of a method cannot be concisely expressed in a single line or is
of a non-functional nature (some mutable state, local or otherwise), the body
must be enclosed in braces::
    
    def sum(ls: List[String]) = {
      val ints = ls map { _.toInt }
      ints.foldLeft(0) { _ + _ }
    }
    
Methods which contain a single ``match`` expression should be declared in the
following way::
    
    // right!
    def sum(ls: List[Int]): Int = ls match {
      case hd :: tail => hd + sum(tail)
      case Nil => 0
    }
    
*Not* like this::
    
    // wrong!
    def sum(ls: List[Int]): Int = {
      ls match {
        case hd :: tail => hd + sum(tail)
        case Nil => 0
      }
    }
    
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

Higher-Order Functions
~~~~~~~~~~~~~~~~~~~~~~

It's worth keeping in mind when declaring higher-order functions the fact that
Scala allows a somewhat nicer syntax for such functions at call-site when the
function parameter is curried as the last argument.  For example, this is the
``foldl`` function in SML::
    
    fun foldl (f: ('b * 'a) -> 'b) (init: 'b) (ls: 'a list) = ...
    
In Scala, the preferred style is the exact inverse::
    
    def foldLeft[A, B](ls: List[A])(init: B)(f: (B, A) => B) = ...
    
By placing the function parameter *last*, we have enabled invocation syntax like
the following::
    
    foldLeft(List(1, 2, 3, 4))(0) { _ + _ }
    
The function value in this invocation is not wrapped in parentheses; it is
syntactically quite disconnected from the function itself (``foldLeft``).  This
style is preferred for its brevity and cleanliness.


Fields
------

Fields should follow the declaration rules for methods, taking special note of
access modifier ordering and annotation conventions.


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


