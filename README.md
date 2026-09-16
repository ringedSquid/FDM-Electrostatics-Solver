# FDM Electrostatics Solver
Electrostatics Solver in 3D!

## Overview
A simple electrostatics simulator that uses the finite-difference method to approximate solutions to Poisson's equation for electrostatics (laplace^2 V = -ρ/ε). It is a 3D Simulation, but only a slice of the space is viewed at a time. The electric field vectors, potential field, and charge densities can be displayed. Users can set up the simulation using a custom-made description language that the program will interpret. This is a very computationaly expensive program, grid sizes bigger than 30x30x30 units take a significant amount of time to complete. 
<br>
This runs entirely in Processing and only requires the installation of the ControlP5 library. 

## Instructions on how to run
Clone this repo from the main branch:
```bash
git clone https://github.com/Stuycs-K/final-project-5-yu-kellen
```
or alternatively:
```bash
git clone git@github.com:Stuycs-K/final-project-5-yu-kellen.git
```
Open the file ```ElectroStaticsSim.pde``` in Processing.
<br>
Make sure that the library ```ControlP5``` is installed. <br>
[https://processing.org/reference/libraries/]
<br>
click ```Open File``` and open one of the many example programs in ```programs/``` or create your own! Once the file is opened, click ```run``` and wait for the simulation to open up a new window. Then using the UI, you can view different slices of the space and different aspects of it (Electric Field, Potential, Charge). 

### How to use the description language
This program interprets a custom description language that describes a scenario for the simulation to run. The syntax is very simple. 
<br>
Every program must start with this line:

```
BEGIN X Y Z GRIDSIZE PIXELS_PER_GRID SHOW_KEY 
```

X, Y, Z (int) describe the size of the grid in cells. <br>
GRIDSIZE (float) describes the sidelength of each cell in the grid in real life units. <br>
PIXELS_PER_GRID (int) describes how many pixels on each side are used to render one cell. <br>
SHOW_KEY (boolean) toggles if the key (scale) for the simulation will show. <br>

Now that you have set up your grid, its time to add materials.
```
MAT MAT_NAME R G B PERM TYPE VAL
```
MAT_NAME (String, single word) is the name of the material. <br>
R, G, B (int) describe the color of the material. <br>
PERM (float) is the permittivity of the material. <br>
TYPE (char) is the type of material. 'c' is for conductors, 'd' is for charged objects. <br>
VAL (float) can describe either: the potential of a conductor (TYPE = 'c') or the charge of an object (TYPE = 'd'). <br>

Lets now add a geometry
```
BOX MAT pX pY pZ sX sY sZ
HBOX MAT pX pY pZ sX sY sZ T
DISC MAT pX pY pZ ORIENT R
WASHER MAT pX pY pZ ORIENT R1 R2
SPHERE MAT pX pY pZ R
HSPHERE MAT pX pY pZ R1 R2
ELLIPSOID MAT pX pY pZ A B C R
HELLIPSOID MAT pX pY pZ A B C R1 R2
POINT MAT pX pY pZ
```
MAT (String) is the name of a predefined material. <br>
pX, pY, pZ (float) is the center positon of the geometry. <br>
sX, sY, sZ (float) is the size of a geometry. <br>
ORIENT (char) is the orientation of a disc/washer. 'x' - faces the x direction, 'y' - faces the y direction, 'z'- faces the z direction. <br>
T (float) is the thickness of a hollow box's walls. <br>
A, B, C (float) is the coefficients for an ellipse (you have to know what this is first). <br>
R (float) is the radius of a sphere/ellipse. <br>
R1 (float) is the inner radius of a hollow sphere/ellipse. <br>
R2 (float) is the outer radius of a hollow sphere/ellipse. <br>

Once you add your geometries, you must put ```SOLVE``` at the end of the program if you want it to run properly. <br>

Here is a quick example (NOTE THAT THE ACTUAL SIM DOES NOT SUPPORT COMMENTS): 
```
//Begin grid with size 50x5x50, set the size of each cell to .001m. 10 pixels per cell, show key.
BEGIN 50 5 50 .001 10 true 
//Define materials, both charged substances
MAT posCharge 240 240 0 8.85418782E-12 d 10
MAT negCharge 120 0 120 8.85418782E-12 d -10
//Place two spheres next to each other
SPHERE posCharge -7 0 0 4
SPHERE negCharge  7 0 0 4
SOLVE
```

## Pictures!
### Electric Field inside a charged hollow sphere
![App Screenshot](https://github.com/Stuycs-K/final-project-5-yu-kellen/blob/main/images/ChargedSphere.png)
### Electric Field of a dipole (positive and negative charged balls)
![App Screenshot](https://github.com/Stuycs-K/final-project-5-yu-kellen/blob/main/images/Dipole.png)
### Induced charge on the surface of a hollow conducting box
![App Screenshot](https://github.com/Stuycs-K/final-project-5-yu-kellen/blob/main/images/InducedCharge.png)
### Shielding effect of conductors
![App Screenshot](https://github.com/Stuycs-K/final-project-5-yu-kellen/blob/main/images/Shielding.png)

## Known Bugs
- Sometimes when running the program, the UI is missing the scrollbar or a part of the rendering window gets cut off. Just rerun the program.




