---
title: Assignments
headerImg: angles.jpg
---

**LATE POLICY:** You have a total of **4** late days that can be used 
in atomic units over the entire quarter. By "atomic" I mean, for example, 
that 35 mins over the deadline is equal to 1 late day.

## Assignment Links

- [00-lambda](https://classroom.github.com/a/ggXupoII), due **10/7 at 23:59:59**
- [01-trees](https://classroom.github.com/a/GaWjIp0f), due **10/28 at 23:59:59**
- [02-while](https://classroom.github.com/a/1C30HWpM), due **11/18 at 23:59:59**
- [03-transformers](https://classroom.github.com/a/d82naey0), due **12/2 at 23:59:59**
 
## Haskell Installation Guide

**Per OS Instructions**

- Windows: install [WSL2](https://learn.microsoft.com/en-us/windows/wsl/install). You will first install the Windows Subsystem for Linux (WSL), with the administrator-level command `wsl --install`. Once you restart, then ensure you are using version 2, with `wsl -l -v`. If you haven't used this before, you are likely already on WSL2. If not, [check this link to see how to upgrade from 1 to 2](https://learn.microsoft.com/en-us/windows/wsl/install).
- MacOS: Ensure you've agreed to the XCode License agreements, to ensure you have `clang` and other build tools available. Simply run `xcode-select --install`
- Linux: You'll need some usual compiler tools, including `clang` and `nasm`. If you're on a Debian-like build, the `build-essential` package should suffice.

**General instructions**

1. Install [GHCup](https://www.haskell.org/ghcup/)
2. In a terminal, run: `ghcup tui`
3. **Install** and **set** these versions of the tools: 
	  1. `Stack`: 2.9.1
	  2. `HLS`: 1.8.0.0
	  3. `Cabal`: 3.6.2.0
	  4. `GHC`: 8.10.7

Once you have `GHC`, `Cabal`, and `Stack` installed,
you can edit your homework in your favorite text editor and build it by running `make`.
For best experience, we recommend using VSCode with the `Haskell` extension;
to make the extension work, you first need to install `HLS` via `ghcup` (see above).

## Virtual Machine

Those of you having trouble installing the Haskell tool chain 
can use the [CSE 230 VM](https://drive.google.com/file/d/16T2-Z7SbqUdLgOOr6wPTHRkxEkBTtXs3/view?usp=sharing).

