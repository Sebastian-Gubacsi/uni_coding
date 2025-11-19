# Texture mapping

## About

This project presents examples of using textures in graphics. 

In addtion, it also shows how to load and play sounds in programs. 

Folders:

- src : contains the main program texture_sound.cpp
- texture : contains texture and sound files 


## Build, Run, and test

It includes a `makefile` that builds `src/texture_sound.cpp` into its executable `texture.exe` 

Build all examples:
```bash
make
```

Build a single example (e.g. koch_curve.exe):
```bash
make texture.exe
```

Build and run a single example using the provided run helper:
```bash
make run
```

Run an executable directly (after building):
```bash
./texture.exe
```

Tests: 

- Right click mouse to bring up menu. 
- Use R or L key to rotate the object.
- Start/stop playing sound. 


Remove all built executables:
```bash
make clean
```
