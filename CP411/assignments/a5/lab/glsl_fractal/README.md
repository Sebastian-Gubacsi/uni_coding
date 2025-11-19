## Hand on Fractal computing by GLSL

### About

This glsl_fractal project contain examples of  fractal computing using GLSL. 

Examples are from Interactive Computer Graphics: A Top-Down Approach with Shader-Based OpenGL (6th Edition) Edward Angel (Author), Dave Shreiner (Author)

It contains the following examples

1. julia_bitmap.cpp : Julia set, dispaly by openGL bitmap
2. julia_texture.cpp : Julia set, dispaly by openGL texture   
3. koch_curve.cpp : koch curve
4. landscape.cpp : middle point 
5. mandelbrot.cpp : Mandelbrot set
6. sierpinski_iterate.cpp  : sierpinski gasket generate by iterations 
7. sierpinski_ran.cpp  :  fsierpinski gasket generate by random approach 
8. sirerpinski_gasket_3d.cpp : 3D sierpinski gasket

 
## Build, Run, and Clean (using the Makefile)

The repository includes a `makefile` that builds each example in `src/` into its own executable (e.g. `koch_curve.exe`). 

Build all examples:
```bash
make
```

Build a single example (e.g. koch_curve.exe):
```bash
make koch_curve.exe
```

Build and run a single example using the provided run helper:
```bash
make run-koch_curve
```

Run an executable directly (after building):
```bash
./koch_curve.exe
```

Remove all built executables:
```bash
make clean
```
