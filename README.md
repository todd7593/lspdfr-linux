# LSPDFR on Linux

Community documentation for running **LSPDFR (LSPD First Response)** and
**RAGE Plugin Hook** with Grand Theft Auto V on Linux using Steam and Proton.

## Project status

Experimental, but working.

A functioning installation has been achieved on Gentoo Linux using:

- Grand Theft Auto V Legacy (Steam)
- LSPDFR 0.4.9 Build 9695
- RAGE Plugin Hook
- GE-Proton11-1
- Protontricks 1.13.1
- AMD Radeon RX 9070 XT

LSPDFR has successfully loaded into Story Mode and character creation has
been completed.

## Purpose

The goal of this project is to document a reproducible Linux installation,
record known compatibility problems and their solutions, and provide useful
Linux-specific tooling for LSPDFR users.

This is an unofficial community project.

This project is not affiliated with Rockstar Games, LCPDFR, LSPDFR,
RAGE Plugin Hook, Valve, or GE-Proton.

Third-party software is not redistributed here. Users should obtain all
required software from its official source.

## Documentation

Documentation is currently being assembled from a known-working Gentoo
installation.

Planned documentation includes:

- Installation
- Proton configuration
- RAGE Plugin Hook launching
- Troubleshooting
- Known-good versions
- Known failures and workarounds
- Plugin compatibility
- Distribution/GPU compatibility reports

## Important discovery

The LSPDFR manual-install package includes `XInput1_4.dll`.

On the tested Proton configuration, having this DLL active in the GTA V
directory caused GTA V to terminate during startup with:

    STATUS_DLL_NOT_FOUND (0xc0000135)

Renaming it to:

    XInput1_4.dll.disabled

allowed GTA V to launch again.

Further testing and documentation are in progress.

## Contributions

Linux users are welcome to contribute test results and fixes once the
project is publicly available.

Please include relevant information such as:

- Linux distribution
- Kernel
- GPU
- GPU driver
- Proton version
- GTA V version
- LSPDFR version
- RAGE Plugin Hook version
- Relevant logs/error messages
