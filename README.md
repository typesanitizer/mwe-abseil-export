The following works:

```
cmake -G Ninja -S . -B build -DABSL_ENABLE_INSTALL=ON
```

but the following doesn't

```
cmake -G Ninja -S . -B build -DABSL_ENABLE_INSTALL=ON -DEXPORT_MYSTATICLIB=ON
```

See the [conan](https://github.com/typesanitizer/mwe-abseil-export/tree/conan)
branch for a clean working solution.

The [fix-errors](https://github.com/typesanitizer/mwe-abseil-export/tree/fix-errors)
branch has a bad solution where I manually specify
a bunch of Abseil details manually. Don't do that.
