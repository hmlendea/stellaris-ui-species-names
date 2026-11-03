# Flow: Mod Loading

## Overview

This flow describes how the Universum Infinitum: Species Names mod is loaded by the Stellaris engine at game startup.

## Sequence Diagram

```
┌─────────────┐     ┌──────────────┐     ┌─────────────────┐     ┌─────────────┐
│   Steam/    │     │   Stellaris  │     │  Mod Loader     │     │   Mod Files │
│  Launcher   │     │   Engine     │     │  (Internal)     │     │  (Disk)     │
└──────┬──────┘     └──────┬───────┘     └────────┬────────┘     └──────┬──────┘
       │                   │                      │                   │
       │ 1. Read descriptor│                      │                   │
       │◄──────────────────│                      │                   │
       │                   │                      │                   │
       │ 2. Validate       │                      │                   │
       │   version, path   │                      │                   │
       │                   │                      │                   │
       │                   │ 3. Load dependency   │                   │
       │                   │    (Name Lists)      │                   │
       │                   │◄─────────────────────│                   │
       │                   │                      │                   │
       │                   │ 4. Parse descriptor  │                   │
       │                   │◄─────────────────────│                   │
       │                   │                      │                   │
       │                   │ 5. Parse species     │                   │
       │                   │    definitions       │                   │
       │                   │◄─────────────────────│                   │
       │                   │                      │                   │
       │                   │ 6. Parse random      │                   │
       │                   │    names             │                   │
       │                   │◄─────────────────────│                   │
       │                   │                      │                   │
       │                   │ 7. Resolve name_list │                   │
       │                   │    references        │                   │
       │                   │◄─────────────────────│                   │
       │                   │                      │                   │
       │                   │ 8. Register species  │                   │
       │                   │    in engine         │                   │
       │                   │                      │                   │
       │ 9. Mod ready      │                      │                   │
       │◄──────────────────│                      │                   │
```

## Detailed Steps

### 1. Launcher Reads Descriptor

**Trigger**: Stellaris launcher starts or refreshes mods

**Action**: Launcher reads `ui-species-names.mod` (root) and `ui-species-names/descriptor.mod`

**Validation**:
- File exists
- Valid syntax
- `supported_version` matches current Stellaris version
- `path` points to existing folder

### 2. Dependency Resolution

**Trigger**: Mod enabled in launcher

**Action**: Launcher checks `dependencies` field in descriptor

**For this mod**:
```txt
dependencies = {
    "ugc_2040234709"  # Name Lists mod
}
```

**Behaviour**: Name Lists mod loaded first (if enabled)

### 3. Engine Mod Loading

**Trigger**: Player clicks "Play"

**Action**: Stellaris engine loads all enabled mods in order

**Load Order**:
1. Core game
2. DLCs
3. Mods (dependency order, then alphabetical)

### 4. Descriptor Parsing

**Component**: Stellaris mod loader

**Parsed Fields**:
- `name` → Mod display name
- `version` → Mod version (for launcher display)
- `supported_version` → Compatibility check
- `tags` → Categorisation
- `path` → Mod content root
- `dependencies` → Load order (already processed)

### 5. Species Definitions Parsing

**Component**: Stellaris species name system

**Files**: `common/species_names/*.txt` (13 files)

**Process**:
1. Enumerate files alphabetically
2. Parse each file as key-value tree
3. For each species definition:
   - Extract `species_key`
   - Extract `name` (display name)
   - Extract `name_list` (reference)
   - Extract `species_class`
   - Validate `species_class` enum
   - Register in species name registry

**Error Handling**:
- Parse error → Log error, skip file, continue
- Invalid `species_class` → Log warning, skip entry
- Duplicate `species_key` → Log warning, use first

### 6. Random Names Parsing

**Component**: Stellaris random name system

**File**: `common/random_names/base/ui-species-names.txt`

**Process**:
1. Parse `prefix` block → array of strings
2. Parse `postfix` block → array of strings
3. Register in genetic modification name generator

### 7. Name List Reference Resolution

**Component**: Stellaris name list system

**Process**:
1. For each species definition, get `name_list` value
2. Look up in global name list registry (populated by all mods)
3. If found: Link species to name list
4. If not found: Log warning, species will have no names

**Dependency**: Name Lists mod must be loaded first to populate registry

### 8. Species Registration

**Component**: Stellaris empire creation system

**Result**: Species available in:
- Empire creation name dropdown (filtered by portrait class)
- Genetic modification name generation

## Timing

| Phase | Timing |
|-------|--------|
| Launcher descriptor read | ~10ms |
| Dependency resolution | ~5ms |
| Engine mod load | ~50ms |
| Descriptor parsing | ~5ms |
| Species definitions parsing | ~20ms |
| Random names parsing | ~2ms |
| Reference resolution | ~10ms |
| Species registration | ~5ms |
| **Total** | **~107ms** |

## Failure Modes

| Failure Point | Symptom | Recovery |
|---------------|---------|----------|
| Descriptor missing | Mod not in launcher | Restore descriptor file |
| Descriptor syntax error | Mod not in launcher | Fix syntax |
| Version mismatch | Warning in launcher, may load | Update `supported_version` |
| Dependency missing | Names empty in-game | Install Name Lists mod |
| Species parse error | Some names missing | Fix syntax in species file |
| Random names parse error | No prefixes/postfixes | Fix syntax in random names file |
| Reference not found | Species has no names | Add name list to Name Lists mod |

## Validation Points

### Pre-Launch (Launcher)

- [ ] Descriptor files exist and match
- [ ] `supported_version` correct
- [ ] `path` correct
- [ ] Dependencies declared

### At Launch (Engine)

- [ ] All species files parse without errors
- [ ] All `name_list` references resolve
- [ ] Random names file parses
- [ ] Species registered for all 8 classes

### In-Game

- [ ] Names appear in empire creation
- [ ] Genetic modification uses prefixes/postfixes
- [ ] No errors in `error.log`

## Debugging

### Enable Debug Logging

Launch options: `-debug`

### Key Log Messages

```
[Info] Loading mod: Universum Infinitum: Species Names
[Info] Parsing species_names/ui_species_extra_arthropoid.txt
[Info] Registered species: ui_species_extra_arthropoid_01
[Warning] name_list "ui_extra_art1" not found
[Info] Parsing random_names/base/ui-species-names.txt
[Info] Loaded 10 prefixes, 10 postfixes
```

### Console Commands (In-Game)

```
debugtooltip  # Hover species name to see source
```

## Related Flows

- [Species Generation](species-generation.md) — How names are generated at runtime
- [Empire Creation](behaviour/empire-creation.md) — User-facing flow