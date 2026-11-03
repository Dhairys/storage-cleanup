# Method

All commands run from the platform-tools folder with USB debugging on. On Windows use PowerShell, and write `.\adb` instead of `adb`.

## 1. Read-only checks

These change nothing.

| Goal | Command |
| --- | --- |
| Confirm the phone is connected | `adb devices` |
| List all package names | `adb shell pm list packages` |
| Disabled packages | `adb shell pm list packages -d` |
| System packages | `adb shell pm list packages -s` |
| User-installed packages | `adb shell pm list packages -3` |
| Packages removed for user 0 | `adb shell pm list packages -u` (compare with the plain list) |
| Installer and APK path | `adb shell pm list packages -i -f <package>` |
| Details for one package | `adb shell dumpsys package <package>` |
| Free space | `adb shell df -h /data` |
| Storage breakdown | `adb shell dumpsys diskstats` |
| Active keyboard | `adb shell settings get secure default_input_method` |

A saved `pm list packages` file only shows that a package name is registered. It does not show whether the package is a system app, who installed it, or whether it is enabled.

## 2. Disable for testing (reversible, APK stays)

```
adb shell pm disable-user --user 0 <package>
```

Restore:

```
adb shell pm enable --user 0 <package>
```

## 3. Uninstall for user 0 (later step)

```
adb shell pm uninstall --user 0 <package>
```

Restore (works for preinstalled system apps whose APK is still on the system partition):

```
adb shell cmd package install-existing --user 0 <package>
```

For apps you installed yourself, reinstall from the store instead.

## 4. Order of work

1. Turn off ads and diagnostics in Settings first (Passwords & security > Privacy > Ad services, diagnostic data, recommendations in Security, Cleaner, Themes, File Manager, Weather and Scanner).
2. Run read-only checks on anything uncertain.
3. Disable, test for a day, then decide on uninstall.
4. If something breaks, run that package's restore command and restart the phone.

## 5. Settings-based reductions that need no ADB

- Per-app battery saver: set shopping, delivery and social apps to restrict background activity.
- Autostart: switch off for apps that do not need it.
- Notifications: turn off promotional channels.
- Sync: limit background sync for accounts you do not use.
