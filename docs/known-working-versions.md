# Known Working Configuration

Initial confirmed configuration: August 2026

## System

- Distribution: Gentoo Linux
- Gentoo Base System: 2.18
- Kernel: 6.18.39-gentoo-consolefix-xbox
- CPU: AMD Ryzen 9 9950X
- GPU: AMD Radeon RX 9070 XT (Navi 48)

## Software

- Steam Launcher: 1.0.0.87
- Protontricks: 1.13.1
- GE-Proton: GE-Proton11-1
- GTA V: Legacy / Steam
- LSPDFR: 0.4.9 Build 9695

## Tested download checksums

### LSPDFR manual installation ZIP

SHA-256:

    05c4116c7d9b7b7e07f92baf07a690f8583fc8bb19e5eb929ceef1b761e28ee1

### GE-Proton11-1 archive

SHA-256:

    ce6dd663ea01725a31805ed5c165723a253cdf0945a6642907330742ae2de5e4

These checksums identify the exact files used for the initial successful
test. Third-party files are not distributed by this project.

## Confirmed plugin compatibility

### RAGENativeUI

- Version: 1.9.3
- Status: Confirmed working

SHA-256:

    d2607481b206e7907c9c1f2cabf15797654aacaaf1746ea202740dcdd5eb8bbb

### Prowler Radar

- Version: 1.3.1
- Status: Confirmed working
- Requires RAGENativeUI 1.9.3 in the tested installation

A Rockstar Launcher Error 17 was observed during earlier testing, but the
error could not be reproduced after restoring the exact same Prowler files.
Prowler Radar should therefore not currently be considered the cause of that
incident.

### Stop The Ped

- Version: 4.9.5.4
- Status: Working in initial testing
- Installed as an LSPDFR plugin

The RAGENativeUI.dll included with Stop The Ped 4.9.5.4 was compared against
the already-tested RAGENativeUI 1.9.3 DLL and was byte-for-byte identical.

Tested Stop The Ped configuration includes:

    TakeOverAllArrests=yes

    [PrisonerTransport]
    PrisonerTransportEnabled=yes
    SelfTransportEnabled=yes

Initial gameplay testing indicates that Stop The Ped can replace problematic
vanilla LSPDFR arrest/transport functionality. More extensive transport
testing is still in progress.

## RAGE Plugin Hook launch requirement

On the tested installation, RAGE Plugin Hook must be launched with the GTA V
installation directory as its working directory.

Launching RPH from another working directory caused problems even when the
correct executable path was supplied.

A local wrapper script is currently used to change into the GTA V directory
before starting RAGE Plugin Hook.
