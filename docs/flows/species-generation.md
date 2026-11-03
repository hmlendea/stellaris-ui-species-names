# Flow: Species Name Generation

## Overview

This flow describes how species names are generated at runtime in Stellaris, using the data provided by this mod and the Name Lists mod.

## Sequence Diagram

```
┌─────────────┐     ┌──────────────────┐     ┌─────────────────┐     ┌──────────────────┐
│   Player    │     │  Empire Creation │     │  Name Generator │     │  Name Lists Mod  │
│   Action    │     │     UI           │     │  (Engine)       │     │  (Data Source)   │
└──────┬──────┘     └────────┬─────────┘     └────────┬────────┘     └────────┬─────────┘
       │                     │                      │                   │
       │ 1. Select portrait  │                      │                   │
       │────────────────────►│                      │                   │
       │                     │                      │                   │
       │                     │ 2. Determine class   │                   │
       │                     │    from portrait     │                   │
       │                     │                      │                   │
       │                     │ 3. Query species     │                   │
       │                     │    definitions       │                   │
       │                     │    by class          │                   │
       │                     │─────────────────────►│                   │
       │                     │                      │                   │
       │                     │ 4. Return display    │                   │
       │                     │    names             │                   │
       │                     │◄─────────────────────│                   │
       │                     │                      │                   │
       │ 5. Show dropdown    │                      │                   │
       │◄────────────────────│                      │                   │
       │                     │                      │                   │
       │ 6. Player selects   │                      │                   │
       │    display name     │                      │                   │
       │────────────────────►│                      │                   │
       │                     │                      │                   │
       │                     │ 7. Get name_list     │                   │
       │                     │    reference         │                   │
       │                     │                      │                   │
       │                     │ 8. Resolve name_list │                   │
       │                     │    to name pool      │                   │
       │                     │─────────────────────►│                   │
       │                     │                      │                   │
       │                     │ 9. Return name pool  │                   │
       │                     │◄─────────────────────│                   │
       │                     │                      │                   │
       │                     │ 10. Random select    │                   │
       │                     │     from pool        │                   │
       │                     │                      │                   │
       │ 11. Empire created  │                      │                   │
       │    with generated   │                      │                   │
       │    name             │                      │                   │
       │◄────────────────────│                      │                   │
```

## Empire Creation Name Generation

### Step 1: Portrait Selection

Player chooses a species portrait in empire creation.

Each portrait has a fixed `species_class`:
- Mammalian portraits → `MAMMALIAN`
- Reptilian portraits → `REPTILIAN`
- etc.

### Step 2: Species Definition Query

Engine queries all registered species definitions where:
```txt
species_class = "SELECTED_CLASS"
```

Returns list of `{ species_key, name, name_list }`

### Step 3: Display Name Presentation

Engine shows `name` field values in dropdown.

Example for Mammalian:
- "Terran Federation" (vanilla)
- "Humanity" (vanilla)
- "Solari" (this mod, ui_species_extra_mammalian_01)
- "Novans" (this mod, ui_species_extra_mammalian_02)
- "Kobold Clan" (this mod, ui_species_media_dnd_kobold)

### Step 4: Player Selection

Player picks a display name (e.g., "Solari").

### Step 5: Name List Resolution

Engine takes the `name_list` reference from selected species:
```txt
name_list = "ui_extra_mam1"
```

Looks up in global name list registry (populated by Name Lists mod).

### Step 6: Name Pool Retrieval

Name Lists mod provides:
```txt
ui_extra_mam1 = {
    "Solari" "Novans" "Terrans" "Earthers" "Spacers"
    "Colonists" "Voidborn" "Starchildren" "Systemborn"
}
```

### Step 7: Random Selection

Engine randomly selects one name from pool using game RNG.

Result: Empire gets name "Voidborn" (for example).

## Genetic Modification Name Generation

### Trigger

Player uses genetic modification on a species (via gene clinics, events, etc.).

