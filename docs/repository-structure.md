# Repository Structure

## Source Tree Layout

```
stellaris-ui-species-names/
├── .github/
│   └── workflows/              # GitHub Actions workflows (if any)
├── ui-species-names/           # Mod root directory (loaded by Stellaris)
│   ├── descriptor.mod          # Mod metadata for Stellaris launcher
│   └── common/                 # Game data directory
│       ├── random_names/
│       │   └── base/
│       │       └── ui-species-names.txt    # Species modification prefixes/postfixes
│       └── species_names/                  # Species name list definitions
│           ├── ui_species_extra_arthropoid.txt
│           ├── ui_species_extra_avian.txt
│           ├── ui_species_extra_fungoid.txt
│           ├── ui_species_extra_humanoid.txt
│           ├── ui_species_extra_mammalian.txt
│           ├── ui_species_extra_molluscoid.txt
│           ├── ui_species_extra_plantoid.txt
│           ├── ui_species_extra_reptilian.txt
│           ├── ui_species_media_distant-worlds.txt
│           ├── ui_species_media_dnd.txt
│           ├── ui_species_media_elder-scrolls.txt
│           ├── ui_species_media_galciv.txt
│           └── ui_species_media_narivia.txt
├── ui-species-names.mod        # Mod metadata for distribution platforms
├── README.md                   # Project overview and installation
├── CONTRIBUTING.md             # Contribution guidelines
├── CODE_OF_CONDUCT.md          # Code of conduct
├── SECURITY.md                 # Security policy
├── PRIVACY.md                  # Privacy policy
├── LICENSE                     # GNU GPL v3.0
├── docs/                       # Generated documentation
│   ├── INDEX.md
│   ├── repository-overview.md
│   ├── repository-structure.md
│   ├── architecture.md
│   ├── data-model.md
│   ├── configuration.md
│   ├── build-and-deployment.md
│   ├── testing.md
│   ├── change-guide.md
│   ├── troubleshooting.md
│   ├── faq.md
│   ├── dependencies.md
│   ├── design-decisions.md
│   ├── documentation-maintenance.md
│   ├── error-handling.md
│   ├── invariants.md
│   ├── integrations.md
│   ├── logging.md
│   ├── quick-start.md
│   ├── security.md
│   ├── state-and-persistence.md
│   ├── concurrency-and-scheduling.md
│   ├── api-reference/
│   │   └── INDEX.md
│   ├── behaviour/
│   │   ├── species-name-selection.md
│   │   └── empire-creation.md
│   ├── components/
│   │   ├── species-name-definitions.md
│   │   ├── random-name-prefixes.md
│   │   └── media-packs.md
│   └── flows/
│       ├── mod-loading.md
│       └── species-generation.md
```

## Module Organisation

### Mod Root (`ui-species-names/`)

This is the directory that Stellaris reads when the mod is loaded. It must be placed in the Stellaris mod directory with this exact structure.

| File/Directory | Purpose |
|----------------|---------|
| `descriptor.mod` | Mod metadata for Stellaris launcher (version, name, supported_version, tags, path) |
| `common/` | Standard Stellaris data directory for game definitions |

### Species Name Lists (`ui-species-names/common/species_names/`)

Contains 13 files defining species name lists:

| File | Category | Species Class / Theme |
|------|----------|----------------------|
| `ui_species_extra_arthropoid.txt` | Base class | Arthropoid (insectoid) |
| `ui_species_extra_avian.txt` | Base class | Avian (bird-like) |
| `ui_species_extra_fungoid.txt` | Base class | Fungoid (fungus-like) |
| `ui_species_extra_humanoid.txt` | Base class | Humanoid (human-like) |
| `ui_species_extra_mammalian.txt` | Base class | Mammalian (mammal-like) |
| `ui_species_extra_molluscoid.txt` | Base class | Molluscoid (mollusc-like) |
| `ui_species_extra_plantoid.txt` | Base class | Plantoid (plant-like) |
| `ui_species_extra_reptilian.txt` | Base class | Reptilian (reptile-like) |
| `ui_species_media_distant-worlds.txt` | Media pack | Distant Worlds (game series) |
| `ui_species_media_dnd.txt` | Media pack | Dungeons & Dragons |
| `ui_species_media_elder-scrolls.txt` | Media pack | The Elder Scrolls |
| `ui_species_media_galciv.txt` | Media pack | Galactic Civilizations |
| `ui_species_media_narivia.txt` | Media pack | Narivia (original setting) |

