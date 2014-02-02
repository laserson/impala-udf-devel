impala-udf-devel
================

Impala SDK for UDF development.

This package is especially geared for people developing on OS X.


### Installation and dependencies

*OS X*

The easiest way to install is `brew install impala-udf-devel` using the homebrew
package manager.

Note: the built-in LLVM might be quite old, but it could be problematic
to upgrade the system-wide LLVM.  If you're using the homebrew package manager,
installing a newer LLVM is keg-only and does not get placed on the path.  You
can access the newer LLVM executables (e.g., `clang`) at `$(brew --prefix
llvm)/bin`.

*Other systems*

```bash
git clone https://github.com/laserson/impala-udf-devel
cd impala-udf-devel
# ensure impala_udf/udf.h is somewhere on the build path
```


### How to use

To build a UDF/UDA, you need to include `impala_udf/udf.h` in your source files.
You can find some more extensive examples of writing C++ UDFs for Impala
[here][1].  Once you're ready to build, look at the included `CMakeLists.txt`
file.  After customizing it appropriately for your environment, run

```bash
cmake .
make
```

to build your UDF.  Copy the LLVM IR `.ll` file into a suitable location in HDFS
in preparation for the `CREATE FUNCTION` statement.  Do *not* copy the machine
code into HDFS (`.so` or `.dylib`) as it may be built for the wrong
architecture.


[1]: https://github.com/cloudera/impala-udf-samples
