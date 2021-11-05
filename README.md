The following works:

```
cmake -G Ninja -S . -B build -DABSL_ENABLE_INSTALL=ON
```

but the following doesn't

```
cmake -G Ninja -S . -B build -DABSL_ENABLE_INSTALL=ON -DEXPORT_MYSTATICLIB=ON
```
