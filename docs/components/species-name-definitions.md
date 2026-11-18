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

Each file declares one or more class blocks. Within a block, every species is a single-line entry:

```txt
ART = {
    ### Extra Arthropoids 1 ###
    bamuth  = { name = Bamuth   plural = Bamuthi    home_planet = Bamuthima    home_system = Bamuth    name_list = "ui_extra_art1" }
}
```

### Fields

| Field | Required | Type | Description |
|-------|----------|------|-------------|
| Class block (`ART`, `AVI`, `FUN`, `HUM`, `MAM`, `MOL`, `PLANT`, `REP`, `MACHINE`) | Yes | Block | Selects the vanilla species class the entries belong to |
| Species key (`bamuth`) | Yes | Identifier | Unique key across the mod, lowercase alphanumeric |
| `name` | Yes | String | Display name used for the species |
| `plural` | Yes | String | Plural form of the species name |
| `home_planet` | Yes | String | Default home planet name |
| `home_system` | Yes | String | Default home system name |
| `name_list` | Yes | String | Reference to a name list supplied by the Name Lists mod |

### Species Classes (Enum)

| Block | Class | Description |
|-------|-------|-------------|
| `ART` | Arthropoid | Insectoid/arachnid species |
| `AVI` | Avian | Bird-like species |
| `FUN` | Fungoid | Fungal/mushroom species |
| `HUM` | Humanoid | Human-like species |
| `MAM` | Mammalian | Mammal-like species |
| `MOL` | Molluscoid | Mollusk/octopus-like species |
| `PLANT` | Plantoid | Plant-like species |
| `REP` | Reptilian | Reptile-like species |
| `MACHINE` | Machine | Robotic species |

## File Categories

### Base Extra Packs (8 files)

One file per species class, 16 to 160 species each:

| File | Class | Name Lists Used | Count |
|------|-------|------------------|-------|
| `ui_species_extra_arthropoid.txt` | ARTHROPOID | `ui_extra_art1` | 16 |
| `ui_species_extra_avian.txt` | AVIAN | `ui_extra_avi1`, `ui_extra_avi2` | 32 |
| `ui_species_extra_fungoid.txt` | FUNGOID | `ui_extra_fun1` | 16 |
| `ui_species_extra_humanoid.txt` | HUMANOID | `ui_extra_hum1` to `ui_extra_hum4`, `ui_demon`, `ui_dwarven`, `ui_elven`, `ui_goblin`, `ui_orc`, `ui_protoss` | 160 |
| `ui_species_extra_mammalian.txt` | MAMMALIAN | `ui_extra_mam1` to `ui_extra_mam3` | 50 |
| `ui_species_extra_molluscoid.txt` | MOLLUSCOID | `ui_extra_mol1` | 16 |
| `ui_species_extra_plantoid.txt` | PLANTOID | `ui_extra_pla1`, `ui_extra_pla2` | 32 |
| `ui_species_extra_reptilian.txt` | REPTILIAN | `ui_extra_rep1` to `ui_extra_rep4`, `ui_lizard` | 80 |

### Media Packs (5 files)

One file per franchise, mixed classes:

| File | Franchise | Name Lists Used | Count |
|------|-----------|------------------|-------|
| `ui_species_media_distant-worlds.txt` | Distant Worlds | `ui_extra_art1`, `ui_extra_hum1`, `ui_extra_mam1`, `ui_extra_mam2`, `ui_extra_rep1` to `ui_extra_rep3` | 27 |
| `ui_species_media_dnd.txt` | Dungeons & Dragons | `ui_dnd_kobold` | 31 |
| `ui_species_media_elder-scrolls.txt` | Elder Scrolls | `ui_elderscrolls_` | 87 |
| `ui_species_media_galciv.txt` | Galactic Civilizations | `ui_galciv_yor` | 17 |
| `ui_species_media_narivia.txt` | Narivia | `ui_narivia_rodah` | 17 |

## File Naming Convention

```
ui_species_<category>_<subject>.txt
```

| Category | Meaning |
|----------|---------|
| `extra` | Base extra packs (original content) |
| `media` | Media franchise packs |

Examples:
- `ui_species_extra_arthropoid.txt`
- `ui_species_media_dnd.txt`
- `ui_species_media_elder-scrolls.txt`

## Integration with Stellaris

### Empire Creation

1. Player selects species portrait
2. Stellaris determines the species class from the portrait
3. Stellaris queries the class block (`ART`, `AVI`, `FUN`, `HUM`, `MAM`, `MOL`, `PLANT`, `REP`, `MACHINE`) for available entries
4. Values from the `name` field are offered as the naming choice
5. On selection, Stellaris uses `name_list` to generate the population names

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
ART = {
    ### Extra Arthropoids 1 ###
    qorvax  = { name = Qorvax   plural = Qorvaxi    home_planet = Qorvazza      home_system = Qorv      name_list = "ui_extra_art1" }
}
```

## Common Issues

| Issue | Cause | Fix |
|-------|-------|-----|
| Name not in dropdown | Entry in the wrong class block | Match the block to the portrait class |
| Empty name list | `name_list` not found | Check Name Lists mod |
| Duplicate in dropdown | Duplicate species key | Use a unique key |
| Parse error | Syntax error (braces, quotes) | Fix syntax |

## Statistics

| Metric | Value |
|--------|-------|
| Total species definitions | 581 |
| Base extra species | 421 (8 base-class files) |
| Media pack species | 160 (5 media-pack files) |
| Files | 13 |
| Unique name list references | 34 |