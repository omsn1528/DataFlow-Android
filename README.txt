DataFlow 2.0  -  Android Studio project   (developer: Always ON)
=====================================================================
STATUS: source code written and reviewed by hand. It has NOT been compiled or run on a
device by the author, so a small first-build fix is possible. Paste any error to Claude.

OPEN
1. Extract this zip into a NEW folder named DataFlow (settings.gradle.kts must sit directly inside it).
2. Android Studio > File > Open > select that DataFlow folder > Trust Project.
3. Wait for Gradle sync (needs internet; first time 5-15 min on slow PCs).
   If it asks to update Gradle or the Android plugin, choose "Don't remind" / skip.
   If you see a Java error: Settings > Build Tools > Gradle > Gradle JDK > pick 17 or 21.

BUILD APK
Build > Build App Bundle(s) / APK(s) > Build APK(s). Do NOT press Run (it starts the emulator).
APK: app\build\outputs\apk\debug\app-debug.apk  (also check app\build\intermediates\apk\debug\)
Copy to the phone and install. The package id is unchanged (app.viday), so it updates the old app.

PERMISSIONS (and why)
- Usage access (you grant it in system settings): lets DataFlow read Android's own mobile-data
  statistics for exact totals, per-app usage and the hourly chart. Optional; without it the app
  falls back to approximate counter snapshots.
- Notifications (asked only when you turn on alerts): threshold alerts.
- Exact alarms (optional): fires the window start/end alarm on time.
- Boot completed: re-arms the alarm after restart.
- Network state: shows whether you are on mobile data or Wi-Fi.
- No internet, SMS, contacts, location or accessibility permission.

FIRST LAUNCH
Read the 4 intro pages (skippable). Settings > Monitoring > Usage access > allow DataFlow.
Settings > Data limit (default 2 GB). Default window 12:00 PM - 12:00 AM; change in Settings.
Turn on Data alerts if wanted. Xiaomi/HyperOS: App info > Battery saver > No restrictions,
and enable Autostart.

HOW IT COUNTS
- With Usage access: totals come from Android's network statistics for the exact window, the same
  source as the Data usage screen. Finished days are filled in (and re-checked) from it.
- Without it: counter snapshots at the window start/end and during the window. Reboots, counter
  resets, late starts and late closes are flagged as gaps. Nothing is guessed.
- Units: Settings > Data units (1024 or 1000). Android's screen may use 1000.

KNOWN LIMITATIONS
- Per-SIM statistics are not available to normal apps; all mobile data is combined (dual-SIM too).
- Android statistics are bucketed and can lag a few minutes; hourly figures are approximate.
- Per-app foreground/background split appears only if the phone reports it.
- Home-screen widget and Quick Settings tile are not included.
- The hourly timeline and per-app list need Usage access and Android 10+.
- Splash shows the logo only (no developer text); "Always ON" appears on Home, Settings and intro.

TEST CHECKLIST (none of these have been run yet)
[ ] Build succeeds, app installs over the old one
[ ] Grant Usage access; Home total matches Android Data usage for the same period (try both unit options)
[ ] Wi-Fi only browsing does not change the total
[ ] Before 12 PM: shows "Not counting"; after 12 PM: counting
[ ] App list shows YouTube/Chrome etc. with icons; Hotspot row appears when tethering
[ ] Alerts fire once per threshold (50/75/90/100) and not again the same day
[ ] Change schedule: confirmation shown, new window applied
[ ] Restart phone, then open app: no huge jump in usage, gap noted if needed
[ ] History after midnight: finished day saved; Correct usage / Delete work
[ ] CSV export, Backup, Restore (try a damaged file: must be rejected)
[ ] Light / Dark / System theme
