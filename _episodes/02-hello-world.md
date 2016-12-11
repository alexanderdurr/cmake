---
layout: episode
title: "Hello-world example"
teaching: 10
exercises: 0
questions:
  - "How are CMake projects configured and built?"
  - "What is an out of source compilation?"
objectives:
  - "Learn how to configure and build CMake projects."
keypoints:
  - "We always compile out of source."
  - "The name and path of the build directory can be changed."
  - "When configuring we point CMake at the location of the CMakeLists.txt file."
---

## Hello-world example

We start with a Fortran program:

```fortran
program hello

    implicit none

    print *, 'hello!'

end program
```

Create a fresh directory and save the Fortran code to a file called
`hello.f90`.

We wish to compile this code to `hello.x`.

For this we create a file called `CMakeLists.txt` which contains:

```cmake
# stop if cmake version is below 2.8
cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

# project name
project(hello)

# we enable Fortran support
enable_language(Fortran)

# we define the executable and its dependencies
add_executable(hello.x hello.f90)
```

Now we create a build directory (out of source compilation), change to it,
and configure the project:

```shell
$ mkdir build
$ cd build/
$ cmake ..

-- The C compiler identification is GNU 6.2.1
-- The CXX compiler identification is GNU 6.2.1
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- The Fortran compiler identification is GNU 6.2.1
-- Check for working Fortran compiler: /usr/bin/gfortran
-- Check for working Fortran compiler: /usr/bin/gfortran  -- works
-- Detecting Fortran compiler ABI info
-- Detecting Fortran compiler ABI info - done
-- Checking whether /usr/bin/gfortran supports Fortran 90
-- Checking whether /usr/bin/gfortran supports Fortran 90 -- yes
-- Configuring done
-- Generating done
-- Build files have been written to: /home/user/example/build
```

Now we are ready to compile the code:

```shell
$ make

Scanning dependencies of target hello.x
[ 50%] Building Fortran object CMakeFiles/hello.x.dir/hello.f90.o
[100%] Linking Fortran executable hello.x
[100%] Built target hello.x
```

Done. In the following we will learn what happened here behind the scenes.

---

## Name and location of the build directory

We have configured and compiled the code like this:

```shell
$ mkdir build
$ cd build/
$ cmake ..
$ make
```

But there is nothing special about `build/` - we could have done this instead:

```shell
$ mkdir -p /tmp/debug
$ cd /tmp/debug
$ cmake /path/to/source
$ make
```

- CMake looks for `CMakeLists.txt` and processes this file
- CMake puts everything into `${PROJECT_BINARY_DIR}` and does not pollute `${PROJECT_SOURCE_DIR}`
- We can build different binaries with the same source:
  - Sequential and parallel builds
  - Debug build or optimized build
  - Production and debugging compilations