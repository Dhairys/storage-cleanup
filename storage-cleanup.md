# Storage cleanup

Starting point: about 3.1 GB free of 105 GB (98% used) on `/data`. Intermediate point: about 11 GB free (90% used). Final reading: 77 GB used of 105 GB, about 28 GB free (roughly 73% used).

## 1. Find what is using space (read-only)

```
adb shell df -h /data
adb shell dumpsys diskstats
adb shell du -h -d 1 /storage/emulated/0
adb shell du -h -d 1 /storage/emulated/0/Android
adb shell du -h -d 1 /storage/emulated/0/DCIM
```

Notes:

- `du` on `/sdcard` reports 0 because `/sdcard` is a symlink. Use `/storage/emulated/0` instead.
- `dumpsys diskstats` lists sizes for apps in the same order as its package list, so the largest apps can be matched by position. Confirm on the phone in Settings > Storage > Apps before deleting anything.
- The system figure in `diskstats` is not part of the user storage total.

Findings on this phone: videos and photos were the largest item by far (`DCIM`, about 28 GB), followed by the `Android` folder (about 19 GB), WhatsApp app data (about 9.7 GB), YouTube data (about 4.7 GB), and Gallery data (about 3.2 GB).

## 2. Safe first steps

```
adb shell pm trim-caches 999G
```

This clears cache only. Then clean WhatsApp media (Settings > Storage and data > Manage storage), delete YouTube offline downloads, and uninstall apps you do not use.

## 3. Back up before deleting

```
mkdir F:\phone-backup
adb pull /storage/emulated/0/DCIM F:\phone-backup
```

Check the copy:

- Phone: `adb shell find /storage/emulated/0/DCIM -type f | wc -l`
- PowerShell: `(Get-ChildItem F:\phone-backup\DCIM -Recurse -File).Count`

The counts should match, and a few files should open on the PC. Keep a second copy of anything irreplaceable.

## 4. Deleting on the PC does not delete on the phone

The two do not sync. Delete the same items on the phone, in Gallery, or match the phone to the PC as below.

Run in **PowerShell**, not Command Prompt, from the platform-tools folder. Use `.\adb`. Paste one line at a time.

Build the list (this deletes nothing):

```
.\adb shell find /storage/emulated/0/DCIM -type f | Out-File -Encoding ascii F:\phone-files.txt
$phone = Get-Content F:\phone-files.txt | Where-Object { $_ -like '/storage*' } | ForEach-Object { $_.Trim() }
$root = 'F:\phone-backup\DCIM'
$pc = Get-ChildItem $root -Recurse -File | ForEach-Object { '/storage/emulated/0/DCIM' + ($_.FullName.Substring($root.Length) -replace '\\','/') }
$del = $phone | Where-Object { $_ -notin $pc }
$del | Set-Content F:\to-delete.txt
$del.Count
```

Read `F:\to-delete.txt` first. It will also list files taken on the phone since the backup, and anything that was never copied. Delete only if the list is exactly what you want gone, because the final step is permanent:

```
Get-Content F:\to-delete.txt | ForEach-Object { .\adb shell "rm '$_'" }
```

## 5. Finish

Empty Gallery "Recently deleted" and the Google Photos Bin, restart the phone, then check `adb shell df -h /data` (look at the Avail column). Aim for at least 10 GB free, ideally 15 GB.

## 6. Do not

- Run `pm clear <package>` on apps you still use. It wipes their data and logins.
- Delete folders under `Android/data` or `Android/obb` unless you know which app they belong to.
- Delete game, emulator or Minecraft folders without copying saves and worlds first.
- Use cleaner apps that promise to free space.

## Lessons from running these commands

- PowerShell commands fail in Command Prompt. The prompt should start with `PS`.
- Paste one command per line so two commands are not glued together.