### Random Names (`ui-species-names/common/random_names/base/`)

| File | Purpose |
|------|---------|
| `ui-species-names.txt` | Species modification prefixes and postfixes for genetic modification events |

### Distribution Descriptors

| File | Purpose |
|------|---------|
| `ui-species-names.mod` | Mod metadata for Steam Workshop, Paradox Mods, Nexus Mods, GitHub Releases |
| `ui-species-names/descriptor.mod` | Mod metadata for Stellaris launcher (identical content) |

Both descriptor files must have identical `version`, `name`, `path`, `tags`, and `supported_version` fields.

## File Format Conventions

### Species Name List Files (`.txt`)

Stellaris-specific format using a custom declarative syntax:

```txt
CATEGORY_NAME = {
    species_key = {
        name = "Display Name"
        plural = "Plural Name"
        home_planet = "Home Planet Name"
        home_system = "Home System Name"
        name_list = "name_list_reference"
    }
    # ... more species definitions
}
```

- **Category**: `ART` (arthropoid), `AVI` (avian), `FUN` (fungoid), `HUM` (humanoid), `MAM` (mammalian), `MOL` (molluscoid), `PLA` (plantoid), `REP` (reptilian), or custom for media packs
- **species_key**: Unique identifier (lowercase, no spaces)
- **name**: Singular display name
- **plural**: Plural display name
- **home_planet**: Default home planet name
- **home_system**: Default home system name
- **name_list**: References a name list from the Name Lists mod (e.g., `ui_extra_art1`, `ui_dnd_kobold`)

### Random Names File

```txt
species_modification_prefix = {
    Prefix1_
    Prefix2_
    # ...
}

species_modification_postfix = {
    Postfix1
    Postfix2
    # ...
}
```

### Descriptor Files (`.mod`)

Key-value format with nested structures:

```txt
version="1.7.4"
name="Universum Infinitum: Species Names"
path="mod/ui-species-names"
tags={
    "Species"
}
supported_version="4.5.*"
```

## Naming Conventions

| Element | Convention | Example |
|---------|------------|---------|
| Mod directory | `ui-species-names` | kebab-case |
| Species name files | `ui_species_extra_{class}.txt` | snake_case with prefix |
| Media pack files | `ui_species_media_{theme}.txt` | snake_case with prefix |
| Species keys | lowercase, no spaces | `bamuth`, `chinad` |
| Name list references | `ui_{category}_{identifier}` | `ui_extra_art1`, `ui_dnd_kobold` |
| Display names | Title Case | `Bamuth`, `Chinadi` |
| Home planet names | Title Case | `Bamuthima` |
| Home system names | Title Case | `Bamuth` |

## Documentation Structure (`docs/`)

See [INDEX.md](./INDEX.md) for the complete documentation catalogue.

### Directory Purposes

| Directory | Purpose |
|-----------|---------|
| `api-reference/` | API reference (N/A for static mod, placeholder only) |
| `behaviour/` | User-facing behaviour documentation |
| `components/` | Per-component deep dives |
| `flows/` | End-to-end execution flows |

## Configuration Files

This mod has no runtime configuration files. All configuration is static and defined in the mod descriptor files.

## Build Artefacts

This mod has no build process. The source files are the distribution artefacts. GitHub Actions workflows (if present) only package releases.

## Test Files

This mod has no automated tests. Validation is manual:
- Install mod in Stellaris
- Verify species names appear in empire creation
- Check for parsing errors in game logs