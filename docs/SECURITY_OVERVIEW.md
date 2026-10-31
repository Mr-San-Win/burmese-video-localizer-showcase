# Security and privacy overview

[Back to overview](../README.md)

This is a high-level summary of implemented controls and verification. It is not a security certification, a complete threat model or a guarantee that the application cannot be compromised.

## Implemented application boundaries

| Area | Approach |
|---|---|
| Authentication | Password hashing, validated expiring access tokens and authenticated application operations. |
| Authorization | Owner-scoped project, voice, configuration, job and result access; negative cross-user tests. |
| Original uploads | Exactly one accepted video per project, actual-content probing, size/duration/dimension checks, generated names and concurrency protection. |
| Voice uploads | Consent attestation, reference transcript, audio validation/preparation and owner-scoped reference storage. |
| Images and render settings | Validated image content and bounded presentation settings; user values are not raw shell commands. |
| Media/results | Private storage and authenticated preview/download rather than publicly exposed recordings. |
| Worker communication | Protected service communication and guarded status/recovery operations. Browser users cannot forge worker completion. |
| Abuse controls | Upload/resource limits, project/voice/job quotas, request limiting and bounded expensive-work admission. |
| Error handling | Sanitized public errors; operational diagnostics avoid credentials and unnecessary private content. |

Model identifiers and serialized-model inputs come from trusted server configuration or installed mappings, not arbitrary browser inputs. Custom reference audio is media conditioning, not an uploaded model checkpoint.

## Custom voice privacy

Reference recordings can identify a speaker and are treated as sensitive user data. References are not listed as public downloads, exposed as raw filesystem paths or copied into this showcase.

Consent is user attestation, not independent verification. Private-beta retention/deletion still has manual operational requirements; fully automated account/reference erasure is not claimed. Backups and retained recovery state must be included in privacy-request handling.

## Dependency and repository review

The project has undergone dependency triage, security regression testing and repository/release-input privacy checks. Incompatible inference dependencies have a documented, time-limited **private-beta risk acceptance**, supported by restricted model-loading inputs and trusted-asset assumptions.

Those dependencies are not represented as patched or risk-free. Compromised trusted model assets or operators remain a supply-chain risk. Upgrade/review obligations remain; private-beta acceptance does not automatically extend to public access.

Secrets, production source, logs, media, custom references, prompts and model assets are excluded from this repository. A scan reduces accidental disclosure risk; it does not prove that every possible historical secret has been detected.

## Deployment is a separate layer

Planned server controls include HTTPS, restricted administrative access, private database/worker services, protected origin access, production secret provisioning, persistent storage, backups and monitoring.

Cloudflare-based Thailand/Myanmar access restriction and origin protection are deployment requirements, **not already-deployed controls**. Country filtering does not prevent VPN/proxy use or replace application authorization.

The local application-security decision is cleared for an invited private beta subject to its risk acceptance. Final image/server acceptance, operational contact details and fresh deployed browser acceptance remain pending. No public production launch is claimed.
