# Frequently Asked Questions

## General

### What does this mod do?

Adds 250+ new species names across 8 base species classes (arthropoid, avian, fungoid, humanoid, mammalian, molluscoid, plantoid, reptilian) and 5 media-themed packs (Distant Worlds, D&D, Elder Scrolls, GalCiv, Narivia) for empire creation and genetic modification.

### Is this a standalone mod?

**No.** It requires **Universum Infinitum - Name Lists** mod to function. The Name Lists mod provides the actual name lists; this mod creates species definitions that reference those lists.

### Which Stellaris version is supported?

Current: **4.5.*** (see `supported_version` in descriptor files). Check the mod page for latest compatibility.

### Is it compatible with other mods?

Yes, generally compatible with:
- Other species mods (adds names, doesn't replace)
- UI mods
- Gameplay mods
- Total conversions (may need updates for new versions)

Known conflicts: Mods that overwrite base species classes or random names may conflict.

## Installation

### How do I install it?

**Steam Workshop** (easiest): Subscribe → Launch Stellaris → Enable in launcher → Play.

**Paradox Mods**: Install via Paradox launcher → Enable → Play.

**Nexus Mods**: Download → Extract to mod folder → Enable in launcher.

**GitHub**: Download release zip → Extract to mod folder → Enable in launcher.

### Where is the mod folder?

| Platform | Path |
|----------|------|
| Windows | `%USERPROFILE%\Documents\Paradox Interactive\Stellaris\mod\` |
| Linux | `~/.local/share/Paradox Interactive/Stellaris/mod/` |
| macOS | `~/Documents/Paradox Interactive/Stellaris/mod/` |
| Steam Deck | `~/.local/share/Steam/steamapps/compatdata/281990/pfx/drive_c/users/steamuser/Documents/Paradox Interactive/Stellaris/mod/` |

### Do I need to install Name Lists mod separately?

**Yes.** Subscribe/install Name Lists mod from the same platform. Both mods must be enabled.

### Load order matters?

Usually automatic. Name Lists should load before Species Names. Launcher handles this.

## Usage

### How do I use the new names?

1. Start new game
2. Empire creation screen
3. Select species class (e.g., Mammalian)
4. Click name dropdown → new names appear alongside vanilla
5. For media packs: select the media pack species portrait

### Can I use these names for existing empires?

Only via **genetic modification** in-game. Select species → Modify → New name generated with prefixes/postfixes.

### Do the media packs add new portraits?

**No.** They use existing Stellaris portraits. Only names are new.

### Can I disable specific packs?

Not directly. To disable a pack, delete its file from `common/species_names/` (not recommended — update mod instead).

## Troubleshooting

### Mod not showing in launcher

See [Troubleshooting](troubleshooting.md#mod-not-appearing-in-launcher).

### Names not appearing in empire creation

See [Troubleshooting](troubleshooting.md#mod-loads-but-names-dont-appear).

### Game crashes on startup

See [Troubleshooting](troubleshooting.md#game-crashes-on-startup).

### "name_list not found" error

Name Lists mod not installed or outdated. Install/update Name Lists mod.

## Development

### Can I add my own names?

Yes. See [Change Guide](change-guide.md#adding-new-species-names).

### How do I contribute?

See [CONTRIBUTING.md](../CONTRIBUTING.md).

### What's the license?

**GNU GPL v3.0** — see [LICENSE](../LICENSE).

### Where is the source code?

GitHub: https://github.com/hmlendea/stellaris-ui-species-names

### How do I report a bug?

GitHub Issues: https://github.com/hmlendea/stellaris-ui-species-names/issues

Include: Stellaris version, mod version, platform, installation method, error log.

## Compatibility

### Works with Stellaris 4.0+?

Tested on 4.5.*. May work on 4.0-4.4 but not guaranteed.

### Works with DLC?

Yes, all DLCs. Names are additive.

### Works with console (PS5/Xbox)?

**No.** Paradox mods not supported on consoles.

### Multiplayer compatible?

Yes, if all players have same mod versions installed.

### Save game compatible?

Adding names: **Yes** (additive).
Removing names: **No** (breaks saves using those names).

## Updates

### How do I update?

**Steam/Paradox**: Auto-updates when launched.
**Nexus/GitHub**: Download new version, replace files.

### Will updates break my save?

Adding new names: **No**.
Changing existing names: **Yes** (empires using old names affected).

### How often are updates released?

When new name lists are added to Name Lists mod, or for Stellaris version updates.

## Advanced

### Can I use this mod's names in my mod?

Yes, GPL v3 allows derivative works. Credit appreciated.

### How are names generated?

Species definitions reference `name_list` from Name Lists mod. Stellaris picks randomly from the list.

### What are prefixes/postfixes?

Applied during genetic modification: "Prefix OriginalName Postfix". Defined in `common/random_names/base/ui-species-names.txt`.

### Can I translate the mod?

Names are proper nouns — translation not typical. Display names in species definitions could be localised (not currently implemented).

### Performance impact?

**Negligible.** Static data only. No scripts, events, or runtime logic.