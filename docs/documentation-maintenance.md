# Documentation Maintenance

## Purpose

This document defines how documentation in the `docs/` directory is maintained, updated, and kept in sync with the codebase.

## Documentation Structure

```
docs/
├── INDEX.md                      # Master index and catalogue
├── repository-overview.md        # High-level purpose and scope
├── repository-structure.md       # Source tree layout
├── architecture.md               # System architecture
├── data-model.md                 # Domain entities and relationships
├── configuration.md              # Configuration schema
├── build-and-deployment.md       # Release and deployment
├── testing.md                    # Test strategy
├── change-guide.md               # How to make changes
├── troubleshooting.md            # Common issues and solutions
├── faq.md                        # Frequently asked questions
├── dependencies.md               # Runtime and build dependencies
├── design-decisions.md           # Architectural decision records
├── documentation-maintenance.md  # This file
├── error-handling.md             # Error handling patterns
├── invariants.md                 # System invariants
├── integrations.md               # External integrations
├── logging.md                    # Logging and diagnostics
├── quick-start.md                # Quick start guide
├── security.md                   # Security considerations
├── state-and-persistence.md      # State management
├── concurrency-and-scheduling.md # Concurrency model
├── components/
│   ├── species-name-definitions.md
│   ├── random-name-prefixes.md
│   └── media-packs.md
├── flows/
│   ├── mod-loading.md
│   └── species-generation.md
├── behaviour/
│   ├── species-name-selection.md
│   └── empire-creation.md
└── api-reference/
    └── INDEX.md                  # Placeholder (static mod)
```

## Maintenance Principles

### 1. Documentation as Code

- Documentation lives in the repository alongside source
- Changes to code should trigger documentation review
- Documentation is versioned with the code

### 2. Single Source of Truth

- Authoritative information in one place
- Cross-references instead of duplication
- Code is the ultimate reference for implementation details

### 3. Audience Awareness

| Document | Primary Audience |
|----------|------------------|
| INDEX.md | All users |
| quick-start.md | New users/contributors |
| change-guide.md | Contributors |
| architecture.md | Maintainers |
| data-model.md | Maintainers |
| troubleshooting.md | Users |
| faq.md | Users |
| components/* | Contributors/maintainers |
| flows/* | Maintainers |
| behaviour/* | Maintainers |

## Update Triggers

### Mandatory Documentation Updates

| Code Change | Documentation to Update |
|-------------|------------------------|
| New species file added | INDEX.md, repository-structure.md, components/species-name-definitions.md |
| New media pack added | INDEX.md, repository-overview.md, components/media-packs.md, dependencies.md |
| New prefix/postfix added | components/random-name-prefixes.md |
| Descriptor version changed | build-and-deployment.md, INDEX.md |
| Stellaris version updated | build-and-deployment.md, dependencies.md, architecture.md |
| Name Lists dependency changed | dependencies.md, architecture.md |
| New design decision made | design-decisions.md |
| Bug fix with user impact | troubleshooting.md, faq.md, change-guide.md |

### Periodic Reviews

| Frequency | Scope |
|-----------|-------|
| Per release | All changed files + INDEX.md |
| Quarterly | Full docs audit for accuracy |
| Major Stellaris version | Architecture, dependencies, build-and-deployment |

## Maintenance Procedures

### Adding New Documentation

1. Create file in appropriate location
2. Follow existing style and structure
3. Add entry to INDEX.md catalogue
4. Cross-reference from related documents
5. Update this file if new category added

### Updating Existing Documentation

1. Locate affected documents (use cross-references)
2. Update content to match current reality
3. Update "Last Updated" in INDEX.md if present
4. Verify cross-references still valid

### Removing Documentation

1. Confirm content is obsolete (not just moved)
2. Remove file
3. Remove references from INDEX.md and other docs
4. Note in design-decisions.md if architectural

## Style Guide

### Formatting

- Markdown with consistent heading levels
- Code blocks for file paths, commands, examples
- Tables for structured data
- Relative links for internal references

### Tone

- Technical, precise, concise
- Present tense for current state
- Future tense for planned changes
- Past tense for historical decisions

### Required Sections

Each document should have:
- Clear title (H1)
- Purpose/scope paragraph
- Structured content with headings
- Cross-references to related docs

## Validation

### Pre-Release Checklist

- [ ] All internal links resolve
- [ ] No broken external links
- [ ] Version numbers consistent across docs
- [ ] File paths match actual repository structure
- [ ] Code examples are accurate
- [ ] No placeholder text remaining

### Automated Checks (Future)

Potential automation:
- Link checker in CI
- Spell check
- Markdown linting
- Cross-reference validation

## Responsibility

| Role | Responsibility |
|------|----------------|
| Maintainer | Overall docs health, architecture docs |
| Contributor | Update docs for their changes |
| Release Manager | Verify docs accuracy at release |

## Tools

- Editor: VS Code with Markdown extensions
- Preview: Built-in Markdown preview
- Link checking: Manual or future CI
- Spell check: Editor extension

## Archive Policy

- Obsolete versions not archived (Git history preserves)
- Major rewrites: note in design-decisions.md
- Deleted content: recoverable from Git

## Metrics

Track (informally):
- Documentation coverage of codebase
- Staleness (time since last update)
- Contributor feedback on clarity
- User questions answered by docs