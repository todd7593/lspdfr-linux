# GTA V Audio Investigation

Status: Active investigation

Initial observations: August 30, 2026

## Symptom

During some GTA V Legacy sessions under Proton, all GTA game audio
intermittently disappears while the game itself continues running.

The failure does not currently have a known reproducible trigger.

## Captured failed-state observations

During a captured audio failure:

- GTA5.exe remained running
- PipeWire remained running and responsive
- WirePlumber remained running
- The normal system audio output remained available
- `wpctl status` no longer showed a GTA V playback stream
- `pactl list sink-inputs short` likewise showed no GTA V playback stream
- The Rockstar Games Launcher audio stream remained visible
- GTA V still had game audio archive files open
- Wine audio components remained loaded, including:
  - winepulse.drv
  - winepulse.so
  - libpulse.so
- Wine audio-related threads remained present, including:
  - wine_mmdevapi
  - audio_client
  - wine_dsound_mix

Changing GTA V's in-game audio settings did not recreate the missing host
audio stream.

## DirectSound mixer observation

During one failed session, GTA5.exe had approximately 120
`wine_dsound_mix` threads.

Repeated measurements remained stable at approximately the same count.

This is currently an observation only.

There is no evidence yet that the number of DirectSound mixer threads causes
the audio failure.

## Current working model

The captured evidence suggests that GTA V or Wine loses its host playback
stream while the game process and much of Wine's internal audio machinery
remain active.

The failure appears to occur somewhere in or around the application/Wine
audio path before audio reaches PipeWire.

This remains a hypothesis and has not been established as the root cause.

## Planned comparison

Future testing will collect three comparable states.

### Stage A - Vanilla GTA V, audio working

Start GTA V Legacy normally without RAGE Plugin Hook.

After entering Story Mode and confirming working audio, capture:

- GTA PID
- PipeWire status
- PulseAudio-compatible sink inputs
- DirectSound mixer count
- relevant Wine/GTA audio threads

### Stage B - Modded GTA V, audio working

Launch the currently tested RAGE Plugin Hook/LSPDFR configuration and repeat
the same measurements while audio is still working.

Current plugin configuration includes:

- LSPDFR
- RAGENativeUI
- Stop The Ped
- Prowler Radar

### Stage C - Modded GTA V, audio failed

If audio disappears, capture the same measurements before changing settings,
restarting PipeWire, reloading LSPDFR, or restarting GTA.

## Investigation rules

To avoid introducing false conclusions:

- Do not assume correlation implies causation
- Record gameplay events near each failure
- Preserve successful sessions as controls
- Avoid random Winetricks packages or DLL overrides during baseline testing
- Avoid PipeWire configuration changes until comparative evidence indicates
  they are relevant
- Do not attribute the failure to particular plugins without reproducible
  evidence

The objective is to collect multiple failed and successful sessions and
compare their timelines before attempting invasive changes.

## Possible upstream value

If the failure can be isolated and reproduced, the collected information may
be useful to Wine, Proton, PipeWire, GE-Proton, or other relevant developers.

Any upstream report should include only verified observations, exact software
versions, reproducible test steps where available, and sanitized diagnostic
information.
