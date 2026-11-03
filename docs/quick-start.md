# Quick Start Guide

## For Players

### Install in 3 Steps

1. **Subscribe on Steam Workshop** (recommended)
   - Visit: https://steamcommunity.com/sharedfiles/filedetails/?id=2040234709
   - Click **Subscribe**
   - Wait for download

2. **Enable in Launcher**
   - Open Stellaris Launcher
   - Go to **Mods** tab
   - Find "Universum Infinitum: Species Names"
   - Check the box to enable
   - **Also enable** "Universum Infinitum - Name Lists" (required)

3. **Play**
   - Click **Play**
   - Start new game
   - Enjoy new species names!

### Alternative: Manual Install

```bash
# 1. Download latest release
# https://github.com/hmlendea/stellaris-ui-species-names/releases

# 2. Extract to mod folder
# Linux/macOS:
unzip ui-species-names.zip -d ~/.local/share/Paradox\ Interactive/Stellaris/mod/

# Windows (PowerShell):
Expand-Archive ui-species-names.zip -DestinationPath "$env:USERPROFILE\Documents\Paradox Interactive\Stellaris\mod\"

# 3. Enable in launcher (same as above)
```

## For Contributors

### Prerequisites

- Stellaris installed (for testing)
- Git installed
- Text editor (VS Code recommended)
- Name Lists mod installed

### Setup

```bash
# 1. Clone repository
git clone https://github.com/hmlendea/stellaris-ui-species-names.git
cd stellaris-ui-species-names

# 2. Link to Stellaris mod folder (optional, for testing)
# Linux/macOS:
ln -s "$PWD/ui-species-names" ~/.local/share/Paradox\ Interactive/Stellaris/mod/ui-species-names

# Windows (PowerShell, as Admin):
New-Item -ItemType SymbolicLink -Path "$env:USERPROFILE\Documents\Paradox Interactive\Stellaris\mod\ui-species-names" -Target "$PWD\ui-species-names"
```

### Make a Change

1. **Edit species names**: Modify files in `ui-species-names/common/species_names/`
2. **Add prefixes/postfixes**: Edit `ui-species-names/common/random_names/base/ui-species-names.txt`
3. **Test**: Launch Stellaris, verify changes work
4. **Validate**: Run checks (see [Change Guide](change-guide.md#validation-before-commit))
5. **Commit**: `git commit -am "Description of change"`
6. **PR**: Push and open pull request

### Key Files

| Purpose | File |
|---------|------|
| Base extra species (8 classes) | `ui-species-names/common/species_names/ui_species_extra_*.txt` |
| Media pack species (5 packs) | `ui-species-names/common/species_names/ui_species_media_*.txt` |
| Genetic modification parts | `ui-species-names/common/random_names/base/ui-species-names.txt` |
| Mod metadata | `ui-species-names.mod`, `ui-species-names/descriptor.mod` |

## For Maintainers

### Release Checklist

1. Update version in both descriptor files
2. Run validation checks
3. Test in-game
4. Tag release: `git tag -a v1.8.0 -m "Release 1.8.0"`
5. Push tags: `git push origin main --tags`
6. Create GitHub Release with zip
7. Upload to Steam Workshop, Paradox Mods, Nexus Mods

### Directory Structure

```
stellaris-ui-species-names/
├── ui-species-names.mod          # Root descriptor (Steam/GitHub)
├── ui-species-names/             # Mod content folder
│   ├── descriptor.mod            # Launcher descriptor
│   └── common/
│       ├── random_names/
│       │   └── base/
│       │       └── ui-species-names.txt
│       └── species_names/
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
└── docs/                         # Documentation
```

## Links

- **Steam Workshop**: https://steamcommunity.com/sharedfiles/filedetails/?id=2040234709
- **Paradox Mods**: https://mods.paradoxplaza.com/mods/25437/Any
- **Nexus Mods**: https://nexusmods.com/stellaris/mods/77
- **GitHub**: https://github.com/hmlendea/stellaris-ui-species-names
- **Name Lists Mod**: https://github.com/hmlendea/stellaris-ui-name-lists
- **Issues**: https://github.com/hmlendea/stellaris-ui-species-names/issues