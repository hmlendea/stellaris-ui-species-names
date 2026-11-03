# Behaviour: Empire Creation

## Overview

This document describes the complete empire creation experience when the Universum Infinitum: Species Names mod is installed.

## Empire Creation Screen Flow

### 1. Species Tab

**Entry Point**: New Game → Empire Creation → Species tab

**Mod Impact**: Species name dropdown enhanced with ~250 additional names

#### Portrait Selection

- 8 base species classes + 5 portrait packs (if DLC owned)
- Each portrait maps to a `species_class`
- Mod adds names for all 8 base classes
- Media packs add names across multiple classes

#### Name Dropdown

**Before Mod** (Vanilla only):
```
▼ Human
▼ Humanity
▼ [class-specific vanilla names]
```

**After Mod** (Vanilla + This Mod):
```
▼ Human (Vanilla)
▼ Humanity (Vanilla)
▼ Solari (ui_species_extra_mammalian_01)
▼ Novans (ui_species_extra_mammalian_02)
▼ Terrans (ui_species_extra_mammalian_03)
▼ Earthers (ui_species_extra_mammalian_04)
▼ Spacers (ui_species_extra_mammalian_05)
▼ Colonists (ui_species_extra_mammalian_06)
▼ Voidborn (ui_species_extra_mammalian_07)
▼ Starchildren (ui_species_extra_mammalian_08)
▼ Systemborn (ui_species_extra_mammalian_09)
▼ Orbital (ui_species_extra_mammalian_10)
▼ Kobold Clan (ui_species_media_dnd_kobold)
▼ Drow Matriarchy (ui_species_media_dnd_drow)
▼ ... (more media pack names)
▼ [other mods' names]
```

#### Name Categories by Class

| Class | Base Extra Count | Media Pack Examples |
|-------|------------------|---------------------|
| ARTHROPOID | 10 | Distant Worlds Teekan, D&D Thri-kreen |
| AVIAN | 10 | Elder Scrolls Kenku, GalCiv Yor |
| FUNGOID | 10 | Narivia Myconid, D&D Myconid |
| HUMANOID | 10 | Elder Scrolls Nord, D&D Human |
| MAMMALIAN | 10 | D&D Kobold, GalCiv Terran |
| MOLLUSCOID | 10 | Distant Worlds Dhayut, Narivia Cephalopod |
| PLANTOID | 10 | Elder Scrolls Spriggan, D&D Vegepygmy |
| REPTILIAN | 10 | D&D Lizardfolk, Elder Scrolls Argonian |

### 2. Name Generation on Empire Creation

**Trigger**: Player clicks "Start Game" after completing empire setup

**Process**:
1. Engine takes selected species `name_list` reference
2. Resolves to name pool in Name Lists mod
3. Randomly selects one name from pool
4. Assigns as empire/species name

**Result Variability**:
- Same display name → different actual names each game
- Deterministic per save seed
- Pool sizes vary (typically 10-20 names per list)

### 3. Trait/Civic/Origin Selection

**Mod Impact**: None — this mod only affects species names

### 4. Empire Name / Ruler Name

**Mod Impact**: None — separate from species names

## User Experience Details

### Discoverability

- Names appear automatically in dropdown
- No special UI indicators for mod names
- Alphabetical mixing with vanilla names
- Media pack names have thematic display names

### Selection Feedback

- Hover: Shows display name only
- Select: No immediate feedback
- Generated name revealed on game start

### Search/Filter

- No search in dropdown (vanilla limitation)
- Scroll through list
- ~30-40 names per class typical

## Media Pack Experience

### Thematic Grouping

Media pack names have franchise-themed display names:

| Pack | Display Name Style | Example |
|------|-------------------|---------|
| Distant Worlds | Species names from game | "Teekan Hive", "Dhayut Syndicate" |
| D&D | Race/faction names | "Kobold Clan", "Drow Matriarchy" |
| Elder Scrolls | Race names | "Argonian Tribe", "Khajiit Caravan" |
| GalCiv | Civilisation names | "Drengin Empire", "Altarian Republic" |
| Narivia | Original species names | "Velari Collective", "Zyth Swarm" |

### Cross-Class Availability

Media packs span multiple classes:
- D&D: Kobold (Mammalian), Lizardfolk (Reptilian), Drow (Humanoid), etc.
- Elder Scrolls: Argonian (Reptilian), Khajiit (Mammalian), etc.
- Player discovers by trying different portraits

## Genetic Modification in Empire Context

### Availability

- Requires Gene Clinics technology
- Available mid-game
- Applies to any species in empire

### Name Change Behaviour

```
Before: "Human"
After:  "Augmented Human Prime"
```

- Automatic on modification completion
- No player choice in prefix/postfix
- Original name preserved in middle
- New name used for all pops of that species

### Multiple Modifications

Each modification = new random prefix/postfix:
1. Human → Augmented Human Prime
2. → Evolved Augmented Human Prime Variant
3. → Modified Evolved Augmented Human Prime Variant Strain

(Stacking behaviour depends on Stellaris version)

## Multiplayer Considerations

### Host Authority

- Host's mod data used for name generation
- Clients receive generated names
- All players see same names

### Synchronisation

- Empire creation: Host generates, syncs to clients
- Genetic modification: Host generates, syncs to clients
- No desync from name generation (deterministic RNG)

### Version Mismatch

- Different mod versions → potential desync
- Different Name Lists versions → different name pools
- Launcher warns on version mismatch

## Accessibility

### Visual

- Standard dropdown UI
- No custom colours/icons
- High contrast compatible

### Screen Readers

- Names read as plain text
- Dropdown navigation standard
- No special ARIA needed (vanilla UI)

### Motor

- Standard click/scroll interaction
- No timed interactions
- Keyboard navigation supported

## Performance

### Dropdown Rendering

- ~30-40 items per class
- Instant population
- No measurable lag

### Name Generation

- Single RNG call
- <1ms
- No loading indicator needed

## Testing Checklist

| Test Case | Expected |
|-----------|----------|
| Each portrait class shows mod names | ✓ |
| Media pack names appear for correct classes | ✓ |
| Generated names come from correct pools | ✓ |
| Genetic modification adds prefix/postfix | ✓ |
| Multiplayer sync works | ✓ |
| Save/load preserves names | ✓ |
| Mod disable removes names from dropdown | ✓ |
| Mod re-enable restores names | ✓ |