### Sequence

```
┌─────────────┐     ┌──────────────────┐     ┌─────────────────┐     ┌──────────────────┐
│   Player    │     │ Genetic          │     │  Name Generator │     │  Random Names    │
│   Action    │     │ Modification UI  │     │  (Engine)       │     │  (This Mod)      │
└──────┬──────┘     └────────┬─────────┘     └────────┬────────┘     └────────┬─────────┘
       │                     │                      │                   │
       │ 1. Modify species   │                      │                   │
       │────────────────────►│                      │                   │
       │                     │                      │                   │
       │                     │ 2. Get original      │                   │
       │                     │    species name      │                   │
       │                     │                      │                   │
       │                     │ 3. Select random     │                   │
       │                     │    prefix            │                   │
       │                     │─────────────────────►│                   │
       │                     │                      │                   │
       │                     │ 4. Return prefix     │                   │
       │                     │◄─────────────────────│                   │
       │                     │                      │                   │
       │                     │ 5. Select random     │                   │
       │                     │    postfix           │                   │
       │                     │─────────────────────►│                   │
       │                     │                      │                   │
       │                     │ 6. Return postfix    │                   │
       │                     │◄─────────────────────│                   │
       │                     │                      │                   │
       │                     │ 7. Combine:          │                   │
       │                     │    Prefix + Original │                   │
       │                     │    + Postfix         │                   │
       │                     │                      │                   │
       │ 8. New species name │                      │                   │
       │◄────────────────────│                      │                   │
```

### Name Construction

```
New Name = [Random Prefix] + " " + [Original Name] + " " + [Random Postfix]
```

### Example

| Original | Prefix (random) | Postfix (random) | Result |
|----------|-----------------|------------------|--------|
| Human | Augmented | Prime | Augmented Human Prime |
| Blorg | Evolved | Variant | Evolved Blorg Variant |
| Ketling | Modified | Strain | Modified Ketling Strain |

### Prefix/Postfix Source

From `common/random_names/base/ui-species-names.txt`:

```txt
prefix = {
    "Adapted" "Augmented" "Evolved" "Modified" "Mutated"
    "Refined" "Enhanced" "Altered" "Transformed" "Revised"
}

postfix = {
    "Prime" "Variant" "Strain" "Line" "Clade"
    "Form" "Type" "Model" "Version" "Iteration"
}
```

## RNG Determinism

### Per-Save Deterministic

- Each save game has a unique RNG seed
- Same save + same action = same generated name
- Different saves = different names

### Not Predictable

- Cannot predict which name from pool
- Cannot predict which prefix/postfix
- By design (gameplay variety)

## Edge Cases

### Empty Name Pool

If `name_list` resolves to empty pool:
- Engine falls back to species key or generic name
- Warning in log

### Missing Name List

If `name_list` reference not found:
- Species appears in dropdown but generates no names
- Warning in log: `name_list "xxx" not found`

### No Prefixes/Postfixes

If random names file not loaded:
- Engine uses vanilla prefixes/postfixes
- No error, just no custom parts

## Performance

| Operation | Complexity | Typical Time |
|-----------|------------|--------------|
| Species query by class | O(s) where s = species per class (~30) | <1ms |
| Name list lookup | O(1) hash | <1ms |
| Random selection | O(1) | <1ms |
| Prefix/postfix selection | O(1) each | <1ms |
| **Total per generation** | | **<5ms** |

## Debugging

### In-Game Console

```
debugtooltip
```
Hover over species name to see:
- Source mod
- Name list reference
- Generated name details

### Log Analysis

```bash
# Empire creation names
grep "empire.*name\|species.*name" error.log

# Genetic modification
grep "genetic.*modif\|prefix\|postfix" error.log
```

## Related Flows

- [Mod Loading](mod-loading.md) — How data gets into engine
- [Empire Creation Behaviour](behaviour/empire-creation.md) — User perspective