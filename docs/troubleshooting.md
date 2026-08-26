# Troubleshooting

This document records problems actually encountered during testing.

## GTA immediately exits after installing LSPDFR

Observed Rockstar Launcher error:

    STATUS_DLL_NOT_FOUND
    0xc0000135

The LSPDFR manual installation placed `XInput1_4.dll` in the GTA V root directory.

On our tested Proton configuration, GTA V launched successfully after renaming:

    XInput1_4.dll

to:

    XInput1_4.dll.disabled

This workaround has only been confirmed on the tested configuration and
should not yet be assumed necessary on every Linux/Proton installation.

## Protontricks fails over SSH

Running some Protontricks commands from a plain SSH session produced:

    Can't find session bus: Cannot autolaunch D-Bus without X11 $DISPLAY

followed by:

    RuntimeError: bwrap launcher crashed, returncode: 69

This does not mean the GTA V Proton prefix is damaged.

Some Protontricks operations require access to the graphical user's
session environment.
