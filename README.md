# OpenMC Windows Installation Guide

## System Requirements
- Windows 10 or Windows 11 (64-bit)
- Python 3.10 or newer
- `pip` installed and available in the system PATH
- ENDF/B HDF5 cross section library (`cross_sections.xml`)

## Step 1 – Install Python
Download Python from: https://www.python.org/downloads/windows/

During installation enable:
- Add Python to PATH
- Install `pip`

Verify:
```cmd
python --version
pip --version
```

## Step 2 – Install OpenMC Windows
Run:
```cmd
openmc-windows-installer.exe
```

The installer will:
- Install the native OpenMC executable
- Install required runtime libraries
- Add OpenMC to the Windows PATH
- Configure the `OPENMC_CROSS_SECTIONS` environment variable
- Install the OpenMC Python module (if `pip` is available)

## Step 3 – Select Nuclear Data
When prompted, select the folder containing: `cross_sections.xml`

Example:
```
D:\endf-b-vii.1-hdf5
```

The installer automatically configures:
`OPENMC_CROSS_SECTIONS=D:\endf-b-vii.1-hdf5\cross_sections.xml`

## Step 4 – Verify Installation
Open a new Command Prompt:
```cmd
openmc --version
```
Expected output:
`OpenMC version 0.15.x`

Python API:
```python
python
import openmc
print(openmc.__version__)
```

## Running a Simulation
```cmd
cd examples
openmc
```

or

```python
import openmc
openmc.run()
```

## Updating the Python Module
```cmd
python -m pip install --upgrade openmc
```

## Uninstalling
Settings → Apps → Installed Apps → OpenMC Windows → Uninstall

Remove Python module:
```cmd
python -m pip uninstall openmc
```

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

## Notes
- Native Windows build (WSL is not required to run).
- Compatible with the OpenMC Python API.
- Uses the official OpenMC HDF5 nuclear data library.
