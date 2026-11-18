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
| **Name Lists Used** | `ui_extra_art1`, `ui_extra_hum1`, `ui_extra_mam1`, `ui_extra_mam2`, `ui_extra_rep1`, `ui_extra_rep2`, `ui_extra_rep3` |
| **Species Count** | 27 |
| **Classes Covered** | Mixed |

### Dungeons & Dragons

| Property | Value |
|----------|-------|
| **File** | `ui_species_media_dnd.txt` |
| **Franchise** | Dungeons & Dragons (tabletop RPG) |
| **Name Lists Used** | `ui_dnd_kobold` |
| **Species Count** | 31 |
| **Classes Covered** | Mixed |

### Elder Scrolls

| Property | Value |
|----------|-------|
| **File** | `ui_species_media_elder-scrolls.txt` |
| **Franchise** | The Elder Scrolls (RPG series) |
| **Name Lists Used** | `ui_elderscrolls_altmer`, `ui_elderscrolls_dremora`, `ui_elderscrolls_khajiit`, `ui_elderscrolls_orc`, `ui_elderscrolls_spriggan`, `ui_extra_elderscrolls_argonian` |
| **Species Count** | 87 |
| **Classes Covered** | Mixed |

### Galactic Civilizations

| Property | Value |
|----------|-------|
| **File** | `ui_species_media_galciv.txt` |
| **Franchise** | Galactic Civilizations (4X game series) |
| **Name Lists Used** | `ui_galciv_yor` |
| **Species Count** | 17 |
| **Classes Covered** | Mixed |

### Narivia

| Property | Value |
|----------|-------|
| **File** | `ui_species_media_narivia.txt` |
| **Franchise** | Narivia (original sci-fi setting) |
| **Name Lists Used** | `ui_narivia_rodah` |
| **Species Count** | 17 |
| **Classes Covered** | Mixed |

## Species Definition Pattern

Media pack species follow the same schema as base extra species:

```txt
REP = {
    ### TES - Argonian ###
    amuseixth   = { name = "Amuseixth"      plural = "Amuseixthi"   home_planet = "Amusei"  home_system = "Amus"    name_list = "ui_extra_elderscrolls_argonian" }
}
```

### Key Naming

Species keys are lowercase identifiers that are unique across the whole mod; the enclosing class block decides the species class.

Examples:
- `ahsu` in `REP`, `name_list = "ui_dnd_kobold"`
- `amuseixth` in `REP`, `name_list = "ui_extra_elderscrolls_argonian"`
- `teekan` in `MAM`, `name_list = "ui_extra_mam2"`
- `zen` in `MACHINE`, `name_list = "ui_galciv_yor"`
- `rodah` in `HUM`, `name_list = "ui_narivia_rodah"`

## Integration with Stellaris

### Portrait Association

Media pack species use **existing Stellaris portraits**. The enclosing class block determines which portrait group they appear under.

| Class block | Portrait group |
|-------------|----------------|
| `REP` | Reptilian portraits |
| `AVI` | Avian portraits |
| `MAM` | Mammalian portraits |
| others | Matching class group |

### Empire Creation

1. Player selects portrait (e.g., Reptilian)
2. Media pack entries inside the `REP` block appear in the name dropdown
3. Names shown are from `name` field (franchise-themed display names)
4. Actual generated names come from Name Lists mod via `name_list` reference

## Name List References

Each media pack reuses name lists supplied by the Name Lists mod:

| Pack | Name Lists Referenced |
|------|-----------------------|
| Distant Worlds | `ui_extra_art1`, `ui_extra_hum1`, `ui_extra_mam1`, `ui_extra_mam2`, `ui_extra_rep1`, `ui_extra_rep2`, `ui_extra_rep3` |
| D&D | `ui_dnd_kobold` |
| Elder Scrolls | `ui_elderscrolls_altmer`, `ui_elderscrolls_dremora`, `ui_elderscrolls_khajiit`, `ui_elderscrolls_orc`, `ui_elderscrolls_spriggan`, `ui_extra_elderscrolls_argonian` |
| GalCiv | `ui_galciv_yor` |
| Narivia | `ui_narivia_rodah` |

## Adding a New Media Pack

### Procedure

1. **Coordinate with Name Lists mod maintainer** — New name lists must be added there first
2. **Create new file**: `ui_species_media_<franchise>.txt`
3. **Add a class block and entries** following the single-line pattern used by existing files
4. **Use a unique lowercase key** for every species
5. **Cover multiple species classes** for variety
6. **Update documentation**: `docs/INDEX.md`, `docs/repository-overview.md`, this file
7. **Test in-game** with relevant portraits

### Example: Adding a Warhammer 40,000 Pack

```txt
# Media Pack: Warhammer 40,000
# Source: Games Workshop

MAM = {
    ### Warhammer 40,000 - Ork ###
    ork     = { name = Ork      plural = Orks     home_planet = Orkworld    home_system = Ork     name_list = "ui_extra_mam1" }
}

HUM = {
    ### Warhammer 40,000 - Aeldari ###
    aeldari = { name = Aeldari  plural = Aeldari  home_planet = Craftworld  home_system = Aeldar  name_list = "ui_extra_hum1" }
}

ART = {
    ### Warhammer 40,000 - Tyranid ###
    tyranid = { name = Tyranid  plural = Tyranids home_planet = Tyran     home_system = Tyra     name_list = "ui_extra_art1" }
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
| Total media species | 160 |
| Species per pack | 17 to 87 |
| Unique name lists per pack | 1 to 6 |
| Name list families | `ui_extra_*`, `ui_dnd_kobold`, `ui_elderscrolls_*`, `ui_galciv_yor`, `ui_narivia_rodah` |

## Future Packs

Potential franchises (require Name Lists mod support first):
- Warhammer 40,000
- Star Wars
- Star Trek
- Mass Effect
- Halo
- Custom community settings