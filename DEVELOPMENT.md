# Development record

These dates record work that happened; they are not backdated Git commits.

## 24 October 2026 — Local backup foundation

Implemented shared core, native Windows UI and CLI with encrypted local-folder backups, authoritative snapshot inventory, stored-file readback verification, retained versions and safe restore. Tested 19 generated-data scenarios. Prepared a portable developer package with a private runtime. Phone and network transport were still unimplemented at this point.

## 28 October 2026 — First Pixel USB integration

Connected a Pixel 7 in File transfer mode. Distinguished sandbox visibility limits from actual device access by repeating read-only storage enumeration outside isolation. Added a read-only WPD adapter, explicit USB file browser and bounded import into an empty PC folder. Independently reread phone bytes and verified local output before passing the folder to encrypted backup.

Ten new USB fixture checks passed; the existing 19 core checks passed. One real original passed USB double-read, encrypted backup and restored-byte verification. No phone files were changed. Interactive acceptance, real cable-disconnect recovery and production-scale performance remain pending.

## Development practice

Changes are recorded in Small/Medium/Large categories, with detailed optional engineering notes for substantial changes. Tests distinguish simulated failures from physical-device evidence. Product source remains private; this repository contains public explanation and nonpersonal visuals only.

## 28 October 2026 — Organized library and repeat USB workflow, 0.3

Added recursive selections, common phone folders, immutable managed import generations, strict verified reuse, durable append journals and file-level resume. Moved blocking USB work to a separate process with cancellation/inactivity termination. Added an in-app library with categories, paged photo tiles, search, albums/modified-date filters, details, exact duplicates, selected restore and photo viewing controls.

Replaced per-file restic verification processes with a streamed archive check while preserving inventory/length/checksum/source-consistency requirements. A 60-small-file local backup fixture improved from 46.143s (0.1) to 3.261s (0.3); this does not measure phone/large-library throughput.

Validated 24 core/library cases, 24 USB/store/worker cases and 12 synthetic-media UI-control cases. A real three-original Pixel test passed controlled worker cancellation, resume, verified repeat reuse, encryption and full/selected restore. No phone writes or personal media published. New human acceptance, physical cable pull and larger libraries remain pending.
