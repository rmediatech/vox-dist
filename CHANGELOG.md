# Changelog

All notable changes to `vox` will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [0.2.0] - 2026-10-30

### 🚀 Added
- **Authoritative Room Lease Manager (`vox-core::lease`)**:
  - **First-Come First-Served Room Custody**: The first participant to connect to an unclaimed room slug automatically becomes the mission Host / Initiator.
  - **Salted Passkey & PIN Protection**: Hosts can establish a tactical squad PIN. Passkeys are salted with 16 bytes of cryptographically secure random bytes and hashed via SHA-256 (`pin_salt`), defending against rainbow table attacks while never storing plaintext passkeys in memory.
  - **Initiator Mission Termination (Kinetic Nuke)**: Minting of unguessable 64-character hexadecimal host capability keys (`host_key`). Hosts can terminate the tactical bridge via `TerminateMission`, broadcasting a `MissionTerminated` directive to all peers and purging the session.
  - **Empirical 0ms Vacancy Recycling**: Immediate memory reclamation upon vacancy or host termination. Rooms leave zero residual state or database traces, ready for immediate instant re-leasing.
- **Web Companion UI Controls (`vox-web`)**:
  - **Host Status Badge**: Dynamic `👑 HOST` badge visible in tactical HUD when holding room lease custody.
  - **Kinetic Mission Nuke Button**: Header control `💥 NUKE ROOM` displayed exclusively for the authenticated mission host.
  - **Passkey PIN Input**: Squad PIN modal field with bidirectional query parameter (`?pin=...`) synchronization and pairing QR code embedding.
  - **Autonomous Error Interception**: Client-side interception of `ACCESS_DENIED` errors, prompting operators for the required squad passkey without dropping UI context.
  - **Clean WebSocket Teardown**: RFC 6455 policy close frame delivery upon unauthorized connection attempts.
- **Robustness & Buffer Protection (`vox-net`)**:
  - Hardened WebSocket broadcast consumers against `tokio::sync::broadcast::error::RecvError::Lagged` buffer overflows in compliance with `SOVEREIGN-ROSTER-SST-01`.
- **Adversarial Crucible Test Battery (`POC TDD+++++`)**:
  - `adversarial_room_lease_crucible_tests.rs`: Multi-client collision race conditions, wrong PIN rejection, host nuke verification, and 0ms memory reclamation.
  - `adversarial_web_lease_tests.rs`: Full end-to-end live loopback WebSocket test verifying passkey authorization, host assignment, and mission termination.

---

## [0.1.0] - 2026-10-29

### 🌟 Initial Sovereign Release
- **Tactical Push-to-Talk (PTT)**: Low-latency sub-millisecond audio streaming with 150ms release tail.
- **Flight-Recorder Telemetry HUD**: Rolling jitter, RTT, and bitrate telemetry with SHA-256 session integrity receipts.
- **Laser Telestrator**: Phosphorescent real-time cursor trails over WebRTC DataChannels.
- **Ephemeral Burner Rooms**: In-memory signaling hub with zero persistent disk tracking.
- **100% Zero-Cloud Autonomy**: Single static Musl binary deployment.
