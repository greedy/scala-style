"Void" Methods
~~~~~~~~~~~~~~

The exception to the "annotate everything public" rule is methods which return
``Unit``.  *Any* method which returns ``Unit`` should be declared using Scala's
syntactic sugar for that case::
    
    def printName() {
      println("Novell")
    }
    
This compiles into::
    
    def printName(): Unit = {
      println("Novell")
    }
    
You should prefer the former style (without the annotation or the equals sign)
as it reduces errors and improves readability.  For the record, it is also
possible (and encouraged!) to declare abstract methods returning ``Unit`` with an
analogous syntax::
    
    def printName()         // abstract def for printName(): Unit
    
