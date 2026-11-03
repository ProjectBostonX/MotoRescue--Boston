# Moto Rescue (Android Studio project)

**Version:** 0.1.0 — USB/Fastboot diagnostic starter project

This is a native Android app project for a Moto G Stylus 5G (2024) used as the host phone to inspect a connected target device. It is intentionally limited to USB detection, Fastboot `getvar` diagnostics, and reboot commands. It does not unlock the bootloader, erase data, or flash partitions.

## Important limits

- The host phone must support USB host/OTG. USB-C to USB-C does not guarantee the host phone will become the USB host; if no device appears, use a USB-C OTG adapter plus a data-capable cable.
- Put the target in **bootloader Fastboot** mode. Android Recovery menus are not the same thing as Fastboot.
- The target bootloader may be locked. This app does not bypass bootloader security.
- This is a starter project, not a tested/verified APK. USB vendor/interface layouts differ; some phones may not be recognized by this simple Fastboot transport.
- Do not add flashing until exact model/variant, bootloader state, image provenance, partition layout, and rollback strategy are verified. A wrong image can brick the phone or erase data.

## Open and build

1. Copy this folder to a computer with Android Studio installed, or use a compatible Android Studio environment.
2. Open the `MotoRescue` folder in Android Studio.
3. Allow Gradle sync. Use JDK 17 and Android SDK Platform 35 (Android Studio can install these).
4. Build > Build APK(s).
5. Install the debug APK on the host Moto G Stylus 5G.
6. On the host, connect the target by a data-capable USB connection. If prompted, grant USB permission.
7. Boot the target to bootloader Fastboot and tap **Request USB permission & connect**.
8. Tap **Run Fastboot diagnostics** and save the displayed log for troubleshooting.

## Current functions

- Lists USB devices and VID/PID.
- Searches for a bulk USB interface suitable for Fastboot.
- Requests Android USB permission and opens the interface.
- Sends read-only `getvar:product`, `getvar:unlocked`, `getvar:current-slot`, `getvar:version`, and `getvar:is-userspace` requests.
- Provides `reboot-bootloader` and `reboot` commands.
- Keeps a simple in-app log.

## Troubleshooting

- If no USB device appears: try a different data cable, OTG adapter, or confirm host USB host support.
- If a USB device appears but no Fastboot interface is found: verify the target is in bootloader Fastboot, not Recovery or Android; some vendor implementations need transport adjustments.
- If commands time out: reconnect and retry; do not repeatedly issue commands while the target is changing modes.
- This app does not currently support ADB, firmware download, image verification, flashing, or Rescue and Smart Assistant integration.

## Project details

- Java, Android SDK 35, minimum Android 8.0 (API 26), Java 17.
- Android Gradle Plugin 8.7.3.
- Gradle wrapper is not included; Android Studio will prompt to configure/download a compatible Gradle distribution.
