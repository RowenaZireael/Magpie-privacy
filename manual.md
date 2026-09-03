# Magpie User Manual

Version 1.0 · iPhone, iPad and Mac · iOS / iPadOS 26.0 or later

[中文版](manual_CN.md)

Magpie is a molecular visualisation and geometry-processing application for iPhone, iPad and Mac. It reads molecular coordinates and calculation outputs, provides a structure editor and local force-field optimisation, and generates quantum-chemistry input and coordinate files. An SSH connection provides access to remote calculation directories and Multiwfn analysis.

## Contents

1. [General use and first steps](#1-general-use-and-first-steps)
2. [Files and folders](#2-files-and-folders)
3. [Connecting to a server](#3-connecting-to-a-server)
4. [Viewing and measuring structures](#4-viewing-and-measuring-structures)
5. [Building and editing molecules](#5-building-and-editing-molecules)
6. [Force-field optimisation](#6-force-field-optimisation)
7. [Generating input and coordinate files](#7-generating-input-and-coordinate-files)
8. [Calculation results](#8-calculation-results)
9. [Trajectories](#9-trajectories)
10. [CUBE surfaces](#10-cube-surfaces)
11. [Molecular orbitals and Quick ESP](#11-molecular-orbitals-and-quick-esp)
12. [Terminal and interactive Multiwfn](#12-terminal-and-interactive-multiwfn)
13. [Settings](#13-settings)
14. [Common questions](#14-common-questions)

## 1. General use and first steps

### 1.1. Working environment

Local is Magpie's on-device file area. Structure viewing, editing, force-field optimisation, input generation, CUBE rendering and calculation-result analysis run locally. An SSH host adds a remote file browser and Terminal. Molecular Orbitals, Quick ESP and interactive Multiwfn use the server's Multiwfn installation.

The workspace consists of a file browser, a document area and a Results drawer. The Molecular Orbitals list and terminal panels open alongside the document. Controls are named as they appear in the app throughout this manual.

Atom numbers shown in Magpie start at 1. Geometry controls use Å for distances and degrees for angles. Generate converts the numbering and units into the selected program's input syntax.

### 1.2. Open a structure

1. Choose **Local** on the server selection screen.
2. Tap the import button in the file browser and choose an XYZ, MOL2, CIF or PDB file from Files.
3. Tap the imported file to open its structure.
4. Drag with one finger to rotate, pinch to zoom, and drag with two fingers to move the view.
5. Tap the ruler to measure distances and angles, or the pencil to edit the geometry.

### 1.3. Build a molecule

1. Enter Local and choose **New 3D Model**.
2. Use **Add atom** or **Add group** to place atoms and fragments.
3. Connect the atoms and adjust their positions.
4. Tap the play button in the editor toolbar to optimise the structure.
5. Open **Generate**, choose **XYZ** or **MOL2**, enter a file name and tap **Save**.

Choose XYZ for coordinates, or MOL2 to retain the structure's bond information.

### 1.4. Review a calculation

Import a supported calculation output file and open it. Use **Results** to switch between the structure trajectory, calculation details, convergence plots, vibrations and analysis. For ORCA IRC and scan calculations, keep the accompanying coordinate and trajectory files beside the main output.

### 1.5. Example: a first coordinate file

Choose New Text File and enter the following XYZ record:

```text
3
Water
O   0.000000   0.000000   0.000000
H   0.758602   0.000000   0.504284
H  -0.758602   0.000000   0.504284
```

Save it as `water.xyz` and open it from the file list. The first line is the atom count; the second is a comment; each remaining line gives an element and its Cartesian coordinates in Å. This file can be used to try the measurement, editor and Generate controls without a server connection.

## 2. Files and folders

### 2.1. File formats

| Type | Formats | Use |
| --- | --- | --- |
| Molecular coordinates | `.xyz`, `.mol2`, `.cif`, `.pdb` | View, measure, edit and generate new files |
| Calculation input | Supported quantum-chemistry input formats, including `.inp`, `.gjf` and `.com` | Open the geometry; use Open as Text to edit the input itself |
| Calculation output | Text output from supported quantum-chemistry packages, commonly `.out` and `.log` | Structures, energies, optimisation, vibrations, IRC, scans and electronic excitations |
| Volumetric data | `.cub`, `.cube` | Molecular orbitals, WFN Analysis, Interaction and ESP surfaces |
| Trajectory | Multi-frame `.xyz`; `.dcd` with a reference XYZ | Play a sequence of structures |
| Remote wavefunction | `.molden`, `.mwfn`, `.gms`, `.wfn`, `.wfx`, `.fchk`, `.fch`, `.chk`, `.gbw` | Open through the server's Multiwfn installation |
| Text | `.txt`, `.text`, `.md`, `.csv`, `.tsv` | Read and edit text |
| Images | PNG, JPEG, HEIC / HEIF, GIF, BMP and TIFF | Preview, zoom and pan |

### 2.2. Navigate and organise

Tap a folder to enter it. The **../** row at the top returns to the parent folder. The path field lets you jump to a directory; the filter narrows the current file list. Use **Refresh** after a remote calculation creates new output.

Long-press a file, or right-click with a pointer, to open its menu:

- **Open as Text** opens the raw contents of an input, output or other text-based file.
- **Copy** creates another copy in the current directory.
- **Rename** changes the file name.
- **Delete** removes the selected item after confirmation.
- **Export File** saves a copy through the system file interface.
- **Download to Local** copies a remote file into Magpie's on-device workspace.

Use **New Folder** to create a directory. Drag a file onto a folder to move it there, or onto **../** to move it up one level. **Settings → File Browser → Show Hidden Files** includes names beginning with a period.

### 2.3. Import from Files or another app

The import button copies files into the directory currently open in Magpie. In Local, the destination is on the device. In Remote, the files are uploaded to the open server directory. An existing file is kept and the imported copy receives a unique name.

You can also share a compatible file from another app and choose Magpie. It opens in Local. If you were connected to a server, Magpie disconnects and imports the shared file into the Local root; if you were already in Local, it uses the current folder. DCD files are imported for later attachment to an XYZ structure. Import wavefunction files using Magpie's own import button.

### 2.4. Edit text

Choose **New Text File**, or use **Open as Text** on an existing file. Edit the contents and use the checkmark **Save** button in the document header. **Save As** creates a separate file in the current directory. Saved text uses Unix line endings, suitable for calculation inputs and shell scripts.

## 3. Connecting to a server

### 3.1. Add an SSH host

1. Return to the server selection screen and add a host.
2. Enter a **Name**, **Host**, **Port** and **Username**. The default SSH port is 22.
3. Choose an authentication method and enter or import its credentials.
4. Tap **Save**, then select the host card to connect.
5. Complete the host-key and authentication prompts. The remote browser opens at the account's home directory.

| Authentication method | What to enter |
| --- | --- |
| Password | The account password |
| Password + Passcode | The password and, optionally, a current passcode; further prompts appear during authentication |
| Private Key | Import an OpenSSH private key file |

When editing an existing host, leaving the password blank keeps the saved password. The saved private key stays in place until another key file is imported. Long-press the host card to edit its settings.

For a server that asks you to approve a push notification and then press Enter, approve the notification, leave the response field empty and tap **Continue**.

The back-to-server-list button disconnects the current server. Local files remain available from the Local card.

### 3.2. Prepare Multiwfn

Install Multiwfn on the server and make it available in its shell environment. For the two binary wavefunction formats, specify the paths to the corresponding conversion programs in the Multiwfn settings:

| Wavefunction | Converter path to configure |
| --- | --- |
| `.chk` | `formchk` |
| ORCA `.gbw` | `orca_2mkl` |

The other wavefunction formats listed above are passed directly to Multiwfn. Put the source files in a writable calculation directory: Magpie creates temporary analysis files beside them.

### 3.3. Multiwfn Prewarm Command

Open the host editor, expand **Advanced**, and enter a **Multiwfn Prewarm Command** when the server needs an environment setup or a foreground resource allocation before running Multiwfn.

Use a single-line shell command that loads the required environment or enters the allocation shell. Include the resource and queue options used by your cluster. The command must complete its setup without further interactive input and keep the session in the foreground.

The prepared environment is shared by interactive Multiwfn, Molecular Orbitals and Quick ESP. It is separate from the ordinary Terminal. Closing a Multiwfn analysis keeps the environment ready for the next one; disconnecting ends it. If an allocation expires, reconnect to prepare a new environment.

For example, if the Multiwfn executable is installed in `/opt/Multiwfn`, the following prewarm command adds that directory to the analysis environment:

```sh
export PATH=/opt/Multiwfn:$PATH
```

Replace the directory with the installation path on the server. A cluster allocation command belongs in the same field when Multiwfn is to run on an allocated compute node; its queue, time and resource options are those of the cluster.

## 4. Viewing and measuring structures

### 4.1. Scene controls

| Action | Gesture or control |
| --- | --- |
| Rotate the view | One-finger drag |
| Zoom | Pinch |
| Pan | Two-finger drag; pointer scrolling also pans |
| Set the rotation centre | Tap an atom outside editing and measurement modes |
| Fit the structure again | **Reset view**, the circular-arrow button |
| Rotate continuously | Auto-rotation button |
| Measure | Ruler button |
| Edit geometry | Pencil button |
| Red–blue stereo view | Glasses button |

Outside editing and measurement modes, tap an atom to make it the centre of subsequent view rotation. The atom is highlighted. Tap another atom to change the centre, or use **Reset view** to return to the overall structure centre and reset the view.

The glasses button enables a red–blue anaglyph for matching 3D glasses. Adjust the red and blue intensity sliders to balance the two images.

Use the header's sidebar and Results buttons to make room for the structure. On iPad, drag panel dividers to adjust the workspace. The iPhone molecular workspace uses landscape orientation; Terminal and Multiwfn use portrait orientation.

### 4.2. Measurements

Enable the ruler, then tap atoms in order:

- Two atoms: distance in Å.
- Three atoms, A–B–C: angle at B.
- Four atoms, A–B–C–D: dihedral angle about B–C.

Tap a selected atom to remove it from the measurement. Double-tap empty space to clear the selection. Measurements leave the coordinates unchanged.

### 4.3. Bonds

MOL2 files retain their explicit bond information. For coordinate-only structures, Magpie determines connections and bond orders from the geometry and local chemical environment. Aromatic, amide and resonant bonds share a partial-double visual style while retaining their separate chemical meanings.

## 5. Building and editing molecules

Tap the pencil to enter **Geometry Editor**, or start with **New 3D Model**. Editing starts from the displayed frame, so a trajectory frame can be used as the starting geometry for a new calculation.

### 5.1. Select and move atoms

Choose **Select atoms**. Tap atoms one by one for an ordered selection, drag a rectangle for a group selection, or double-tap to select all atoms.

- **R** rotates the selected atoms.
- **T** translates the selected atoms.
- Drag in the scene after choosing R or T to apply the transformation.
- Tap the active transform again, or press Esc, to leave that transform mode.

These operations change the selected coordinates. Ordinary scene rotation changes only the viewing angle. Tap an active editor tool again to return to view mode.

### 5.2. Add or replace an atom

1. Choose **Add atom**.
2. Tap the element symbol to open the periodic table and choose an element.
3. Choose **Bond Order**: Single, Double, Triple or Partial Double.
4. Tap empty space to add an unconnected atom, or drag out from an existing atom to add a bonded atom.

While Add atom is active, tapping an existing atom replaces its element. Dragging from one existing atom to another creates a bond. If they are already bonded, repeating the drag cycles Single → Double → Triple → Single; a Partial Double becomes Double.

### 5.3. Add a group or ring

Choose **Add group**, then select a fragment from **Group / Structure**. Tap empty space to place it as a separate fragment, or drag from an existing atom to attach it. Tapping a terminal atom replaces that atom with the selected fragment, which is useful for substituting a hydrogen with a functional group.

For example, to build phenol, place **Benzene** on a new canvas, change the fragment choice to **Hydroxyl**, and tap one of the ring's terminal hydrogen atoms. The hydroxyl group replaces that hydrogen and attaches to the ring. Optimise the resulting structure, then save it with Generate.

### 5.4. Edit or remove a bond

In Select atoms mode, select two atoms and long-press the selection. The menu provides **Add Bond** or **Delete Bond**, the bond-type choices, and **Delete Atoms**. With a larger selection, use Delete Atoms to remove the selected atoms.

### 5.5. Change a bond length, angle or dihedral

Tap the atoms in order rather than box-selecting them. The matching geometry button appears in the editor toolbar.

| Ordered selection | Control | Moving side |
| --- | --- | --- |
| A, B | Bond Length | The A side moves; B stays fixed |
| A, B, C | Angle | A moves around B |
| A, B, C, D | Dihedral | The A side rotates about B–C |

Choose the control and adjust its slider. Distances are shown in Å and angles in degrees. Use **Reset view** after extending a structure beyond the visible area.

### 5.6. Keyboard shortcuts

| Key | Action |
| --- | --- |
| R | Rotate selection |
| T | Translate selection |
| Esc | Leave the active transform |
| Delete | Delete selected atoms |
| Command–Z | Undo |
| Shift–Command–Z | Redo |

### 5.7. Save the edited structure

Open **Generate** from Geometry Editor and save the geometry as an input or coordinate file. Save before leaving the editor: **Stop editing** returns to the original document, rather than writing the edited coordinates back into the source file.

## 6. Force-field optimisation

### 6.1. Optimise a structure

1. Open **Settings → Geometry Editor → Force Field** and choose **UFF** or **MMFF94s**. UFF is the default.
2. Return to Geometry Editor and prepare the atoms and bonds.
3. Tap the editor toolbar's play button, **Optimize geometry**.
4. Watch the geometry relax. You can rotate, pan and zoom the view during optimisation.
5. Let the optimisation converge, or tap pause to accept the displayed geometry.
6. Use **Generate** to save it.

One optimisation is one undo step. To adjust atoms or bonds, pause the optimisation first. Stopping the editor while an optimisation is still running cancels that run.

Both force fields use the current structure and bond assignments. Separate molecules on the same canvas are optimised together, including their intermolecular interactions. For transition-metal coordination structures, choose UFF.

### 6.2. Optimise part of a structure

Enable **Settings → Geometry Editor → Freeze Selected Atoms**. Select the atoms that should remain fixed, then start the optimisation. The selection is captured when you press play; the remaining atoms are free to move. Turn the setting off to return to full-structure optimisation.

### 6.3. Default formal charges

Magpie assigns formal charges for force-field atom typing from the displayed elements, bonds, explicit hydrogens and recognised aromatic or resonance groups. An atom with no bonds uses the following ion-family defaults:

| Isolated atom | Default formal charge |
| --- | --- |
| Alkali metal, such as Li, Na or K | +1 |
| Alkaline-earth metal, such as Be, Mg or Ca | +2 |
| Chalcogen, such as O, S or Se | −2 |
| Halogen, such as F, Cl, Br or I | −1 |

Thus, an unconnected Na atom is treated as Na⁺ and an unconnected Cl atom as Cl⁻. These family defaults apply to unbonded atoms; bonded main-group atoms are assigned charges from their local bonding environment. For example, nitrogen with four single bonds is assigned +1, while oxygen with only one single bond is assigned −1. Hydrogens contribute to this valence count when they are present in the displayed structure.

Transition-metal centres use preset oxidation states for force-field typing, including in coordination structures. The defaults for the first three d-block series are:

| Elements | Default oxidation state |
| --- | --- |
| Cu, Ag | +1 |
| Mn, Fe, Ni, Zn, Ru, Pd, Cd, Pt, Hg | +2 |
| Sc, Y, Cr, Co, Rh, Ir, Au | +3 |
| Ti, Zr, Hf | +4 |
| V, Nb, Ta, Tc | +5 |
| Mo, W, Os | +6 |
| Re | +7 |

The assigned formal charges describe the topology supplied to the force field. **Charge** and **Mult** in Generate set the total charge and multiplicity of the quantum-chemistry input; they do not change these force-field assignments. Each optimisation uses the current structure, so adding hydrogens or changing bond orders updates the charge assignment on the next run.

## 7. Generating input and coordinate files

**Generate** creates a file from the current editor geometry. It opens with ORCA selected; use **Format** to choose a supported quantum-chemistry input format or an XYZ, MOL2, CIF or PDB coordinate file.

### 7.1. Supported quantum-chemistry input formats

1. Choose the program package and **Job**.
2. Set **Functional** and **Basis**. The method menu also includes non-DFT choices; the available controls follow the selected method.
3. Enter **Charge**, **Mult**, **Mem GB** and **Cores**.
4. Set the job-specific options, dispersion and solvation as needed.
5. Review the generated text, enter the file name and tap **Save**.

Mem GB is the total memory setting. For ORCA, Magpie divides it by the core count when writing `%maxcore`. **Additional keywords** adds keywords to the generated input. ORCA provides an auxiliary-basis choice for applicable methods.

| Job | Purpose |
| --- | --- |
| SPE | Single-point energy |
| OPT | Geometry optimisation |
| FREQ | Frequency calculation |
| OPT+FREQ | Optimisation followed by frequencies |
| TS | Transition-state optimisation |
| IRC | Intrinsic reaction coordinate |
| Scan | One- or two-dimensional relaxed scan |
| TDDFT | Electronic excited states |
| AIMD | ORCA molecular dynamics |

For IRC, choose Both, Forward or Backward and set the path controls. For TDDFT, set **Excited states** to the number of roots to request.

Saving from Local writes into the current Local folder. Saving while connected to SSH writes into the current remote directory. Generate prepares the file; run the calculation with the server's normal program or scheduler commands in Terminal.

### 7.2. Relaxed scans

The following procedure uses ORCA as an example.

1. Select **Job → Scan** and choose **Dimensions → 1D** or **2D**.
2. Set the coordinate type to Bond, Angle or Dihedral.
3. Enter the atom numbers in the displayed order. Magpie's atom numbering starts at 1.
4. Set the start, end and point count.
5. For a 2D scan, define Coordinate 2 independently.

An ordered selection of two to four atoms in the editor can prefill Coordinate 1 for a 1D scan. Select Scan as the job explicitly. Bond coordinates use Å; angle and dihedral coordinates use degrees.

For an ORCA bond scan between atoms 1 and 2 from 0.9 to 1.3 Å, enter:

| Field | Value |
| --- | --- |
| Dimensions | 1D |
| Coordinate type | Bond |
| Atom numbers | 1, 2 |
| Start | 0.9 |
| End | 1.3 |
| Points | 9 |

This defines nine positions, including both endpoints, separated by 0.05 Å. The generated block uses ORCA's zero-based indices:

```text
%geom
  Scan
    B 0 1 = 0.9, 1.3, 9
  end
end
```

In a 2D scan, the two coordinates define a grid; for example, 9 points on Coordinate 1 and 7 on Coordinate 2 specify 63 coordinate combinations.

### 7.3. Edit the generated text

The text below the controls is editable. After you make a manual edit, it is kept instead of being regenerated by later setting changes. Tap **Reset** to rebuild the text from the current controls, or change Format to start a new template.

### 7.4. Coordinate export

- **XYZ** stores element symbols and Cartesian coordinates.
- **MOL2** includes atoms and chemical bond information, including aromatic and amide assignments.
- **CIF** and **PDB** provide coordinate files for workflows using those formats.

These exports use the current structure, not the complete trajectory or calculation output. To keep an original multi-frame file, use **Export File** in the browser.

For the structure and block syntax of ORCA inputs, see the [ORCA 6 input reference](https://www.faccts.de/docs/orca/6.0/manual/contents/structure.html).

### 7.5. ORCA molecular dynamics

In Generate, choose **ORCA → Job → AIMD**. Set the electronic-structure method and the dynamics controls.

| Control | Meaning | Default |
| --- | --- | --- |
| Time step (fs) | Integration time step | 1 fs |
| Steps | Number of MD steps | 1000 |
| Initial temp. (K) | Temperature used to initialise velocities | 298.15 K |
| Thermostat | CSVR, NHC, Berendsen or None | CSVR |
| Bath temp. (K) | Thermostat target temperature | 298.15 K |
| Time constant (fs) | Thermostat coupling time | 100 fs |
| Trajectory Format | XYZ or DCD | XYZ |
| Stride | Write a trajectory frame every N steps | 1 |

**Keep center of mass** controls the centre of mass during the simulation.

#### 7.5.1. Cell walls

Under **Cell wall**, choose None, Cube, Rectangular, Sphere or Ellipsoid. Enter the dimensions in Å and the wall spring constant in kJ/mol/Å². These are non-periodic harmonic walls.

With a wall selected, **Center geometry at origin** moves the geometry's arithmetic centre to the origin in the generated input. It leaves the editor coordinates unchanged. This is a preparation step, separate from Keep center of mass during the run.

#### 7.5.2. Output files

For an input named `sample.inp`:

- XYZ output uses `sample_traj.xyz`.
- DCD output uses `sample_traj.dcd` and a reference structure, `sample.xyz`.

After running the calculation, refresh the remote folder. Open the XYZ trajectory directly, or open `sample.xyz` and attach `sample_traj.dcd` as described below.

#### 7.5.3. Example: write a DCD trajectory

With a structure open in Geometry Editor, choose ORCA and AIMD, then use these settings:

| Control | Value |
| --- | --- |
| File name | `sample.inp` |
| Time step (fs) | 0.5 |
| Steps | 2000 |
| Initial temp. (K) | 298.15 |
| Thermostat | CSVR |
| Bath temp. (K) | 298.15 |
| Time constant (fs) | 100 |
| Trajectory Format | DCD |
| Stride | 10 |
| Cell wall | None |
| Keep center of mass | Off |

The simulation length is 1 ps and the coordinate output interval is 5 fs. Generate writes the following MD block alongside the chosen electronic-structure settings and coordinates:

```text
%md
  Timestep 0.5_fs
  Initvel 298.15_K
  Thermostat CSVR 298.15_K Timecon 100_fs
  Dump Position Format XYZ Stride 0 Filename "sample.xyz"
  Dump Position Format DCD Stride 10 Filename "sample_traj.dcd"
  Run 2000
end
```

After the calculation, open `sample.xyz` and load `sample_traj.dcd` from Results. Detailed MD command definitions are in the [ORCA 6 molecular-dynamics reference](https://www.faccts.de/docs/orca/6.0/manual/contents/detailed/moldyn.html).

## 8. Calculation results

Open a supported calculation output and show **Results**. The panel menu follows the data recorded in the calculation.

### 8.1. Details and optimisation

**Details** contains **Info**, **Thermo** and **Convergence** tables. Use them for the program and job information, charge and multiplicity, energies, thermochemical quantities and convergence criteria.

For an optimisation, use the trajectory controls to inspect individual steps. The convergence plots show how the reported criteria change through the optimisation and highlight the current step.

### 8.2. Vibrations

Choose **Vibrations**, select a mode from the frequency menu, then tap **Play Vibration**. The arrows move between neighbouring modes. **Displacement Amplitude** changes the size of the displayed motion. Frequencies are shown in cm⁻¹; negative frequencies identify imaginary modes in the output.

### 8.3. IRC and one-dimensional scans

Choose **IRC** or **Scan** in Results to view the energy profile and its linked trajectory. Tap a point on the curve to display that geometry. Relative energies are shown in kcal/mol.

Keep ORCA's companion files in the same folder as the main output. Magpie reads the available IRC paths, combined scan coordinates and numbered or trajectory XYZ files when assembling the results.

### 8.4. Two-dimensional scans

Tap **2D Scan** in the Results header to open the potential-energy surface.

- **Surface** shows a rotatable 3D energy surface for a complete grid.
- **Contour** shows the two scan coordinates and the energy contours.
- **Top view** and **Reset view** adjust the 3D presentation.
- Selecting a point in the contour view links it to the corresponding molecular frame.

The axes use the scan coordinates and relative energy in kcal/mol. Incomplete grids use the contour view, with gaps retained where calculation points are missing.

### 8.5. UV–Vis and orbital transitions

For a TDDFT or other supported excited-state output, **UV-Vis Spectrum** displays the absorption spectrum against wavelength in nm. The displayed FWHM (full width at half maximum) gives the peak width used for spectral broadening.

**Orbital Transitions** lists the excited states, orbital pairs, spin labels and contribution percentages reported or derived from the output. This is separate from the Molecular Orbitals sidebar, which generates spatial orbitals from a wavefunction file.

## 9. Trajectories

### 9.1. Multi-frame XYZ

Open the XYZ file and select **Trajectory**. Tap Play, drag the Frame slider to inspect a particular structure, and adjust **Speed** in frames per second. Enable **Settings → Molecule Viewer → Loop Trajectory Playback** to repeat the sequence.

### 9.2. DCD with a reference XYZ

1. Put the DCD and its reference XYZ in the same Local or Remote folder.
2. Open the single-frame XYZ.
3. In Results, tap **Load trajectory (.dcd)** beside Details.
4. Choose the matching DCD file.
5. Use the Trajectory controls to play or inspect the frames.

The XYZ supplies the element identities and atom order; the DCD supplies the changing coordinates. Use the XYZ written with the trajectory so that both have the same atom count and ordering. Magpie reads standard ORCA-style DCD coordinate trajectories; fixed-atom compressed and four-dimensional variants need conversion before import.

To reuse a frame, pause at that frame, enter Geometry Editor and choose Generate.

## 10. CUBE surfaces

Open a `.cub` or `.cube` file and choose a mode in **CUBE Visualization**.

| Mode | First CUBE | Second CUBE | Display |
| --- | --- | --- | --- |
| Molecular Orbital | Orbital values | — | Positive and negative orbital lobes |
| WFN Analysis | A signed scalar field, such as a Fukui function or spin density | — | Positive green and negative blue surfaces |
| Interaction | The field defining the surface | The field used for colouring | A blue–green–red coloured surface |
| ESP | Electron density | Electrostatic potential | Potential mapped onto a density surface |

### 10.1. A single-field surface

Open the CUBE, choose Molecular Orbital or WFN Analysis, then adjust the Surface controls in Results. WFN Analysis displays the data already contained in the CUBE; generate that field in your analysis program first.

### 10.2. A coloured surface

1. Open the CUBE that defines the surface geometry.
2. Choose Interaction or ESP.
3. When Magpie asks for the colouring CUBE, tap the second file in the browser.
4. Adjust the isovalue and appearance after the pair loads.

For ESP, open the density CUBE first and the potential CUBE second. For Interaction, use the surface and colouring fields produced by the same analysis. Keep both fields in the same molecular coordinate system.

### 10.3. Surface controls

- **Iso Value** selects the value at which the surface is drawn.
- **Render Quality** changes the surface sampling quality.
- **Surface Opacity** makes the surface more transparent or opaque.
- **Settings → Molecule Viewer → Surface Material** chooses Constant or Lambert shading.

Lower the render quality while adjusting a large surface, then raise it for closer inspection.

### 10.4. ESP colour scale

The scale runs from blue at the minimum through white at the midpoint to red at the maximum. Values are in atomic units. Tap an endpoint to edit it; on iPad the fields are edited inline, while iPhone uses a separate prompt.

**Auto** fits the range to the potential values sampled on the currently displayed density surface. After changing Iso Value, tap Auto again to fit the new surface. To compare several structures using the same colours, enter the same minimum and maximum for each. White marks the middle of the chosen range and represents zero only for a symmetric range.

For example, a minimum of −0.030 and a maximum of +0.030 a.u. place zero at white. With −0.020 and +0.040 a.u., white represents +0.010 a.u. Values below or above the chosen limits use the endpoint colours.

### 10.5. Save CUBE data to Local

For remote CUBE files, choose **Save** for a single field or **Save Both** for a paired surface. Select an existing Local folder or create a new one. Both files are needed to reopen an Interaction or ESP pair.

## 11. Molecular orbitals and Quick ESP

These tools work from a remote wavefunction file using the server's prepared Multiwfn environment.

### 11.1. Molecular orbitals

1. Connect to the server and open a wavefunction file.
2. Tap the **Molecular Orbitals** button in the workspace header.
3. Browse the orbital list, which shows energy, occupation and HOMO / LUMO labels. Unrestricted wavefunctions have separate α and β columns.
4. Tap an orbital to generate and display its surface.
5. Adjust Iso Value, Render Quality and Surface Opacity in Results.

Orbitals near the frontier region are prepared ahead of time. Double-tap a more distant orbital to also prepare the uncached orbitals between it and the nearby cached region of the same spin. Use **Settings → Analysis → Orbital Energy Unit** to switch between a.u. and eV.

### 11.2. Quick ESP

1. Open a remote wavefunction file.
2. Tap the **Quick ESP** button beside Molecular Orbitals.
3. Multiwfn generates the density and potential fields, and Magpie displays the coloured surface with an automatically fitted initial range.
4. Adjust the surface or enter a shared colour range for comparisons.
5. Choose **Save Both** to keep the two CUBE files in Local, or **Skip** to continue without saving them.

The orbital and Quick ESP calculations use temporary analysis files. Saving the CUBE results to Local lets you reopen those surfaces without a server connection.

## 12. Terminal and interactive Multiwfn

### 12.1. Terminal

While connected to SSH, open **Terminal** from the workspace header. It starts in the current remote directory. Use it to run commands, submit calculations and inspect the server's output. Close the panel with its × button when finished, then refresh the file browser to see new files.

### 12.2. Interactive Multiwfn

Select a remote analysis file and open **Multiwfn** from the header. The panel contains the program's terminal output and shortcut buttons for recognised menu options.

Tap a numbered option or enter the response directly in the terminal. Continue through Multiwfn's menus as you would in an SSH session. The restart button starts the analysis again for the selected file. Use the program's exit command or close the panel to end the analysis; the prepared environment remains available until you disconnect.

Molecular Orbitals, Quick ESP and interactive Multiwfn share the Multiwfn environment. Finish or close the current analysis before starting another of these tools. The ordinary Terminal is a separate session.

## 13. Settings

| Section | Setting | Use |
| --- | --- | --- |
| Molecule Viewer | Viewer Background | Choose the canvas background |
| Molecule Viewer | Lighting Intensity | Adjust the main light |
| Molecule Viewer | Fill Light | Adjust illumination in shaded areas |
| Molecule Viewer | Surface Material | Constant (Default) for flat shading; Lambert for diffuse lighting |
| Molecule Viewer | Loop Trajectory Playback | Repeat trajectories |
| Geometry Editor | Force Field | Choose UFF or MMFF94s |
| Geometry Editor | Freeze Selected Atoms | Hold the selected atoms fixed in the next optimisation |
| File Browser | Show Hidden Files | Show dot-prefixed files and folders |
| Analysis | Orbital Energy Unit | Choose a.u. or eV |

About shows the app version. Credits and Open Source Software list the scientific software, libraries and their notices.

## 14. Common questions

### 14.1. Where did my generated file go?

Generate saves into the current browser directory. Look in Local if you were working locally, or refresh the remote directory if you were connected to a server. CUBE Save / Save Both uses the Local folder chosen in its destination picker.

### 14.2. How do I keep an edited structure?

Use Generate before stopping the editor. Choose MOL2 to keep the bond assignments, or XYZ for coordinates. Use Open as Text when the task is to change the original input file rather than create a new geometry file.

### 14.3. Why is there no DCD button?

Open the single-frame reference XYZ first and show Results. The DCD attachment button appears for that structure. Put the DCD in the same folder.

### 14.4. Why are vibrations, spectra or scan points missing?

Open the main calculation output containing those results. A coordinate file contains geometry rather than frequency or excitation data. For ORCA IRC and scans, include the companion files in the same directory and refresh the folder before reopening the output.

### 14.5. Why will a wavefunction not open?

Open it from Remote, with Multiwfn available in the prepared environment. In the Multiwfn settings, check the configured path to `formchk` for `.chk`, or `orca_2mkl` for `.gbw`. Also check that the source directory is writable. If a cluster allocation has ended, reconnect to prepare a fresh environment.

### 14.6. What should I change when force-field optimisation reports an error?

Inspect the displayed elements, bonds and hydrogens. Correct an unintended bond or bond order in Geometry Editor, then try again. Use UFF for transition-metal coordination. MMFF94s can optimise recognised aromatic and resonance structures, but an isolated generic Partial Double bond needs a defined chemical bond assignment.

### 14.7. Why does a surface look empty or unusually coloured?

For an empty surface, lower Iso Value. For a paired surface, check the order of the two CUBE files. For ESP, tap Auto to fit the displayed surface, or restore the numerical range used for the comparison.

### 14.8. A file is too large to import

The import limit is 512 MiB per file. CUBE files support up to 20 million grid points and one scalar dataset per file. Regenerate a coarser CUBE or export a shorter trajectory for on-device inspection.

### 14.9. Report an issue

Use the repository's [Issues page](https://github.com/RowenaZireael/Magpie-privacy/issues). Include the Magpie version, device and system version, file type, the steps that reproduce the problem, and the error text. A small example file or screenshot helps reproduce it.
