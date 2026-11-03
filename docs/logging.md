# Logging and Diagnostics

## Overview

This mod has **no runtime logging** — it is a static data mod. All diagnostics come from the **Stellaris engine** logging our mod's data during parsing and loading.

## Stellaris Engine Logging

### Log Files

| Platform | Path |
|----------|------|
| Windows | `%USERPROFILE%\Documents\Paradox Interactive\Stellaris\logs\error.log` |
| Linux | `~/.local/share/Paradox Interactive/Stellaris/logs/error.log` |
| macOS | `~/Documents/Paradox Interactive/Stellaris/logs/error.log` |

### Log Levels (Stellaris)

- `Error` — Critical failures (mod disabled)
- `Warning` — Non-critical issues (missing references)
- `Info` — General information (mod loaded)
- `Debug` — Verbose (requires debug mode)

### Our Mod's Log Signature

Search for these patterns in `error.log`:

```bash
# Mod loading
grep "ui-species-names" error.log

# Species definitions
grep "species_names" error.log

# Random names
grep "random_names" error.log

# Name list references
grep "name_list" error.log
```

## Expected Log Output

### Normal Operation (Success)

```
[Info] Mod "Universum Infinitum: Species Names" v1.7.4 loaded
[Info] Parsing species_names/ui_species_extra_arthropoid.txt
[Info] Parsing species_names/ui_species_extra_avian.txt
...
[Info] Parsing random_names/base/ui-species-names.txt
```

### Common Warnings (Non-Fatal)

```
[Warning] name_list "ui_extra_art1" not found
[Warning] Duplicate species key "ui_species_extra_arthropoid_01" ignored
```

### Errors (Fatal - Mod Disabled)

```
[Error] Parse error in species_names/ui_species_extra_arthropoid.txt:123: Expected '}' but found EOF
[Error] Failed to load mod "ui-species-names": descriptor.mod missing
```

## Diagnostic Commands

### Quick Health Check

```bash
# Check mod loaded
grep "ui-species-names" error.log | head -5

# Check for errors
grep -i "error.*ui-species-names\|ui-species-names.*error" error.log

# Check for warnings
grep -i "warning.*ui-species-names\|ui-species-names.*warning" error.log

# Count species parsed
grep "Parsing species_names" error.log | wc -l
```

### Reference Validation

```bash
# All name_list references from our mod
grep -h "name_list" ui-species-names/common/species_names/*.txt | \
  sed 's/.*name_list = "\([^"]*\)".*/\1/' | sort -u

# Check which resolve (requires Name Lists mod loaded)
# In-game console: debugtooltip -> hover species name
```

## No Application Logging

This mod does not:
- Write log files
- Use logging frameworks
- Have log levels
- Have structured logging
- Have log rotation
- Have log aggregation
- Send telemetry

## Debugging Workflow

### 1. Enable Stellaris Debug Logging

Launch options: `-debug` or edit `settings.txt`:
```
debug = yes
```

### 2. Reproduce Issue

- Start game
- Trigger issue (load mod, create empire, genetic modification)
- Exit game

### 3. Analyse Log

```bash
# Full mod-related log
grep -i "ui-species-names\|species_names\|random_names" error.log > mod-diagnostic.log

# Parse errors only
grep -A5 -B5 "Parse error" error.log

# Missing references
grep "not found" error.log | grep -i "ui_"
```

### 4. Correlate with Source

Match log line numbers to source files:
- Species files: `common/species_names/*.txt`
- Random names: `common/random_names/base/ui-species-names.txt`
- Descriptors: `ui-species-names.mod`, `ui-species-names/descriptor.mod`

## Log Retention

- Stellaris rotates logs on startup (keeps last few)
- No mod-specific retention policy
- Users should copy logs before restarting for bug reports

## Future Enhancements

| Enhancement | Effort | Value |
|-------------|--------|-------|
| Custom validation script with structured output | Medium | High |
| Pre-load validation tool | Medium | Medium |
| In-game debug console commands | Low (Stellaris side) | Medium |