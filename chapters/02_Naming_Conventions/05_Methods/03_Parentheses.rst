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

