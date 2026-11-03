# Design Decisions

## Overview

This document records significant design decisions, their rationale, and context for future maintainers.

## Decision Records

### 1. Static Data Mod Architecture

**Decision**: Implement as pure static data mod (declarative configuration only).

**Date**: Project inception

**Context**: Stellaris mods can be scripted (Lua) or static data. This mod only needs to define species names.

**Alternatives Considered**:
- Lua scripted mod with dynamic name generation
- Hybrid approach with some scripting

**Rationale**:
- Simplicity: No runtime logic to maintain
- Performance: Zero overhead, parsed once at startup
- Reliability: No script errors possible
- Compatibility: Works across Stellaris versions with minimal updates
- Distribution: Single zip file, no special requirements

**Consequences**:
- Cannot generate names dynamically
- Cannot react to game state
- Limited to predefined name lists
- Easy to understand and modify

### 2. Dependency on Name Lists Mod

**Decision**: Separate name lists into dedicated mod (Universum Infinitum - Name Lists).

**Date**: Early development

**Context**: Name lists are large and shared across potential mods.

**Alternatives Considered**:
- Bundle name lists in this mod
- Inline names directly in species definitions

**Rationale**:
- Separation of concerns: Name lists reusable by other mods
- Maintainability: Update names in one place
- Size: This mod stays small (~50KB vs ~500KB with names)
- Community: Other modders can use name lists
- Updates: Name lists can evolve independently

**Consequences**:
- Hard dependency required
- Two mods to install
- Coordination needed for releases
- Reference drift risk

### 3. Species Definition Structure

**Decision**: One species definition per name list reference, grouped by species class/media pack in separate files.

**Date**: Initial implementation

**Context**: Stellaris expects species definitions in `common/species_names/`.

**Alternatives Considered**:
- Single large file with all species
- One file per species
- Group by source (modder-created vs media)

**Rationale**:
- Maintainability: Logical grouping by class/pack
- Discoverability: Easy to find species by type
- Merge safety: Less conflict when multiple contributors edit
- Stellaris convention: Matches vanilla file organisation

**Consequences**:
- 13 files to maintain
- Cross-file duplicate key checks needed
- Consistent naming convention required

### 4. Naming Convention for Species Keys

**Decision**: Use `ui_species_<category>_<identifier>` pattern.

**Date**: Early development

**Examples**:
- `ui_species_extra_arthropoid_01`
- `ui_species_media_dnd_kobold`

**Alternatives Considered**:
- Simple numeric: `species_001`, `species_002`
- Descriptive only: `arthropoid_xenomorph`
- UUID-based

**Rationale**:
- Namespacing: `ui_` prefix avoids conflicts with vanilla/other mods
- Categorisation: `extra` vs `media` distinguishes source
- Class identification: Species class in key
- Readability: Human-parseable
- Sorting: Groups naturally in file listings

**Consequences**:
- Longer keys
- Convention must be documented and enforced

### 5. Media Pack Organisation

**Decision**: Separate file per media franchise, not merged with base classes.

**Date**: Media pack addition

**Context**: 5 media franchises added over time.

**Alternatives Considered**:
- Merge into base class files (e.g., D&D kobold in reptilian file)
- Single media file with all franchises

**Rationale**:
- Attribution: Clear source per franchise
- Optional: Players could delete unwanted pack files
- Legal: Clear separation for IP considerations
- Maintenance: Franchise updates isolated

**Consequences**:
- More files
- Species class mixed within media files
- Duplicate class handling in game (works fine)

### 6. Genetic Modification Prefixes/Postfixes

**Decision**: Define in `common/random_names/base/ui-species-names.txt` separate from species definitions.

**Date**: Genetic modification support added

**Context**: Stellaris uses random_names for genetic modification naming.

**Alternatives Considered**:
- Inline in each species definition
- Separate mod for prefixes/postfixes
- Use vanilla prefixes/postfixes only

