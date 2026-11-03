# Documentation Index

## Repository Summary

Universum Infinitum: Species Names is a Stellaris mod that adds hundreds of new species names to the game. The mod consists of static text files defining species name lists for different species classes (arthropoid, avian, fungoid, humanoid, mammalian, molluscoid, plantoid, reptilian) and media-themed name packs (Distant Worlds, D&D, Elder Scrolls, Galactic Civilizations, Narivia). It requires the Universum Infinitum - Name Lists mod as a dependency.

## Root Document Map

- [ARCHITECTURE.md](../ARCHITECTURE.md) — High-level architecture (to be created)
- [SECURITY.md](../SECURITY.md) — Security policy and vulnerability reporting
- [ROADMAP.md](../ROADMAP.md) — Project roadmap (to be created)
- [PRIVACY.md](../PRIVACY.md) — Privacy and personal data handling
- [LICENSE](../LICENSE) — GNU General Public License v3.0
- [CONTRIBUTING.md](../CONTRIBUTING.md) — Contribution guidelines
- [CODE_OF_CONDUCT.md](../CODE_OF_CONDUCT.md) — Code of conduct

## Documentation Catalogue

### Core Documentation

| File | Description |
|------|-------------|
| [repository-overview.md](./repository-overview.md) | Repository purpose, scope, and entry points |
| [repository-structure.md](./repository-structure.md) | Source tree layout and module organisation |
| [architecture.md](./architecture.md) | High-level architecture complementing root ARCHITECTURE.md |
| [data-model.md](./data-model.md) | Domain entities, relationships, and persistence |
| [configuration.md](./configuration.md) | Configuration schema, sources, and precedence |
| [build-and-deployment.md](./build-and-deployment.md) | Build pipeline, deployment, and environments |
| [testing.md](./testing.md) | Test strategy, organisation, and coverage |
| [change-guide.md](./change-guide.md) | How to modify common areas safely |
| [troubleshooting.md](./troubleshooting.md) | Common issues and solutions |
| [faq.md](./faq.md) | Frequently asked questions |

### Component Deep Dives

| File | Description |
|------|-------------|
| [components/species-name-definitions.md](./components/species-name-definitions.md) | Species name list structure and format |
| [components/random-name-prefixes.md](./components/random-name-prefixes.md) | Species modification prefixes and postfixes |
| [components/media-packs.md](./components/media-packs.md) | Media-themed species name packs |

### Execution Flows

| File | Description |
|------|-------------|
| [flows/mod-loading.md](./flows/mod-loading.md) | How Stellaris loads the mod and its name lists |
| [flows/species-generation.md](./flows/species-generation.md) | How species names are used during empire creation |

### API Reference

| File | Description |
|------|-------------|
| [api-reference/INDEX.md](./api-reference/INDEX.md) | API reference index (N/A for static mod) |

### Cross-Cutting Concerns

| File | Description |
|------|-------------|
| [dependencies.md](./dependencies.md) | External and internal dependencies |
| [design-decisions.md](./design-decisions.md) | Key architectural and design choices |
| [documentation-maintenance.md](./documentation-maintenance.md) | How to keep docs current |
| [error-handling.md](./error-handling.md) | Error taxonomy and handling patterns |
| [invariants.md](./invariants.md) | System-wide invariants and contracts |
| [integrations.md](./integrations.md) | External system integrations |
| [logging.md](./logging.md) | Logging framework (N/A for static mod) |
| [quick-start.md](./quick-start.md) | Getting started guide for newcomers |
| [security.md](./security.md) | Security model complementing root SECURITY.md |
| [state-and-persistence.md](./state-and-persistence.md) | State management (N/A for static mod) |
| [concurrency-and-scheduling.md](./concurrency-and-scheduling.md) | Threading and async (N/A for static mod) |

### Behaviour Documentation

| File | Description |
|------|-------------|
| [behaviour/species-name-selection.md](./behaviour/species-name-selection.md) | How species names appear in-game |
| [behaviour/empire-creation.md](./behaviour/empire-creation.md) | Empire creation with custom species names |

## Navigation Aids

- **Start here** (newcomers): [quick-start.md](./quick-start.md) → [repository-overview.md](./repository-overview.md) → [repository-structure.md](./repository-structure.md)
- **Deep dive** (component owners): [components/](./components/) → [data-model.md](./data-model.md) → [configuration.md](./configuration.md)
- **Flows** (debuggers): [flows/](./flows/) → [architecture.md](./architecture.md)

## Maintenance Metadata

- Last reviewed: 2026-11-03
- Owner: Repository maintainers
- Coverage status: Initial generation in progress