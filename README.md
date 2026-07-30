# OpenMC Windows Installation Guide (v0.1-beta)

- This is beta version; hence number of particles is restricted to 10000, and batches to 200.   
- **Get the stable full version at:** https://shetsdp.github.io/blogs/openmc-windows.html   
- Fill this form to know future updates: https://www.google.com/   
- Installing video guide: https://www.youtube.com/   
- Technical Note: https://www.google.com/   

Author:   
Sachin Shet   
https://www.google.com/   


## System Requirements
- Windows 10 or Windows 11 (64-bit)
- Python 3.10 or newer
- `pip` installed and available in the system PATH
- ENDF/B HDF5 cross section library (`cross_sections.xml`)

## Step 1 – Install Python
Download Python from: https://www.python.org/downloads/windows/

Link: https://www.python.org/ftp/python/3.14.6/python-3.14.6-amd64.exe

During installation enable:
- Add Python to PATH

Verify:
```cmd
python --version
python -m pip --version
```
## Step 2 – Prepare Nuclear Data

Download Nuclear data from OpenMC Website https://openmc.org/data/

Link: https://anl.box.com/shared/static/9igk353zpy8fn9ttvtrqgzvw1vtejoz6.xz

Create a folder `OpenMC` in a drive, where you have write permission, and extract the cross sections data in it.

Example:
```
D:\OpenMC\endf-b-vii.1-hdf5\
```

## Step 3 – Install OpenMC Windows

Download `openmc-windows-v0.1-beta-installer.exe` from the release page and execute the installer.

The installer will:
- Install the native OpenMC executable
- Install required runtime libraries
- Add OpenMC to the Windows PATH
- Configure the `OPENMC_CROSS_SECTIONS` environment variable
- Install the OpenMC Python module (if `pip` is available)

When prompted, select the folder containing: `cross_sections.xml`

Select `D:\OpenMC\endf-b-vii.1-hdf5\`

The installer automatically configures:
`OPENMC_CROSS_SECTIONS=D:\OpenMC\endf-b-vii.1-hdf5\cross_sections.xml`

## Step 4 – Verify Installation

Signout and Signin back to your windows account. This will add new directory to the system PATH variable.

Open a new Command Prompt (Win+R, type `cmd`, Enter):

```cmd
openmc --version
```
Expected output:
```cmd
OpenMC version 0.15.3
Commit hash: 27e38e894697bb32a1dac7848d2618818b6b8daf
Copyright (c) 2011-2025 MIT, UChicago Argonne LLC, and contributors
MIT/X license at <https://docs.openmc.org/en/latest/license.html>
Build type:            Release
Compiler ID:           GNU 15.2.0
MPI enabled:           no
Parallel HDF5 enabled: no
PNG support:           yes
DAGMC support:         no
libMesh support:       no
MCPL support:          no
Coverage testing:      no
Profiling flags:       no
UWUW support:          no
```

Python API:
```python
python
import openmc
print(openmc.__version__)
```
Expected output:
`0.15.3`

## Running a Simulation

Copy OpenMC examples to your `OpenMC` directory

Copy `C:\Program Files (x86)\OpenMC\examples` to `D:\OpenMC` directory.

```cmd
cd D:\OpenMC\examples\jezbel\
```

```cmd
python jezbel.py
```

OpenMC Should be running at this point. Congratulations.


# Important Notes
- Native Windows build (WSL or DOCKER is not required to run).
- Compatible with the OpenMC Python API.
- Uses the official OpenMC HDF5 nuclear data library.
- Work in progress to build stable OpenMC GUI

## Troubleshooting
1. **'openmc' is not recognized**
   - Restart Command Prompt.
   - Verify OpenMC installation directory is in PATH.
2. **Python module installation failed**
   - Run: `python -m pip install openmc`
3. **OPENMC_CROSS_SECTIONS is not set**
   - Check: `echo %OPENMC_CROSS_SECTIONS%`
   - If empty, create the environment variable manually.
4. **Missing DLL errors**
   - Ensure all DLLs remain in the same directory as `openmc.exe`.
