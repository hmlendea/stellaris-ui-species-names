# Behaviour: Species Name Selection

## Overview

This document describes the user-facing behaviour of species name selection in Stellaris when this mod is installed.

## Empire Creation Flow

### 1. Portrait Selection

**User Action**: Click on a species portrait in empire creation screen.

**System Response**:
- Engine determines `species_class` from portrait
- Queries all species definitions with matching class
- Includes vanilla + this mod's definitions

### 2. Name Dropdown Population

**System Response**: Populate name dropdown with `name` field from all matching species definitions.

**Display Order**:
1. Vanilla species names (hardcoded order)
2. This mod's species names (alphabetical by `species_key`)
3. Other mods' species names (load order)

**Example for Mammalian Portrait**:
```
▼ Human (Vanilla)
▼ Humanity (Vanilla)
▼ Solari (ui_species_extra_mammalian_01)
▼ Novans (ui_species_extra_mammalian_02)
▼ Terrans (ui_species_extra_mammalian_03)
▼ Kobold Clan (ui_species_media_dnd_kobold)
▼ ... (more)
```

### 3. User Selection

**User Action**: Click a name from dropdown.

**System Response**:
- Store selected `species_key` and `name_list` reference
- No immediate name generation

### 4. Empire Finalisation

**User Action**: Complete empire creation (name empire, choose traits, etc.) and start game.

**System Response**:
- Engine generates actual species name using `name_list`
- Randomly selects from name pool in Name Lists mod
- Empire created with generated name

## Name Generation Behaviour

### Randomness

- Each empire creation = new random selection
- Same display name → different actual names possible
- Deterministic per save game seed

### Name Pool Source

| Display Name Selected | Name List Used | Pool Source |
|----------------------|----------------|-------------|
| Vanilla names | Vanilla lists | Stellaris core |
| `ui_species_extra_*` | `ui_extra_*` | Name Lists mod |
| `ui_species_media_*` | `ui_media_*` | Name Lists mod |

### Fallback Behaviour

If `name_list` not found:
- Engine may use display name as actual name
- Or generate generic name
- Warning in log

## Genetic Modification Behaviour

### Trigger

Player opens genetic modification interface (gene clinics, events, traditions).

### Name Generation

**System Response**: Automatically generates new species name:
```
[Random Prefix] [Original Species Name] [Random Postfix]
```

### Prefix/Postfix Source

From `common/random_names/base/ui-species-names.txt`:
- 10 prefixes (Adapted, Augmented, Evolved, etc.)
- 10 postfixes (Prime, Variant, Strain, etc.)
- 100 possible combinations

### User Control

**None** — Name generation is automatic. Player cannot:
- Choose specific prefix/postfix
- Opt out of name change
- Preview before confirming

### Original Name Preservation

Original species name always appears in middle:
- "Human" → "Augmented Human Prime"
- "Blorg" → "Evolved Blorg Variant"
- Never replaces original entirely

## Multiplayer Behaviour

### Synchronisation

- Host's mod version used
- All clients must have same mod version
- Name generation uses host's RNG seed
- Clients receive generated names from host

### Desync Risks

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| Different mod versions | Medium | Version check on join |
| Different Name Lists versions | Medium | Same version required |
| RNG divergence | Low | Deterministic per seed |

## Save/Load Behaviour

### Save Game

- Generated empire names stored in save
- Species definitions not stored (reloaded on load)
- Name list references not stored (re-resolved on load)

### Load Game

- Mod files reloaded
- Name lists re-resolved
- Empire names preserved
- Future genetic modifications use current mod data

## Edge Cases

### Mod Removed After Empire Creation

- Empire keeps generated name
- Species definition no longer available for new empires
- Genetic modification may use vanilla prefixes/postfixes

### Name Lists Mod Updated

- New name lists available for new empires
- Existing empires unaffected
- Genetic modification uses current prefixes/postfixes

### Duplicate Display Names

If two species definitions have same `name`:
- Both appear in dropdown
- Selection ambiguous (first match used)
- Avoid by using unique display names

## Accessibility

### Text Display

- All names plain text
- No special formatting
- Screen reader compatible

### Colour Blind

- No colour-dependent information
- Standard UI colours only

## Performance

### Dropdown Population

- ~30 names per class (vanilla + this mod)
- Negligible UI impact
- No lazy loading needed

### Name Generation

- Single random selection
- <1ms
- No perceptible delay

## Testing Scenarios

| Scenario | Expected Behaviour |
|----------|-------------------|
| Fresh install, new game | All mod names appear in dropdowns |
| Mod disabled, load save | Empire names preserved, no mod names in new games |
| Name Lists missing | Mod names in dropdown, but empty actual names |
| Genetic modification | New name with prefix/postfix |
| Multiplayer, same versions | Synchronised name generation |
| Multiplayer, version mismatch | Desync or join failure |