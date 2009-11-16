Trivial Conditionals
--------------------

There are certain situations where it is useful to create a short ``if``/``else``
expression for nested use within a larger expression.  In Java, this sort of
case would traditionally be handled by the ternary operator (``?``/``:``), a
syntactic device which Scala lacks.  In these situations (and really any time
you have a extremely brief ``if``/``else`` expression) it is permissible to place
the "then" and "else" branches on the same line as the ``if`` and ``else``
keywords::
    
    val res = if (foo) bar else baz
    
The key here is that readability is not hindered by moving both branches inline
with the ``if``/``else``.  Note that this style should never be used with
imperative ``if`` expressions nor should curly braces be employed.

