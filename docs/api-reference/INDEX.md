# API Reference

## Overview

This mod is a **static data mod** with **no programmable API**. It provides declarative configuration files that are parsed by the Stellaris engine at runtime.

## No Public API

| API Type | Present? | Details |
|----------|----------|---------|
| REST API | No | No network interface |
| GraphQL | No | No query interface |
| gRPC | No | No RPC interface |
| Library/SDK | No | No code library |
| CLI | No | No command-line interface |
| Scripting API | No | No Lua/scripting exposure |
| Event hooks | No | No event system |
| Callbacks | No | No callback mechanism |

## Data Interface (Declarative)

The only "interface" is the **file format** that Stellaris parses:

### Species Definition Format

```txt
species_key = {
    name = "Display Name"
    name_list = "reference"
    species_class = "CLASS"
}
```

### Random Names Format

```txt
prefix = {
    "Prefix 1"
    "Prefix 2"
}

postfix = {
    "Postfix 1"
    "Postfix 2"
}
```

### Descriptor Format

```txt
name = "Mod Name"
version = "1.7.4"
supported_version = "4.5.*"
tags = { "Species" "Name Lists" }
path = "ui-species-names"
dependencies = { "ugc_2040234709" }
```

## Engine Integration Points

Stellaris engine integrates with this mod at these internal points:

| Integration Point | Engine System | Data Consumed |
|-------------------|---------------|---------------|
| Mod loading | Mod loader | Descriptor files |
| Species names | Empire creation | `common/species_names/*.txt` |
| Genetic modification | Species modification | `common/random_names/base/ui-species-names.txt` |
| Name resolution | Name list system | `name_list` references |

## For Modders

### Extending This Mod

To add species names that work with this mod:

1. Create species definitions in your mod's `common/species_names/`
2. Reference name lists from Name Lists mod (or provide your own)
3. Ensure load order after Name Lists mod

### Referencing This Mod's Data

**Not possible** — This mod does not expose data for other mods to reference programmatically.

Other mods can:
- Add their own species definitions (additive)
- Provide their own name lists
- Override prefixes/postfixes (last loaded wins)

## For Tooling

### Parsing Mod Files

If building tools to parse this mod's files:

**Format**: Stellaris custom declarative syntax (key-value with nested blocks)

**Parser Requirements**:
- Handle `{ }` nesting
- Handle quoted strings
- Handle arrays (implicit via repetition)
- UTF-8 encoding
- LF line endings

**Example Parser Output** (JSON representation):

```json
{
  "species_definitions": [
    {
      "key": "ui_species_extra_mammalian_01",
      "name": "Solari",
      "name_list": "ui_extra_mam1",
      "species_class": "MAMMALIAN"
    }
  ],
  "prefixes": ["Adapted", "Augmented", "Evolved", ...],
  "postfixes": ["Prime", "Variant", "Strain", ...]
}
```

## Version Compatibility

| Mod Version | Stellaris Version | Format Changes |
|-------------|-------------------|----------------|
| 1.x | 4.5.* | Current format |
| Future | 4.6+ | May change if Stellaris changes format |

## Related Documentation

- [Data Model](../data-model.md) — Domain entities
- [Configuration](../configuration.md) — Configuration schema
- [Components: Species Name Definitions](../components/species-name-definitions.md)
- [Components: Random Name Prefixes](../components/random-name-prefixes.md)
- [Components: Media Packs](../components/media-packs.md)