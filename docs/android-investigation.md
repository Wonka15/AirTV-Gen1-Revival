# AirTV Gen1 Android investigation

## Goal

Investigate the stock Android TV environment on the original AirTV Player and determine whether the experience can be improved without replacing the operating system. The first phase is read-only inventory through Android Debug Bridge (ADB), using a Mac.

## Current status

- The owner reports that the AirTV Player still boots and works.
- The owner remembers enabling Developer Options previously.
- USB debugging is currently not enabled.
- The Mac-side ADB connection has not yet been tested.
- No root access, custom launcher, modified firmware, or alternate OS is claimed to work.

Treat all planned capabilities as hypotheses until tested on the exact physical unit.

## Phase 1 — Prepare the Mac

1. Download Google's official [Android SDK Platform-Tools](https://developer.android.com/tools/releases/platform-tools) for macOS.
2. Extract the archive and open Terminal in the extracted `platform-tools` directory.
3. Verify the installation:

```bash
./adb version
```

## Phase 2 — Inspect Android settings

On the AirTV Player, inspect Settings and record the exact menu labels and Android build information. If Developer Options are not visible, open About and check whether the Android TV OS build entry supports the standard seven-click activation gesture. Menu labels can vary by vendor firmware.

Only enable USB debugging when ready to connect the Mac. If the device exposes a wireless debugging option, record its exact name and pairing instructions before enabling it. Do not assume that legacy ADB over TCP port 5555 is available.

## Phase 3 — Establish a connection

Prefer a supported USB ADB connection if the hardware and firmware expose one. Otherwise, use the device's own wireless debugging/pairing interface if present and supported by its Android version.

For a wireless-debugging pairing flow, follow the IP address, port, and pairing-code instructions displayed by the AirTV. The modern Platform-Tools workflow uses `adb pair` followed by `adb connect`; do not substitute a guessed address or port.

After connection:

```bash
./adb devices -l
```

Approve the RSA authorization prompt on the television only if it is the Mac you intend to trust. Keep debugging disabled when the investigation session is finished, especially if wireless debugging was enabled.

## Phase 4 — Read-only inventory

Once ADB is authorized, collect baseline information:

```bash
./adb shell getprop
./adb shell getprop ro.product.model
./adb shell getprop ro.build.version.release
./adb shell getprop ro.build.fingerprint
./adb shell cat /proc/cpuinfo
./adb shell df -h
./adb shell pm list packages
```

Save the output locally with the date and the exact AirTV model label. Redact serial numbers, Wi-Fi details, account identifiers, and other private information before publishing logs.

These commands are intended for inspection. ADB shell access does not imply root access; do not use `su` or attempt privilege escalation as part of this first phase.

## Phase 5 — Reversible experience experiments

Only after the baseline is recorded, investigate compatible TV launchers and media applications. Prefer installing a test app without disabling or uninstalling stock packages. Verify remote-control navigation, boot behavior, app compatibility, playback, audio, and storage behavior. Keep a clear path back to the stock launcher.

## Safety boundaries

During this initial investigation:

- Do not factory-reset the device.
- Do not select OEM unlocking or unlock the bootloader.
- Do not root the device or attempt privilege escalation.
- Do not remove or disable preinstalled system packages.
- Do not flash firmware, write partitions, or change bootloader variables.
- Do not assume a UART pad's voltage or pinout.
- Do not expose ADB to a public or untrusted network.
- Do not publish logs containing credentials, serial numbers, MAC addresses, or account data.

Before any future system-level modification, identify a verified stock firmware image and a tested recovery method. If no recovery path exists, preserve the stock system.

## Project milestone

**Milestone A — ADB inventory complete:** A successful authorized ADB connection, saved stock build fingerprint, Android version, package inventory, CPU information, and storage report, with private identifiers redacted.

No milestone is complete until the results come from the physical AirTV Player and can be reproduced.
