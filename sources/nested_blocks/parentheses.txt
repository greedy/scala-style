Parentheses
-----------

In the rare cases when parenthetical blocks wrap across lines, the opening and
closing parentheses should be unspaced and kept on the same lines as their content
(Lisp-style)::
    
    (this + is a very ++ long *
      expression)
      
The only exception to this rule is when defining grammars using parser combinators::
    
    lazy val e: Parser[Int] = (
        e ~ "+" ~ e  ^^ { (e1, _, e2) => e1 + e2 }
      | e ~ "-" ~ e  ^^ { (e1, _, e2) => e1 - e2 }
      | """\d+""".r  ^^ { _.toInt }
    )
    
Parser combinators are an internal DSL, however, meaning that many of these style
guidelines are inapplicable.


