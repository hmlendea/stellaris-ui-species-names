# Change Guide

## Purpose

This guide documents how to make changes to the mod, covering common modification patterns, validation steps, and release procedures.

## Common Change Types

### Adding New Species Names

**Files to modify**: One or more files in `ui-species-names/common/species_names/`

**Pattern**:
```txt
new_species_key = {
    name = "Display Name"
    name_list = "ui_name_list_reference"
    species_class = "CLASS"
}
```

**Steps**:
1. Choose appropriate file by species class (arthropoid, avian, fungoid, humanoid, mammalian, molluscoid, plantoid, reptilian) or media pack
2. Add new species definition at end of file
3. Ensure `name_list` reference exists in Name Lists mod
4. Use unique key (prefix with `ui_species_` for consistency)
5. Validate: no duplicate keys, correct syntax

### Adding New Media Pack

**Files to create**: New file in `ui-species-names/common/species_names/` named `ui_species_media_<pack-name>.txt`

**Pattern**:
```txt
# Media Pack: <Pack Name>
# Source: <Source Material>

ui_species_media_<pack>_<species> = {
    name = "Display Name"
    name_list = "ui_media_<pack>_<list>"
    species_class = "CLASS"
}
```

**Steps**:
1. Create new file with descriptive name
2. Add species definitions following pattern
3. Ensure all `name_list` references exist in Name Lists mod
4. Update documentation (INDEX.md, repository-overview.md)

### Adding Genetic Modification Prefixes/Postfixes

**File to modify**: `ui-species-names/common/random_names/base/ui-species-names.txt`

**Pattern**:
```txt
# Prefixes
prefix = {
    "New Prefix"
    "Another Prefix"
}

# Postfixes
postfix = {
    "New Postfix"
    "Another Postfix"
}
```

**Steps**:
1. Add entries to appropriate block (prefix or postfix)
2. Keep alphabetical or thematic grouping
3. Test in-game: genetically modify species, verify new parts appear

### Updating Stellaris Version Compatibility

**Files to modify**:
- `ui-species-names.mod`
- `ui-species-names/descriptor.mod`

**Change**:
```txt
supported_version = "4.5.*"
```
→
```txt
supported_version = "4.6.*"
```

**Steps**:
1. Update both files identically
2. Test mod loads on new Stellaris version
3. Check for any format changes in Stellaris modding docs
4. Update version (MINOR bump recommended)

## Validation Before Commit

### Syntax Validation

```bash
# Check descriptor consistency
diff ui-species-names.mod ui-species-names/descriptor.mod

# Check for duplicate species keys
grep -h "^\s*[a-z_]\+ = {" ui-species-names/common/species_names/*.txt | \
  sed 's/^\s*\([a-z_]\+\) = {.*/\1/' | sort | uniq -d

# Check name_list references exist (manual cross-reference with Name Lists mod)
grep -h "name_list" ui-species-names/common/species_names/*.txt | \
  sed 's/.*name_list = "\([^"]*\)".*/\1/' | sort -u

# Verify file encoding (all should be UTF-8)
file ui-species-names/common/species_names/*.txt
file ui-species-names/common/random_names/base/ui-species-names.txt
```

### In-Game Validation

1. Install mod in Stellaris
2. Launch game
3. Check launcher log for errors
4. Open empire creation
5. Verify new names appear for modified classes/packs
6. Test genetic modification (if prefixes/postfixes changed)

## Release Procedure

### Version Bump

| Change Type | Version Bump |
|-------------|--------------|
| New species names, media packs | MINOR (1.7.4 → 1.8.0) |
| Bug fixes, typos, descriptor updates | PATCH (1.7.4 → 1.7.5) |
| Breaking format changes | MAJOR (1.7.4 → 2.0.0) |

### Release Steps

1. Update version in both descriptor files
2. Run validation checks
3. Test in-game
4. Commit changes: `git commit -am "Release v1.8.0 - Added X species"`
5. Tag: `git tag -a v1.8.0 -m "Release version 1.8.0"`
6. Push: `git push origin main --tags`
7. Create GitHub Release with zip archive
8. Upload to Steam Workshop, Paradox Mods, Nexus Mods

## Common Pitfalls

| Pitfall | Symptom | Prevention |
|---------|---------|------------|
| Descriptor mismatch | Mod doesn't appear or wrong version | Always update both files, run `diff` |
| Duplicate species key | Undefined behaviour, one ignored | Run duplicate check before commit |
| Invalid name_list reference | Species has no names in-game | Cross-reference with Name Lists mod |
| Wrong species_class | Names don't appear for that class | Use exact class names: ARTHROPOID, AVIAN, FUNGOID, HUMANOID, MAMMALIAN, MOLLUSCOID, PLANTOID, REPTILIAN |
| Encoding issues | Parse errors on some platforms | Save as UTF-8, LF line endings |
| Missing comma/braces | Parse error, mod fails to load | Validate syntax, test in-game |

## File Format Reference

### Species Definition

```txt
species_key = {
    name = "Display Name"           # Required: shown in UI
    name_list = "reference"         # Required: must exist in Name Lists mod
    species_class = "CLASS"         # Required: one of 8 base classes
    # Optional: portrait, etc. (not used in this mod)
}
```

### Random Names (Prefixes/Postfixes)

```txt
prefix = {
    "Prefix 1"
    "Prefix 2"
}

postfix = {
    "Postfix 1"
    "Postfix 2"
}
```

### Descriptor File

```txt
name = "Universum Infinitum: Species Names"
version = "1.7.4"
supported_version = "4.5.*"
tags = {
    "Species"
    "Name Lists"
}
path = "ui-species-names"
```

## Coordination with Name Lists Mod

This mod **depends on** Universum Infinitum - Name Lists mod.

### When Name Lists Mod Changes

- New name lists added → Can add species referencing them
- Name lists renamed/removed → Must update or remove species referencing them
- Version bump in Name Lists → No action needed unless refs change

### Communication

- Check Name Lists mod changelog before releasing
- Coordinate major changes with Name Lists maintainer
- Test against latest Name Lists mod version

## Rollback

If a change breaks the mod:

1. `git revert <commit>` or `git reset --hard <tag>`
2. Re-run validation
3. Release patch version