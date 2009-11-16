Higher-Kinds
~~~~~~~~~~~~

While higher-kinds are theoretically no different from regular type parameters
(except that their kind_ is at least ``*=>*`` rather than simply ``*``), their
naming conventions do differ somewhat.  Generally, higher-kinded parameters are
two upper-case characters, usually repeated.  For example::
    
    class HOMap[AA[_], BB[_]] { ... }
    
It is also (sometimes) acceptable to give full, descriptive names to higher-kinded
parameters.  In this case, use all-caps to make it clear you are not referring
to a class or trait.  Thus, the following would be an equally valid definition of ``HOMap``::
    
    class HOMap[KEY[_], VALUE[_]] { ... }
    
In such cases, the type naming conventions should be observed.

.. _kind: http://en.wikipedia.org/wiki/Kind_(type_theory)

