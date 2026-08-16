# Security

Tholos is a local-first, offline-by-design Electron notebook. The full,
externally-reviewable security review — threat model, STEAM security
objectives, findings register, and scan-evidence summary — is published at:

**→ [Tholos Security Review](https://codypinto23.github.io/Tholos-Public/security-review.html)**

## Posture at a glance

- **One runtime network channel**: the GitHub Releases update check. No
  telemetry, no CDN assets (fonts are bundled), embeddings run from a local,
  offline-pinned model. Remote images in notes are blocked by CSP.
- **Signed, CI-built releases** (since v1.0.0): every artifact is built on a
  clean CI runner from a frozen lockfile; Windows installers are
  Authenticode-signed via Azure Trusted Signing (publisher *Cody Pinto*) and
  timestamped; every release carries a CI-generated `SHA256SUMS.txt`; the
  packaged binary validates its own code archive against a build-time hash
  (Windows/macOS) via Electron fuses.
- **Hardened renderer**: Chromium sandbox + `contextIsolation`, no
  `nodeIntegration`, strict `script-src 'self'` CSP, `html:false` markdown
  rendering, deny-all permission handler, scheme-allowlisted external links.
- **The renderer can never name a filesystem path** — all file operations go
  through native dialogs or main-issued single-use tokens.
- **Locked Sections**: AES-256-GCM with Argon2id-derived per-section keys
  (OWASP parameters), envelope v2 with address-binding AAD and post-lock
  residue scrubbing; keys live only in main-process memory, are zeroized on
  lock/quit, and are excluded from search indexes and the agent surface *by
  construction*.
- **AI agent access (MCP)** is loopback-only behind a constant-time bearer
  check, per-section opt-in, and satisfies Meta's Rule of Two structurally:
  the server exposes zero network-capable and zero code-executing tools.
  Every tool call is recorded in an append-only audit log (ids only, never
  content); the bearer token is encrypted at rest via the OS credential
  store and masked in the UI behind reveal-on-demand.
- **Supply chain**: sha512-integrity lockfile, 7-day package cooling-off
  window, per-package build-script approvals, guarded installs, SHA-256
  pinned build-time model download, and no install hooks in the project.
- **Continuous assurance**: property-based fuzz suites run on every PR;
  coverage-guided fuzzing runs as a per-PR smoke and a nightly deep job.

Known residual risks are documented in the review's findings register (§8)
with per-finding status — as of v1.0.0, all findings from the review are
remediated, with the remaining residuals (e.g. no independent Linux package
signature) stated there explicitly.

## Supported versions

Only the [latest release](../../releases/latest) receives updates. Tholos
updates itself in place, so staying current is one click.

## Reporting a vulnerability

Please report suspected vulnerabilities privately — do not open public
issues for them:

- **GitHub**: Security → Advisories → "Report a vulnerability" on this
  repository, or
- **Email**: codypinto23@gmail.com

You can expect an acknowledgment within a week.
