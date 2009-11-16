Type Parameters (generics)
--------------------------

Type parameters are typically a single upper-case letter (from the English
alphabet).  Conventionally, parameters blindly start at ``A`` and ascend up to
``Z`` as necessary.  This contrasts with the Java convention of using ``T``, ``K``,
``V`` and ``E``.  For example::
    
    class List[A] {
      def map[B](f: A => B): List[B] = ...
    }

.. toctree::

   higher_kinds
