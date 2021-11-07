suckless-101
============

Guide on how to patch, compile and install suckless software.

Table of contents:

* [Introduction](#introduction)
* [Toolchain](#toolchain)
* [Manual pages](#manual-pages)
* [Getting the source](#getting-the-source)
* [Dependencies](#dependencies)
* [Compiling](#compiling)
* [Installation](#Installation)
* [Patching](#patching)
* [Customization](#customization)

## Introduction

The guide explains how to patch, compile and install suckless software.

`dwm` is used for examples.

## Toolchain

To successfully compile program source code you'll need a C
compiler and several other tools installed on your system:

* C compiler `gcc`, (`clang` or `tcc` should work as well)
* `git`
* `make`
* `pkg-config`
* `patch`

Some distributions provide a package that includes most of the desired
tools:

* `base-devel` in Void Linux, Arch Linux
* `build-essential` in Debian, Ubuntu

You may find similar packages for other Linux distributions by
searching for _"build-essential equivalent [DISTRO NAME]"_.

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
    
You may find source code for other programs by browsing suckless git
repositories:

https://git.suckless.org/

## Dependencies

To compile program you'll need to install runtime and build dependencies.

To find required dependencies examine `config.mk` and `Makefile`.

For example `dwm` dependencies on Void Linux are satisfied by the
following packages:

* libX11-devel
* libXft-devel
* libXinerama-devel

**NOTE:** It is important to install development variants of packages
to get C header files. These files are required to compile the source code.

Another way to find dependencies would be to examine compile errors.
Here error text says that `Xft.h` header file is missing:

    drw.c:6:10: fatal error: X11/Xft/Xft.h: No such file or directory
        6 | #include <X11/Xft/Xft.h>
        |          ^~~~~~~~~~~~~~~

Examine each error to find a name of a missing C header file and
install the package which provides it.

One way to quickly locate the desired package is by using a package
manager or a separate utility to search packages by filenames they
contain.

For example on Void Linux such program can be installed with `xtools`
package:

    $ xlocate Xft.h
    libXft-devel-2.3.3_1	/usr/include/X11/Xft/Xft.h

## Compiling

To compile a program run `make` in its root directory:

    $ make

In case of compilation errors:

* check that required build tools present,
* check missing dependencies.

## Installation

Most suckless software will have a Makefile target to install built binaries,
man files, etc.

To install in home directory run

    $ make PREFIX=$HOME/.local/ install

This way you won't need root rights and program files won't mess with system
files. This is a prefered way to install built software.

**NOTE:** You'll need to add `$HOME/.local/bin` to your PATH variable.

---

To install system-wide run

    # make install

> Here `#` in front of command meens a root shell.
> Run such commands as root user (with `sudo` for example).


## Patching

Patches are files that tell the differences between two files. With the
difference, you can, for instance, include lines in a source code that create
new functionality.

There are lots of patches available for various suckless programs. You can find
patches for `dwm` and others by browsing the website:

https://tools.suckless.org/dwm/patches/

Download patch file with `curl`:

    $ curl -O https://dwm.suckless.org/patches/alpha/dwm-alpha-20201019-61bb8b2.diff

Apply downloaded patch file with `patch` tool:

    $ patch -i dwm-alpha-20201019-61bb8b2.diff

Don't forget to rebuild and install program after you've made changes to source
code.

Some patches will change `config.def.h` file. This file is copied by Makefile
once to `config.h` file. Remove `config.h` and run `make` or run `make -B`.
**Note:** any changes you've made in config.h will be lost.

In case you feel you are totally messed something run

    $ git checkout .

to undo changes made by patches (and you).

Another way to manage patches is by using git branches.


## Customization

Most suckless programs are customized by editing source code or `config.h` file:

https://dwm.suckless.org/customisation/

Don't forget to rebuild and install program after you've made changes to source
code.
