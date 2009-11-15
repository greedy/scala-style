Parentheses
~~~~~~~~~~~

Unlike Ruby, Scala attaches significance to whether or not a method is *declared*
with parentheses (only applicable to methods of arity_-0).  For example::
    
    def foo1() = ...
    
    def foo2 = ...
    
These are different methods at compile-time.  While ``foo1`` can be 
called with or without the parentheses, ``foo2`` *may not* be called
*with* parentheses.

Thus, it is actually quite important that proper guidelines be observed regarding
when it is appropriate to declare a method without parentheses and when it is
not.

Methods which act as accessors of any sort (either encapsulating a field or a
logical property) should be declared *without* parentheses except if they have side effects.
While Ruby and Lift use a ``!`` to indicate this, the usage of parens is preferred [#dsl_note]_.  

Further, the callsite should follow the declaration; if declared with parentheses,
call with parentheses.  While there is temptation to save a few characters,
if you follow this guideline, your code will be *much* more readable and 
maintainable.

::

  // doesn't change state, call as birthdate
  def birthdate = firstName

  // updates our internal state, call as age()
  def age() = {
    _age = updateAge(birthdate)
    _age
  }

.. _arity: http://en.wikipedia.org/wiki/Arity

.. [#dsl_note] Please note that fluid APIs and internal domain-specific languages have a
               tendency to break the guidelines given below for the sake of syntax.  Such
               exceptions should not be considered a violation so much as a time when these
               rules do not apply.  In a DSL, syntax should be paramount over convention.

