# Hands-on GLSL programming

## About

This `glsl_cube` project contains GLSL examples that draw a cube. Examples are adapted from "Interactive Computer Graphics: A Top-Down Approach with Shader-Based OpenGL" (Edward Angel & Dave Shreiner).

## Prerequisites
- A C++ compiler (e.g. `g++`)
- Make (GNU make)
- OpenGL development libraries and headers (platform dependent)
	- On Windows with MinGW: `-lfreeglut -lopengl32 -lglu32 -lglew32` (used in the Makefile)
	- On Linux: you may need `-lGL -lGLU -lglut -lGLEW`

## Build, Run, and Clean (using the Makefile)

The repository includes a `makefile` that builds each example in `src/` into its own executable (e.g. `cube1.exe`). From the project root (`work/assignments/a5/lab/glsl_cube`) use:

Build all examples:
```bash
make
```

Build a single example (e.g. cube3):
```bash
make cube3.exe
```

Build and run a single example using the provided run helper:
```bash
make run-cube3
```

Run an executable directly (after building):
```bash
./cube3.exe
```

Remove all built executables:
```bash
make clean
```

Notes:
- The Makefile links all `src/glsl/*.cpp` files into each example. If you modify those shared sources, re-run `make` to rebuild targets.
- If you are on a different platform, update the linker flags in the Makefile to match your environment.
