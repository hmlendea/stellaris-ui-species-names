# Configuration

## Configuration Schema

This mod has **no runtime configuration**. All configuration is static and defined in mod descriptor files.

### Mod Descriptor Configuration

Both `ui-species-names.mod` and `ui-species-names/descriptor.mod` contain identical configuration:

| Field | Type | Required | Description | Example |
|-------|------|----------|-------------|---------|
| `version` | String | Yes | Mod version (semantic versioning) | `1.7.4` |
| `name` | String | Yes | Display name in launcher | `Universum Infinitum: Species Names` |
| `path` | String | Yes | Install path relative to mod directory | `mod/ui-species-names` |
| `tags` | Object | Yes | Categorisation tags | `{ "Species" }` |
| `supported_version` | String | Yes | Stellaris version compatibility | `4.5.*` |

### Configuration Sources

| Source | Priority | Description |
|--------|----------|-------------|
| `ui-species-names.mod` | Primary (distribution) | Read by Steam Workshop, Paradox Mods, Nexus Mods, GitHub Releases |
| `ui-species-names/descriptor.mod` | Primary (launcher) | Read by Stellaris launcher |

Both files **must be identical**. No override or merge occurs.

### Configuration Precedence

```
1. ui-species-names.mod (distribution platforms)
2. ui-species-names/descriptor.mod (Stellaris launcher)
   → Must be identical; no precedence resolution
```

## Environment-Specific Configuration

This mod has **no environment-specific configuration**. The same files work on:
- Windows
- Linux
- macOS
- Steam Deck (SteamOS)

No platform-specific overrides exist.

## Secrets and Sensitive Data

This mod **contains no secrets, credentials, or sensitive data**. All files are:
- Public text files
- No API keys, tokens, or passwords
- No personal data
- Safe for public distribution

## Configuration Validation

### At Release Time

- Both descriptor files must have identical content
- `version` must follow semantic versioning
- `supported_version` must match target Stellaris version
- `path` must be `mod/ui-species-names`

### At Game Startup (Stellaris)

- Launcher validates `descriptor.mod` syntax
- Launcher checks `supported_version` against running Stellaris version
- Incompatible mods are disabled with warning

### At Mod Load (In-Game)

- Name list parser validates species definition syntax
- Unresolved `name_list` references logged as errors
- Invalid species entries skipped

## Modifying Configuration

### Updating Mod Version

1. Update `version` in both descriptor files
2. Ensure both files remain identical
3. Tag release in Git
4. Publish to distribution platforms

### Updating Supported Stellaris Version

1. Update `supported_version` in both descriptor files (e.g., `4.5.*` → `4.6.*`)
2. Test mod with new Stellaris version
3. Release new mod version

### Adding/Removing Tags

1. Modify `tags` block in both descriptor files
2. Keep `Species` tag (required for categorisation)
3. Additional tags optional

## Configuration File Locations

| File | Repository Path | Installed Path |
|------|-----------------|----------------|
| Distribution descriptor | `ui-species-names.mod` | `<stellaris_mod_dir>/ui-species-names.mod` |
| Launcher descriptor | `ui-species-names/descriptor.mod` | `<stellaris_mod_dir>/ui-species-names/descriptor.mod` |

## No Runtime Configuration

This mod does not support:
- Configuration files in user directory
- In-game settings menu
- Command-line arguments
- Environment variables
- Remote configuration
- Feature flags

All behaviour is determined by static data files at game startup.