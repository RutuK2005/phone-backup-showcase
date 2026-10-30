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

## 28 October 2026 — Wi-Fi companion and unattended setup, 0.4

Built a native Android companion and separate PC HTTPS receiver. Added one-use QR pairing, certificate pinning, protected credentials, per-device revocation, on-phone checksums, missing-object uploads, whole-file retries, immutable PC generations and verified encrypted snapshot receipts. Added explicit account-protected unattended unlock, tray/sign-in/single instance and known USB selection polling. Android traffic is bound to Wi-Fi; local files use scoped media/folder permissions. Android controls periodic timing and the PC must be awake.

24 core, 24 USB, 25 LAN/JVM interoperability and 12 packaged UI checks passed, plus nine Android unit checks. Android debug APK builds; lint has zero errors and ten reviewable warnings. The actual Java client ran against the Windows receiver with generated Unicode/empty/binary originals, pinned TLS, repeat/revoke and byte-checked restore. A real Windows handshake exposed an unsupported ephemeral-key mode, which was corrected and retested. A packaged-host trace confirmed relative private-runtime loading without DOTNET_ROOT environment variables.

Physical Pixel 7 Android 17 install/permissions, Wi-Fi/Keystore/background execution, real firewall/startup acceptance and overnight/battery/scale tests remain next. This is an engineering preview, not a consumer release. Product source, debug signing keys and personal media remain outside this public repository. No activity was fabricated or backdated.

## 28 October 2026 — Beginner setup and actual readable backup storage, 0.5

User feedback exposed setup friction: mandatory vault/password/staging concepts. Implemented default readable Simple history with checksummed copies, safe restore and portable reopen; optional private encrypted archives; recommended-location setup, grouped USB selection, managed transfer paths and a simpler Wi-Fi flow. Both backends share the gallery/receiver/automation through a storage interface. Existing encrypted vaults were preserved.

Validated 21 Simple storage cases, 25 private and 26 Simple receiver/actual-Java cases, 12 private and 13 Simple UI checks, existing 24 core/24 USB fixtures and nine Android units. Added a regression for readable bytes edited after an earlier Wi-Fi success receipt: those bytes are rechecked and a new good version is saved while earlier bytes remain. Physical Pixel/Doze/UAC/login/reconnect and broad release gates remain pending. This is implemented preview code, not just an onboarding mockup.

## 30 October 2026 — Existing-folder consolidation and Memories gallery, 0.8

Built on the 0.6 copy-only organizer and 0.7 automatic folder-add progress/continuous timeline. Added collection video playback and Unicode file selection, optional automatic local face suggestions with names/merge/correction/hiding, favorites and extracted Google Takeout metadata. Combining earlier output with new input creates a fresh collection; no existing originals are deleted or overwritten.

The organizer now has 53 passing fixture scenarios, including a serialized plan-size guard that refuses oversized metadata before creating the destination. Native face/video tests use one public portrait and generated video; these demonstrate inference/decoding, not real-library accuracy or universal codec coverage. Visual package review caught a blank initial page caused by hidden tab headers; explicit startup selection and a visible-controls regression were added. Earlier USB/storage/HTTPS and packaged backup-library checks also passed. Personal media and the user's ongoing copy were excluded from engineering tests.

Third-party engines are exact-pinned and documented. Native plugins/model provenance still have commercial release gates; no public product binaries are distributed here. Physical Android automation, broad media/face accuracy and large-library acceptance remain open. This record is published on the actual work date, with no synthetic/backdated Git activity.
