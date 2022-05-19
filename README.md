                           GLVis visualization tool

                     _/_/_/  _/      _/      _/  _/
                  _/        _/      _/      _/        _/_/_/
                 _/  _/_/  _/      _/      _/  _/  _/_/
                _/    _/  _/        _/  _/    _/      _/_/
                 _/_/_/  _/_/_/_/    _/      _/  _/_/_/

                             https://glvis.org

Math test: $x^2+y^2$

[GLVis](https://glvis.org) is an OpenGL tool for visualization of
finite element meshes and functions. It is a multiplatform OpenGL
application that can be built on Linux/Unix systems, including Mac OS
X, and under Windows. It can also be used in a Jupyter notebook, or in
a web browser, see https://glvis.org/live.

For building instructions, see the file [INSTALL](INSTALL). Copyright
information and licensing restrictions can be found in the file
[COPYRIGHT](COPYRIGHT).

When started without any options, glvis starts a server which waits
for a socket connections (on port `19916` by default) and visualizes
any received data. This way the results of simulations on a remote
(parallel) machine can be visualized on the local user desktop.

GLVis can also be used to visualize a mesh with or without a finite
element function (solution), as in

```
glvis -m cube.mesh3d
```

For parallel computations, GLVis supports input from several parallel
socket connections as well as the visualization of parallel meshes and
grid functions saved in separate files from the command line as in

```
glvis -np 4 -m mesh -g solution
```

In both cases, it will stitch the results to show the global mesh and
solution. GLVis can also run a batch sequence of commands (GLVis
scripts), or display previously saved socket streams.

For a complete list of command line options, type

```
glvis -h
```

Depending on the data type, variety of manipulations can be performed
by using the mouse and by typing (case sensitive) keystrokes in the
GLVis window. Below is a partial list of the available
functionality. Some of these keys can also be provided as input, using
the `-k` command-line option and the `keys` script command.

GLVis is distributed under the terms of the BSD-3 license. All new
contributions must be made under this license. See [LICENSE](LICENSE)
and [NOTICE](NOTICE) for details.

SPDX-License-Identifier: BSD-3-Clause\
LLNL Release Number: LLNL-CODE-443271\
DOI: 10.11578/dc.20171025.1249


Mouse functions
===============

Button            | Description
----------------- | -----------
<kbd>Left</kbd>   | Rotate the viewpoint
<kbd>Middle</kbd> | Translate the viewpoint
<kbd>Right</kbd>  | Zoom in (up) / Zoom out (down)
<kbd>Left</kbd> + <kbd>Shift</kbd> | Start spinning the viewpoint (according to the dragging vector)


Basic key commands
==================

Key          |  Description
------------ | ------------
<kbd>h</kbd> | Prints a short help message in the terminal
<kbd>r</kbd> | Reset the plot to 3D view
<kbd>R</kbd> | Cycle through the six 2D projections<br> (camera looking above/below in `x`/`y`/`z` directions)
<kbd>j</kbd> | Turn on/off perspective
<kbd>s</kbd> | Turn on/off unit cube scaling
<kbd>c</kbd> | Toggle the colorbar and caption display state
<kbd>C</kbd> | Change the main plot caption
<kbd>p</kbd> / <kbd>P</kbd> | Cycle forward/backwards through color palettes<br> (lots of options, use <kbd>F6</kbd> for a menu)
<kbd>t</kbd> | Cycle materials and lights (5 states)
<kbd>l</kbd> | Turns on/off the light
<kbd>g</kbd> | Toggle background color (white/black)
<kbd>a</kbd> | Toggle the bounding box _axes_. The options are: <br>:white_small_square: none <br>:white_small_square:  bounding box with coordinates of the corners <br>:white_small_square: bounding box without coordinates <br>:white_small_square:  red, green, blue colored main `x`, `y`, `z` axes + dashed axes
<kbd>m</kbd> | Toggle the _mesh_ state. The options are: <br>:white_small_square: no mesh or level lines <br>:white_small_square: draw the element edges (i.e. the mesh) <br>:white_small_square: draw the level lines (use <kbd>F5 </kbd> to modify the level lines)
<kbd>e</kbd> | Toggle the _elements_ state (see below for vector functions). The options are: <br>:white_small_square: show surface elements (corresponding to the function) <br>:white_small_square: show no surface elements <br>:white_small_square: show element attributes (2D) <br>:white_small_square: show element `det(J)` (2D) <br>:white_small_square: show element `1/det(J)` (2D) <br>:white_small_square: show element `kappa` (2D) <br>:white_small_square: show element `kappa + 1/kappa` (2D)
<kbd>S</kbd> | Take an image snapshot or record a movie (in spinning mode). <br> By default, the screenshots are taken in `png` format, using libpng. <br> When GLVis is compiled with `libtiff` support (see [INSTALL](INSTALL)) then the <br> screenshots are taken internally and saved in TIFF format (`.tif` extension). <br> If both of these options are disabled during the build process, GLVis will use <br> `SDL` to take screenshots in `bmp` format, which it will then convert to `png`<br> if ImageMagick's `convert` tool is available.
<kbd>G</kbd> | 3D scene export to [glTF format](https://www.khronos.org/gltf)
<kbd>Ctrl</kbd> + <kbd>p</kbd> | Print to a PDF file using `gl2ps`. Other vector formats (SVG, EPS) are also possible, but keep in mind that the printing takes a while and the generated files are big.
<kbd>q</kbd> | Exit


Advanced key commands
=====================
f - Change the shading type (the way the elements and mesh are drawn)
    The options are: -> one triangle / quad per element with a constant normal
                     -> one triangle / quad per element with normals averaged
                        at the vertices
                     -> multiple triangles / quads per element, also allowing
                        for the visualization of discontinuous functions and
                        curvilinear elements (use o/O to control subdivisions)

o/O - Control element subdivisions (2D)
      there are two subdivision factors: -> element subdivision factor s1
                                         -> boundary subdivision factor s2
O - Cycle through the "subdivision functions", (prints a message in the
    terminal when changed)
    The options are: -> Increase subdivision factor:      s1 += s2
                     -> Decrease subdivision factor:      s1 -= s2
                     -> Increase bdr subdivision factor:  s2++
                     -> Decrease bdr subdivision factor:  s2--
o - perform the current "subdivision function"

A - Turn on/off the use of anti-aliasing/multi-sampling
b - Toggle the boundary in 2D scalar mode.
    The options are: -> no boundary
                     -> black boundary
                     -> boundary colored with the boundary attribute
    Use Shift+F9/F10 to cycle through the boundary attributes.
L - Turn on/off logarithmic scale
\ - Set light source position (see Right+Shift)
* - Zoom in
/ - Zoom out
+ - Stretch in z-direction
- - Compress in z-direction
[ - Enlarge the bounding box (relative to the colorbar)
] - Shrink the bounding box (relative to the colorbar)
( - Shrink the visualization window
) - Enlarge the visualization window
. - Start/stop z-spinning (speed/direction can be controlled with '0'/'Enter')

arrow keys        - Manual rotation
1,2,3,4,5,6,7,8,9 - Manual rotation along coordinate axes
Ctrl+arrow keys   - Translate the viewpoint

Ctrl+o - Toggle an element ordering curve in 2D and 3D

i - Toggle cutting (clipping) plane in 2D
y/Y - Rotate cutting plane (theta) in 2D
z/Z - Translate cutting plane in 2D

n/N - Cycle through numberings.
      The options are: -> none
                       -> show element numbering
                       -> show vertex numbering

` - Toggle a ruler, with initial origin at the center of the bounding box. The
    origin can be later moved with '~'.
    The options are: -> none
                     -> coordinate axes lines
                     -> coordinate axes planes
~ - Enter new ruler origin

k/K - Adjust the transparency level.
      The balance of transparency can be further adjusted with ',' and '<'.

! - Toggle the use of (1D) texture (smooth interpolation of colors)
    The options are: -> use discrete texture, the number of colors used depends
                        on the current palette
                     -> use smooth texture (interpolated from current palette)

F3/F4 - Shrink/Zoom each element towards its center, to better visualize the
        different element shapes
Ctrl+F3/F4 - Cut the interiors of 3D faces to expose more of the mesh
F5 - Change the range and number of the level lines
F6 - Palette menu (negative repeat number flips the palette)
F7 - Change the minimum and maximum values
F8      - List of material subdomains to show
F9/F10  - Walk through material subdomains
F11/F12 - Shrink/Zoom material subdomains (to the centers of the attributes)
Shift+F7 - Set the bounding box from the terminal


Advanced mouse functions
========================
Middle+Ctrl       - Object translation (moves the camera left/right/up/down)
Middle+Ctrl+Shift - Object translation (turns the camera left/right/up/down)
Middle+Ctrl+Alt   - Moves the camera forward/backward (vertical mouse motion)
                    and tilts the camera left/right (horizontal mouse motion)
Right+Ctrl        - Object scaling (see also '[' and ']')
Left+Alt          - Tilt
Right+Shift       - Change light source position (see '\')


Vector data commands
====================
v - Toggle the "vector" state (uses vector subdivision factor, accept u/U)
    The options are: -> do not show vectors
                     -> show vectors as displacement
                     -> show vector field; vectors are uniformly scaled;
                        the color varies with the magnitude (or the current
                        "vector-to-scalar function", see keys u/U)
                     -> show vector field as above, but the vectors are scaled
                        proportionally to their magnitude
V - Change the scaling of the vectors relative to the default

d - Toggle the "displaced mesh" state: (see also keys 'n'/'b')
    The options are: -> do not show displaced mesh
                     -> show displaced mesh
                     -> assuming displacement field show deformation using
                        Cartesian lines
                     -> assuming displacement field show deformation using
                        polar lines
n - increase the displacement amount in 10% steps, wraps around from 100% to 0%
b - decrease the displacement amount in 10% steps, wraps around from 0% to 100%
B - Toggle the boundary in 2D vector mode

e - Toggle the "elements" state (vector data version)
    The options are: -> show surface elements corresponding to the current
                        "vector-to-scalar function"
                     -> do not show surface elements
                     -> assuming a displacement field show det(J)/det(J_d)
                     -> assuming a displacement field show det(J_d)/det(J)

u/U - Change the "vector-to-scalar function" and the vector subdivision factor
U - Toggle the functionality of 'u' (prints a message in the terminal when
    changed).
    The options are: -> Increase the vector subdivision factor
                     -> Decrease the vector subdivision factor
                     -> Cycle through "vector-to-scalar functions" choices:
                        -> magnitude:    sqrt(vx^2+vy^2)
                        -> direction from -pi to pi: atan2(vy,vx)
                        -> x-component:  vx
                        -> y-component:  vy
                        -> divergence:   div(v)
                        -> curl:         curl(v)  [skipped for H(div) elements]
                        -> anisotropy in grad(v)  [skipped for H(div) elements]

3D data commands
================
i   - Toggle cutting (clipping) plane
      The options are: -> none
                       -> cut through the elements
                       -> show only elements behind the cutting plane
I   - Toggle the cutting plane algorithm used when the option "cut through the
      elements" is selected. The two algorithms are:
         -> slower, more accurate algorithm for curved meshes (default)
         -> faster algorithm suitable for meshes with planar faces
x/X - Rotate cutting plane (phi)
y/Y - Rotate cutting plane (theta)
z/Z - Translate cutting plane
E   - Display/Hide the elements in the cutting plane
M   - Display/Hide the mesh in the cutting plane

o/O - Refine/de-refine elements

u/U - Move level surface value up/down
v/V - Add/Delete a level surface value

w/W - Move boundary elements up/down in direction of the normal (i.e. "plot"
      the boundary values in normal direction)

F3/F4   - Shrink/Zoom boundary elements (to the centers of the attributes)
F8      - List of boundary subdomains to show
F9/F10  - Walk through boundary subdomains
F11/F12 - Shrink/Zoom material subdomains (to the centers of the attributes)


3D vector data commands
=======================
v - Toggle the "vector" state
    The options are: -> do not show vectors
                     -> show vectors as displacement
                     -> show vector field; vectors are uniformly scaled;
                        the color varies with the magnitude (or the current
                        "vector-to-scalar function", see key F)
                     -> show vector field as above, but the vectors are scaled
                        proportionally to their magnitude
                     -> show the subset of the vector field with scalar function
                        around a given value (adjusted with keys u/U and w/W)
                     -> show the vector field restricted to the boundary of the
                        domain
V - Cycle the "vector" state in the opposite direction of 'v'

u/U - Move the level field vectors (in the appropriate "vector" state)
w/W - Add/Delete level field vector (in the appropriate "vector" state)

d - Toggle the "displaced mesh" state: (see also keys 'n'/'b')
    The options are: -> do not show displaced mesh
                     -> show displaced mesh
n - increase the displacement amount in 10% steps, wraps around from 100% to 0%
b - decrease the displacement amount in 10% steps, wraps around from 0% to 100%

F - Change the "vector-to-scalar function"
    The options are: -> magnitude:   sqrt(vx^2+vy^2+vz^2)
                     -> x-component: vx
                     -> y-component: vy
                     -> z-component: vz
