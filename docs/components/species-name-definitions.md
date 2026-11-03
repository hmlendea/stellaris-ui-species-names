# Component: Species Name Definitions

## Overview

The species name definitions are the core content of this mod. They define which species names appear in empire creation and genetic modification.

## File Structure

```
ui-species-names/common/species_names/
├── ui_species_extra_arthropoid.txt
├── ui_species_extra_avian.txt
├── ui_species_extra_fungoid.txt
├── ui_species_extra_humanoid.txt
├── ui_species_extra_mammalian.txt
├── ui_species_extra_molluscoid.txt
├── ui_species_extra_plantoid.txt
├── ui_species_extra_reptilian.txt
├── ui_species_media_distant-worlds.txt
├── ui_species_media_dnd.txt
├── ui_species_media_elder-scrolls.txt
├── ui_species_media_galciv.txt
└── ui_species_media_narivia.txt
```

## Species Definition Schema

```txt
species_key = {
    name = "Display Name"
    name_list = "reference_to_name_list"
    species_class = "CLASS"
}
```

### Fields

| Field | Required | Type | Description |
|-------|----------|------|-------------|
| `species_key` | Yes | Identifier | Unique key, format: `ui_species_<category>_<id>` |
| `name` | Yes | String | Display name in empire creation dropdown |
| `name_list` | Yes | String | Reference to name list in Name Lists mod |
| `species_class` | Yes | Enum | One of 8 vanilla classes |

### Species Classes (Enum)

| Value | Description |
|-------|-------------|
| `ARTHROPOID` | Insectoid/arachnid species |
| `AVIAN` | Bird-like species |
| `FUNGOID` | Fungal/mushroom species |
| `HUMANOID` | Human-like species |
| `MAMMALIAN` | Mammal-like species |
| `MOLLUSCOID` | Mollusk/octopus-like species |
| `PLANTOID` | Plant-like species |
| `REPTILIAN` | Reptile-like species |

## File Categories

### Base Extra Packs (8 files)

One file per species class, ~10 species each:

| File | Class | Name List Prefix | Count |
|------|-------|------------------|-------|
| `ui_species_extra_arthropoid.txt` | ARTHROPOID | `ui_extra_art` | ~10 |
| `ui_species_extra_avian.txt` | AVIAN | `ui_extra_avi` | ~10 |
| `ui_species_extra_fungoid.txt` | FUNGOID | `ui_extra_fun` | ~10 |
| `ui_species_extra_humanoid.txt` | HUMANOID | `ui_extra_hum` | ~10 |
| `ui_species_extra_mammalian.txt` | MAMMALIAN | `ui_extra_mam` | ~10 |
| `ui_species_extra_molluscoid.txt` | MOLLUSCOID | `ui_extra_mol` | ~10 |
| `ui_species_extra_plantoid.txt` | PLANTOID | `ui_extra_pla` | ~10 |
| `ui_species_extra_reptilian.txt` | REPTILIAN | `ui_extra_rep` | ~10 |

### Media Packs (5 files)

One file per franchise, mixed classes:

| File | Franchise | Name List Prefix | Count |
|------|-----------|------------------|-------|
| `ui_species_media_distant-worlds.txt` | Distant Worlds | `ui_media_dw_` | ~18 |
| `ui_species_media_dnd.txt` | Dungeons & Dragons | `ui_media_dnd_` | ~18 |
| `ui_species_media_elder-scrolls.txt` | Elder Scrolls | `ui_media_es_` | ~18 |
| `ui_species_media_galciv.txt` | Galactic Civilizations | `ui_media_gc_` | ~18 |
| `ui_species_media_narivia.txt` | Narivia | `ui_media_nar_` | ~18 |

## Key Naming Convention

```
ui_species_<category>_<identifier>
```

| Category | Meaning |
|----------|---------|
| `extra` | Base extra packs (original content) |
| `media` | Media franchise packs |

Examples:
- `ui_species_extra_arthropoid_01`
- `ui_species_media_dnd_kobold`
- `ui_species_media_es_argonian`

## Integration with Stellaris

### Empire Creation

1. Player selects species portrait
2. Stellaris determines species class from portrait
3. Stellaris queries all species definitions with matching `species_class`
4. Names from `name` field shown in dropdown
5. On selection, Stellaris uses `name_list` to generate actual names

### Genetic Modification

1. Player genetically modifies species
2. Stellaris generates new name using:
   - Random prefix from `common/random_names/base/ui-species-names.txt`
   - Original species name
   - Random postfix from same file
3. Result: `Prefix OriginalName Postfix`

## Name List Resolution

### Flow

```
Species Definition (this mod)
       │
       ▼
name_list = "ui_extra_art1"
       │
       ▼
Name Lists Mod (dependency)
       │
       ▼
common/random_names/...
       │
       ▼
name_list ui_extra_art1 = { "Name1" "Name2" ... }
       │
       ▼
Stellaris resolves reference
       │
       ▼
Names available in game
```

### Validation

All `name_list` references must exist in Name Lists mod. Check with:

```bash
# Extract all references
grep -h "name_list" ui-species-names/common/species_names/*.txt | \
  sed 's/.*name_list = "\([^"]*\)".*/\1/' | sort -u

# Cross-reference with Name Lists mod files
```

## Adding New Species

### Procedure

1. Choose appropriate file (by class or media pack)
2. Add definition at end of file
3. Use next sequential identifier
4. Ensure `name_list` exists in Name Lists mod
5. Test in-game

### Example

```txt
# In ui_species_extra_arthropoid.txt
ui_species_extra_arthropoid_11 = {
    name = "Xenomorph Hive"
    name_list = "ui_extra_art11"
    species_class = "ARTHROPOID"
}
```

## Common Issues

| Issue | Cause | Fix |
|-------|-------|-----|
| Name not in dropdown | Wrong `species_class` | Match portrait class |
| Empty name list | `name_list` not found | Check Name Lists mod |
| Duplicate in dropdown | Duplicate `species_key` | Use unique key |
| Parse error | Syntax error (braces, quotes) | Fix syntax |

## Statistics

| Metric | Value |
|--------|-------|
| Total species definitions | ~250 |
| Base extra species | ~80 (10 per class × 8) |
| Media pack species | ~90 (18 per pack × 5) |
| Files | 13 |
| Name list references | ~250 (unique: ~170) |