# Testing and reliability

[Back to overview](../README.md)

Evidence below is summarized from the private project's current engineering and acceptance records, reviewed for this showcase on **31 October 2026**. No tests or AI inference were rerun to publish these documents. Raw logs, recordings, identifiers and verification exports remain private.

## Recorded automated evidence

These are **separate recorded runs**, not one cumulative count. Several suites overlap. They are not code-coverage percentages, production load results or final baked-release certification.

| Recorded suite | Passing tests | Scope |
|---|---:|---|
| Java backend security/HTTP regression | 156 | Authentication, ownership, uploads, media/storage boundaries, job/worker HTTP behavior and public page handling; isolated database fixtures. |
| Python 3.12 worker security/recovery regression | 124 | Storage, custom voices, render settings, recovery, capacity and per-unit checkpoint behavior using mocks/offline fixtures. |
| Focused model-boundary and related adapter regression | 58 | Includes 16 new boundary cases plus existing transcription/TTS/custom-voice tests; no model inference. Overlaps other worker evidence. |
| Frontend tests | 42 | Authentication/API integration, upload order, voice/style/consent binding, visual settings, safe errors and policy pages. |
| Release contracts | 12 | Build inputs, locking and permitted dependency changes; not an accepted image build. |
| Deployment configuration contracts | 10 | Configuration invariants; not proof of actual server deployment. |

Additional recorded checks include fixture-based database/media backup and restoration, worker restart persistence, compatibility matches/misses and private build-context exclusion tests. These are scoped checks, not claims that production disaster recovery has been operated.

## What the tests establish

- Unauthenticated and cross-user resource access is rejected on tested routes.
- Missing, repeated, unexpected, empty, corrupt and oversized media inputs fail safely within tested contracts.
- Duplicate/concurrent state-changing requests cannot simply attach multiple originals or dispatch duplicate supported retries.
- Authenticated callbacks and attempt fencing prevent stale completion from overwriting a newer attempt.
- Compatible completed unit artifacts are reused; missing/corrupt/incompatible work is not trusted.
- Transient localization/shortening failures are distinct from permanent failures.
- Public errors avoid low-level provider, storage and credential details.
- Frontend voice, style, consent and render configuration reach the intended backend contract.

A mock proves application control flow, not provider availability, model numerical behavior or subjective output quality.

## Browser and deterministic media evidence

Live local control-plane checks exercised real frontend/backend account, owner voice, upload and configuration paths without AI. Current visual-setting checks include subtitle settings, watermark upload, blur configuration and cross-user rejection.

Separate deterministic rendering checks used retained compatible media to inspect Burmese glyphs, subtitle visibility, watermark and blur while preserving audio. This is not a fresh combined custom-voice browser-to-render inference run.

Large-result streaming/range tests used deterministic data and integrity checks. Physical-device/browser support and an actual deployed server still require acceptance; universal mobile compatibility is not claimed.

## Real completed video evidence

An earlier real custom-narrator acceptance run produced a short final MP4 using the actual localization, custom-voice TTS and media path. The recorded result was approximately **6.9 seconds**, **480 × 480**, **30 fps**, **H.264/AAC**. Decoding and representative subtitle visibility were checked.

That run included recovery and predates some later UI/security/release work. It is evidence that the core real pipeline completed—not a claim that the latest frozen website has passed a fresh full E2E or that every visual setting was used in that run.

No private test video, voice reference, output file or screenshots from that run are published here. The public assets are separately captured, labeled UI fixtures and a still-image slideshow; they are not new E2E or model-quality evidence.

## Human acceptance is separate

Technical decoding, stream checks, subtitle-frame inspection and successful job state do not establish Burmese naturalness, translation fidelity, narrator consistency or custom-voice similarity. Human listening and visual review remain separate acceptance decisions.

## Current limits and remaining gates

- Final pinned release images have not been accepted.
- A fresh current-version full browser/inference acceptance run remains hardware-blocked.
- Actual server HTTPS, origin protection, persistent storage, backup restore and service isolation remain deployment gates.
- Retained workspace is required for recovery; automatic distributed failover is not implemented.
- Stranded processing may require operator handling; passing restart persistence checks does not prove automatic resume.
- No public-user scale, sustained load, production uptime or production cost claim is made.

The next active gate is final release-image build and acceptance on adequate hardware. This repository reports completed evidence and remaining work without turning planned checks into completed ones.
