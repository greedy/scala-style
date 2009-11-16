Methods with Numerous Arguments
-------------------------------

When calling a method which takes numerous arguments (in the range of five or
more), it is often necessary to wrap the method invocation onto multiple lines.
In such cases, the wrapped lines should be indented so that each parameter lines
up with the first::
    
    foo(someVeryLongFieldName,
        andAnotherVeryLongFieldName,
        "this is a string",
        3.1415)
        
Great care should be taken to avoid these sorts of invocations well into the
length of the line.  More specifically, such an invocation should be avoided
when each parameter would have to be indented more than 50 spaces to achieve
alignment.  In such cases, the invocation itself should be moved to the next
line and indented two spaces::
    
    // right!
    val myOnerousAndLongFieldNameWithNoRealPoint = 
      foo(someVeryLongFieldName,
          andAnotherVeryLongFieldName,
          "this is a string",
          3.1415)
    
    // wrong!
    val myOnerousAndLongFieldNameWithNoRealPoint = foo(someVeryLongFieldName,
                                                       andAnotherVeryLongFieldName,
                                                       "this is a string",
                                                       3.1415)
                                                       
Better yet, just try to avoid any method which takes more than two or three
parameters!


