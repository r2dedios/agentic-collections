<!-- Catalog fragment: documentation_section — maintained via create-collection workflow -->

## Skills Overview

### container-cve-validator

Full CVE validation pipeline for Red Hat container images:
1. Input validation (CVE ID or RHSA advisory, image reference)
2. CVE reconnaissance (MITRE, OSV.dev, Go vuln DB)
3. SBOM extraction from container attestations (attestation/build-time, image index handling)
4. Red Hat VEX validation (product_tree matching, status determination, parent RPM check)
5. Newer image availability scan (parallel registry check for patched images)
6. Report with VEX data gap assessment and remediation guidance

### coreos-cve-validator

CVE validation for RHCOS in specific OCP releases:
1. OCP release metadata extraction via `oc adm release info`
2. CoreOS RPM list extraction via `podman`
3. RPM classification (RHEL/OCP/Fast Datapath sources)
4. VEX validation with RHEL EUS stream awareness
5. RHCOS VEX discrepancy detection

### cve-recon

Lightweight CVE research — queries multiple databases and returns merged metadata without image/VEX analysis.

### image-inspect

Container image metadata extraction — labels, registry ownership, SBOM artifact reference resolution.

## Helper Scripts

9 Python scripts in `scripts/` handle all deterministic data fetching. Skills orchestrate these scripts and perform all interpretation logic.
