# Troubleshooting

## Common Issues

### Mod Not Appearing in Launcher

**Symptoms**: Mod not listed in Stellaris launcher mod list.

**Causes & Solutions**:

| Cause | Solution |
|-------|----------|
| Wrong mod directory | Verify mod is in correct platform directory (see [Build and Deployment](build-and-deployment.md#mod-directory-locations)) |
| Descriptor file missing | Ensure `descriptor.mod` exists in `ui-species-names/` directory |
| Descriptor syntax error | Check `descriptor.mod` for valid syntax, compare with `ui-species-names.mod` |
| File encoding | Save descriptor as UTF-8 with LF line endings |
| Steam Workshop not synced | Restart Steam, wait for download, verify subscription |

### Mod Loads But Names Don't Appear

**Symptoms**: Mod enabled, no errors, but new species names not in empire creation.

**Causes & Solutions**:

| Cause | Solution |
|-------|----------|
| Name Lists mod not installed | Install [Universum Infinitum - Name Lists](https://steamcommunity.com/sharedfiles/filedetails/?id=2040234709) |
| Wrong species_class | Use exact class: ARTHROPOID, AVIAN, FUNGOID, HUMANOID, MAMMALIAN, MOLLUSCOID, PLANTOID, REPTILIAN |
| Invalid name_list reference | Verify `name_list` value exists in Name Lists mod |
| Duplicate species key | Check for duplicate keys across all species files |
| File not loaded | Verify file is in `common/species_names/` with `.txt` extension |

### Game Crashes on Startup

**Symptoms**: Stellaris crashes immediately after enabling mod.

**Causes & Solutions**:

| Cause | Solution |
|-------|----------|
| Syntax error in species file | Check game log (`error.log`), fix malformed braces, missing quotes |
| Invalid character in name | Use only valid characters in `name` field |
| Circular reference | Not applicable (no references between species files) |
| Stellaris version mismatch | Update `supported_version` in descriptor files |

### Genetic Modification Names Not Working

**Symptoms**: After genetic modification, species name doesn't get prefix/postfix.

**Causes & Solutions**:

| Cause | Solution |
|-------|----------|
| Random names file missing | Verify `ui-species-names/common/random_names/base/ui-species-names.txt` exists |
| Syntax error in random names file | Check prefix/postfix blocks have correct braces |
| File encoding | Save as UTF-8 with LF line endings |
| Mod load order | Ensure this mod loads after Name Lists mod (usually automatic) |

### "Failed to Load Mod" Error

**Symptoms**: Launcher shows error "Failed to load mod".

**Causes & Solutions**:

| Cause | Solution |
|-------|----------|
| Descriptor version format | Use `version = "1.7.4"` (string with quotes) |
| Missing required fields | Descriptor must have: name, version, supported_version, tags, path |
| Path mismatch | `path = "ui-species-names"` must match folder name exactly |
| Unsupported Stellaris version | Update `supported_version` to match installed Stellaris |

## Diagnostic Commands

### Check Mod Files

```bash
# Verify descriptor consistency
diff ui-species-names.mod ui-species-names/descriptor.mod

# Check file structure
find ui-species-names -type f -name "*.txt" | sort

# Check encoding
file ui-species-names/common/species_names/*.txt
file ui-species-names/common/random_names/base/ui-species-names.txt
file ui-species-names.mod
file ui-species-names/descriptor.mod
```

### Check for Syntax Issues

```bash
# Find unmatched braces (basic check)
grep -n "{" ui-species-names/common/species_names/*.txt | wc -l
grep -n "}" ui-species-names/common/species_names/*.txt | wc -l
# Counts should match

# Check for duplicate species keys
grep -h "^\s*[a-z_]\+ = {" ui-species-names/common/species_names/*.txt | \
  sed 's/^\s*\([a-z_]\+\) = {.*/\1/' | sort | uniq -d

# List all name_list references
grep -h "name_list" ui-species-names/common/species_names/*.txt | \
  sed 's/.*name_list = "\([^"]*\)".*/\1/' | sort -u
```

### Check Game Logs

**Log locations**:

| Platform | Path |
|----------|------|
| Windows | `%USERPROFILE%\Documents\Paradox Interactive\Stellaris\logs\error.log` |
| Linux | `~/.local/share/Paradox Interactive/Stellaris/logs/error.log` |
| macOS | `~/Documents/Paradox Interactive/Stellaris/logs/error.log` |

**Search for mod-related errors**:
```bash
grep -i "ui-species-names\|species_names\|random_names" error.log
grep -i "failed to load\|parse error\|syntax" error.log
```

## Platform-Specific Issues

### Windows

- **Path length limit**: Mod path too long → Move Stellaris install to shorter path
- **Line endings**: CRLF causes parse errors → Save files with LF (use Notepad++ or VS Code)
- **Permissions**: Mod directory read-only → Check folder permissions

### Linux

- **Case sensitivity**: File names case-sensitive → Use exact case in references
- **Steam Proton prefix**: Mod directory in compatdata → Use correct path for Steam Deck/Linux Steam
- **Flatpak Stellaris**: Different data path → `~/.var/app/com.valvesoftware.Steam/data/Steam/steamapps/compatdata/281990/pfx/drive_c/users/steamuser/Documents/Paradox Interactive/Stellaris/mod/`

### macOS

- **Gatekeeper**: Downloaded mod blocked → `xattr -d com.apple.quarantine ui-species-names.zip`
- **Case sensitivity**: APFS case-insensitive by default but can be case-sensitive
- **Steam Play**: Similar to Linux Proton paths

## Dependency Issues

### Name Lists Mod Not Found

**Error**: `name_list "ui_extra_art1" not found`

**Solutions**:
1. Install Name Lists mod from same platform (Steam/Paradox/Nexus/GitHub)
2. Enable Name Lists mod in launcher (load order: Name Lists first)
3. Verify Name Lists mod version has the referenced name lists
4. Check Name Lists mod `common/random_names/` for the referenced lists

### Version Mismatch

**Error**: Mod works but some names missing

**Cause**: Name Lists mod updated, references changed

**Solution**:
1. Check Name Lists mod changelog
2. Update `name_list` references in species files
3. Release patch version

## Getting Help

### Before Reporting

1. Check this troubleshooting guide
2. Verify mod and Name Lists mod are latest versions
3. Check game log for specific error messages
4. Try clean install: unsubscribe, delete mod folder, resubscribe

### Reporting Issues

**GitHub Issues**: [stellaris-ui-species-names/issues](https://github.com/hmlendea/stellaris-ui-species-names/issues)

**Include**:
- Stellaris version
- Mod version
- Platform (Windows/Linux/macOS/Steam Deck)
- Installation method (Steam/Paradox/Nexus/GitHub/Manual)
- Error log excerpt
- Steps to reproduce

### Community

- [Paradox Forum Thread](https://forum.paradoxplaza.com/forum/threads/universum-infinitum-species-names.1567890/)
- [Steam Workshop Comments](https://steamcommunity.com/sharedfiles/filedetails/?id=2040234709)
- [Discord](https://discord.gg/stellaris-modding) (if available)

## Known Limitations

| Limitation | Workaround |
|------------|------------|
| No automated testing | Manual validation before release |
| Depends on external mod | Document dependency clearly |
| No hot-reload | Restart game after mod changes |
| Platform-specific paths | Document all platform paths |
| No version pinning for dependency | Test with latest Name Lists mod |