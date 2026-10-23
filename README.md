# Sawone (GitHub Action)

**One step, any language or framework.** Sawone detects what a repository contains and runs the right
open-source scanners — threat model, secrets, SAST, SCA, licences, IaC, Kubernetes, CI/CD, container, DAST and
WAF — prioritises with CISA KEV and EPSS, honours an expiring baseline of accepted risks, maps results to
ASVS / NIST SSDF / NCA ECC / SAMA CSF, and produces SARIF, JUnit and a PDF report (English and Arabic).

This repository is the **public entry point** to Sawone: the action and reusable workflows. The scanning engine
ships as a signed container image — `ghcr.io/hackin2minutes-oss/sawone-scanner` — which these workflows pull and
verify; the engine's source is maintained privately. Nothing here needs the engine source to run.

```yaml
jobs:
  sawone:
    permissions: { contents: read, actions: read, security-events: write }
    uses: hackin2minutes-oss/sawone-action/.github/workflows/sawone-scan.yml@<commit-sha> # v1.x.y
```

## Using it

**Reusable workflow** (recommended — parallel jobs per phase, previous-report trend, one merged report):

```yaml
name: security
on:
  pull_request:
  push: { branches: [main] }
permissions: {}
jobs:
  scan:
    permissions:
      contents: read
      actions: read            # previous-report trend + code-scanning upload
      security-events: write   # code scanning
    uses: hackin2minutes-oss/sawone-action/.github/workflows/sawone-scan.yml@<commit-sha> # v1.x.y
    with:
      phases: all              # or plan,code,build for a fast PR check
```

**Single-step action** (runs the whole scan in one container):

```yaml
- uses: hackin2minutes-oss/sawone-action@<commit-sha> # v1.x.y
  with:
    path: .
```

Other reusable workflows in this repo: `sawone-pr-comment.yml` (PR summary comment), `sawone-monitor.yml`
(daily rescan of running images), `sawone-dashboard.yml` (portfolio dashboard) and `sawone-release.yml`
(signing, SBOM attestation, SLSA provenance of your artifact). See `examples/` for ready-to-copy callers.

## Verifying what runs

The engine image is signed with Sigstore cosign. The scan workflow resolves `scanner-image` to an immutable
digest and verifies that signature before running, using `scanner-identity-regexp` (default: the Sawone release
workflow). **Pin by digest** for the strongest guarantee:

```yaml
    with:
      scanner-image: ghcr.io/hackin2minutes-oss/sawone-scanner@sha256:<digest>
```

You can confirm a tag's digest and signature yourself:

```bash
cosign verify ghcr.io/hackin2minutes-oss/sawone-scanner:1 \
  --certificate-identity-regexp '^https://github\.com/hackin2minutes-oss/sawone/\.github/workflows/release\.yml@' \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com
```

## Requirements

- A runner with Docker (GitHub-hosted `ubuntu-*`, or an equivalent ephemeral runner): the engine starts sibling
  scanner containers on the host Docker daemon.
- `security-events: write` to publish findings to GitHub code scanning (public repos get it free).

## Results

The `sawone-reports` artifact: `security-report.pdf` / `-ar.pdf`, `summary.md`, `findings.json`, `sarif/`,
`junit.xml`, `evidence/`, plus the raw tool output. On public repositories findings also appear under
**Security → Code scanning**.

## Companion scanners

Built on the same engine, consumed the same way:
[SawOne-A](https://github.com/hackin2minutes-oss/sawone-a) (Android) and
[SawOne-SI](https://github.com/hackin2minutes-oss/sawone-si) (AI / LLM applications).

Licensed MIT.
