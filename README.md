[![Donate](https://img.shields.io/badge/-%E2%99%A5%20Donate-%23ff69b4)](https://hmlendea.go.ro/funding)
[![Latest Release](https://img.shields.io/github/v/release/hmlendea/stellaris-ui-species-names)](https://github.com/hmlendea/stellaris-ui-species-names/releases/latest)
[![Build Status](https://github.com/hmlendea/stellaris-ui-species-names/actions/workflows/nexus-mods.yml/badge.svg)](https://github.com/hmlendea/stellaris-ui-species-names/actions/workflows/nexus-mods.yml)
[![License](https://img.shields.io/github/license/hmlendea/stellaris-ui-species-names)](https://github.com/hmlendea/stellaris-ui-species-names/blob/master/LICENSE)

# Universum Infinitum: Species Names

A Stellaris mod that adds hundreds of new species names to the game.

## 📑 Table of Contents

- [Capabilities](#-capabilities)
- [Usage](#-usage)
- [System Requirements](#️-system-requirements)
- [Installation](#-installation)
  - [Manual Installation](#manual-installation)
- [Compatibility](#-compatibility)
- [Integrations](#-integrations)
- [Privacy and Data](#️-privacy-and-data)
- [Documentation](#-documentation)
- [GitHub Actions](#️-github-actions)
- [Architecture](#️-architecture)
- [Troubleshooting](#-troubleshooting)
- [FAQ](#-faq)
- [Contributing](#-contributing)
- [Code of Conduct](#-code-of-conduct)
- [Related Projects](#-related-projects)
- [Security](#-security)
- [Project Engagement](#-project-engagement)
- [License](#-license)

## ✨ Capabilities

- Adds hundreds of new species names across all vanilla species classes (arthropoid, avian, fungoid, humanoid, mammalian, molluscoid, plantoid, reptilian)
- Includes media-themed name packs (Distant Worlds, Dungeons & Dragons, The Elder Scrolls, Galactic Civilizations, Narivia)
- Provides random name prefixes for additional variety
- Integrates with the Universum Infinitum - Name Lists mod for extended name generation

## 🚀 Usage

After installation, the new species names are automatically available when creating or modifying empires in Stellaris. No additional configuration is required.

## 🖥️ System Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| Stellaris | 4.5.* | Latest stable |
| Universum Infinitum - Name Lists | Latest | Latest |

## 📦 Installation

[![Obtain it from Steam Workshop](https://raw.githubusercontent.com/hmlendea/readme-assets/master/badges/stores/steam-workshop.png)](https://steamcommunity.com/sharedfiles/filedetails/?id=2040234709)
[![Obtain it from Paradox Mods](https://raw.githubusercontent.com/hmlendea/readme-assets/master/badges/stores/paradox-mods.png)](https://mods.paradoxplaza.com/mods/25437/Any)
[![Obtain it from Nexus Mods](https://raw.githubusercontent.com/hmlendea/readme-assets/master/badges/stores/nexus.png)](https://nexusmods.com/stellaris/mods/77)
[![Obtain it from GitHub](https://raw.githubusercontent.com/hmlendea/readme-assets/master/badges/stores/github.png)](https://github.com/hmlendea/stellaris-ui-species-names/releases)

### Manual Installation

1. Download the [latest release](https://github.com/hmlendea/stellaris-ui-species-names/releases/latest)
2. Extract the contents into your game's mod directory
3. Install [Universum Infinitum - Name Lists](https://github.com/hmlendea/stellaris-ui-name-lists) (required mod)
4. Enable both mods in the Stellaris launcher

## 🧩 Compatibility

| Component | Supported Versions | Notes |
|-----------|--------------------|-------|
| Operating System | Linux, macOS, Windows | OS-agnostic; actively tested on Linux |
| Stellaris | 4.5.* | Compatible with native and Steam Play on Linux |
| Other mods | Any | No known conflicts |

## 🔌 Integrations

| Integration | Compatibility | Purpose | Required |
|-------------|---------------|---------|----------|
| Universum Infinitum - Name Lists | Latest version | Provides base name list infrastructure | Yes |

## 🛡️ Privacy and Data

Universum Infinitum: Species Names does not collect, process, transmit, or persist personal data. The mod consists of static species-name text files and descriptor metadata with no executable code, telemetry, analytics, or diagnostics.

For the detailed description of how the application handles privacy and personal data, see [PRIVACY.md](./PRIVACY.md).

## 📚 Documentation

Comprehensive documentation is available in the [docs/](./docs/) directory:

| Resource | Description |
|----------|-------------|
| [Quick Start](./docs/quick-start.md) | Installation and setup |
| [Change Guide](./docs/change-guide.md) | How to modify the mod |
| [Architecture](./docs/architecture.md) | System design and data flow |
| [Troubleshooting](./docs/troubleshooting.md) | Common issues and solutions |
| [FAQ](./docs/faq.md) | Frequently asked questions |
| [Full Documentation Index](./docs/INDEX.md) | Complete catalogue |

## ⚙️ GitHub Actions

| Workflow | Purpose | What it does |
|----------|---------|--------------|
| [ nexus-mods.yml ](https://github.com/hmlendea/stellaris-ui-species-names/blob/master/.github/workflows/nexus-mods.yml) | Release to Nexus Mods | Downloads the GitHub release asset and uploads it to Nexus Mods on tag push |
| [ steam-workshop.yml ](https://github.com/hmlendea/stellaris-ui-species-names/blob/master/.github/workflows/steam-workshop.yml) | Release to Steam Workshop | Downloads the GitHub release asset, extracts it, and uploads to Steam Workshop on tag push |

## 🏗️ Architecture

Universum Infinitum: Species Names is a static Stellaris mod consisting of species-name definition files and a mod descriptor. It integrates with the Universum Infinitum - Name Lists mod to extend the game's name generation system.

See the [architecture documentation](./ARCHITECTURE.md) for the system context, principal components, runtime flows, ownership boundaries, dependencies, constraints, and extension points.

## 🩺 Troubleshooting

See [Troubleshooting Guide](./docs/troubleshooting.md) for diagnostic procedures and resolutions to recurring problems.

## ❓ FAQ

See the [Frequently Asked Questions](./docs/faq.md) for responses to frequently raised inquiries.

## 🤝 Contributing

You are welcome to submit any suggestion, feedback, or modification to this project.

When doing so, please:
- Maintain cross-platform compatibility
- Submit focused pull requests that conform to the existing code style
- Maintain your branch synchronised with `master`
- Raise a new [issue](https://github.com/hmlendea/stellaris-ui-species-names/issues) for problems or suggestions

See the [contributing guidelines](./CONTRIBUTING.md) for details on how to report issues, suggest enhancements, and submit changes.

## 📜 Code of Conduct

See the [Code of Conduct](./CODE_OF_CONDUCT.md) for the standards of conduct expected in all project spaces.

## 🔗 Related Projects

- [Universum Infinitum: Flags](https://github.com/hmlendea/stellaris-ui-flags) — Custom flag emblems
- [Universum Infinitum: Galaxy Sizes](https://github.com/hmlendea/stellaris-ui-galaxy-sizes) — Additional galaxy size options
- [Universum Infinitum: Name Lists](https://github.com/hmlendea/stellaris-ui-name-lists) — Required dependency; base name list infrastructure
- [Universum Infinitum: Prescripted Countries](https://github.com/hmlendea/stellaris-ui-prescripted-countries) — Pre-made empires
- [Universum Infinitum: Star Names](https://github.com/hmlendea/stellaris-ui-star-names) — Custom star names

## 🔒 Security

Universum Infinitum: Species Names is a static mod with no executable code, telemetry, analytics, or diagnostics.

For information on reporting security vulnerabilities, see [SECURITY.md](./SECURITY.md).

## 💝 Project Engagement

Discovered a problem or have a suggestion? [Open an issue](https://github.com/hmlendea/stellaris-ui-species-names/issues)!

If you find this project useful, consider [funding it](https://hmlendea.go.ro/funding) or starring ⭐️ it on GitHub, or giving it a thumbs up and adding it as a favourite on the [Steam Workshop](https://steamcommunity.com/sharedfiles/filedetails/?id=2040234709)!

[![Donate](https://raw.githubusercontent.com/hmlendea/readme-assets/master/donate_generic.png)](https://hmlendea.go.ro/funding)

## 📄 License

This project is being distributed under the `GNU General Public License v3.0 or later`.
See [LICENSE](./LICENSE) for additional information.
