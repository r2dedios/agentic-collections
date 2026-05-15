<!-- Catalog fragment: deploy_and_use — maintained via create-collection workflow -->

## Prerequisites

- **Python 3** with `requests` package (`pip install requests`)
- **regctl** — remote image metadata inspection ([install](https://regclient.org/install/))
- **cosign** — SBOM extraction from container attestations ([install](https://github.com/sigstore/cosign))
- **oc** — OpenShift CLI, required for CoreOS validation only ([download](https://console.redhat.com/openshift/downloads))
- **podman** — required for CoreOS validation only

For CoreOS validation, save your pull secret from https://console.redhat.com/openshift/downloads to `~/.docker/config.json`.

## Installation

### Via Lola (recommended)

```bash
lola install -f rh-security-validation
```

### From source (Claude Code)

```bash
git clone https://github.com/RHEcosystemAppEng/agentic-collections
cd agentic-collections
# Open in Claude Code — skills load automatically from rh-security-validation/skills/
```

## Usage

Skills are invoked via Claude Code's skill system:

```
/container-cve-validator CVE-2024-45490 registry.redhat.io/ubi9/ubi:latest
/coreos-cve-validator CVE-2024-45490 4.20.17
/cve-recon CVE-2024-45490
/image-inspect registry.redhat.io/ubi9/ubi:latest
```
