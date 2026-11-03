# Build and Deployment

## Build Pipeline

This mod has **no build process**. The source files are the distribution artefacts.

### No Compilation

- No source code to compile
- No transpilation, bundling, or minification
- No asset processing
- No dependency installation

### No Build Tools

- No `package.json`, `Cargo.toml`, `.csproj`, `pom.xml`, `build.gradle`
- No Makefile, CMake, Meson, Bazel
- No CI build steps beyond validation

## Release Process

### Manual Release (Current)

1. **Update version** in both descriptor files:
   - `ui-species-names.mod`
   - `ui-species-names/descriptor.mod`

2. **Verify consistency**:
   ```bash
   diff ui-species-names.mod ui-species-names/descriptor.mod
   # Should produce no output
   ```

3. **Create Git tag**:
   ```bash
   git tag -a v1.7.4 -m "Release version 1.7.4"
   git push origin v1.7.4
   ```

4. **Create GitHub Release**:
   - Go to GitHub Releases
   - Click "Draft a new release"
   - Select tag `v1.7.4`
   - Upload mod archive (zip of `ui-species-names/` directory)
   - Publish

5. **Publish to Steam Workshop**:
   - Use Steam Workshop upload tool
   - Select mod directory
   - Publish update

6. **Publish to Paradox Mods**:
   - Use Paradox Mods upload tool or web interface
   - Upload mod archive
   - Publish update

7. **Publish to Nexus Mods**:
   - Log into Nexus Mods
   - Update mod page with new version
   - Upload mod archive

### Release Artefact

The distribution artefact is a **zip archive** containing:
```
ui-species-names/
├── descriptor.mod
└── common/
    ├── random_names/
    │   └── base/
    │       └── ui-species-names.txt
    └── species_names/
        ├── ui_species_extra_arthropoid.txt
        ├── ui_species_extra_avian.txt
        ├── ui_species_extra_fungoid.txt
        ├── ui_species_extra_humanoid.txt
        ├── ui_species_extra_mammalian.txt
        ├── ui_species_extra_molluscoid.txt
        ├── ui_species_extra_plantoid.txt
        ├── ui_species_extra_reptilian.txt
        ├── ui_species_media_distant-worlds.txt
        ├── ui_species_media_dnd.txt
        ├── ui_species_media_elder-scrolls.txt
        ├── ui_species_media_galciv.txt
        └── ui_species_media_narivia.txt
```

### Versioning Scheme

**Semantic Versioning** (MAJOR.MINOR.PATCH):
- **MAJOR**: Breaking changes (e.g., Stellaris major version requiring format changes)
- **MINOR**: New species names, new media packs, new features
- **PATCH**: Bug fixes, typo corrections, descriptor updates

Current: `1.7.4`

## Deployment Environments

| Environment | Description | Deployment Method |
|-------------|-------------|-------------------|
| Player machine (Windows) | Stellaris mod directory | Steam Workshop auto-update / manual zip extract |
| Player machine (Linux) | Stellaris mod directory | Steam Workshop auto-update / manual zip extract |
| Player machine (macOS) | Stellaris mod directory | Steam Workshop auto-update / manual zip extract |
| Steam Workshop | Distribution platform | Steam Workshop upload tool |
| Paradox Mods | Distribution platform | Paradox Mods upload |
| Nexus Mods | Distribution platform | Nexus Mods web upload |
| GitHub Releases | Distribution platform | GitHub Release assets |

### Mod Directory Locations

