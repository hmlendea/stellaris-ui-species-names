# Security

## Overview

This mod is a **static data mod** with no executable code, no network communication, no user input processing, and no sensitive data handling. The attack surface is minimal.

## Threat Model

### Assets

| Asset | Sensitivity | Protection |
|-------|-------------|------------|
| Mod source code | Public (open source) | GitHub visibility |
| Species names | Public domain / creative | No protection needed |
| Name list references | Public (in Name Lists mod) | No protection needed |
| Distribution artefacts | Public downloads | Platform integrity |

### Threat Actors

| Actor | Capability | Motivation | Risk |
|-------|------------|------------|------|
| Malicious contributor | Submit PR with malicious content | Supply chain attack | Low (code review, no execution) |
| Compromised platform | Modify uploaded mod | Distribute malware | Medium (platform security) |
| Malicious user | Social engineering | Trick users | Low (no auth in mod) |

### Attack Vectors (Assessed)

| Vector | Applicable? | Reason |
|--------|-------------|--------|
| Code injection | No | No code execution |
| Deserialization attacks | No | No deserialization |
| Path traversal | No | No file operations |
| XSS | No | No web interface |
| SQL injection | No | No database |
| Supply chain | Low | Reviewed PRs, signed releases |
| Typosquatting | Low | Official channels only |

## Security Controls

### Source Code

- **Open source**: All code visible for audit
- **Code review**: All changes via PR review
- **Signed commits**: Recommended for maintainers
- **Branch protection**: `main` branch protected

### Distribution

| Platform | Security Features |
|----------|-------------------|
| Steam Workshop | Valve review, signed downloads, auto-update integrity |
| Paradox Mods | Paradox review, launcher verification |
| Nexus Mods | Community moderation, checksums |
| GitHub Releases | Signed tags, SHA256 checksums, GPG signing available |

### Runtime

- **No code execution**: Stellaris parses declarative data only
- **No permissions**: Mod runs in Stellaris sandbox
- **No network**: Mod makes no connections
- **No file I/O**: Mod only read by Stellaris

## Vulnerability Management

### Reporting

- **GitHub Security Advisories**: For supply chain issues
- **GitHub Issues**: For mod-specific issues (public)
- **Email**: For sensitive reports (see SECURITY.md)

### Response

| Severity | SLA | Action |
|----------|-----|--------|
| Critical (RCE in Stellaris via mod) | N/A | Not applicable |
| High (Malicious content in release) | 24h | Remove release, investigate, re-release |
| Medium (Misleading content) | 7d | Correct in next release |
| Low (Typos, style) | Next release | Fix when convenient |

## Compliance

### Data Protection

- **No personal data** collected, processed, or stored
- **No telemetry** or analytics
- **No user accounts** or authentication
- **GDPR/CCPA**: Not applicable

### Licensing

- **GPL v3.0**: Copyleft, source distribution required
- **No proprietary code** included
- **Name Lists mod**: Same license, same repository owner

## Secure Development Practices

### For Contributors

1. **No secrets** in commits (API keys, passwords)
2. **No executable code** in mod files
3. **Validate** changes don't introduce executable content
4. **Sign commits** if possible

### For Maintainers

1. **Review all PRs** for unexpected content
2. **Verify release artefacts** match source
3. **Use GPG signing** for tags/releases
4. **Monitor dependency** (Name Lists mod) for issues

## Platform Security

### Steam Workshop

- Valve content review
- Automatic malware scanning
- Signed content delivery
- Revocation capability

### Paradox Mods

- Paradox moderation
- Launcher integrity checks
- Dependency verification

### Nexus Mods

- Community reporting
- File checksums displayed
- Malware scanning

### GitHub

- Dependency graph (not applicable)
- Code scanning (not configured)
- Secret scanning (enabled by default)
- Signed commits verification

## Incident Response

### If Malicious Release Detected

1. **Immediate**: Delete release from all platforms
2. **Investigate**: Check commit history, contributor access
3. **Remediate**: Revoke compromised credentials, rotate keys
4. **Communicate**: Security advisory, user notification
5. **Re-release**: Clean version with incremented patch

### If Contributor Account Compromised

1. Remove collaborator access
2. Audit recent commits
3. Force password reset / 2FA
4. Review branch protection rules

## Security Checklist (Per Release)

- [ ] No executable code in mod files
- [ ] No external references (URLs, paths)
- [ ] No encoded/obfuscated content
- [ ] Release artefacts match source exactly
- [ ] GPG signature on tag (if configured)
- [ ] Checksums published for manual installs
- [ ] Dependency (Name Lists) at expected version

## Future Considerations

| Enhancement | Priority | Effort |
|-------------|----------|--------|
| GPG signing for all releases | Medium | Low |
| GitHub CodeQL scanning | Low | Low |
| Automated release verification | Medium | Medium |
| SBOM generation | Low | Low |