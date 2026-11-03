# State and Persistence

## Overview

This mod is a **static data mod** with **no runtime state** and **no persistence mechanism**. All data is declarative configuration loaded at game startup.

## State Model

### No Application State

| State Type | Present? | Details |
|------------|----------|---------|
| In-memory objects | No | No code execution |
| Session state | No | No sessions |
| User preferences | No | No settings UI |
| Cache | No | No caching layer |
| Database | No | No database |
| File-based state | No | No write operations |

### Stellaris Engine State (External)

The Stellaris engine maintains state derived from our mod:

| Engine State | Source | Persistence |
|--------------|--------|-------------|
| Loaded species definitions | `common/species_names/*.txt` | Save game |
| Available name lists | `name_list` references | Save game |
| Prefix/postfix pools | `common/random_names/base/ui-species-names.txt` | Save game |
| Empire names (generated) | Runtime generation | Save game |

## Data Flow

```
Mod Files (Static)
       │
       ▼
Stellaris Parser (Startup)
       │
       ▼
Engine Internal State (Runtime)
       │
       ├──► Empire Creation UI
       ├──► Genetic Modification
       └──► Save Game Serialisation
```

## Persistence Boundaries

### What Persists (Stellaris Save Games)

- Empire names chosen by player
- Species names after genetic modification
- Game-generated names from our name lists

### What Does Not Persist (Mod Scope)

- Mod file content (reloaded each startup)
- Name list references (re-resolved each startup)
- Prefix/postfix pools (reloaded each startup)

## Save Game Compatibility

### Additive Changes (Safe)

| Change | Save Compatible? | Reason |
|--------|------------------|--------|
| New species definitions | Yes | New options only |
| New prefixes/postfixes | Yes | Expanded pool |
| New media packs | Yes | New options only |
| Fix typos in display names | Yes | Cosmetic |

### Breaking Changes (Incompatible)

| Change | Save Compatible? | Reason |
|--------|------------------|--------|
| Remove species definition | No | Empires using it break |
| Rename species key | No | Reference lost |
| Change `name_list` reference | No | Different names generated |
| Remove prefix/postfix | Maybe | Existing modified names OK, new ones affected |

## Version Upgrade Behaviour

### Mod Version Upgrade

1. Player updates mod (Steam auto-update or manual)
2. Next game launch: Stellaris reloads all mod files
3. New definitions available immediately
4. Existing saves: New options available, old choices preserved

### Stellaris Version Upgrade

1. Stellaris updates
2. Mod `supported_version` updated
3. Mod reloads on next launch
4. Save games: Stellaris handles migration (mod data unaffected)

## No State Management Code

This mod does not implement:
- State machines
- Event sourcing
- CQRS
- Snapshotting
- Migration scripts
- State validation
- Concurrency control (no concurrent access)

## Configuration as State

The closest concept to "state" is the **mod configuration** (the `.txt` files themselves):

| Property | Value |
|----------|-------|
| Format | Stellaris declarative syntax |
| Encoding | UTF-8 |
| Line endings | LF |
| Location | `ui-species-names/common/` |
| Mutability | Edit source, reload game |
| Version control | Git |

## Backup and Recovery

### Mod Files

- **Source of truth**: Git repository
- **Backup**: Git history, GitHub remote
- **Recovery**: `git checkout`, `git restore`

### Player Data

- **Save games**: Managed by Stellaris
- **Mod settings**: None (no settings)
- **Recovery**: Stellaris save management

## Observability

### No State Metrics

- No health checks
- No performance metrics
- No business metrics
- No audit logs

### Debugging State Issues

1. Check `error.log` for parse/load issues
2. Verify mod files match expected content
3. Compare with Git repository
4. Test clean install

## Future Considerations

| Feature | Feasibility | Notes |
|---------|-------------|-------|
| Mod settings UI | Requires Stellaris support | Not currently possible |
| Dynamic name lists | Requires scripting | Would need Lua mod |
| Per-species prefix pools | Requires engine support | Not in current API |
| Name list versioning | Requires Name Lists mod changes | Coordination needed |