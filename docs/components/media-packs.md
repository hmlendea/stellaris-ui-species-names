# Component: Media Packs

## Overview

Media packs are themed species name collections based on existing fictional franchises. Each pack is a separate file containing species definitions that reference franchise-specific name lists from the Name Lists mod.

## File Structure

```
ui-species-names/common/species_names/
├── ui_species_media_distant-worlds.txt
├── ui_species_media_dnd.txt
├── ui_species_media_elder-scrolls.txt
├── ui_species_media_galciv.txt
└── ui_species_media_narivia.txt
```

## Pack Details

### Distant Worlds

| Property | Value |
|----------|-------|
| **File** | `ui_species_media_distant-worlds.txt` |
| **Franchise** | Distant Worlds (4X game series) |
| **Name List Prefix** | `ui_media_dw_` |
| **Species Count** | ~18 |
| **Classes Covered** | Mixed |

### Dungeons & Dragons

| Property | Value |
|----------|-------|
| **File** | `ui_species_media_dnd.txt` |
| **Franchise** | Dungeons & Dragons (tabletop RPG) |
| **Name List Prefix** | `ui_media_dnd_` |
| **Species Count** | ~18 |
| **Classes Covered** | Mixed |

### Elder Scrolls

| Property | Value |
|----------|-------|
| **File** | `ui_species_media_elder-scrolls.txt` |
| **Franchise** | The Elder Scrolls (RPG series) |
| **Name List Prefix** | `ui_media_es_` |
| **Species Count** | ~18 |
| **Classes Covered** | Mixed |

### Galactic Civilizations

| Property | Value |
|----------|-------|
| **File** | `ui_species_media_galciv.txt` |
| **Franchise** | Galactic Civilizations (4X game series) |
| **Name List Prefix** | `ui_media_gc_` |
| **Species Count** | ~18 |
| **Classes Covered** | Mixed |

### Narivia

| Property | Value |
|----------|-------|
| **File** | `ui_species_media_narivia.txt` |
| **Franchise** | Narivia (original sci-fi setting) |
| **Name List Prefix** | `ui_media_nar_` |
| **Species Count** | ~18 |
| **Classes Covered** | Mixed |

## Species Definition Pattern

Media pack species follow the same schema as base extra species:

```txt
ui_species_media_<franchise>_<identifier> = {
    name = "Display Name"
    name_list = "ui_media_<franchise>_<list>"
    species_class = "CLASS"
}
```

### Key Naming

```
ui_species_media_<franchise-abbrev>_<species-id>
```

Examples:
- `ui_species_media_dnd_kobold`
- `ui_species_media_es_argonian`
- `ui_species_media_dw_teekan`
- `ui_species_media_gc_drengin`
- `ui_species_media_nar_velari`

## Integration with Stellaris

### Portrait Association

Media pack species use **existing Stellaris portraits**. The `species_class` determines which portrait group they appear under.

| Species Class | Portrait Group |
|---------------|----------------|
| `REPTILIAN` | Reptilian portraits |
| `AVIAN` | Avian portraits |
| `MAMMALIAN` | Mammalian portraits |
| etc. | etc. |

### Empire Creation

1. Player selects portrait (e.g., Reptilian)
2. Media pack species with `species_class = "REPTILIAN"` appear in name dropdown
3. Names shown are from `name` field (franchise-themed display names)
4. Actual generated names come from Name Lists mod via `name_list` reference

## Name List References

Each media pack references name lists from Name Lists mod with franchise-specific prefixes:

| Pack | Name List Prefix | Example References |
|------|------------------|-------------------|
| Distant Worlds | `ui_media_dw_` | `ui_media_dw_teekan`, `ui_media_dw_dhayuut` |
| D&D | `ui_media_dnd_` | `ui_media_dnd_kobold`, `ui_media_dnd_drow` |
| Elder Scrolls | `ui_media_es_` | `ui_media_es_argonian`, `ui_media_es_khajiit` |
| GalCiv | `ui_media_gc_` | `ui_media_gc_drengin`, `ui_media_gc_altarian` |
| Narivia | `ui_media_nar_` | `ui_media_nar_velari`, `ui_media_nar_zyth` |

## Adding a New Media Pack

### Procedure

1. **Coordinate with Name Lists mod maintainer** — New name lists must be added there first
2. **Create new file**: `ui_species_media_<franchise>.txt`
3. **Add species definitions** following the pattern
4. **Use consistent abbreviation** for franchise (3-4 letters)
5. **Cover multiple species classes** for variety
6. **Update documentation**: INDEX.md, repository-overview.md, this file
7. **Test in-game** with relevant portraits

### Example: Adding "Warhammer 40k" Pack

```txt
# File: ui_species_media_warhammer40k.txt
# Media Pack: Warhammer 40,000
# Source: Games Workshop

ui_species_media_wh40k_ork = {
    name = "Ork"
    name_list = "ui_media_wh40k_ork"
    species_class = "MAMMALIAN"
}

ui_species_media_wh40k_eldar = {
    name = "Aeldari"
    name_list = "ui_media_wh40k_eldar"
    species_class = "HUMANOID"
}

ui_species_media_wh40k_tyranid = {
    name = "Tyranid"
    name_list = "ui_media_wh40k_tyranid"
    species_class = "ARTHROPOID"
}
```

## Legal Considerations

### Trademark/Copyright

- **Names only**: This mod provides species *display names* and references to name lists
- **No assets**: No images, models, or copyrighted text beyond names
- **Transformative**: Names used in different context (Stellaris species)
- **Attribution**: Franchise noted in file comments

### Risk Mitigation

| Risk | Mitigation |
|------|------------|
| Trademark claim | Use descriptive names, not logos/art |
| Copyright claim | Names are short phrases, borderline |
| DMCA takedown | Respond promptly, modify if needed |
| Platform policy | Follow Steam/Paradox/Nexus guidelines |

## Statistics

| Metric | Value |
|--------|-------|
| Media packs | 5 |
| Total media species | ~90 |
| Species per pack | ~18 |
| Name list references per pack | ~18 |
| Franchise abbreviations | dw, dnd, es, gc, nar |

## Future Packs

Potential franchises (require Name Lists mod support first):
- Warhammer 40,000
- Star Wars
- Star Trek
- Mass Effect
- Halo
- Custom community settings