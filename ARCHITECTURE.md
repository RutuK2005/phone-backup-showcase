# Current architecture — preview 0.4

```mermaid
flowchart LR
    Phone[Android / MTP] -->|read only| Worker[Isolated Windows USB worker]
    Companion[Native Android companion] -->|Wi-Fi-bound pinned HTTPS| LAN[Authenticated PC receiver]
    LAN -->|missing content only| Store
    UI[WPF desktop] -->|structured protocol| Worker
    Worker --> Scan[Recursive scan and strict verification]
    Scan --> Store[Plaintext managed PC store]
    Store --> Gen[Immutable original generations]
    Gen --> Core[Shared backup core]
    CLI[CLI] --> Core
    UI --> Core
    Core --> Restic[Pinned restic]
    Restic --> Vault[Encrypted vault and recovery inventory]
    Vault --> Verify[Streamed original-byte verification]
    Vault --> Library[In-memory paged library]
    Library --> UI
    Vault --> Restore[Fresh-folder selected or full restore]
```

## Transport and recovery

The adapter exposes list/stat/read only. A worker process isolates blocking Windows transport calls. The desktop validates structured messages and success/exit state; cancellation and an inactivity deadline stop the owned worker. Progress is tied to actual enumeration/read/local-check activity.

Managed store plans and flushed append journals record completed originals. Repeats/resumes check phone bytes and local hashes, not filename/size/time alone. Earlier generations remain immutable. Torn unfinished journals and unjournaled committed files receive explicit recovery checks. Incomplete runs never become a completed import result.

## Storage and library

The backup core captures inventories inside encrypted snapshots, streams stored originals through strict archive/inventory/length/hash validation and rechecks PC sources before verified tagging. The metadata format remains compatible with prior v1 vaults. Restores require a new/empty destination and verify every restored original; selected export also validates membership in the saved inventory.

The library indexes the selected verified snapshot in memory. Search, folder albums, modified dates, categories and checksum duplicates are metadata operations. Bounded thumbnail pages decode verified originals into detached display pixels, without persistent plaintext thumbnails/catalog. Media decoding and temporary inventory/secret handling still need production hardening.

## Wi-Fi and automation

One-use QR pairing pins the PC certificate and issues a device token; the phone never receives the vault passphrase. The PC stores protected token hashes, the phone encrypts its token with Android Keystore, and each side exposes revocation. Phone-side SHA-256 inventories and PC object rehashes decide which whole originals need transport. Immutable generations feed the same encrypted verification/recovery core; receipt alone does not indicate a verified backup.

WorkManager requests Wi-Fi/battery-not-low periodic work, with optional charging. Android may defer work or impose quotas. Windows has opt-in per-account protected unlock, sign-in/tray/single-instance behavior and known USB reconnect polling after a manual selection. The published app locates its private runtime for startup. Private-profile/LocalSubnet firewall rules are an explicit setup action. The PC must be awake; there is no SSID allowlist, cloud relay or mobile-data fallback for bound backup connections.

## Tradeoffs

- Plaintext staging is explicitly retained; encrypted direct streaming/staging is future work.
- New generations use local copies rather than hardlinks, preserving independence but consuming disk space.
- Repeat USB verification still reads all selected phone bytes once. Wi-Fi skips unchanged network uploads but currently hashes all selected phone originals each run; battery/scale profiling remains necessary.
- Multi-file phone state is not an atomic snapshot. A physical cable-pull test is separate from killing a worker.
- restic is an evaluated storage integration, not a guarantee for every future cloud/mobile requirement.
