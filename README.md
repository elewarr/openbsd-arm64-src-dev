# Use with care!
####  Please, do not use kernel with these patches on a board without proper cooling!
#### I'm not responsible for any damage.
#### Please, review the code before use.

---
#### Description
This is set of scripts for OpenBSD kernel development (huge words for just some humble attempts) for Pine A64+ arm64 boards. 

_Please note, some things may also work for other Sunxi boards but it was never tested._

With u-boot from this repository: https://github.com/elewarr/openbsd-ports-u-boot, A64 is able to:
1. read CPU/GPU temperature properly
1. adjust CPU speed (review u-boot patches for details) using `apm`, please note *throttling is not supported at the moment*, set desired value using `apm` manually

#### Environment
1. `env` - setup basic environment (*review before use*)
1. `bin/` - scripts
1. `build_cross_tools` - build toolset necessary to crosscompile kernel
1. `build_kernel` - build `GENERIC.MP`
1. `deploy` - copy new kernel over ssh and install it, also write u-boot SPL
1. `checkout` - repo from cvs
1. `cross_env` - environment used by `build_kernel`
1. `patch` - apply all `*.patches` from `patches/`
1. `update` - repo from cvs
1. `update-patches` - diff all modified files with their `*.orig` counterparts and put to `patches/`
1. `patches/` - A64 patches

#### Prerequisites
1. build the port from https://github.com/elewarr/openbsd-ports-u-boot 
1. There is a problem with cross-tools compilation on LLVM 8: https://bugs.llvm.org/show_bug.cgi?id=42478

For now add following entries to `/etc/mk.conf`:
```
CXXFLAGS+=-O2
CPPFLAGS+=-O2
```
It's only required for `./bin/build_cross_tools`.

#### Setup
1. `git clone git@github.com:elewarr/openbsd-arm64-src-dev.git`
1. `cd openbsd-arm64-src-dev`
1. `. ./env`
1. `./bin/checkout`
1. `doas ./bin/build_cross_tools`

#### Apply patches
1. `./bin/patch`

#### Build kernel
1. `./bin/build_kernel`

### Deploy
*Review and edit `./env` before use.*
1. `./bin/deploy`

#### Generate new patches - one per file (*will overwrite existing ones*)
1. `./bin/make-patches`
