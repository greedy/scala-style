Inference
---------

Use type inference as much as possible.  You should almost never annotate the type
of a ``val`` field as their type will be immediately evident in their value::
    
    val name = "Daniel"
    
However, type inference has a way of coming back to haunt you when used on
non-trivial methods which are part of the public interface.  Just for the sake
of safety, you should annotate all public methods in your class.

Function Values
~~~~~~~~~~~~~~~

Function values support a special case of type inference which is worth calling
out on its own::
    
    val ls: List[String] = ...
    ls map { str => str.toInt }
    
In cases where Scala already knows the type of the function value we are declaring,
there is no need to annotate the parameters (in this case, ``str``).  This is an
intensely helpful inference and should be preferred whenever possible.  Note that
implicit conversions which operate on function values will nullify this inference,
forcing the explicit annotation of parameter types.

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
    

