Ascription
----------

Type ascription is often confused with type annotation, as the syntax in Scala
is identical.  The following are examples of ascription:

* ``Nil: List[String]``
* ``Set(values: _*)``
* ``"Daniel": AnyRef``

Ascription is basically just an up-cast performed at compile-time for the sake of
the type checker.  Its use is not common, but it does happen on occasion.  The
most often seen case of ascription is invoking a varargs method with a single
``Seq`` parameter.  This is done by ascribing the ``_*`` type (as in the second
example above).

Ascription follows the type annotation conventions; a space follows the colon.

