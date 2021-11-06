[Conan](https://conan.io/) can be used to install Abseil,
which can then be consumed by CMake using `find_package`.
This process doesn't require manually specifying Abseil's exports.

```
conan install . --install-folder build/conan
# The above step will install Abseil into a global cache
# and reference that. So deleting the build directory will
# still give a cache hit.
# Under build/conan, it will install CMake configuration
# which can be consumed by the current project's CMake.

cmake -G Ninja -S . -B build -DEXPORT_MYSTATICLIB=ON
cmake --build build
```

Using Conan involves a few small changes to the CMake configuration,
as well as a small configuration file `conanfile.txt`.

I followed the [Conan instructions for find_package()](https://docs.conan.io/en/latest/integrations/build_system/cmake/cmake_find_package_generator.html#in-a-conanfile-txt).
