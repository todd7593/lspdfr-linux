# GTA V Enhanced Investigation

This document tracks testing of GTA V Enhanced with RAGE Plugin Hook (RPH) and LSPDFR under Linux/Proton.

Confirmed observations are separated from hypotheses so that the investigation remains reproducible and evidence-based.

## Current Test Environment

- GTA V Enhanced — Steam AppID 3240220
- GTA V Enhanced version 1.0.1158.13
- RAGE Plugin Hook / LSPDFR Enhanced
- GE-Proton11-1
- Gentoo Linux
- AMD Radeon RX 9070 XT
- BattlEye disabled for RPH/LSPDFR testing

Legacy GTA V testing is tracked separately.

## September 12, 2026

### Enhanced Baseline

GTA V Enhanced launched and ran successfully under GE-Proton11-1.

ScriptHookV and Native Trainer were present and functional.

A controller control test of approximately 1 hour 40 minutes of sustained active gameplay completed without an Xbox Wireless Controller physical shutdown or other observed controller problem.

RPH/LSPDFR was not running during this control test.

This does not prove that RPH/LSPDFR causes the controller shutdown previously observed during Legacy testing, but it shows that the controller, Bluetooth connection, Proton, and GTA V Enhanced can remain stable together for an extended active session.
### Enhanced Prefix .NET Repair

`RAGEPluginHook.exe` initially failed with a .NET Framework initialization error requesting .NET Framework v4.0.

The Enhanced prefix's `winetricks.log` contained historical entries for `dotnet40` and `dotnet45`, but registry inspection showed that the expected .NET Framework v4 Full registration was absent.

This demonstrated that historical Winetricks entries alone were not sufficient evidence that the current prefix had a functional registered .NET Framework installation.

The Enhanced prefix was repaired using Protontricks with GE-Proton11-1.

After the repair, the registry contained:

```text
[Software\\Microsoft\\.NET Framework Setup\\NDP\\v4\\Full]
"Install"=dword:00000001
"InstallPath"="C:\\windows\\Microsoft.NET\\Framework64\\v4.0.30319\\"
"MSI"=dword:00000001
"Release"=dword:00070bf6
"Servicing"=dword:00000000
"TargetVersion"="4.0.0"
"Version"="4.7.03062"
### Current RPH Hook Failure

With RPH now able to start normally and recognize GTA V Enhanced, selecting `Save and launch` caused RPH to begin its hook attempt.

RPH then displayed:

```text
Could not hook game process. Insufficient permissions or bad anti-virus.
Please try again. If the problem persists, please restart your computer.
### Comparison With Earlier Enhanced Testing

An earlier Enhanced test on August 23, 2026 failed at a different stage.

That failure involved:

```text
System.InvalidProgramException
Invalid IL code
Unknown heap type: #Strings
Unknown heap type: #Blob
Unknown heap type: #Schema
