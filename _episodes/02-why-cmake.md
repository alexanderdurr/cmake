---
layout: episode
title: "Why CMake?"
teaching: 5
exercises: 0
questions:
  - I am already using Makefiles, do I need CMake?
  - What are typical problems with Makefiles?
  - Why CMake and not Autotools?
  - I am a Python developer, is any of this relevant for me?
objectives:
  - Building software involves many layers of tools. The objective is to be able to place CMake in this stack.
keypoints:
  - CMake is not a replacement for Makefiles.
  - CMake can generate Makefiles.
  - CMake is an alternative to Autotools.
---

## Why is Make not enough?

- Make knows about targets and dependencies
- Make does not know which compiler (options) we want and which environment we are on

---

## About [CMake](https://cmake.org)

- Cross-platform
- Open-source
- [Actively developed](https://github.com/Kitware/CMake)
- Manages the build process in a compiler-independent manner
- Designed to be used in conjunction with the native build environment
- Written in C++ (does not matter but if you want to build CMake yourself, C++ is all you need)
- CMake is a generator - this means it does not compile the code
- Not a replacement for Makefiles, rather a replacement for Autotools

---

## Why CMake?

Separation of source and build path:

- **Out-of-source compilation** (possibility to compile several builds with the same source)

Portability:

- Really **cross-platform** (Linux, Mac, Windows, AIX, iOS, Android)
- CMake defines portable variables about the system
- Cross-platform system- and library-discovery

Language support:

- Excellent support for **Fortran, C, C++**, and Java, as well as mixed-language projects
- CMake understands Fortran 90 dependencies very well; no need to program a dependency scanner
- Excellent support for multi-component and multi-library projects

Supports modular code development:

- Makes it possible and relatively easy to download, configure, build, install, and link **external modules**

Provides tools:

- Generates user interface (command-line or text-UI or GUI)
- Full-fledged **testing and packaging framework** with CTest and CPack
- CTest can run sequential tests in parallel

Popular:

- CMake is used by **many prominent projects**:
  MySQL, Boost, VTK, Blender, KDE, LyX, Mendeley, MikTeX, Compiz,
  Google Test, ParaView, Second Life, Avogadro, and many more ...

General:

- Not bound to the generation of Makefiles

---

## Note to Python developers

One day you might need to implement low-level operations to your Python library
in Fortran or C or C++ and then CMake can come in handy.
