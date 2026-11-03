# Repository Overview

## Purpose

This repository contains **Universum Infinitum: Species Names**, a Stellaris mod that adds hundreds of new species names to the game. The mod is purely data-driven — it consists of static text files that define species name lists for Stellaris to use during empire creation and species generation.

## Scope

### What This Repository Owns

- Species name definitions for 8 base species classes (arthropoid, avian, fungoid, humanoid, mammalian, molluscoid, plantoid, reptilian)
- Media-themed species name packs (5 packs: Distant Worlds, D&D, Elder Scrolls, Galactic Civilizations, Narivia)
- Species modification prefixes and postfixes for genetic modification events
- Mod descriptor files for Stellaris and distribution platforms (Steam Workshop, Paradox Mods, Nexus Mods, GitHub Releases)
- Documentation and contribution guidelines

### What This Repository Does Not Own

- The Stellaris game engine or its name list processing logic
- The Universum Infinitum - Name Lists mod (required dependency, separate repository)
- Distribution platform infrastructure (Steam Workshop, Paradox Mods, Nexus Mods)
- Game localisation files (this mod uses English names only)

## Entry Points

### For Players

- **Steam Workshop**: Subscribe to the mod via Steam
- **Paradox Mods**: Install via Paradox launcher
- **Nexus Mods**: Download and install manually
- **GitHub Releases**: Download latest release and extract to mod directory

### For Contributors

- **Source files**: `ui-species-names/common/species_names/*.txt` — species name definitions
- **Random names**: `ui-species-names/common/random_names/base/ui-species-names.txt` — modification prefixes/postfixes
- **Mod descriptors**: `ui-species-names.mod` and `ui-species-names/descriptor.mod` — mod metadata

### For Stellaris (Runtime)

Stellaris loads the mod by reading:
1. `descriptor.mod` — mod metadata (version, name, supported game version, tags)
2. `common/species_names/*.txt` — species name list definitions
3. `common/random_names/base/ui-species-names.txt` — species modification name parts

## Principal Capabilities

1. **Base species name expansion** — Adds ~15 new species per base class (8 classes × ~15 = ~120 names)
2. **Media-themed name packs** — Adds ~25-30 species per media pack (5 packs × ~25 = ~125 names)
3. **Genetic modification names** — Provides prefixes/postfixes for genetically modified species
4. **Cross-platform compatibility** — Works on Windows, Linux, and macOS (no executable code)

## Component Relationships

```
┌─────────────────────────────────────────────────────────────┐
│                    Stellaris Game Engine                     │
│  (reads mod files, processes name lists at runtime)         │
└─────────────────────────────────────────────────────────────┘
                              ▲
                              │ reads
                              │
        ┌─────────────────────┼─────────────────────┐
        ▼                     ▼                     ▼
┌───────────────┐    ┌───────────────┐    ┌───────────────┐
│ Base Species  │    │ Media Packs   │    │ Random Names  │
│ Name Lists    │    │ (5 packs)     │    │ (prefixes/    │
│ (8 files)     │    │               │    │  postfixes)   │
└───────────────┘    └───────────────┘    └───────────────┘
        ▲                     ▲                     ▲
        │                     │                     │
        └─────────────────────┼─────────────────────┘
                              │
                              ▼
        ┌───────────────────────────────────────┐
        │     Universum Infinitum - Name Lists  │
        │         (required dependency)         │
        │  (provides base name list framework)  │
        └───────────────────────────────────────┘
```

## Dependency Direction

```
Stellaris Game Engine
       │
       ▼ (reads)
Universum Infinitum: Species Names (this mod)
       │
       ▼ (requires)
Universum Infinitum - Name Lists (dependency mod)
```

## Runtime Topology

- **No runtime process** — This is a static data mod
- **No executable code** — Pure text files read by Stellaris
- **No network communication** — No telemetry, analytics, or external connections
- **No persistent state** — Mod files are read-only at game runtime

## Major State

- **Mod version**: Defined in `ui-species-names.mod` and `descriptor.mod` (currently 1.7.4)
- **Supported game version**: `4.5.*` (Stellaris 4.5.x)
- **Species name data**: ~250+ species definitions across 13 files

## Major Integrations

| Integration | Type | Purpose |
|-------------|------|---------|
| Stellaris | Host application | Reads and processes mod files |
| Universum Infinitum - Name Lists | Required mod dependency | Provides name list framework |
| Steam Workshop | Distribution platform | Mod distribution |
| Paradox Mods | Distribution platform | Mod distribution |
| Nexus Mods | Distribution platform | Mod distribution |
| GitHub Releases | Distribution platform | Mod distribution |

## System-Wide Invariants

1. **Static data only** — No executable code, scripts, or binaries
2. **Cross-platform** — Files use UTF-8 encoding, LF line endings
3. **Dependency required** — Universum Infinitum - Name Lists must be installed
4. **Version alignment** — Mod version must match in both descriptor files
5. **Game version compatibility** — `supported_version` must match target Stellaris version