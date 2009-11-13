Type Parameters (generics)
--------------------------

Type parameters are typically a single upper-case letter (from the English
alphabet).  Conventionally, parameters blindly start at ``A`` and ascend up to
``Z`` as necessary.  This contrasts with the Java convention of using ``T``, ``K``,
``V`` and ``E``.  For example::
    
    class List[A] {
      def map[B](f: A => B): List[B] = ...
    }

Higher-Kinds
~~~~~~~~~~~~

While higher-kinds are theoretically no different from regular type parameters
(except that their kind_ is at least ``*=>*`` rather than simply ``*``), their
naming conventions do differ somewhat.  Generally, higher-kinded parameters are
two upper-case characters, usually repeated.  For example::
    
    class HOMap[AA[_], BB[_]] { ... }
    
It is also (sometimes) acceptable to give full, descriptive names to higher-kinded
parameters.  Thus, the following would be an equally valid definition of ``HOMap``::
    
    class HOMap[Key[_], Value[_]] { ... }
    
In such cases, the type naming conventions should be observed.


