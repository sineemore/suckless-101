suckless-101
============

Guide on how to patch, compile and install suckless software.

Table of contents:

* [Introduction](#introduction)
* [Git](#git)
* [Toolchain](#toolchain)
* [Manual pages](#manual-pages)
* [Getting the source](#getting-the-source)
* [Dependencies](#dependencies)
* [Compiling](#compiling)
* [Installing](#installing)
* [Patching](#patching)

## Introduction

The guide explains how to patch, compile and install suckless software.

There are several topics on installing C compiler toolchain, getting
dependencies and succesfully compiling the software.

`dwm` is used for examples.

## Git

*to be written*

## Toolchain

To successfully compile program source code you need to have a C
compiler and several other tools installed on your systems:

* C compiler `gcc`, `clang` or `tcc`
* `git`
* `make`
* `pkg-config`
* `patch`

Some distributions provide a package that includes most of the desired
tools:

* `base-devel` in Void Linux, Arch Linux
* `build-essential` in Debian, Ubuntu

You may find similar packages for other Linux distributions by
searching for "build-essential equivalent [DISTRO NAME]".

After you've installed required tools ensure all of them present:

    $ which gcc git make pkg-config patch
    /usr/bin/gcc
    /usr/bin/git
    /usr/bin/make
    /usr/local/bin/pkg-config
    /usr/bin/patch

## Manual pages

To get documentation for installed programs use `man`:

    $ man patch

Most manual pages you will read with `man` will include a program
description and comprehensive guide on command line parameters and
configuration options.

An important plus of reading man pages locally is that the manual page
will provide documentation of the actual program you have installed and
not some other older/newer version of it.

## Getting the source

After installing required tools you may continue with cloning the
program source code.

To get the source code of `dwm` use `git`:

    $ git clone https://git.suckless.org/dwm
    
You may find source code of other programs by browsing suckless git
repositories:

https://git.suckless.org/

## Dependencies

Programs you have on your system require runtime and build
dependencies. When using package manager to install software required
dependencies are installed automatically.

Before compiling the progran tools you'll need to install dependencies
by hand.

To find required dependencies examine `config.mk` and `Makefile`.

For example `dwm` dependencies on Void Linux are satisfied by the
following packages:

* libX11-devel
* libXft-devel
* libXinerama-devel

**NOTE:** It is important to install development variants of packages
to get C header files required for compiling the source code.

Another way to find dependencies would be to examine compile errors.
Here error text says that `Xft.h` header file is missing:

    drw.c:6:10: fatal error: X11/Xft/Xft.h: No such file or directory
        6 | #include <X11/Xft/Xft.h>
        |          ^~~~~~~~~~~~~~~

Examine each error to find a name of a missing C header file and
install the package which provides it.

One way to quickly locate the desired package is by using a package
manager or separate utility to search packages by filenames it
contains.

For example on Void Linux such program can be installed with `xtools`
package:

    $ xlocate Xft.h
    libXft-devel-2.3.3_1	/usr/include/X11/Xft/Xft.h

## Compiling

To compile a program run `make` in its root directory:

    $ make

## Installation

## Patching
