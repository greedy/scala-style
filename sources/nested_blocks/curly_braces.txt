Curly Braces
------------

Opening curly braces (``{``) must be on the same line as the declaration they
represent::
    
    def foo = {
      ...
    }
    
Technically, Scala's parser *does* support GNU-style notation with opening braces
on the line following the declaration.  However, the parser is not terribly
predictable when dealing with this style due to the way in which semi-colon
inference is implemented.  Many headaches will be saved by simply following the
curly brace convention demonstrated above.


