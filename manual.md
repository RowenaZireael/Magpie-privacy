# Magpie User Manual and Support

Magpie is a free molecular visualisation and scientific post-processing workspace for iPhone and iPad. It is designed for viewing molecular structures, preparing geometries, generating scientific files, reviewing calculation results, and working with files on a user-controlled remote computer.

This guide describes the main user workflows. The controls shown in the app depend on the selected file and on which data are available in that file.

## Quick Start

1. Open Magpie and choose the local workspace.
2. Import a file from the iOS or iPadOS Files interface, or create a new text file or empty molecular model.
3. Tap a supported file to open it.
4. Use the 3D workspace, editor, trajectory controls, or result panels that appear for the selected document.
5. Use Generate when you want to create a new input or coordinate file from the current structure.
6. Save or export the result when finished.

An optional SSH/SFTP connection can be configured when you need to work with files on a server that you own, administer, or are authorised to use.

## Workspace and File Management

The local workspace is the starting point for on-device work. From the file browser you can:

- Browse folders and open supported documents.
- Import files through the system Files interface.
- Create a plain-text document.
- Create a new empty molecular model for geometry building.
- Rename, copy, or delete files.
- Save generated files into the current folder.
- Export or share a file through the system interface when that action is available.
- Download a remote file into the local workspace while connected to a server.

### Supported File Categories

- Molecular coordinates: XYZ (.xyz), MOL2 (.mol2), CIF (.cif), and PDB (.pdb).
- Scientific input files: .inp, .gjf, and .com.
- Computational output: supported text output, commonly using .out or another recognised text extension.
- Volumetric data: CUBE files (.cub and .cube).
- Remote wavefunction sources: .molden, .fchk, .fch, .chk, and .gbw when the required software is available on the user's server.
- General preview: common images and plain-text files.

The available viewer and result tools are determined by the contents of a file. A valid structure may open even when a file does not contain trajectories, frequencies, spectra, or other optional results.

## Viewing a Molecular Structure

After opening a supported molecular file, the central 3D workspace displays the atoms and bonds that Magpie can determine from the document.

- Drag in the scene to inspect the molecule from different directions.
- Use the system zoom gesture to change the viewing distance.
- Select atoms when you need measurements, editing actions, or a scan coordinate.
- Use the frame controls when the document contains more than one geometry.
- Open the available drawers or result panels for document details and analysis.

The viewer can present single, double, triple, and partial-double bond styles when that information is available. Explicit bond information in a MOL2 document is retained. Coordinate-only formats may require Magpie to determine connections from the molecular geometry.

Viewer appearance can be adjusted in Settings, including the background, lighting, and surface presentation options.

## Trajectories and Vibrational Modes

A computational output may contain an optimisation trajectory, reaction path, relaxed scan, or vibrational modes.

### Trajectory Controls

- Move the frame slider to inspect an individual geometry.
- Use the playback control to animate the available frames.
- Pause playback before selecting a specific point for closer inspection.
- For a reaction path or one-dimensional scan, selecting a point in the energy curve also selects its associated molecular frame.

For reaction-path and relaxed-scan results, Magpie presents accepted or converged points when the source output provides enough information to identify them. Failed or incomplete points are not used to invent missing structures or energies.

### Vibrational Modes

When frequency data are present:

1. Open the vibration control in the molecular workspace.
2. Choose a mode from the available list.
3. Start or stop the animation.
4. Adjust the amplitude when the control is available.

The vibration selector only appears when the current document contains recognised mode data.

## Editing Molecular Geometry

Open the editing tools from a molecular structure or from a new empty model. The editor supports:

- Selecting one or more atoms.
- Changing the element assigned to a selected atom.
- Adding atoms by placing them in the 3D scene.
- Adding molecular fragments or functional groups.
- Creating bonds between atoms.
- Choosing single, double, triple, or partial-double bond presentation where supported.
- Changing bond lengths.
- Changing bond angles.
- Changing dihedral angles.
- Undoing and redoing editing operations.

The order of atom selection matters for measurements and coordinate-based operations:

- Two atoms define a distance.
- Three atoms define an angle.
- Four atoms define a dihedral.

