# Magpie User Manual and Support

Magpie is a free molecular visualisation and scientific post-processing app for iPhone and iPad. It is designed for computational chemistry research, teaching and learning.

## Getting Started

When Magpie opens, choose the local workspace to work with files on your device. You can also configure an optional remote connection to a server that you own, administer or are authorised to use.

### Local Workspace

1. Open the local workspace.
2. Import an existing file from the iOS or iPadOS Files interface, or create a new text file or molecular model.
3. Tap a file to open it.
4. Use the file menu to rename, copy, delete, export or save files when those actions are available.

Magpie can work with common molecular coordinate files, computational chemistry input and output files, volumetric data files, images and plain text files.

## Viewing Molecules

After opening a supported molecular file, use the 3D workspace to rotate and zoom the structure. Depending on the file contents, Magpie may also display:

- Atoms, bonds and molecular geometry
- Optimisation or reaction-path frames
- Vibrational modes
- Volumetric and molecular-orbital surfaces
- Calculation details and convergence information
- Spectra and electronic transitions
- One- and two-dimensional scan results

Use the available trajectory controls to move between frames or play an animation.

## Editing Molecular Geometry

Open the editing tools from the molecular workspace to:

- Select atoms and change elements
- Add or modify bonds
- Adjust bond lengths, angles and dihedral angles
- Add atoms or molecular fragments
- Undo or redo editing operations

Edits remain in the current editing session until you save or generate a new file.

## Generating Files

Use **Generate** in the molecular workspace to create a computational chemistry input file or a coordinate file from the current structure.

1. Open a molecular structure.
2. Select **Generate**.
3. Choose the required format and calculation settings.
4. Review the generated text.
5. Save the generated file to the local workspace.

## Reviewing Computational Results

When a supported computational output file contains recognised results, Magpie may provide dedicated panels for calculation details, thermochemistry, convergence, trajectories, spectra and scan data.

For a two-dimensional scan, use the **2D Scan** button to open the potential-energy surface. Complete data may be displayed as a rotatable surface, while sparse data is shown as a contour plot.

## Volumetric Data and Molecular Orbitals

Open a supported volumetric data file to display its surface with the associated molecular structure. Some workflows may require selecting or pairing related files.

Remote molecular-orbital workflows require compatible scientific tools to be installed and available on the server configured by the user.

## Optional Remote Access

Magpie can connect directly to a user-configured SSH/SFTP server.

1. Add a server profile with the server address, port, username and authentication method.
2. Verify the server identity when prompted.
3. Browse remote folders and open supported files.
4. Use the terminal when command-line access is required.
5. Disconnect when the remote session is no longer needed.

Only connect to servers that you own, administer or are authorised to access. Magpie does not provide a remote server, user account or cloud-storage service.

## Troubleshooting

### A file does not open

- Confirm that the file uses a supported format and filename extension.
- Confirm that text-based files are valid and complete.
- Try importing the file into the local workspace again.

### A remote connection fails

- Confirm the server address, port and username.
- Confirm that the device has network access to the server.
- Check the selected authentication method and credentials.
- Contact the server administrator if the server rejects the connection or requires additional authentication.

### A view or animation does not update

Close the current file and open it again. If the issue continues, close and relaunch Magpie.

## Privacy and Security

Magpie has no developer-operated backend, advertising, analytics service, user account system or cloud storage. Local files remain on the device unless the user chooses to import, export or transfer them. Optional remote connections are made directly to the server selected by the user.

Do not send passwords, private keys, verification codes or confidential scientific files when requesting support.

## Contact Support

For support, feedback or feature requests, contact:

**Email:** [umpire-mesons-4q@icloud.com](mailto:umpire-mesons-4q@icloud.com)

When reporting a problem, please include the device model, iOS or iPadOS version, Magpie version, file type and steps needed to reproduce the issue. Remove confidential information before sharing examples.

_Last updated: 31 July 2026._
