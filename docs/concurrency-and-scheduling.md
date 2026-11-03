# Concurrency and Scheduling

## Overview

This mod has **no concurrency** and **no scheduling** — it is a static data mod loaded once at Stellaris startup. All processing is single-threaded and synchronous within the Stellaris engine.

## Concurrency Model

### No Application Concurrency

| Concurrency Aspect | Present? | Details |
|-------------------|----------|---------|
| Threads | No | No code execution |
| Async operations | No | No async I/O |
| Parallel processing | No | No computation |
| Locks/mutexes | No | No shared state |
| Race conditions | No | No concurrent access |
| Deadlocks | No | No locking |

### Stellaris Engine Concurrency (External)

The Stellaris engine may use concurrency internally, but our mod is unaffected:

| Engine Aspect | Impact on Mod |
|---------------|---------------|
| Mod loading | Single-threaded at startup |
| Parsing | Sequential file processing |
| Name generation | Single-threaded when called |
| Save/load | Engine-managed |

## Scheduling Model

### No Application Scheduling

| Scheduling Aspect | Present? | Details |
|------------------|----------|---------|
| Timers | No | No time-based operations |
| Cron jobs | No | No periodic tasks |
| Event loop | No | No event-driven code |
| Background jobs | No | No background processing |
| Retry logic | No | No transient failures |
| Rate limiting | No | No API calls |

### Stellaris Engine Scheduling (External)

| Engine Schedule | Mod Interaction |
|-----------------|-----------------|
| Game startup | Mod loaded once |
| Empire creation | Name lists queried on demand |
| Genetic modification | Prefix/postfix queried on demand |
| Save game | State serialised by engine |
| Load game | State deserialised by engine |

## Load Order

### Mod Load Order (Stellaris Launcher)

```
1. Core game files
2. DLC files
3. Mods (alphabetical by folder name, unless dependencies declared)
   ├── Universum Infinitum - Name Lists (dependency)
   └── Universum Infinitum: Species Names (this mod)
4. User settings
```

### Dependency Declaration

In `descriptor.mod`:
```txt
dependencies = {
    "ugc_2040234709"  # Name Lists mod Steam Workshop ID
}
```

This ensures Name Lists loads before Species Names.

## File Processing Order

Within our mod, Stellaris processes files in this order:

1. `descriptor.mod` (mod metadata)
2. `common/species_names/*.txt` (alphabetical)
   - `ui_species_extra_arthropoid.txt`
   - `ui_species_extra_avian.txt`
   - `ui_species_extra_fungoid.txt`
   - `ui_species_extra_humanoid.txt`
   - `ui_species_extra_mammalian.txt`
   - `ui_species_extra_molluscoid.txt`
   - `ui_species_extra_plantoid.txt`
   - `ui_species_extra_reptilian.txt`
   - `ui_species_media_distant-worlds.txt`
   - `ui_species_media_dnd.txt`
   - `ui_species_media_elder-scrolls.txt`
   - `ui_species_media_galciv.txt`
   - `ui_species_media_narivia.txt`
3. `common/random_names/base/ui-species-names.txt`

Order within `species_names/` doesn't matter — all species definitions are registered before use.

## Resource Contention

### No Resource Contention

| Resource | Contention? | Reason |
|----------|-------------|--------|
| CPU | No | No computation |
| Memory | No | No allocation |
| Disk I/O | No | Read-only at startup |
| Network | No | No network |
| GPU | No | No rendering |
| File handles | No | Engine manages |

## Performance Characteristics

### Time Complexity

| Operation | Complexity | Notes |
|-----------|------------|-------|
| Mod load | O(n) files | n = 14 files |
| Species registration | O(s) species | s ≈ 250 |
| Name list resolution | O(r) references | r ≈ 250 |
| Prefix/postfix load | O(p) parts | p ≈ 50 |
| Empire creation query | O(1) | Hash lookup |
| Genetic modification | O(1) | Random selection |

### Space Complexity

| Data | Size | Notes |
|------|------|-------|
| Mod files on disk | ~50 KB | Uncompressed |
| Engine memory | ~100 KB | Parsed structures |
| Save game impact | Minimal | Only chosen names stored |

## No Scaling Concerns

- Single-player or multiplayer: same mod load
- Mod size fixed: ~250 species, ~50 name parts
- No user-generated content
- No dynamic scaling

## Determinism

### Fully Deterministic

- Mod load: Same files → same result
- Name selection: Stellaris RNG (seeded per game)
- Genetic modification: Stellaris RNG
- No external inputs
- No time-dependent behaviour

### RNG Notes

Stellaris uses deterministic RNG per save game:
- Same save + same action = same generated name
- Different saves = different names (different seeds)
- Mod provides pools, engine picks randomly

## Thread Safety

### Not Applicable

- No shared mutable state
- No concurrent access
- No thread-local storage
- No atomic operations

## Future Considerations

| Feature | Concurrency Impact | Feasibility |
|---------|-------------------|-------------|
| Lua scripting | Would introduce async/event model | Requires rewrite |
| Dynamic reloading | Would need thread-safe state | Not supported by Stellaris |
| Background validation | Could add build-time concurrency | CI/CD only |
| Parallel file parsing | Engine-level optimisation | Not mod-controllable |