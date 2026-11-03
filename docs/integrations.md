# Integrations

## Overview

This document describes all external integrations for the Universum Infinitum: Species Names mod.

## Stellaris Game Engine

### Integration Type: Host Platform

| Aspect | Details |
|--------|---------|
| **Role** | Runtime host — parses and loads mod data |
| **Interface** | Declarative mod format (custom key-value syntax) |
| **Version Contract** | `supported_version = "4.5.*"` in descriptor |
| **Data Flow** | Mod files → Stellaris parser → Game systems |
| **Failure Mode** | Mod disabled, errors in log |

### Integration Points

1. **Mod Descriptor** (`descriptor.mod`, `ui-species-names.mod`)
   - Identifies mod to launcher
   - Declares version, supported game version, tags, path

2. **Species Definitions** (`common/species_names/*.txt`)
   - Defines species name options for empire creation
   - Referenced by species class and portrait

3. **Random Names** (`common/random_names/base/ui-species-names.txt`)
   - Provides prefixes/postfixes for genetic modification
   - Integrated into species name generation pipeline

### Compatibility Requirements

- Stellaris 4.5.* (current)
- No DLC required
- Works with all DLC combinations
- No script/API usage (pure data)

## Universum Infinitum - Name Lists Mod

### Integration Type: Hard Dependency

| Aspect | Details |
|--------|---------|
| **Role** | Provides name list data (`name_list` references) |
| **Interface** | `name_list` key in species definitions |
| **Version Contract** | None (backward compatible) |
| **Data Flow** | This mod references → Name Lists provides → Stellaris resolves |
| **Failure Mode** | Species have no names (empty dropdown) |

### Integration Points

**Base Extra Packs** (8 files):
- `ui_extra_art1` through `ui_extra_art10`
- `ui_extra_avi1` through `ui_extra_avi10`
- `ui_extra_fun1` through `ui_extra_fun10`
- `ui_extra_hum1` through `ui_extra_hum10`
- `ui_extra_mam1` through `ui_extra_mam10`
- `ui_extra_mol1` through `ui_extra_mol10`
- `ui_extra_pla1` through `ui_extra_pla10`
- `ui_extra_rep1` through `ui_extra_rep10`

**Media Packs** (5 franchises):
- `ui_media_dw_*` (Distant Worlds)
- `ui_media_dnd_*` (Dungeons & Dragons)
- `ui_media_es_*` (Elder Scrolls)
- `ui_media_gc_*` (Galactic Civilizations)
- `ui_media_nar_*` (Narivia)

### Coordination Protocol

1. **Reference Stability**: Name Lists mod maintains backward compatibility
2. **Communication**: Major changes discussed between maintainers
3. **Testing**: This mod tested against latest Name Lists before release
4. **Release Sync**: Not required but preferred for major additions

## Distribution Platforms

### Steam Workshop

| Aspect | Details |
|--------|---------|
| **Integration Type** | Distribution channel |
| **Interface** | Steam Workshop upload tool / API |
| **Artefact** | Zip of `ui-species-names/` directory |
| **Metadata** | Title, description, tags, preview image, changelog |
| **Update Mechanism** | Auto-update for subscribers |
| **Dependency Declaration** | Workshop collection or description text |

### Paradox Mods

| Aspect | Details |
|--------|---------|
| **Integration Type** | Distribution channel |
| **Interface** | Paradox Mods web upload / launcher integration |
| **Artefact** | Zip of `ui-species-names/` directory |
| **Metadata** | Title, description, tags, dependencies, version |
| **Update Mechanism** | Auto-update via Paradox launcher |
| **Dependency Declaration** | Formal dependency on Name Lists mod (ugc ID) |

### Nexus Mods

| Aspect | Details |
|--------|---------|
| **Integration Type** | Distribution channel |
| **Interface** | Nexus Mods web upload / Vortex integration |
| **Artefact** | Zip of `ui-species-names/` directory |
| **Metadata** | Title, description, category, version, changelog |
| **Update Mechanism** | Manual or Vortex auto-update |
| **Dependency Declaration** | Description text, optional dependency field |

### GitHub Releases

| Aspect | Details |
|--------|---------|
| **Integration Type** | Distribution channel + source hosting |
| **Interface** | GitHub Releases API / web UI |
| **Artefact** | Zip of `ui-species-names/` directory |
| **Metadata** | Tag, release notes, assets |
| **Update Mechanism** | Manual download |
| **Dependency Declaration** | README, release notes |

## Development Tools

### Git / GitHub

| Aspect | Details |
|--------|---------|
| **Integration Type** | Source control, issue tracking, releases |
| **Interface** | Git CLI, GitHub web UI, GitHub API |
| **Branching** | `main` branch, tags for releases |
| **Issues** | Bug reports, feature requests |
| **Actions** | Potential CI (not currently configured) |

### Text Editors

| Tool | Purpose |
|------|---------|
| VS Code | Primary editor, Markdown preview, Git integration |
| Notepad++ | Windows fallback, encoding/line ending control |
| Any UTF-8 editor | Mod file editing |

## Community Platforms

### Paradox Forum

| Aspect | Details |
|--------|---------|
| **Integration Type** | Community discussion, announcements |
| **Interface** | Web forum |
| **Usage** | Release announcements, feedback, support |

### Steam Workshop Comments

| Aspect | Details |
|--------|---------|
| **Integration Type** | User feedback, bug reports |
| **Interface** | Steam Workshop page comments |
| **Usage** | User issues, compatibility reports |

### Discord (Stellaris Modding)

| Aspect | Details |
|--------|---------|
| **Integration Type** | Real-time discussion, coordination |
| **Interface** | Discord server |
| **Usage** | Modder coordination, technical discussion |

## No Integrations

The following are explicitly **not integrated**:

- No external APIs (REST, GraphQL, gRPC)
- No databases
- No message queues
- No authentication providers
- No telemetry/analytics
- No CI/CD pipelines (currently)
- No container orchestration
- No cloud services
- No payment processing
- No user accounts (mod is free)

## Integration Health Checks

### Pre-Release Validation

| Integration | Check |
|-------------|-------|
| Stellaris | Mod loads on target version |
| Name Lists | All references resolve |
| Steam Workshop | Upload succeeds, mod appears |
| Paradox Mods | Upload succeeds, dependency resolves |
| Nexus Mods | Upload succeeds, category correct |
| GitHub | Release created, assets attached |

### Ongoing Monitoring

| Integration | Monitoring |
|-------------|------------|
| Stellaris | Test on new version betas |
| Name Lists | Watch for breaking changes |
| Platforms | Check download stats, user reports |
| Community | Monitor issues, comments, forum |

## Future Integration Possibilities

| Integration | Trigger | Effort |
|-------------|---------|--------|
| GitHub Actions CI | Contributor demand | Low |
| Automated reference validation | Name Lists machine-readable format | Medium |
| Localisation platform (Crowdin, etc.) | Translation demand | Medium |
| Mod manager API (Vortex, etc.) | Platform support | Low |
| Stellaris modding API (if released) | Paradox provides | Unknown |