Curly-Braces
------------

Curly-braces should be omitted in cases where the control structure represents
a pure-functional operation and all branches of the control structure (relevant
to ``if``/``else``) are single-line expressions.  Remember the following guidelines:

* ``if`` - Omit braces if you have an ``else`` clause.  Otherwise, surround the
  contents with curly braces even if the contents are only a single line.
* ``while`` - Never omit braces (``while`` cannot be used in a pure-functional manner).
* ``for`` - Omit braces if you have a ``yield`` clause.  Otherwise, surround the
  contents with curly-braces, even if the contents are only a single line.
* ``case`` - Omit braces if the ``case`` expression fits on a single line.  Otherwise,
  use curly braces for clarity (even though they are not *required* by the parser).
  
::
    
    val news = if (foo)
      goodNews()
    else
      badNews()
    
    if (foo) {
      println("foo was true")
    }
    
    news match {
      case "good" => println("Good news!")
      case "bad" => println("Bad news!")
    }


