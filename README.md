triqs_arpack
============

C++ interface between ARPACK [1] and TRIQS arrays library [2].

Copyright (C) 2016-2017 by I. Krivenko

Dependencies
------------

* TRIQS library version 1.4 or newer;
* ARPACK library, preferably the latest ARPACK-NG version [3].

Installation
------------

This C++ interface is essentially a header-only wrapper.
Only the test programs require linking to the ARPACK library.

Installation is done in a few simple steps, assuming that TRIQS library is installed under `/path/to/triqs`:

```
$ git clone https://github.com/krivenko/triqs_arpack.git triqs_arpack.git
$ cd triqs_arpack.git
$ cmake -DTRIQS_PATH=/path/to/triqs .
$ make
$ make test
$ make install
```

Compilation of the tests can be disabled with CMake flag `-DTests=OFF` *(not recommended)*.

In case CMake fails to find ARPACK, you can give it a hint by passing an ARPACK installation prefix via `-DARPACK_DIR=/path/to/arpack`.

Usage
-----

Once **triqs_arpack** is installed, you can use it to build your TRIQS application.

Make sure to have the following lines somewhere in your `CMakeLists.txt` file.

```cmake
# Append TRIQS-installed CMake modules to the CMake search path
list(APPEND CMAKE_MODULE_PATH ${TRIQS_PATH}/share/triqs/cmake)

# Detect ARPACK
find_package(ARPACK REQUIRED)

# Add TRIQS include dirs
# triqs_arpack places its header files into the installation tree of TRIQS
include_directories(${TRIQS_INCLUDE_ALL})

# Link my_target to TRIQS and ARPACK
target_link_libraries(my_target ${TRIQS_LIBRARY_ALL} ${ARPACK_LIB})
```

In the C++ sources you can now include

```c++
// Version information of triqs_arpack
#include <triqs/arrays/arpack/version.hpp>

// C++ wrappers around FORTRAN procedures *aupd and *eupd
#include <triqs/arrays/arpack/arpack.hpp>

// arpack_worker: high level C++ interface to ARPACK
#include <triqs/arrays/arpack/arpack_worker.hpp>
```

Documentation
-------------

Not at the moment... :(

For the time being you are invited to use source files in `test/c++` as examples.

Acknowledgements
----------------

Special thanks to Michael Danilov <mike.d.ft402 (at) gmail ! com> for his contribution of `FindARPACK.cmake`.

[1]: http://www.caam.rice.edu/software/ARPACK/
[2]: https://triqs.ipht.cnrs.fr/1.x/index.html
[3]: https://github.com/opencollab/arpack-ng
