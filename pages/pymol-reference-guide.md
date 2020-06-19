# PyMOL Beginner's Reference Guide

PyMOL is a standard molecular modeling tool. Below is a reference list of common commands and actions that you may use when working with protein models:

## Basic Control

```bash
reinit # Resets entire session
```

## Loading and Fetching Data

```bash
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

If the view gets too convoluted, you can reset the view to the default state: `reset`

## Representation Control

## Manipulating Representations

```bash
# Hide this object property
hide {property}, {selection-expression} 

# Show object property
show {property}, {selection-expression} 

# Modifies selection color
color {color}, {selection-expression} 

## Examples ##

# Hide stick representation in chain A only
hide sticks, chain A

# Show sphere representation for C and C-alpha atoms
show spheres, name c+ca
```

- Manipulating object visualizations can be done via the command line and the GUI.
- Properties that can be shown are the same labels as indicated in the GUI.
- You can also use the `help {command}` command to see a list of potential arguments

### List of Most Common Representations
- **Cartoon:** Great of visualizing secondary structure
- **Sticks:** Good for being able to see the overall amino acid
- **Ribbon:** Shows connections between alpha carbons (good for overall peptide backbone)
- **Spheres:** Approximates Van Der Waals Radius for atoms -- prefect for looking for steric clashes or whether things fit together properly
- **Surface:** Important for thinking about protein-protein interactions, protein binding, etc.


### Coloring
Coloring can be done using the color button in the GUI or using the color method:

```
color {color}, {selection-expression}
```

## Selection

Selecting an object or a subset of an object is extremely important for manipulating and visualizing in PyMOL.

- Clicking on items is a common way of controling your selection
	- Change the selection type under Mouse->Selection Mode

The command line will return information on your selection:

```
/{object}/item/chain/residue-name/atom-name
```

### Selection Names
Selections are initially stored as `sele` unless named. You can rename through the action menu or via the `set_name {name}, selection` command

Selections can also be done using the command line, often the only way for complex selection criteria.

```
select {selection-name}, {selection-expression}
```

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

## Manipulating Objects
You can also manipulate objects directly using the command line:

```bash
# Create object from selection
create {new-object}, {selection-expression} 

# Deletes object or selection
delete {object/selection} 

# Creates a new object from source
copy {new}, {source} 
```

## Additional Functions

### Measuring Distances

```
# Creates distance objects between selection 1 and 2

distance {name}, {selection-expression-1}, {selection-expression-2}
```

- Note: in many cases, it can often be easier to do this using the interactive wizard tool instead!

### Aligning

```
# Align mobile and stationary by moving mobile over stationary
# Does this by minimizing the all-atom RMSD
align {mobile}, {stationary}
``` do this using the interactive wizard tool instead!