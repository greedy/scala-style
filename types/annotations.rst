Annotations
-----------

Type annotations should be patterned according to the following template::
    
    value: Type
    
This is the style adopted by most of the Scala standard library and all of
Martin Odersky's examples.  The space between value and type helps the eye in
accurately parsing the syntax.  The reason to place the colon at the end of the
value rather than the beginning of the type is to avoid confusion in cases such
as this one::
    
    value :::
    
This is actually valid Scala, declaring a value to be of type ``::``.  Obviously,
the prefix-style annotation colon muddles things greatly.  The other option is
the "two space" syntax::
    
    value : Type
    
This syntax is preferable to the prefix-style, but it is not widely adopted due
to its increased verbosity.


