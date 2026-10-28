# Phone Backup

A Windows-first Android backup product in development: preserve original photos, videos and selected files on your own PC, with a clear way to verify and restore them.

**Version 0.4 developer preview.** Product implementation is private. This public showcase describes measured engineering progress without distributing personal media or proprietary source.

![Library interface — explicitly labeled generated demo artwork, no personal media](assets/windows-preview.png)

The image shows the implemented library UI with generated layout-review artwork, not a real user library. Automated library tests separately use synthetic originals in an actual encrypted vault.

## Current capabilities

- Native C#/.NET 10 + WPF desktop interface with shared backup core and CLI.
- Organized vault library: photo tiles, Photos/Videos/Documents/Other categories, search, folder-based albums, modified-month filters, date/name/size sorting, details and exact-checksum duplicate groups.
- Selected-original export/restore, full-backup recovery, and photo navigation/zoom/fit. EXIF orientation is applied for display; originals are never converted. In-app preview supports bounded JPEG/PNG; videos/other formats remain recoverable originals.
- Read-only USB phone folder/file selection with common-folder shortcuts and recursive scanning.
- Managed USB import store: immutable generations, verified local reuse, durable checkpoints and file-level resume. A separate worker process can be stopped on cancellation or inactivity rather than blocking the interface on Windows USB calls.
- Combined USB import → encrypted backup → library workflow using a pinned restic engine. Stored originals are checksum-verified before a snapshot appears as complete; older versions survive source edits/deletion.
- Native Android companion and Windows HTTPS receiver: one-use QR pairing, exact certificate pinning, per-device revocation, on-phone SHA-256, missing-content uploads, reusable completed uploads and verified encrypted snapshots. Actual Java network classes passed a Windows receiver interoperability test; physical Android Wi-Fi acceptance is pending.
- Opt-in account-protected unattended vault unlock, tray/sign-in setup, Android Wi-Fi scheduling and known USB reconnection selection. Android controls background timing; the PC must be awake. Setup includes clear revocation and a Private-profile/LocalSubnet firewall helper.

![Wi-Fi setup before pairing — no credentials or personal data](assets/wifi-setup.png)

## Evidence and practical limits

| Check | Result | What it establishes |
|---|---|---|
| Core/library integration | 24 passed | Encryption, retention, safe/selected restore, cancellation, hostile metadata, cache defense, filters and corruption detection |
| USB/store/worker fixtures | 24 passed | Recursion, strict repeat reuse, edits with unchanged size/time, journals, orphan recovery, cancellation and hung-process termination |
| Automated UI control smoke | 12 passed | Real encrypted synthetic library: thumbnails, bounded pages, search/filters/duplicates, details/export, EXIF and detached thumbnail buffers |
| LAN receiver and actual Java client interoperability | 25 passed | Pinning/pairing boundaries, authorization, retries, corruption repair, retained revisions, restart, exact-byte restore and actual JVM-to-Windows protocol execution |
| Android unit checks / build | 9 passed; APK built | Pairing/path/hash boundaries. Lint: 0 errors, 10 warnings. This does not validate Android permissions, Keystore or WorkManager execution on a phone |
| Pixel 7 hardware proof | Passed for 3 originals | Controlled worker cancellation, checkpoint resume, repeat verification/reuse, encrypted backup and full/selected restore |
| Physical cable pull / full Camera-library copy | Pending | Not established by a subprocess stop or a small sample |

The user confirmed recovery in an earlier preview. Physical Pixel 7 / Android 17 companion installation, permission/pairing, Wi-Fi transfer, locked-phone/Doze/overnight behavior and Windows startup/firewall acceptance remain pending. Varied devices, power loss, disk full, large-library throughput, codec isolation and consumer-release hardening remain open. Guardrails (20k selected files, 10k entries per directory, depth 32) are not a production scale certification.

## Measured performance

A generated local fixture of 60 x 8 KiB files took **46.143 seconds** in preview 0.1 and **3.261 seconds** with 0.3 streamed verification (14.15x on this test). Initialization was excluded; backup timing included source scans, encryption and verification. This is a small-file result on one PC, not USB or large-media throughput.

The improvement removes one restic process per original by verifying a single bounded directory archive against the authoritative inventory. Checksums, file lengths, missing/extra-entry detection and source consistency checks remain in place. Metadata queries were also exercised across 20,000 items; media loading is a separate cost.

## Explicit tradeoffs

The USB and Wi-Fi stores contain **unencrypted** PC originals, prior generations and checkpoints; the vault is a separate encrypted copy. The UI discloses this. No automatic phone cleanup, duplicate deletion or staging prune occurs.

Strict USB repeat runs freshly read unchanged phone files once; new/changed originals are read twice. The Wi-Fi companion hashes originals on the phone and uploads only missing/damaged content. It still freshly hashes all selected originals each run; phone I/O/battery and large-library profiling remain open. Full new PC generations consume additional staging space. No metadata-only content skip is claimed.

Gallery metadata/thumbnails stay in memory, with bounded pages/cache and detached display buffers. Native media parsing still needs stronger isolation. Dates mean modification time, not capture time; albums currently map original folders. The library is scoped to the selected verified backup version, not an aggregate across all devices/backup sets.

See [architecture](ARCHITECTURE.md) and [development record](DEVELOPMENT.md).

## Next milestones

1. Small Pixel Wi-Fi installation/pairing/backup/restore acceptance, then real cable reconnect and lock/Doze/overnight/reboot tests.
2. Measure phone battery/hash costs and larger-library throughput; reduce staging/storage costs.
3. Receiver, recovery and media/process hardening; signing, updates and unattended recovery.
4. Richer media support and persistent custom collections.
5. Optional optimized copies alongside originals, then release/signing/dependency review and external beta.

Cloud, household features and iPhone remain future scope. No consumer download or release date is promised here.

## Technology and attribution

C#, .NET 10, WPF, Windows Portable Devices via community [MediaDevices](https://github.com/Bassman2/MediaDevices), and [restic](https://github.com/restic/restic). [Immich](https://github.com/immich-app/immich) and [LocalSend](https://github.com/localsend/localsend) were product references, not copied application source. Upstream work is attributed; commercial dependency/security review remains a release gate. AI-assisted development uses shared change records, explicit test evidence and human-directed product decisions.
