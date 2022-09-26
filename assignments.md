---
title: Assignments
headerImg: angles.jpg
---

**LATE POLICY:** You have a total of **4** late days that can be used 
in atomic units over the entire quarter. By "atomic" I mean, for example, 
that 35 mins over the deadline is equal to 1 late day.

## Assignment Links

COMING SOON

<!-- - [00-lambda](https://classroom.github.com/a/PwNVGSom), due **10/8 at 23:59:59**
- [01-trees](https://classroom.github.com/a/EKaa5k6e), due **10/22 at 23:59:59**
- [02-while](https://classroom.github.com/a/apPaNw-v), due **11/12 at 23:59:59** -->
 
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
can use the CSE 230 VM (COMING SOON).

