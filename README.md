# Super Smash Bros. 64 Decompilation

- SHA1: `e2929e10fccc0aa84e5776227e798abc07cedabf`
- MD5: `f7c52568a31aadf26e14dc2b6416b2ed`

To set up and build the rom, see below

## Clone this branch

`git clone --single-branch --branch main https://github.com/VetriTheRetri/ssb-decomp-re.git`

## Install dependencies

`bash ./installDependencies.sh`

This script will also tell you where to place the ROM in case it's not found in the right location (`<repo root>/baserom.us.z64`). Having the ROM there is required to be able to run `make extract` which extracts assembly and assets from the ROM.

## Extract files, and run the initial build

`make init` or `make clean && make extract && make`

Extracting is required every time the splat yaml (`smashbrothers.us.yaml` of `smashbrothers.jp.yaml`) file is modified or anything inside the `symbols` folder (which is used by splat). So it's recommended to run `make init` every time you pull changes.

## Build the ROM

`make`

or with parallel jobs for faster build: `make -j$(nproc)`

## Build With Docker

This repository includes a Docker-based build path so you can build without installing host dependencies.

1. Build the image:
`make docker-image`
2. Put the base ROM at `<repo root>/baserom.us.z64` (or `baserom.jp.z64` for JP).
3. Run initial extract + build:
`make docker-init`
4. Run regular ROM builds:
`make docker-rom`

Use JP with `VERSION=jp`, for example:
`make VERSION=jp docker-init`
`make VERSION=jp docker-rom`

The built ROM is written to `build/smashbrothers.<version>.z64` in your local repo directory.

### MacOS specific

- MIPS binutils can be obtained from [macports](https://ports.macports.org/port/mips-elf-binutils/)
- GNU make can be obtained from [macports](https://ports.macports.org/port/gmake/)

## Debugging
There's a few handy scripts to help with debugging non matches after making changes.

| Tool           | Details                                                                |
|----------------|------------------------------------------------------------------------|
|`first_diff.py` | Finds the location, and cause of most diffs from the baserom           |
|`livediff.sh`   | Run it with the function you're looking to do some decomp work on<br />and it will set up a live diffing session where all changes saved will<br />automatically build and udpate the session. |
|`mips_to_c.sh`  | Pass a file, and function to this and have it generate all required<br />context, and a file in m2cfiles folder with the m2c output to start<br  />working with for matching purposes.         |
