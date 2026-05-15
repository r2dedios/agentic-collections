# rh-security-validation

Advanced CVE validation for Red Hat container images and OpenShift CoreOS.

## What it does

Validates whether CVEs reported by security scanners truly affect your Red Hat container images or CoreOS nodes — eliminating false positives using official Red Hat security data.

- **Container CVE validation** — checks official SBOM attestations and Red Hat VEX/CSAF data to confirm or deny scanner findings
- **CoreOS CVE validation** — extracts RPM packages from OCP release CoreOS images and validates against VEX data with RHEL EUS stream awareness
- **CVE reconnaissance** — queries MITRE, OSV.dev, and Go vulnerability database for detailed CVE metadata
- **Image inspection** — fetches container image labels, registry ownership, and SBOM artifact references

## Skills

| Skill | Description |
|-------|-------------|
| `container-cve-validator` | Full CVE validation pipeline for container images — SBOM extraction, VEX analysis, newer image scan, remediation guidance |
| `coreos-cve-validator` | CVE validation for RHCOS in a specific OCP release — RPM extraction, VEX analysis with RHEL EUS stream matching |
| `cve-recon` | CVE reconnaissance — affected packages, ecosystems, version ranges from MITRE/OSV/Go vuln DB |
| `image-inspect` | Container image metadata — labels, registry ownership, tag/digest resolution via SBOM |

## Prerequisites

| Tool | Required by | Install |
|------|-------------|---------|
| `python3` + `requests` | All skills | System package manager, `pip install requests` |
| `regctl` | Image inspection, newer image scan | https://regclient.org/install/ |
| `cosign` | SBOM extraction | https://github.com/sigstore/cosign |
| `oc` | CoreOS validation | https://console.redhat.com/openshift/downloads |
| `podman` | CoreOS validation | System package manager |

For CoreOS validation, a pull secret from https://console.redhat.com/openshift/downloads must be saved to `~/.docker/config.json`.

## Installation

### Via Lola (recommended)

```bash
lola install -f rh-security-validation
```

### From source

```bash
git clone https://github.com/RHEcosystemAppEng/agentic-collections
cd agentic-collections
# Open in Claude Code — skills are automatically available
```

## Usage

```
/container-cve-validator CVE-2024-45490 registry.redhat.io/ubi9/ubi:latest
/container-cve-validator RHSA-2026:3337 registry.redhat.io/ubi9/ubi:latest
/coreos-cve-validator CVE-2024-45490 4.20.17
/cve-recon CVE-2024-45490
/image-inspect registry.redhat.io/ubi9/ubi:latest
```

## Data Sources

All validation uses official Red Hat data — no third-party manipulation:

- **SBOMs**: Build-time and release-time SPDX attestations from container images via `cosign`
- **VEX**: CSAF VEX files from `security.access.redhat.com/data/csaf/v2/vex/`
- **CVE metadata**: MITRE CVE API, OSV.dev, Go vulnerability database
- **RHSA advisories**: CSAF advisories from `security.access.redhat.com/data/csaf/v2/advisories/`

## Related

- [ai-cve-validator](https://github.com/p-rog/ai-cve-validator) — full project with CrewAI automated approach and examples
