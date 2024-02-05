CMake Visibility vs Linkage Demo
================================

This is a playground for demonstrating symbol visibility conflicts between libraries in cmake
and ways to resolve them, e.g by using PUBLIC/PRIVATE visibility tags on links.

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

But can you still see *their* symbols?


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
