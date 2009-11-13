Methods
-------

Textual (alphabetic) names for methods should be in the camelCase style with the
first letter lower-case::
    
    def myFairMethod = ...
    
This section is not a comprehensive guide to idiomatic methods in Scala.  Further
information may be found in the method invocation section.

Accessors/Mutators
~~~~~~~~~~~~~~~~~~

Scala does *not* follow the Java convention of prepending ``set``/``get`` to
mutator and accessor methods (respectively).  Instead, the following conventions
are used:

* For accessors of *most* boolean and non-boolean properties, the name of the
  method should be the name of the property
* For accessors of *some* boolean properties, the name of the method may be the
  capitalized name of the property with "``is``" prepended (e.g. ``isEmpty``).
  This should only be the case when no corresponding mutator is provided.  Please
  note that the Lift_ convention of appending "``_?``" to boolean accessors is
  non-standard and not used outside of the Lift framework.
* For mutators, the name of the method should be the name of the property with
  "``_=``" appended.  As long as a corresponding accessor with that particular
  property name is defined on the enclosing type, this convention will enable
  a call-site mutation syntax which mirrors assignment.

::
    
    class Foo {
    
      def bar = ...
      
      def bar_=(bar: Bar) {
        ...
      }
      
      def isBaz = ...
    }
    
    val foo = new Foo
    foo.bar             // accessor
    foo.bar = bar2      // mutator
    foo.isBaz           // boolean property

Quite unfortunately, these conventions fall afoul of the Java convention to name
the private fields encapsulated by accessors and mutators according to the
property they represent.  For example::
    
    public class Company {
        private String name;
        
        public String getName() {
            return name;
        }
        
        public void setName(String name) {
            this.name = name;
        }
    }
    
If we were to attempt to adopt this convention within Scala while observing the
accessor naming conventions given above, the Scala compiler would complain about
a naming colision between the ``name`` field and the ``name`` method.  There are
a number of ways to avoid this problem and the community has yet to standardize
on any one of them.  The following illustrates one of the less error-prone
conventions::
    
    class Company {
      private val _name: String = _
      
      def name = _name
      
      def name_=(name: String) {
        _name = name
      }
    }
    
While Hungarian notation is terribly ugly, it does have the advantage of
disambiguating the ``_name`` field without cluttering the identifier.  The
underscore is in the prefix position rather than the suffix to avoid any danger
of mistakenly typing ``name _`` instead of ``name_``.  With heavy use of Scala's
type inference, such a mistake could potentially lead to a very confusing error.

Note that fields may actually be used in a number of situations where accessors
and mutators would be required in languages like Java.  Always prefer fields over
methods when given the choice.

Parentheses
~~~~~~~~~~~

Unlike Ruby, Scala attaches significance to whether or not a method is *declared*
with parentheses (only applicable to methods of arity_-0).  For example::
    
    def foo1() = ...
    
    def foo2 = ...
    
These are different methods at compile-time.  We can invoke ``foo1`` omitting
the parentheses if we choose (e.g. ``foo1``), or we may include the parentheses
as part of the invocation syntax (e.g. ``foo1()``).  However, ``foo2`` is limited
to *only* parentheses-less invocations (e.g. ``foo2``).  If we attempt to call
``foo2`` using parentheses, the compiler will produce an error.

Thus, it is actually quite important that proper guidelines be observed regarding
when it is appropriate to declare a method without parentheses and when it is
not.  Please note that fluid APIs and internal domain-specific languages have a
tendency to break the guidelines given below for the sake of syntax.  Such
exceptions should not be considered a violation so much as a time when these
rules do not apply.  In a DSL, syntax should be paramount over convention.

* Methods which act as accessors of any sort (either encapsulating a field or a
  logical property) should be declared *without* parentheses except in the
  following case:
* Methods which have *any* side-effects outside of their internal scope should
  be declared *with* parentheses.  Ruby (and Lift) uses the ``!`` suffix to denote
  this case.  Note that a method need not be defined as a pure function internally
  to qualify as "side-effect free".  The question is whether the method changes
  some global or instance variable.  If the answer to this question is "yes",
  then parentheses should be used **for both declaration and invocation**.

Let me restate that these conventions apply not only to the declaration site, but
also the call site.  Thus, if you are calling a method which you know has
side-effects (returning ``Unit`` is usually a sure sign of this), then you should
qualify the invocation with parentheses (e.g. ``foo()``).  Avoid the temptation
to omit parentheses simply because it saves two characters!

Operators
~~~~~~~~~

Avoid!  Despite the degree to which Scala facilitates this area of API design,
operator definition should not be undertaken lightly, particularly when the
operator itself is non-standard (for example, ``>>#>>``).  As a general rule,
operators have two valid use-cases:

* Domain-specific languages (e.g. ``actor1 ! Msg``)
* Logically mathematical operations (e.g. ``a + b`` or ``c :: d``)

In the former case, operators may be used with impunity so long as the syntax is
actually beneficial.  However, in the course of standard API design, operators
should be strictly reserved for purely-functional operations.  Thus, it is
acceptable to define a ``>>=`` operator for joining two monads, but it is not
acceptable to define a ``<<`` operator for writing to an output stream.  The
former is mathematically well-defined and side-effect free, while the latter is
neither of these.

Operator definition should be considered an advanced feature in Scala, to be used
only by those most well-versed in its pitfalls.  Without care, excessive operator
overloading can easily transform even the simplest code into symbolic soup.


