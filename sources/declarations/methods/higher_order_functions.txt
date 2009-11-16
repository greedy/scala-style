Higher-Order Functions
~~~~~~~~~~~~~~~~~~~~~~

It's worth keeping in mind when declaring higher-order functions the fact that
Scala allows a somewhat nicer syntax for such functions at call-site when the
function parameter is curried as the last argument.  For example, this is the
``foldl`` function in SML::
    
    fun foldl (f: ('b * 'a) -> 'b) (init: 'b) (ls: 'a list) = ...
    
In Scala, the preferred style is the exact inverse::
    
    def foldLeft[A, B](ls: List[A])(init: B)(f: (B, A) => B) = ...
    
By placing the function parameter *last*, we have enabled invocation syntax like
the following::
    
    foldLeft(List(1, 2, 3, 4))(0) { _ + _ }
    
The function value in this invocation is not wrapped in parentheses; it is
syntactically quite disconnected from the function itself (``foldLeft``).  This
style is preferred for its brevity and cleanliness.

