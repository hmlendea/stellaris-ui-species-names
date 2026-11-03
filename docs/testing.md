# Testing

## Test Strategy

This mod is a **static data mod** with no executable code. Testing is **manual validation** only.

### No Automated Tests

- No unit tests
- No integration tests
- No end-to-end tests
- No test framework
- No CI test pipeline

### Validation Approach

Testing consists of **manual verification** in Stellaris:

1. Install mod in Stellaris
2. Launch game
3. Verify mod loads without errors
4. Verify species names appear in empire creation
5. Check game logs for parsing errors

## Test Organisation

### Manual Test Cases

| Test Case | Steps | Expected Result |
|-----------|-------|-----------------|
| Mod loads in launcher | 1. Install mod<br>2. Open Stellaris launcher<br>3. Check mod list | Mod appears with correct version, enabled |
| Mod loads in game | 1. Start new game<br>2. Check launcher log | No errors related to mod |
| Base species names | 1. Empire creation<br>2. Select each species class<br>3. Check name dropdown | New names appear for all 8 classes |
| Media pack names | 1. Empire creation<br>2. Select media pack species<br>3. Check name dropdown | New names appear for all 5 packs |
| Genetic modification | 1. Play game<br>2. Genetically modify species<br>3. Check new name | Prefix/postfix applied correctly |
| Dependency resolution | 1. Install without Name Lists mod<br>2. Check game log | Errors for unresolved name_list refs |
| Cross-platform | 1. Test on Windows, Linux, macOS | Mod works identically on all |

### Test Data

Test data is the mod itself — no separate test fixtures needed.

## Coverage

### Covered by Manual Testing

- Mod descriptor parsing
- Species definition parsing
- Name list reference resolution
- UI integration (empire creation)
- Genetic modification naming
- Cross-platform file compatibility

### Not Covered (No Automated Tests)

- Syntax validation in CI
- Regression detection
- Performance benchmarks
- Stress testing
- Edge case handling (duplicate keys, malformed entries)

## Verification Commands

### Pre-Release Validation

```bash
# 1. Check descriptor consistency
diff ui-species-names.mod ui-species-names/descriptor.mod

# 2. Check for duplicate species keys
grep -h "^\s*[a-z_]\+ = {" ui-species-names/common/species_names/*.txt | \
  sed 's/^\s*\([a-z_]\+\) = {.*/\1/' | sort | uniq -d

# 3. Check name_list references
grep -h "name_list" ui-species-names/common/species_names/*.txt | \
  sed 's/.*name_list = "\([^"]*\)".*/\1/' | sort -u

# 4. Verify file encoding
file ui-species-names/common/species_names/*.txt
file ui-species-names/common/random_names/base/ui-species-names.txt
file ui-species-names.mod
file ui-species-names/descriptor.mod
```

### In-Game Verification

No commands — manual gameplay verification only.

## Material Coverage Gaps

| Gap | Impact | Mitigation |
|-----|--------|------------|
| No automated syntax validation | Syntax errors only caught at game startup | Manual validation before release |
| No reference validation in CI | Unresolved name_list refs only caught in-game | Manual check against Name Lists mod |
| No duplicate key detection | Undefined behaviour in Stellaris | Manual grep check before release |
| No cross-version testing | Compatibility with new Stellaris versions unknown | Test on new Stellaris version release |
| No dependency version check | Name Lists mod changes may break refs | Coordinate with Name Lists mod maintainer |

## Test Constraints

### Prohibited

- No automated test framework can validate Stellaris parser behaviour
- No headless Stellaris for CI testing
- No mocking of Stellaris mod loader

### Required

- Stellaris installation for testing
- Name Lists mod installed
- Manual gameplay verification

## Future Improvements

Potential validation enhancements:
- Custom script to validate species definition syntax
- Cross-reference check against Name Lists mod (if machine-readable)
- Duplicate key detection in pre-commit hook
- Encoding/line ending validation in CI