# Privacy Policy — Rova

_Last updated: 2026-05-03_

Rova is an Android app for hands-free periodic video recording. This page explains what the app does with data on your device. It covers the current internal-beta build of Rova (`com.aritr.rova`).

## Summary

- Rova records video and (optionally) audio **locally on your Android device**.
- Rova **does not upload** recordings or any other personal data to any server.
- Rova **does not use analytics, advertising, or tracking SDKs**.
- Rova **does not send crash reports** to any remote backend in the current build.
- Recordings leave the device **only when you explicitly share them** through Android's system share sheet.

## What the app processes

- **Video frames** captured from the camera you select.
- **Audio**, if microphone permission is granted. Without microphone permission the app records video-only.
- **Recording configuration** you choose (duration, interval, loop count, resolution, presets). Stored on the device.
- **Session metadata** (start time, segment list, termination reason) used to merge segments and recover from crashes. Stored on the device.

No account, no sign-in, no contact-list access, no location access.

## Where files are written

- App-private storage at `Android/data/com.aritr.rova/files/` for in-progress segments, manifests, and intermediate merge outputs.
- The public **Movies** directory for finalized merged videos, using the right Android API for the device:
  - API 29+: `MediaStore` (scoped storage, no external storage permission needed).
  - API 26–28: scoped temp file then `MediaScannerConnection`.
  - API 24–25: direct path under legacy `WRITE_EXTERNAL_STORAGE`.

Files written to the public Movies directory are visible to other apps on the device, the same as recordings made by the stock camera app.

## What the app does NOT do

- Does not request the `INTERNET` permission. The app has no network capability.
- Does not bundle any network or analytics library (no Firebase, no Crashlytics, no Google Analytics, no third-party SDKs that phone home).
- Does not collect device identifiers, advertising IDs, IMEI, MAC address, or contact data.
- Does not access location.
- Does not read your photo library, files, or other app data.
- Does not run a background service when you are not actively recording.

## Permissions and why

| Permission | Why it is requested |
|---|---|
| `CAMERA` | Capture video. Required to start. |
| `RECORD_AUDIO` | Capture audio. Optional — without it the session is video-only. |
| `FOREGROUND_SERVICE`, `FOREGROUND_SERVICE_CAMERA`, `FOREGROUND_SERVICE_MICROPHONE` | Continue recording with the screen off via a foreground service. |
| `POST_NOTIFICATIONS` | Show the recording notification (Android 13+). |
| `WAKE_LOCK` | Keep the CPU awake across short segment boundaries during a session. |
| `SCHEDULE_EXACT_ALARM` | Schedule the segment-boundary and loop-stop alarms that drive the periodic recording loop. |
| `REQUEST_IGNORE_BATTERY_OPTIMIZATIONS` | Optional prompt — guides you to exempt Rova from Doze so long unattended sessions are not killed. You can decline. |
| `WRITE_EXTERNAL_STORAGE` (API ≤ 28 only) | Legacy storage write path on Android 9 and below. Not used on API 29+. |

## Sharing recordings

Sharing happens only when you tap **Share** in the Rova History tab. This invokes the Android system share sheet, and the destination app (e.g. Photos, Drive, Messages) handles the file from that point. Rova does not control or observe what the receiving app does.

## Vendor / device settings shortcuts

If a session was killed by your device's battery manager, Rova may offer a button that opens your device's auto-start or battery-optimization settings screen (e.g. on Xiaomi, Samsung, OnePlus, Vivo, Oppo). Tapping the button hands off to the system Settings app — Rova reads no data from those screens.

## Android Auto Backup

The app currently has Android's default `allowBackup` enabled. This means app preferences (e.g. saved recording presets) may be included in Android's system backup if you have it enabled on your device. Recorded video files are stored under `Android/data/com.aritr.rova/files/` and finalized merges are in the public Movies directory; the public Movies files are not part of app-specific backup. If you want to fully exclude all app data from backup, disable backup for Rova in Android system settings.

## Children

The app is not directed at children under 13. The app does not knowingly collect any data from children.

## Changes

If the app's behavior changes (for example, if a future release adds crash reporting or cloud sync), this page will be updated and the **Last updated** date at the top will change.

## Contact

For privacy questions about Rova, contact: **[contact email — to be added before public release]**.
