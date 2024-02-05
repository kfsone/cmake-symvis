CMake Visibility vs Linkage Demo
================================

This demonstrates how to resolve conflicts between libraries by using PUBLIC/PRIVATE
specs on imports.

```cmake
target_link_libraries (mylib yourlib)
```

defaults to 'PUBLIC', which means any symbols in `yourlib` will be exposed in the export table
of `mylib`, and also all the compiler properties/flags/include paths/etc.

```cmake
target_link_libraries (mylib PRIVATE yourlib)
```

means that I will be a full consumer of yourlib still, but the linker will not expose its symbols
upstream.


Instructions
============

Clone the repository and cmake-configure:

```sh
cmake -G Ninja -B build -S .
#                        ^- source from this directory (where CMakeLists.txt is),
#               ^- use './build' as the cmake cache/build directory,
#      ^- optionally specify the project generator to use
```

Attempt to build:

```sh
cmake --build build  # assuming you used '-B build',
# cmake --build output  # if you used '-B output' instead, e.g
```

How to fix the error
--------------------

The setup simulates a mix of 1st/3rd party libraries, and as such both libc and libe define a
`void terminal()` method outside of namespaces. Our compilation wants to use the libc 'terminal',
but when we try to use it the compiler recognizes a conflict between that and a symbol in the
'libe' library used by 'libd'.

In this scenario, we don't *want* anyone to see the internals of whatever libd uses, so we
can make it a PRIVATE linkage.