When adding an atom from an existing atom, choose the desired bond order before completing the placement. Fragment attachment uses a suitable connection direction and bond length as a starting geometry; review the structure before generating a calculation file.

Edits belong to the current editing session. To keep the result, use Generate and save an input or coordinate file.

## Generating Input and Coordinate Files

Use Generate in the molecular workspace to create a new file from the current geometry.

### Basic Workflow

1. Open or build a molecular structure.
2. Make any required geometry edits.
3. Select Generate.
4. Choose an input format or coordinate format.
5. Configure the available settings.
6. Review the generated text.
7. Choose a filename and save the document into the workspace.

### Available Output Formats

- Scientific input: .inp or .gjf.
- General coordinates: .xyz.
- Coordinates with explicit bond information: .mol2.
- Crystallographic-style coordinates: .cif.
- Biomolecular-style coordinates: .pdb.

### Calculation Settings

Depending on the chosen input format and job, the Generate sheet can include:

- Job type, including optimisation, frequency, transition-state, reaction-path, scan, and excited-state workflows where supported.
- Molecular charge and spin multiplicity.
- Method and basis selection.
- Dispersion and solvation options.
- Processor and memory fields.
- Reaction-path direction and path controls.
- One-dimensional or two-dimensional relaxed-scan settings.
- Excited-state count.

Selecting two to four atoms in order can prefill a scan coordinate. A distance uses two atoms, an angle uses three, and a dihedral uses four. After choosing Scan, select one- or two-dimensional mode and check the start, end, step, and point values shown for the selected format.

When a recognised input or output file is used as the source, Magpie carries forward compatible settings such as the job type, scan coordinates, reaction-path controls, or excited-state count when those values can be recovered reliably. Always review the generated text before using it for a calculation.

## Reviewing Computational Results

Open a supported computational output file to review the data that Magpie recognises. The document may provide:

- Molecular frames and optimisation-step navigation.
- A calculation status indicating complete, incomplete, or failed output.
- Information rows for the calculation and molecular system.
- Thermochemistry values when reported.
- Convergence values and convergence plots.
- Vibrational modes.
- Reaction-path and relaxed-scan results.
- Absorption spectra and reported electronic transitions.
- Input-setting hints that can be reused by Generate.

### Details and Convergence

Use the Details panel to inspect available information, thermochemistry, and convergence rows. Missing sections normally mean that the source file did not contain recognised values for that calculation type.

### Reaction Paths and One-Dimensional Scans

The analysis view combines trajectory controls with an energy curve. Move through the path with the frame controls or select a point in the curve. The displayed molecule follows the selected result frame.

### Two-Dimensional Scans

For a recognised two-dimensional relaxed scan:

1. Use Trajectory to inspect the molecular frames.
2. Use Details to review values associated with the current frame.
3. Tap 2D Scan in the bottom bar to open the potential-energy surface.
4. Rotate a complete 3D surface or inspect the contour view.
5. Select a plotted point to display the associated molecular geometry.

A complete rectangular grid can be shown as a rotatable surface. Sparse or incomplete data are shown as a contour plot. Missing scan points remain gaps; Magpie does not bridge across absent corners or create artificial calculation results.

### Spectrum and Electronic Transitions

When recognised excited-state data are present, Magpie separates the broadened absorption spectrum from the list of reported electronic transitions. Use the spectrum for the wavelength and relative-intensity overview, and the transition panel for the states and orbital contributions printed by the source output.

## CUBE Volumetric Data

Open a .cub or .cube file to display scalar-field data around its molecular structure.

- A single CUBE file can be opened as a surface document.
- A workflow may ask for a second compatible CUBE file when one field is used for the surface and another for colouring.
- Wait for the download, parsing, and surface-building progress to finish before changing files.
- Surface appearance and related rendering preferences can be adjusted in Settings.

Very large grids may take longer to parse and render. If a file does not open, confirm that its header, grid dimensions, units, and scalar values form a valid single-dataset CUBE document.

## Molecular Orbitals from a Remote System

Magpie can prepare orbital visualisations from supported wavefunction files stored on a configured remote system. This is an optional workflow and requires compatible scientific analysis software to be installed and working on that server.

