# Redmi Note 9 Pro Max (MIUI 14) debloat and storage notes

A record of a manual, one-package-at-a-time ADB cleanup of a Redmi Note 9 Pro Max running MIUI 14, plus the steps used to free storage.

This is documentation only. It contains no script that removes anything. Every change was reviewed and approved individually before it was run.

## Contents

- [debloat-log.md](debloat-log.md): each package reviewed, what it is, the action taken, and the exact restore command
- [method.md](method.md): read-only checks, the disable and uninstall commands, and how to restore
- [storage-cleanup.md](storage-cleanup.md): finding what fills the phone, backing up, and deleting safely

## Ground rules

1. Never remove telephony, Settings, System UI, the launcher, the keyboard, security, the package installer, Google Play Services, account services, connectivity or update components.
2. Do not treat an online debloat list as proof a package is safe. Identify what each package does and check what depends on it.
3. Prefer `disable-user` first. Uninstall for user 0 only after a stable period.
4. Write down the restore command before running a change.
5. Change one package (or one dependent pair) at a time and use the phone for a day between changes.
6. Back up anything you cannot replace before deleting it.

## Caveats

- Package behaviour differs between MIUI builds and regions. Results here are for one device and one build.
- Package descriptions come from general knowledge of MIUI, not from Xiaomi documentation.
- `pm uninstall --user 0` on a user-installed app may not be reversible with `install-existing`; reinstall from the store instead.
- Major system updates can bring removed packages back.