| Platform | Path |
|----------|------|
| Windows | `%USERPROFILE%\Documents\Paradox Interactive\Stellaris\mod\` |
| Linux | `~/.local/share/Paradox Interactive/Stellaris/mod/` |
| macOS | `~/Documents/Paradox Interactive/Stellaris/mod/` |
| Steam Deck | `~/.local/share/Steam/steamapps/compatdata/281990/pfx/drive_c/users/steamuser/Documents/Paradox Interactive/Stellaris/mod/` |

## Installation (Player Perspective)

### Steam Workshop (Recommended)

1. Visit [Steam Workshop page](https://steamcommunity.com/sharedfiles/filedetails/?id=2040234709)
2. Click "Subscribe"
3. Launch Stellaris launcher
4. Mod appears in mod list, enable it
5. Play

### Paradox Mods

1. Visit [Paradox Mods page](https://mods.paradoxplaza.com/mods/25437/Any)
2. Click "Install" (requires Paradox account)
3. Mod appears in Stellaris launcher
4. Enable and play

### Nexus Mods

1. Visit [Nexus Mods page](https://nexusmods.com/stellaris/mods/77)
2. Download latest version (manual or Vortex)
3. Extract to Stellaris mod directory
4. Enable in launcher

### GitHub Releases

1. Visit [GitHub Releases](https://github.com/hmlendea/stellaris-ui-species-names/releases)
2. Download latest `ui-species-names.zip`
3. Extract to Stellaris mod directory
4. Enable in launcher

### Manual Installation (All Platforms)

```bash
# 1. Download latest release
# 2. Extract to mod directory
# Linux/macOS:
unzip ui-species-names.zip -d ~/.local/share/Paradox\ Interactive/Stellaris/mod/

# Windows (PowerShell):
Expand-Archive ui-species-names.zip -DestinationPath "$env:USERPROFILE\Documents\Paradox Interactive\Stellaris\mod\"

# 3. Enable in Stellaris launcher
```

## Dependency Management

### Required Dependency

**Universum Infinitum - Name Lists** must be installed:
- [Steam Workshop](https://steamcommunity.com/sharedfiles/filedetails/?id=2040234709)
- [Paradox Mods](https://mods.paradoxplaza.com/mods/25437/Any)
- [Nexus Mods](https://nexusmods.com/stellaris/mods/77)
- [GitHub](https://github.com/hmlendea/stellaris-ui-name-lists)

### Dependency Version

No version pinning — this mod works with any version of Name Lists mod that provides the referenced name lists.

## CI/CD

### GitHub Actions

No workflows currently configured. If workflows are added, they should follow the canonical naming convention:
- `steam-workshop.yml` — Steam Workshop deployment
- `nexus-mods.yml` — Nexus Mods deployment
- `github-release.yml` — GitHub Release automation

### Validation Checks

Manual validation before release:
- [ ] Both descriptor files identical
- [ ] `supported_version` matches target Stellaris version
- [ ] All `name_list` references exist in Name Lists mod
- [ ] No duplicate species keys
- [ ] File encoding UTF-8, line endings LF
- [ ] Mod loads in Stellaris without errors

## Rollback Procedure

If a release has issues:

1. **GitHub Releases**: Delete release, re-tag previous version
2. **Steam Workshop**: Revert to previous version via Workshop tool
3. **Paradox Mods**: Upload previous version
4. **Nexus Mods**: Upload previous version, mark current as outdated

Players with auto-update may need to manually revert.

## Operational Considerations

### No Infrastructure

- No servers, databases, or services to operate
- No monitoring, alerting, or logging infrastructure
- No scaling concerns

### No Secrets in Deployment

- No API keys needed for distribution (manual upload)
- No credentials in mod files
- No environment-specific secrets

### Backup and Recovery

- Source code in Git (full history)
- Releases tagged in Git
- Distribution platforms retain previous versions
- No user data to backup

## Platform-Specific Notes

### Steam Workshop

- Auto-updates for subscribers
- Version detection via `descriptor.mod`
- Changelog shown in Workshop page

### Paradox Mods

- Integrated with Paradox launcher
- Dependency resolution (shows Name Lists as required)
- Version management via Paradox platform

### Nexus Mods

- Manual or Vortex installation
- Category: Stellaris → Species
- Version tracking via Nexus

### GitHub Releases

- Direct download
- No auto-update
- Source code included in repo