1. Connect to the server and browse to a supported wavefunction file.
2. Open the file and allow Magpie to prepare the molecular geometry and orbital inventory.
3. Review orbital energy, occupation, spin, and frontier-orbital information when available.
4. Select an orbital to build and display its surface.
5. Change orbitals from the molecular-orbital sidebar.

Magpie may prefetch and temporarily cache orbital artifacts during the active session to make nearby selections faster. If preparation fails, first confirm that the remote file is readable and that the required analysis command is installed and available in the server environment.

## Optional SSH/SFTP Workspace

Magpie can connect directly to a server configured by the user. No remote connection is required for local viewing, editing, generation, or result review.

### Add a Server Profile

Provide:

- Server address.
- SSH port.
- Username.
- Password or private-key authentication, as supported by the server.
- The desired starting path, with the remote home folder available through the usual tilde path.

On the first connection, carefully compare and accept the host identity only when it matches the server you intended to use. If the server uses keyboard-interactive authentication or a verification prompt, complete the additional prompt shown by Magpie.

### Browse and Manage Remote Files

After connecting, you can:

- Browse remote folders.
- Open supported remote files in the appropriate viewer.
- Download a remote file into the local workspace.
- Create, rename, copy, save, or delete items when the action is available and your server permissions allow it.
- Use the same active connection for file browsing, terminal access, and compatible remote analysis workflows.

### Interactive Terminal

Open Terminal when you need a command-line session on the connected server. The terminal uses the active SSH connection and supports interactive input. Its presentation adapts to the device: it can appear beside the workspace on iPad and as a dedicated full-screen view on iPhone.

Close the terminal session when it is no longer required, and disconnect from the server when all remote work is complete.

## Settings

Settings contains controls for the molecular viewer and scientific surface presentation. Available options may include:

- Viewer background colour.
- Main and fill-light intensity.
- Volumetric and orbital surface appearance.
- Molecular-orbital display preferences.
- App information, acknowledgements, scientific credits, and licence notices.

Return to the open document after changing a display preference to review the result.

## Troubleshooting

### A File Does Not Open

- Confirm that the filename uses a supported extension.
- Confirm that the file is complete and is not an HTML download or other unrelated document renamed with a scientific extension.
- For text-based scientific files, confirm that the coordinates or output sections are present and readable.
- Import the file into the local workspace again and retry.
- If only advanced result panels are absent, the structure may be valid while the optional result data are missing or unrecognised.

### A Trajectory, Vibration, or Result Panel Is Missing

- Confirm that the source calculation contains the relevant frames or result section.
- Confirm that the calculation reached the stages required to print those results.
- Reopen the file after it has been fully written or transferred.
- For related companion files on a remote system, keep them in the same folder with their expected base filename.

### A CUBE or Orbital Surface Does Not Appear

- Wait for parsing and surface-building progress to finish.
- Confirm that the CUBE file contains a valid grid and one scalar dataset.
- For a paired CUBE workflow, select compatible files covering the same molecular region.
- For remote orbitals, confirm that the required server-side software is installed and that the source file is supported.

### A Remote Connection Fails

- Check the server address, port, username, and authentication method.
- Confirm that the device can reach the server's network.
- Check the password, key, and any additional verification prompt.
- If the host identity has changed unexpectedly, stop and ask the server administrator before continuing.
- Contact the server administrator if your account lacks access to the selected path or command.

### The Viewer or Animation Stops Updating

- Pause and restart the trajectory or vibration animation.
- Close the current document and open it again.
- If the issue continues, close and relaunch Magpie.

### A Generated File Cannot Be Saved

- Confirm that the filename and extension match the chosen format.
- Confirm that the destination folder is writable.
- For a remote destination, confirm that the connection is active and that no file with the same protected name is blocking creation.
- Save to the local workspace first, then export or transfer the file.

## Contact Support

For help, feedback, or a feature request, contact:

**Email:** [umpire-mesons-4q@icloud.com](mailto:umpire-mesons-4q@icloud.com)

When reporting a problem, include the device model, iOS or iPadOS version, Magpie version, file extension, whether the file was local or remote, and the steps needed to reproduce the issue. Do not send passwords, private keys, verification codes, or confidential scientific files.

Last updated: 31 July 2026.

