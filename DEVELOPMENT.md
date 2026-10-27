# Development record

These dates record work that happened; they are not backdated Git commits.

## 24 October 2026 — Local backup foundation

Implemented shared core, native Windows UI and CLI with encrypted local-folder backups, authoritative snapshot inventory, stored-file readback verification, retained versions and safe restore. Tested 19 generated-data scenarios. Prepared a portable developer package with a private runtime. Phone and network transport were still unimplemented at this point.

## 28 October 2026 — First Pixel USB integration

Connected a Pixel 7 in File transfer mode. Distinguished sandbox visibility limits from actual device access by repeating read-only storage enumeration outside isolation. Added a read-only WPD adapter, explicit USB file browser and bounded import into an empty PC folder. Independently reread phone bytes and verified local output before passing the folder to encrypted backup.

Ten new USB fixture checks passed; the existing 19 core checks passed. One real original passed USB double-read, encrypted backup and restored-byte verification. No phone files were changed. Interactive acceptance, real cable-disconnect recovery and production-scale performance remain pending.

## Development practice

Changes are recorded in Small/Medium/Large categories, with detailed optional engineering notes for substantial changes. Tests distinguish simulated failures from physical-device evidence. Product source remains private; this repository contains public explanation and nonpersonal visuals only.
