# Debloat log

Device: Redmi Note 9 Pro Max, MIUI 14. Every item below was approved individually.

Restore commands assume the action recorded in the Action column. If a package was disabled and later uninstalled, the restore is the `install-existing` command.

Status values: **approved** means it was approved for the action shown. Fill in the date and result as you confirm each one on the phone.

## Group A: advertising, telemetry and preinstalled third-party

| ID | Package | What it is | Action | Restore | Result |
| --- | --- | --- | --- | --- | --- |
| A1 | `com.miui.msa.global` | MIUI System Ads | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.miui.msa.global` | |
| A2 | `com.miui.analytics` | Xiaomi analytics and telemetry | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.miui.analytics` | |
| A3 | `com.xiaomi.mipicks` | GetApps store | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.xiaomi.mipicks` | |
| A4 | `com.miui.hybrid` | Quick Apps engine | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.miui.hybrid` | |
| A5 | `com.miui.hybrid.accessory` | Quick Apps helper | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.miui.hybrid.accessory` | |
| A6 | `com.xiaomi.glgm` | Xiaomi Games | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.xiaomi.glgm` | |
| A7 | `com.facebook.appmanager` | Facebook App Manager | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.facebook.appmanager` | |
| A8 | `com.facebook.services` | Facebook background services | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.facebook.services` | |
| A9 | `com.facebook.system` | Facebook System stub | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.facebook.system` | |
| A10 | `com.mi.globalminusscreen` | App Vault (left-of-home page) | Uninstall for user 0, after switching App Vault off in Home settings | `adb shell cmd package install-existing --user 0 com.mi.globalminusscreen` | |
| A11 | `com.microsoft.bing` | Bing app | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.microsoft.bing` | |
| A12 | `com.indus.appstore` | Indus Appstore | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.indus.appstore` | |

## Group B: optional Xiaomi apps

| ID | Package | What it is | Action | Restore | Result |
| --- | --- | --- | --- | --- | --- |
| B1 | `com.miui.player` | Mi Music | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.miui.player` | |
| B2 | `com.xiaomi.midrop` | ShareMe file transfer | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.xiaomi.midrop` | |
| B3 | `com.miui.bugreport` | Feedback app | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.miui.bugreport` | |
| B4 | `com.duokan.phone.remotecontroller` | Mi Remote (infrared) | Initially kept; later asked to remove. Confirm before treating as removed | `adb shell cmd package install-existing --user 0 com.duokan.phone.remotecontroller` | |
| B5 | `com.miui.touchassistant` | Quick Ball | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.miui.touchassistant` | |
| B6 | `cn.wps.xiaomi.abroad.lite` | WPS Office Lite | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 cn.wps.xiaomi.abroad.lite` | |
| B7 | `com.mi.healthglobal` | Mi Health | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.mi.healthglobal` | |
| B8 | `com.milink.service` | Mi Link (casting, cross-device) | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.milink.service` | |
| B9 | `com.xiaomi.mi_connect_service` | Mi Connect (nearby devices) | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.xiaomi.mi_connect_service` | |

## Extra items added later (not in the original review's remove list)

| Package | What it is | Action | Restore |
| --- | --- | --- | --- |
| `com.android.thememanager` | Themes | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.android.thememanager` |
| `com.facemoji.lite.xiaomi` | Emoji keyboard (Gboard was the active keyboard) | Uninstall for user 0 | `adb shell cmd package install-existing --user 0 com.facemoji.lite.xiaomi` |

## Deliberately kept

| Package | Reason |
| --- | --- |
| `com.xiaomi.joyose` | Cloud-controlled performance and thermal tuning; unclear impact if removed |
| `com.miui.powerkeeper` | Battery saver and background limits |
| `com.miui.daemon` | Performance and profiling daemon; no proven gain |
| `com.xiaomi.xmsf`, `com.xiaomi.xmsfkeeper` | Xiaomi push framework |
| `com.miui.cleaner` | Part of Security; turn off its recommendations instead |
| `com.mi.android.globalFileexplorer` | Likely default file handler |
| `com.google.android.apps.turbo` | Device Health Services; battery statistics |
| `com.miui.yellowpage` | Dialer-adjacent caller ID |
| Factory test tools (`com.longcheertel.*`, `com.goodix.gftest`, `com.fingerprints.sensortesttool`) | No battery gain, possible hardware ties |

## Never touched

Telephony and IMS packages, Settings, System UI, the launcher, Gboard, Security and the package installer, Google Play Services and Play Store, Xiaomi account and cloud packages, connectivity and Bluetooth, and the updater.
