# AirTV Gen1 OS strategy and compatibility plan

## The central problem

The original AirTV Player may still have useful hardware, but its aging Android TV software is likely to be the biggest practical obstacle to a modern media-hub revival. Third-party device references report Android TV 7.1.1 for this model. **That version is not yet verified on our physical unit.** The first task is to capture the exact build from Settings or ADB.

A newer operating system is not automatically possible just because the processor is ARM-based. Android and Linux both need a compatible boot chain, kernel, device tree, display pipeline, GPU, Wi-Fi, audio, storage, and other device-specific drivers.

## Project objective

Investigate the safest and most realistic way to turn the AirTV Gen1 into a useful, TV-friendly media device. Preserve the original installation until a verified backup and recovery path exist.

## Three software paths

### Path A — Extend stock Android TV (first priority)

Start with read-only inventory and reversible app tests. This path has the lowest hardware risk and will tell us how much useful life remains in the stock system.

Record:

- Exact Android version, build number, build fingerprint, and security patch level.
- CPU ABI and supported APK architectures.
- Android System WebView and Chrome versions.
- Available RAM, internal storage, and external USB storage behavior.
- Installed package list and Play Store availability.
- Remote-control navigation, HDMI output, audio, networking, and hardware video decoding behavior.

Then test one application at a time. Do not install a large bundle and do not remove stock apps to make room before the baseline is recorded.

### Path B — Investigate a newer Android build

A newer Android version could improve app compatibility, but feasibility is unknown. Research must establish:

1. Whether the bootloader permits a documented alternate boot or recovery path.
2. Whether a usable kernel source and matching configuration exist for this exact board.
3. Whether a device tree and vendor boot components can be obtained or reconstructed.
4. Whether display, HDMI, audio, Ethernet, Wi-Fi, Bluetooth, USB, storage, and remote input drivers are available.
5. Whether the Vivante GC7000XS graphics stack can provide working acceleration.
6. Whether a complete, recoverable image can be built and tested without risking the only working unit.

Android 9 or newer is an investigation target, not a promise or an announced upgrade. Do not unlock, flash, root, or write partitions during the initial research.

### Path C — Investigate ARM Linux

Treat Linux as a separate experimental track. A kernel reference, open-source publication, or SoC family support does not prove that a complete distribution can boot this AirTV board. The same device-specific boot, display, GPU, network, audio, and peripheral requirements apply.

SteamOS is not the target: it is designed primarily for x86-64 AMD hardware. A lightweight ARM Linux media system or a remote game-streaming client would be more plausible research directions, but neither is currently demonstrated.

## Application compatibility watchlist

These are candidates to investigate, not confirmed working AirTV apps. Compatibility can change by release; check the exact APK's minimum Android SDK, ABI, and dependencies before installation.

| Application | Research priority | Current compatibility note |
|---|---|---|
| Nuvio | First test | Its Android TV download information reports Android 5.0+; verify the exact release and test on-device. |
| Kodi | First test | Strong local-media candidate; select a release compatible with the device's Android version and ABI. |
| Stremio | First test | Official Smart TV guidance reports Android TV 5.0+; actual playback and service compatibility remain untested. |
| Jellyfin | Next | Android TV client is reported to support Android 6+; requires a Jellyfin server elsewhere on the network. |
| ARVIO | Investigate | Interesting media-hub candidate; exact minimum Android version must be confirmed. |
| Odin | Investigate | Server/client ecosystem; AirTV client version and OS floor need verification. |
| AIOStreams | Investigate carefully | Android TV app has a WebView dependency; reported WebView/Chrome requirement may be a blocker on old firmware. |
| WuPlay | Likely blocked if Android 7.1.1 is confirmed | Latest beta compatibility notes report Android 9+; check older releases only if there is a clear reason. |
| Emby | Further research | Verify exact Android TV client release and minimum SDK. |
| Cloudstream / Silo | Further research | Confirm exact project identity, release source, and minimum Android version before testing. |

Only install applications from their official project or trusted distribution channels, and use media sources and services you are authorized to access. Nuvio and similar library interfaces do not themselves grant rights to media.

## Test protocol

For each candidate, record:

- App name, release/version, official download source, minimum SDK, and APK ABI.
- Whether it installs, launches, and survives a reboot.
- First-launch time and navigation responsiveness using the original remote.
- Memory and storage impact.
- Playback success for representative local/network files, including resolution, codec, and container.
- Audio output, subtitles, seeking, and playback stability.
- Whether hardware decoding is used and whether the device overheats or becomes unstable.

Do not describe an app as supported based only on its Android minimum version. A successful installation is not the same as smooth playback.

## Safety and recovery gates

- Keep the stock system intact during initial inventory.
- Do not factory reset, root, unlock the bootloader, remove system packages, flash firmware, or write partitions as part of compatibility testing.
- Do not expose ADB to public or untrusted networks.
- Before any operating-system experiment, obtain a verified stock backup and document a tested recovery method. If neither is available, do not proceed with destructive changes.
- Keep all conclusions labeled as **official**, **reported**, **observed**, **tested**, or **unknown**.

## Milestones

1. **OS baseline captured:** exact build fingerprint, Android version, ABI, WebView, memory, and storage recorded from the physical device.
2. **App matrix completed:** at least three candidates tested individually with reproducible results.
3. **Boot and driver feasibility assessed:** evidence collected for bootloader, kernel, device tree, GPU, and peripheral support.
4. **OS decision documented:** choose stock Android optimization, newer Android research, Linux research, or stop if recovery risk is unacceptable.

No milestone is complete until the result is reproducible on the physical AirTV Player.
