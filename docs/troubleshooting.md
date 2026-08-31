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

## Vanilla LSPDFR prisoner transport terminates GTA V

Vanilla LSPDFR prisoner transport has caused the complete GTA V Legacy
process to terminate during testing.

The failure has been reproduced more than once immediately after requesting
prisoner transport.

During one captured occurrence, LSPDFR successfully assigned the prisoner to
its transport manager, but no managed LSPDFR fatal exception was recorded
before GTA V disappeared.

Current status:

- Reproducible on the tested configuration
- Root cause unknown
- Avoid vanilla LSPDFR prisoner transport for now
- Stop The Ped prisoner transport is being tested as a workaround

This should not be confused with the Duty Garage failure below.

## LSPDFR Duty Garage throws vehicle spawn exception

Opening or using the LSPDFR Duty Garage produced:

    System.InvalidOperationException:
    Could not spawn new vehicle.

The exception originated from `DutyGarageMenu.cs`.

Unlike the prisoner transport failure, GTA V and RAGE Plugin Hook remained
running while LSPDFR force-terminated.

Attempting to reload LSPDFR afterward resulted in an unusable or frozen
session.

Current workaround:

- Do not use the LSPDFR Duty Garage
- If LSPDFR terminates with a fatal exception, restart GTA V rather than
  attempting to reload LSPDFR in the same game session
