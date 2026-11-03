# Dependencies

## Runtime Dependencies

### Required: Universum Infinitum - Name Lists

| Property | Value |
|----------|-------|
| **Name** | Universum Infinitum - Name Lists |
| **Type** | Stellaris mod (name list provider) |
| **Relationship** | Hard dependency — this mod cannot function without it |
| **Provides** | `name_list` references (e.g., `ui_extra_art1`, `ui_dnd_kobold`, `ui_media_dw_*`) |
| **Version Pinning** | None — works with any version providing referenced lists |
| **Distribution** | Same platforms: Steam Workshop, Paradox Mods, Nexus Mods, GitHub |

#### Name List References Used

This mod references the following name lists from Name Lists mod:

**Base Extra Packs** (8 files, ~160 species):
- `ui_extra_art1` — `ui_extra_art10` (Arthropoid)
- `ui_extra_avi1` — `ui_extra_avi10` (Avian)
- `ui_extra_fun1` — `ui_extra_fun10` (Fungoid)
- `ui_extra_hum1` — `ui_extra_hum10` (Humanoid)
- `ui_extra_mam1` — `ui_extra_mam10` (Mammalian)
- `ui_extra_mol1` — `ui_extra_mol10` (Molluscoid)
- `ui_extra_pla1` — `ui_extra_pla10` (Plantoid)
- `ui_extra_rep1` — `ui_extra_rep10` (Reptilian)

**Media Packs** (5 files, ~90 species):
- `ui_media_dw_*` (Distant Worlds)
- `ui_media_dnd_*` (Dungeons & Dragons)
- `ui_media_es_*` (Elder Scrolls)
- `ui_media_gc_*` (Galactic Civilizations)
- `ui_media_nar_*` (Narivia)

### Stellaris Game Engine

| Property | Value |
|----------|-------|
| **Name** | Stellaris |
| **Version** | 4.5.* (per `supported_version`) |
| **Role** | Host runtime — parses mod files, provides UI, executes game logic |
| **Mod API** | Declarative data format (custom key-value syntax) |

## Build-Time Dependencies

**None.** No build process, no compilation, no package managers, no CI dependencies.

## Development Dependencies

### Optional Tools

| Tool | Purpose | Required |
|------|---------|----------|
| Git | Version control | Yes (for contributors) |
| Text editor (VS Code, Notepad++) | Edit mod files | Yes |
| Stellaris | Testing | Yes |
| diff | Descriptor validation | No (manual) |
| grep | Reference validation | No (manual) |

### No Package Managers

- No `npm`, `pip`, `cargo`, `nuget`, `maven`, `gradle`
- No `package.json`, `requirements.txt`, `Cargo.toml`, `.csproj`
- No lock files

## Dependency Graph

```
┌─────────────────────────────────────┐
│         Stellaris 4.5.*             │
│         (Host Runtime)              │
└──────────────┬──────────────────────┘
               │ loads
               ▼
┌─────────────────────────────────────┐
│  Universum Infinitum: Species Names │
│  (This Mod)                         │
│  - Species definitions              │
│  - Random name prefixes/postfixes   │
└──────────────┬──────────────────────┘
               │ references
               ▼
┌─────────────────────────────────────┐
│  Universum Infinitum: Name Lists    │
│  (Dependency Mod)                   │
│  - Name list definitions            │
│  - Actual name pools                │
└─────────────────────────────────────┘
```

## Version Compatibility Matrix

| This Mod | Name Lists Mod | Stellaris | Status |
|----------|----------------|-----------|--------|
| 1.7.x | Any recent | 4.5.* | ✅ Supported |
| 1.6.x | Any recent | 4.4.* | ⚠️ Legacy |
| 1.5.x | Any recent | 4.3.* | ⚠️ Legacy |

## Dependency Management Procedures

### Adding New Name List References

1. Verify name list exists in Name Lists mod
2. Add species definition referencing it
3. Test in-game
4. No version bump needed for Name Lists mod

### When Name Lists Mod Updates

| Change in Name Lists | Action Required |
|---------------------|-----------------|
| New name lists added | Optional: add species referencing them |
| Name lists renamed | Update references in species files |
| Name lists removed | Remove or update species referencing them |
| Format changes | Check compatibility, update if needed |

### Coordinating Releases

- Monitor Name Lists mod releases
- Test this mod against new Name Lists version
- Release patch if references change
- Communicate with Name Lists maintainer for major changes

## Platform-Specific Dependency Resolution

| Platform | Resolution Method |
|----------|-------------------|
| Steam Workshop | Automatic (subscribed mods load together) |
| Paradox Mods | Automatic (dependency declared in descriptor) |
| Nexus Mods | Manual (user must install both) |
| GitHub | Manual (user must install both) |

### Paradox Mods Descriptor Dependency

In `descriptor.mod` (and `ui-species-names.mod`):
```txt
dependencies = {
    "ugc_2040234709"  # Name Lists mod Steam ID
}
```
*Note: Actual dependency declaration may vary by platform.*

## Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Name Lists mod abandoned | Low | High | Fork/maintain name lists if needed |
| Breaking changes in Name Lists | Medium | High | Test before release, coordinate |
| Stellaris version breaks format | Low | High | Update `supported_version`, test on beta |
| Reference drift over time | Medium | Medium | Periodic validation, automated checks |

## No Transitive Dependencies

This mod does not introduce any transitive dependencies. The only runtime dependency is the Name Lists mod, which itself has no dependencies beyond Stellaris.