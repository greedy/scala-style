Ascription
----------

Type ascription is often confused with type annotation, as the syntax in Scala
is identical.  The following are examples of ascription:

* ``Nil:List[String]``
* ``Set(values:_*)``
* ``"Daniel":AnyRef``

Ascription is basically just an up-cast performed at compile-time for the sake of
the type checker.  Its use is not common, but it does happen on occaision.  The
most often seen case of ascription is invoking a varargs method with a single
``Seq`` parameter.  This is done by ascribing the ``_*`` type (as in the second
example above).

Ascription usually follows the type annotation conventions except that no spaces
are inserted between value and type.  This more compact form is *usually* prefered
as it improves compactness without hindering readability.  With ascription, the
type is a logical part of the value being explicitly stated.  This is not the
case with a type annotation.

Of course, there are times when the "spaceless syntax" breaks down and hinders
legibility.  In such cases, the correct "fallback" is to use the convention
employed for type annotations (e.g. ``Nil: List[String]``).


