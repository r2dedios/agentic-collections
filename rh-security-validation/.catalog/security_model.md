<!-- Catalog fragment: security_model — maintained via create-collection workflow -->

## Security Model

- All data fetched from official Red Hat sources and public official CVE metadata sources (security.access.redhat.com, cveawg.mitre.org, api.osv.dev)
- No credentials stored in skills or scripts
- No MCP servers — all data fetching via local Python scripts using public APIs
- Pull secrets for `quay.io/openshift-release-dev/` required only for CoreOS validation and must be configured by the user in `~/.docker/config.json`
- Scripts validate all user input (CVE ID format, image reference format) before processing
- No data is sent to third-party services beyond the public APIs listed above
