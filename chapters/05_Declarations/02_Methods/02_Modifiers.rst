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
    
