# PyMOL Beginner's Reference Guide

PyMOL is a standard molecular modeling tool. Below is a reference list of common commands and actions that you may use when working with protein models:

## Basic Control
```python
reinit # Resets entire session
reset # Resets visualization window to default
```

## Loading and Fetching Data

```python
load {file} # Loads PDB or PyMOL session from file
fetch {pdb-id} # Fetches ID from PDB
```

## Camera Control

There are four basic camera controls:
1. **Rotation**: Rotate view around a central point
	- Left mouse button
2. **Translation (Move)**: Move the central point left/right, up/down
	- ⌥-Left Mouse
3. **Zoom**: Zooms in and out towards 
	- Right Mouse, Forward and Backward
4. **Clipping**: Adjusts visible region (in Z direction)
	- Mostly when zoomed in on particular regions
	- Scroll Wheel 

In addition to moving the camera, you can have PyMOL set the center point on a specific atom:
1. ⌘-Left Click the atom you want to center on
2. Use `center {selection-expression}` in the command line

## Selection Syntax
```
select {selection-name}, {selection-expression}
```

Selecting an object or a subset of an object is extremely important for manipulating and visualizing in PyMOL

### Selection Expression Guide
| Property Selector | Short Form Selector | Identifier and Example                                                   |
| :---------------: | :-----------------: | :----------------------------------------------------------------------: |
|       name        |          n          |                   Atom Name<br>`select name c+o+n+ca`                    |
|       resn        |          r          |          Residue Name (Three Letter Code)<br>`select resn glu`           |
|       resi        |          i          |           Residue Number (Integer Index)<br>`select resi 200`            |
|       chain       |          c          |                      PDB Chain<br>`select chain a`                       |
|        ss         |         ss          | Secondary Structure<br>(h = helix, s = sheet, l = loop)<br>`select ss h` |
[Selection Expression Guide]

### Selection Algebra
| Operator  | Shortcut | Effect                                        |
| :-------: | :------: | :-------------------------------------------: |
|  not s1   |   ! s1   |            Selects atoms not in s1            |
| s1 and s2 | s1 & s2  |        Selects atoms in both s1 and s2        |
| s1 or s2  | s1 \| s2 |       Selects atoms in either s1 and s2       |
| s1 in s2  | s1 in s2 | Selects atoms in s1 whos identifiers match s2 |
[Selection Algebra]

### Proximity Selection Expressions
| Operator               | Shortcut | Effect                                                               |
| :--------------------: | :------: | :------------------------------------------------------------------: |
| s1 within {dist} of s2 |    w     |      Selects atoms in s1 that are within {dist} angstroms of s2      |
|    s1 around {dist}    |    a     |  Selects atoms with centers within {dist} angstroms of atoms in s1   |
|    s1 expand {dist{    |    x     | Epxands s1 by including atoms within {dist} angstroms of atoms in s1 |
[Proximity Selection]

## Manipulating Representations

```python
hide {property}, {selection-expression} # Hide this object property
show {property}, {selection-expression} # Show object property
color {color}, {selection-expression} # Modifies selection color

## Examples ##

# Hide stick representation in chain A only
hide sticks, chain A

# Show sphere representation for C and C-alpha atoms
show spheres, name c+ca

# Color everything except chain A and B blue (using or)
color blue, ! chain A or chain B
```

- Manipulating object visualizations can be done via the command line and the GUI.
- Properties that can be shown are the same labels as indicated in the GUI.
- You can also use the `help {command}` command to see a list of potential arguments

## Manipulating Objects
You can also manipulate objects directly using the command line:

```python
create {new-object}, {selection-expression} # Create object from selection
delete {object/selection} # Deletes object or selection
copy {new}, {source} # Creates a new object from source
```

## Additional Functions

### Aligning

```python
# Align mobile and stationary by moving mobile over stationary
# Does this by minimizing the all-atom RMSD
align {mobile}, {stationary}
```

### Measuring Distances

```python
# Creates distance objects between selection 1 and 2

distance {name}, {selection-expression-1}, {selection-expression-2}
```

- Note: in many cases, it can often be easier to do this using the interactive wizard tool instead!