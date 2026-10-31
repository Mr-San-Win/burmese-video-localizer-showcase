# Engineering decisions

[Back to overview](../README.md)

## Java control plane, Python inference worker

**Choice:** keep authentication, relational domain state and orchestration in Spring Boot; run AI/media execution in Python.

**Why:** Java provides a strong transactional API/domain foundation. Python is the native environment for the selected ML/audio libraries. The boundary keeps resource-heavy execution separate from user-facing HTTP responsibilities.

**Tradeoff:** service authentication, status delivery, failure handling and compatibility must be designed explicitly.

## Asynchronous long-running jobs

**Choice:** processing is a persisted job rather than a synchronous upload request.

**Why:** inference can take much longer than an ordinary web request. Users need progress, safe errors and the ability to return later.

**Tradeoff:** job state must remain meaningful across worker failures; a browser polling successfully does not prove that inference is still alive.

## Checkpoint-based recovery

**Choice:** persist completed unit work and validate its compatibility before reuse.

**Why:** a later provider failure should not automatically discard expensive speech generation.

**Tradeoff:** retained artifacts consume storage, partial operations require clear completion status, and changed inputs must invalidate dependent work. Current recovery still assumes retained compatible workspace; distributed hydration is not implemented.

## Measured synchronization over optimistic estimates

**Choice:** use timing-aware localization and advisory estimation before TTS, then measured audio for the authoritative fit decision.

**Why:** speech duration is not deterministic from text length. Repeating correction after a measured result already fits wastes provider and inference work.

**Tradeoff:** estimation cannot guarantee a fit or replace final timing validation. Factual fidelity remains more important than making text shorter.

## Private custom voices

**Choice:** reuse reference-conditioned voice profiles through the same selection abstraction as built-ins.

**Why:** this enables reusable authorized narration without a separate training product. Owner-scoped storage and explicit consent are central requirements.

**Tradeoff:** consent is attestation, references are sensitive, preview inference is expensive, and deletion/revocation must account for retained artifacts and backups.

## Cost-aware deployment preparation

**Choice:** measure control-plane and inference requirements separately before choosing hosting.

**Why:** ordinary web traffic and model inference have different memory, latency and utilization characteristics.

**Tradeoff:** separate GPU execution may help future economics, but remote/distributed execution is not described as currently deployed. No unmeasured cost or performance claim is used to select infrastructure.

## Security versus inference-library compatibility

**Choice:** apply compatible security patches, inspect actual model-loading input boundaries, and document time-limited private-beta risk acceptance where immediate coordinated upgrades are not validated.

**Why:** blindly replacing tightly coupled ML dependencies can break execution or alter output. Conversely, an incompatible upgrade is not a reason to ignore an advisory.

**Tradeoff:** trusted model supply-chain risk remains. Restricted inputs, review triggers and upgrade obligations are compensating controls, not a permanent substitute for patched dependencies.

## Evidence before claims

**Choice:** distinguish mocked tests, live control-plane checks, deterministic media replay, real inference E2E and human review.

**Why:** each answers a different question. A job reaching completed does not prove readable subtitles or acceptable voice quality.

**Tradeoff:** release status is intentionally qualified while final hardware-dependent acceptance is pending. Implementation has been AI-assisted; ownership includes inspecting results and documenting limitations.
