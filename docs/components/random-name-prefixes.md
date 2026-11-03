# Component: Random Name Prefixes and Postfixes

## Overview

This component provides the prefixes and postfixes applied to species names during genetic modification in-game.

## File Location

```
ui-species-names/common/random_names/base/ui-species-names.txt
```

## File Structure

```txt
# Prefixes for genetically modified species
prefix = {
    "Adapted"
    "Augmented"
    "Evolved"
    "Modified"
    "Mutated"
    "Refined"
    "Enhanced"
    "Altered"
    "Transformed"
    "Revised"
}

# Postfixes for genetically modified species
postfix = {
    "Prime"
    "Variant"
    "Strain"
    "Line"
    "Clade"
    "Form"
    "Type"
    "Model"
    "Version"
    "Iteration"
}
```

## Schema

### Prefix Block

```txt
prefix = {
    "Prefix 1"
    "Prefix 2"
    ...
}
```

- Array of quoted strings
- Applied before original species name
- Randomly selected by Stellaris

### Postfix Block

```txt
postfix = {
    "Postfix 1"
    "Postfix 2"
    ...
}
```

- Array of quoted strings
- Applied after original species name
- Randomly selected by Stellaris

## Integration with Stellaris

### Genetic Modification Flow

```
Player initiates genetic modification
         │
         ▼
Stellaris generates new species name
         │
         ├──► Selects random prefix from prefix block
         │
         ├──► Uses original species name
         │
         └──► Selects random postfix from postfix block
         │
         ▼
Result: "Prefix OriginalName Postfix"
```

### Example Outputs

| Original | Prefix | Postfix | Result |
|----------|--------|---------|--------|
| Human | Augmented | Prime | Augmented Human Prime |
| Blorg | Evolved | Variant | Evolved Blorg Variant |
| Ketling | Modified | Strain | Modified Ketling Strain |

## Design Principles

### Thematic Consistency

- **Prefixes**: Suggest improvement, change, adaptation
- **Postfixes**: Suggest classification, versioning, lineage
- **Tone**: Scientific, biological, evolutionary

### Balance

- Equal prefix/postfix count (10 each = 100 combinations)
- No duplicates within blocks
- No overlap with vanilla prefixes/postfixes
- Sufficient variety for repeated modifications

### Extensibility

- Easy to add more entries
- No code changes needed
- Stellaris handles random selection

## Adding New Prefixes/Postfixes

### Procedure

1. Edit `ui-species-names/common/random_names/base/ui-species-names.txt`
2. Add new quoted string to appropriate block
3. Maintain alphabetical or thematic grouping
4. Test in-game: genetically modify species, verify new parts appear

### Example

```txt
prefix = {
    "Adapted"
    "Augmented"
    "Bio-Engineered"    # New entry
    "Evolved"
    ...
}

postfix = {
    "Prime"
    "Prototype"         # New entry
    "Variant"
    ...
}
```

## Validation

### Syntax Checks

```bash
# Check file structure
cat ui-species-names/common/random_names/base/ui-species-names.txt

# Verify prefix block
grep -A 20 "prefix = {" ui-species-names/common/random_names/base/ui-species-names.txt

# Verify postfix block
grep -A 20 "postfix = {" ui-species-names/common/random_names/base/ui-species-names.txt

# Check for duplicates
grep -o '"[^"]*"' ui-species-names/common/random_names/base/ui-species-names.txt | sort | uniq -d
```

### In-Game Test

1. Start game with mod enabled
2. Play until genetic modification available
3. Modify a species
4. Verify new prefix/postfix appears in generated name
5. Repeat multiple times to see variety

## Common Issues

| Issue | Cause | Fix |
|-------|-------|-----|
| Prefix/postfix not applied | File not loaded | Check file path, encoding |
| Vanilla parts used instead | Load order | Ensure mod loads after vanilla |
| Duplicate parts | Duplicate entries | Remove duplicates |
| Parse error | Missing braces/quotes | Fix syntax |

## Relationship to Name Lists Mod

**Independent** — This component does not reference Name Lists mod. It provides modification parts directly.

However, the **base species names** (before modification) come from Name Lists mod via species definitions.

## Statistics

| Metric | Value |
|--------|-------|
| Prefix count | 10 |
| Postfix count | 10 |
| Total combinations | 100 |
| File size | ~1 KB |
| Lines | ~25 |