# Error Handling

## Overview

This mod is a **static data mod** with no executable code. Error handling consists of **prevention through validation** and **graceful degradation** by the Stellaris engine.

## Error Categories

### 1. Parse Errors (Stellaris Engine)

**Source**: Stellaris mod loader parsing mod files.

**Triggers**:
- Syntax errors in `.txt` files (unmatched braces, missing quotes, invalid characters)
- Encoding issues (non-UTF-8)
- Invalid key names

**Behaviour**: Mod fails to load, error in game log, mod disabled.

**Prevention**:
- Validate syntax before release
- Use UTF-8 with LF line endings
- Test in-game after changes

### 2. Reference Errors (Stellaris Engine)

**Source**: Stellaris resolving `name_list` references.

**Triggers**:
- `name_list` value doesn't exist in any loaded mod
- Name Lists mod not installed
- Name Lists mod loaded after this mod

**Behaviour**: Species definition loads but has no names (empty dropdown), warning in log.

**Prevention**:
- Cross-reference all `name_list` values with Name Lists mod
- Document dependency clearly
- Test with fresh install

### 3. Duplicate Key Errors (Stellaris Engine)

**Source**: Multiple species definitions with same key.

**Triggers**:
- Same key in multiple files
- Same key twice in one file

**Behaviour**: Undefined — one definition used, other ignored, no error logged.

**Prevention**:
- Run duplicate key check before release
- Use namespaced keys (`ui_species_...`)

### 4. Version Compatibility Errors

**Source**: `supported_version` mismatch.

**Triggers**:
- Stellaris version newer than `supported_version`
- Major format changes in Stellaris

**Behaviour**: Launcher shows warning, mod may still work or may fail.

**Prevention**:
- Update `supported_version` on Stellaris major releases
- Test on beta branches

## Error Handling Patterns

### Prevention (Primary Strategy)

| Check | When | Tool |
|-------|------|------|
| Descriptor consistency | Pre-commit, pre-release | `diff` |
| Duplicate species keys | Pre-release | `grep` + `sort` + `uniq` |
| Reference validity | Pre-release | Manual cross-reference |
| Encoding/line endings | Pre-release | `file` command |
| In-game load test | Pre-release | Manual |

### Graceful Degradation (Stellaris Engine)

Stellaris handles errors by:
- Skipping malformed entries (continues loading rest)
- Logging warnings (not errors) for missing references
- Disabling mod only for critical parse errors

### No Runtime Error Handling

- No try/catch (no code)
- No fallback values (static data)
- No retry logic (load-time only)
- No user-facing error messages (launcher shows generic)

## Diagnostic Information

### Game Log Location

| Platform | Path |
|----------|------|
| Windows | `%USERPROFILE%\Documents\Paradox Interactive\Stellaris\logs\error.log` |
| Linux | `~/.local/share/Paradox Interactive/Stellaris/logs/error.log` |
| macOS | `~/Documents/Paradox Interactive/Stellaris/logs/error.log` |

### Key Log Patterns

```bash
# Mod loading
grep "ui-species-names" error.log

# Parse errors
grep -i "parse\|syntax\|brace" error.log

# Missing references
grep -i "name_list\|not found" error.log

# Version warnings
grep -i "supported_version\|version" error.log
```

## Common Error Scenarios

### Scenario: Mod Not Loading

**Symptoms**: Mod not in launcher, or shows as failed.

**Diagnosis**:
1. Check `error.log` for parse errors
2. Verify `descriptor.mod` syntax
3. Check file encoding
4. Verify folder structure

**Resolution**: Fix syntax, re-save as UTF-8 LF.

### Scenario: Names Missing In-Game

**Symptoms**: Mod loads, no errors, but names don't appear.

**Diagnosis**:
1. Check `error.log` for "name_list not found"
2. Verify Name Lists mod installed and enabled
3. Check load order (Name Lists first)
4. Verify `name_list` spelling

**Resolution**: Install/update Name Lists mod, fix references.

### Scenario: Duplicate Names / Weird Behaviour

**Symptoms**: Some names appear twice, or wrong names for species.

**Diagnosis**:
1. Check for duplicate species keys
2. Verify `species_class` values
3. Check for conflicting mods

**Resolution**: Remove duplicates, fix class values.

## Validation Commands Reference

```bash
# Full validation suite
./validate.sh  # (if created)

# Individual checks
diff ui-species-names.mod ui-species-names/descriptor.mod

grep -h "^\s*[a-z_]\+ = {" ui-species-names/common/species_names/*.txt | \
  sed 's/^\s*\([a-z_]\+\) = {.*/\1/' | sort | uniq -d

grep -h "name_list" ui-species-names/common/species_names/*.txt | \
  sed 's/.*name_list = "\([^"]*\)".*/\1/' | sort -u

file ui-species-names/common/species_names/*.txt
file ui-species-names/common/random_names/base/ui-species-names.txt
```

## Error Reporting

### For Users

Report via GitHub Issues with:
- Stellaris version
- Mod version
- Platform
- Installation method
- Relevant `error.log` excerpt

### For Contributors

Add validation to change guide, update troubleshooting.

## Future Improvements

- Custom validation script (parse Stellaris format)
- CI integration for syntax checks
- Automated reference checking against Name Lists mod (if machine-readable)
- Pre-commit hooks for contributors