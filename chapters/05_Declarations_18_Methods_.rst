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


