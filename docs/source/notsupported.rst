.. _notsupported:

Not Supported Python Programs
=============================

HPAT statically compiles user codes to generate efficient parallel programs.
Hence, the user code needs to be `statically compilable`.
This means that HPAT should be able to infer all the variable types, and be able
to analyze the computations.

Type Stability
--------------

To enable type inference, the program should be `type stable`, which means every
variable should have a single type. The example below is not type stable since
variable ``a`` can be both a float and an array of floats::

    if flag:
        a = 1.0
    else:
        a = np.ones(10)

The use of ``isinstance`` operator of Python often means type instabillity and
is not supported.

Similarly, function calls should also be deterministic. The below example is
not supported since function ``f`` is not known in advance::

    if flag:
        f = np.zeros
    else:
        f = np.random.ranf
    A = f(10)

One can usually avoid these cases in numerical code without significant effort.
