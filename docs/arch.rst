Architecture
============

pikepdf uses `pybind11 <https://github.com/pybind/pybind11>`_ to bind the
C++ interface of QPDF. pybind11 was selected after evaluating Cython, CFFI and
SWIG as possible binding solutions.

In addition to bindings pikepdf includes support code written in a mix of C++
and Python, mainly to present a clean Pythonic interface to a C++.

Internals
---------

Internally the package presents a module named ``pikepdf`` from which objects
can be imported. The C++ extension module is currently named ``pikepdf._qpdf``.
Users of ``pikepdf`` should not directly access to ``_qpdf`` as it is
subject to change at any time.

Thread safety
-------------

Because of the global interpreter lock (GIL), it is safe to share pikepdf
objects across Python threads. Also because of the GIL, there may not be much
performance gain from doing so.

If one or more threads will be modifying pikepdf objects, you will have to
coordinate all read and write access with a :class:`threading.Lock`.

It is not currently possible to pickle pikepdf objects or marshall them across
process boundaries (as would be required to use pikepdf in
:mod:`multiprocessing`). If this were implemented, it would not be much more
efficient than saving the file and sending it to another process.
