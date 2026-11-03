# System Invariants

## Overview

This document defines the invariants — conditions that must always hold true — for the Universum Infinitum: Species Names mod. These invariants ensure correctness, compatibility, and maintainability.

## File-Level Invariants

### Descriptor Files

| Invariant | Description | Validation |
|-----------|-------------|------------|
| `ui-species-names.mod` == `ui-species-names/descriptor.mod` | Both descriptor files must be identical | `diff` check |
| `version` format | Semantic version: `MAJOR.MINOR.PATCH` | Regex: `^\d+\.\d+\.\d+$` |
| `supported_version` format | Stellaris version pattern: `X.Y.*` | Regex: `^\d+\.\d+\.\*$` |
| `path` value | Must equal `"ui-species-names"` | Exact string match |
| `tags` array | Must contain `"Species"` and `"Name Lists"` | Array contains both |

### Species Definition Files

| Invariant | Description | Validation |
|-----------|-------------|------------|
| Unique species keys | No duplicate keys across all files in `common/species_names/` | `grep` + `sort` + `uniq -d` |
| Key naming convention | All keys match `^ui_species_(extra|media)_[a-z_]+$` | Regex validation |
| Required fields present | Each species has `name`, `name_list`, `species_class` | Field existence check |
| `species_class` values | Must be one of 8 vanilla classes | Enum validation |
| `name_list` references | Must exist in Name Lists mod | Cross-reference check |
| File encoding | UTF-8, LF line endings | `file` command |
| No trailing whitespace | Clean formatting | Editor/linter |

### Random Names File

| Invariant | Description | Validation |
|-----------|-------------|------------|
| Structure | Contains `prefix` and `postfix` blocks | Block existence |
| Array format | Each block contains quoted strings | Syntax check |
| No duplicates within block | Unique prefixes, unique postfixes | `sort` + `uniq -d` |
| Non-empty | At least one entry per block | Count > 0 |

## Runtime Invariants

### Mod Loading

| Invariant | Description |
|-----------|-------------|
| Name Lists mod loaded first | Dependency load order respected |
| All species definitions parsed | No parse errors in any file |
| All `name_list` references resolved | No "not found" warnings for our refs |
| Mod version reported correctly | Launcher shows `version` from descriptor |

### Empire Creation

| Invariant | Description |
|-----------|-------------|
| All 8 base classes have entries | At least one species per class |
| Media pack species appear | When corresponding portrait selected |
| Names drawn from correct list | `name_list` reference honoured |
| No vanilla names replaced | Additive only |

### Genetic Modification

| Invariant | Description |
|-----------|-------------|
| Prefix applied | Random prefix from `prefix` block |
| Postfix applied | Random postfix from `postfix` block |
| Original name preserved | Format: `Prefix OriginalName Postfix` |
| Parts from this mod used | Not vanilla parts (when this mod loaded) |

## Data Integrity Invariants

### Cross-Mod Consistency

| Invariant | Description |
|-----------|-------------|
| Name Lists provides all referenced lists | Every `name_list` in this mod exists in Name Lists |
| No orphaned references | No `name_list` value without provider |
| Version compatibility | This mod's `supported_version` ≤ Name Lists' `supported_version` |

### Internal Consistency

| Invariant | Description |
|-----------|-------------|
| Species count matches expectation | ~250+ species across files |
| Media packs self-contained | Each media file references only its franchise lists |
| Base extra files class-pure | Each extra file contains only its class |

## Distribution Invariants

### Release Artefact

| Invariant | Description |
|-----------|-------------|
| Zip contains `ui-species-names/` folder | Correct root structure |
| All 13 species files present | No missing files |
| Both descriptor files present | Root and mod folder |
| No extra files | Only expected files in archive |

### Platform Consistency

| Invariant | Description |
|-----------|-------------|
| Same version on all platforms | Steam, Paradox, Nexus, GitHub |
| Same file content on all platforms | Byte-identical archives |
| Changelog consistent | Same release notes everywhere |

## Development Invariants

### Git Repository

| Invariant | Description |
|-----------|-------------|
| `main` branch always releasable | Passes all validation |
| Tags match release versions | `v1.7.4` for version `1.7.4` |
| No uncommitted changes in release | Clean working tree |
| Commit messages follow convention | Descriptive, present tense |

### Code Review

| Invariant | Description |
|-----------|-------------|
| All validation checks pass | Pre-merge validation |
| Documentation updated | For user-facing changes |
| No duplicate keys introduced | Checked in review |

## Invariant Violation Response

| Severity | Response |
|----------|----------|
| Critical (mod won't load) | Block release, fix immediately |
| High (missing names, wrong behaviour) | Block release, fix before release |
| Medium (cosmetic, minor inconsistency) | Fix in next patch |
| Low (style, documentation) | Fix when convenient |

## Validation Automation

### Current (Manual)

```bash
# Run all checks
./validate-all.sh  # (to be created)
```

### Planned (Automated)

- Pre-commit hooks for contributors
- CI pipeline validation
- Release gate checks

## Invariant Catalogue Summary

| Category | Count | Critical |
|----------|-------|----------|
| Descriptor files | 5 | 5 |
| Species definitions | 8 | 6 |
| Random names | 4 | 2 |
| Runtime | 8 | 4 |
| Data integrity | 3 | 3 |
| Distribution | 4 | 4 |
| Development | 4 | 2 |
| **Total** | **36** | **26** |