**Rationale**:
- Stellaris architecture: Random names are separate system
- Consistency: All modified species use same prefix/postfix pool
- Simplicity: Single file to maintain
- Extensibility: Easy to add more parts

**Consequences**:
- Separate file to maintain
- Applies to all species (not per-species)
- Must not conflict with vanilla parts

### 7. Versioning Scheme

**Decision**: Semantic Versioning (MAJOR.MINOR.PATCH) with Stellaris version in `supported_version`.

**Date**: First release

**Context**: Multiple distribution platforms need version tracking.

**Alternatives Considered**:
- Date-based versioning
- Stellaris-version-only (4.5.0, 4.5.1)
- Simple incrementing integer

**Rationale**:
- Industry standard: SemVer understood by users/tools
- Clear change signalling: MAJOR=breaking, MINOR=features, PATCH=fixes
- Independent of Stellaris version: Mod can patch without Stellaris update
- Platform compatibility: Works with Steam, Paradox, Nexus, GitHub

**Consequences**:
- Two version numbers to track (mod version + supported_version)
- Must bump correctly on each release

### 8. No Build Process

**Decision**: Distribute source files directly, no compilation/build step.

**Date**: Project inception

**Context**: Mod files are plain text, parsed by Stellaris directly.

**Alternatives Considered**:
- Build script to validate/concatenate
- Preprocessor for templating
- CI pipeline with validation

**Rationale**:
- Simplicity: Zero tooling required
- Transparency: What you see is what loads
- Accessibility: Anyone can edit with text editor
- Portability: Works on any OS without dependencies
- Stellaris loads source directly

**Consequences**:
- No automated validation in CI
- Manual validation required before release
- Syntax errors only caught at game startup

### 9. File Encoding and Line Endings

**Decision**: UTF-8 encoding, LF line endings for all files.

**Date**: Project inception

**Context**: Cross-platform mod distribution.

**Alternatives Considered**:
- Platform-native (CRLF on Windows)
- UTF-16
- No enforcement

**Rationale**:
- Stellaris parser: Handles UTF-8 LF on all platforms
- Git: LF normalised in repo
- Editors: Modern editors handle UTF-8 LF everywhere
- Consistency: No platform-specific issues

**Consequences**:
- Windows contributors must configure editors
- Validation step needed for releases

### 10. License Choice

**Decision**: GNU GPL v3.0

**Date**: Project inception

**Context**: Open source mod, derivative works expected.

**Alternatives Considered**:
- MIT (permissive)
- Apache 2.0 (patent clause)
- CC-BY-SA (creative works)
- Proprietary/closed

**Rationale**:
- Copyleft: Derivative mods must share source
- Community: Encourages contribution back
- Compatibility: GPL v3 compatible with Stellaris modding ecosystem
- Legal clarity: Well-understood terms

**Consequences**:
- Commercial use restricted
- Derivative works must be GPL v3
- Must include license text

## Rejected Decisions

### Dynamic Name Generation via Lua

**Rejected**: Complexity not justified for static name lists.

### Inline Names in Species Definitions

**Rejected**: Duplicates name data, harder to maintain, larger mod size.

### Single File for All Species

**Rejected**: Merge conflicts, hard to navigate, doesn't match Stellaris conventions.

### Version Pinning for Name Lists Dependency

**Rejected**: Name Lists mod maintains backward compatibility; pinning creates update friction.

### Automated CI Validation

**Rejected**: No headless Stellaris for testing; validation scripts would duplicate parser logic.

## Future Decision Points

| Decision Needed | Trigger | Options |
|-----------------|---------|---------|
| Stellaris 4.6+ format changes | New Stellaris major version | Adapt format, maintain compatibility layer |
| Name Lists mod restructuring | Major Name Lists update | Update references, coordinate release |
| New media franchise | Community request | Add new media pack file |
| Automated validation tooling | Contributor demand | Custom parser/validator script |
| Localisation support | Translation requests | Add localisation files |