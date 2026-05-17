# PHASE 4 – RN TEST MIGRATION & EXECUTION

## ZIEL
Migriere alle gültigen Tests aus Phase 2 nach React Native/Jest und führe sie gegen den RN Code aus.

---

## INPUT

### Aus Phase 2 erforderlich:
* features/<FEATURE_NAME>/21_test_implementation.md → Mapping TEST-ID zu Dateien
* features/<FEATURE_NAME>/22_test_execution_report.md → Test Execution Results
* features/<FEATURE_NAME>/23_test_quality_report.md → VALID/WEAK/INVALID Klassifikation
* Legacy Test Dateien (Android + iOS, zur Referenz)

### Aus Phase 3 erforderlich:
* rn-expo-project/src/features/<FEATURE>/ → Der implementierte Code
* features/<FEATURE_NAME>/31_rn_architecture_decisions.md → Architektur Decisions
* features/<FEATURE_NAME>/33_rn_dependency_mapping.md → Was wurde installiert

### Regelwerke:
* base/output_rules.md
* base/validation_rules.md
* base/error_rules.md

---

## OUTPUT

### Dateien zu erzeugen:
* features/<FEATURE_NAME>/41_test_migration_mapping.md
* features/<FEATURE_NAME>/42_rn_test_implementation.md
* features/<FEATURE_NAME>/43_test_execution_report_rn.md

### Code zu erzeugen:
* rn-expo-project/src/features/<FEATURE>/__tests__/<FeatureName>.test.ts
* [Optional] rn-expo-project/src/features/<FEATURE>/__tests__/hooks.test.ts
* [Optional] rn-expo-project/src/features/<FEATURE>/__tests__/utils.test.ts

---

## EXECUTION STEPS

---

### STEP 0: TEST READINESS CHECK

**Input: 23_test_quality_report.md**

```
Prüfe:
[ ] VALID Tests vorhanden?
[ ] >= 80% der Tests klassifiziert?

Wenn INVALID Tests (V-0709 aus Phase 2):
  - SKIP diese Tests in Phase 4
  - Dokumentiere Grund
  
Falls < 80% VALID Tests:
  - WARNUNG ausgeben
  - Aber fortsetzen (nicht STOPPEN)
```

---

### STEP 1: TEST MIGRATION MAPPING

**Erstelle: 41_test_migration_mapping.md**

```markdown
# Test Migration Mapping for <FEATURE>

## Migration Status Overview
- Total Tests in Phase 2: <N>
- Tests VALID: <N> → MIGRIEREN
- Tests WEAK: <N> → EVALUIEREN
- Tests INVALID: <N> → SKIP

## Test-by-Test Mapping

| TEST-ID | Legacy Framework | Quality | RN Framework | Status | Notes |
|---------|-----------------|---------|-------------|--------|-------|
| TEST-SC-001 | JUnit4 (Android) | VALID | Jest | READY | Direct mapping possible |
| TEST-SC-002 | XCTest (iOS) | VALID | Jest | READY | Async handling required |
| TEST-EP-005 | JUnit4 (Android) | INVALID | - | SKIP | Entry Point missing |

## Framework Mapping (Android JUnit4 → Jest)

| JUnit4 | Jest | Migration Note |
|--------|------|-----------------|
| @Before | beforeEach() | State setup |
| @After | afterEach() | State cleanup |
| @Test | test() or it() | Test case |
| assertEquals() | expect().toBe() or toEqual() | Assertion |
| assertTrue() | expect().toBe(true) | Boolean assertion |
| assertThrows() | expect().toThrow() | Error assertion |
| SharedPreferences | AsyncStorage mock | Storage mocking |

## Framework Mapping (iOS XCTest → Jest)

| XCTest | Jest | Migration Note |
|--------|------|-----------------|
| override func setUp() | beforeEach() | State setup |
| override func tearDown() | afterEach() | State cleanup |
| func test_X() | test('X', async () => {}) | Async required |
| XCTAssertEqual() | expect().toEqual() | Assertion |
| XCTAssertThrows | expect().toThrow() | Error assertion |
| UserDefaults | AsyncStorage mock | Storage mocking |
```

---

### STEP 2: JEST SETUP

**Prüfe Projekt-Konfiguration:**

```bash
cd rn-expo-project

# Prüfe ob jest.config.js existiert
# Falls nicht:
npm install --save-dev jest @testing-library/react-native
```

**Konfiguriere jest.config.js (falls neu):**

```javascript
module.exports = {
  preset: 'react-native',
  setupFilesAfterEnv: ['<rootDir>/jest.setup.js'],
  testEnvironment: 'node',
  collectCoverageFrom: [
    'src/**/*.{ts,tsx}',
    '!src/**/*.d.ts',
  ],
};
```

**Konfiguriere jest.setup.js (für Mocks):**

```javascript
// Mock AsyncStorage für Tests
jest.mock('@react-native-async-storage/async-storage', () => ({
  getItem: jest.fn(() => Promise.resolve(null)),
  setItem: jest.fn(() => Promise.resolve()),
  removeItem: jest.fn(() => Promise.resolve()),
  clear: jest.fn(() => Promise.resolve()),
}));

// Mock axios für API Tests
jest.mock('axios', () => ({
  create: jest.fn(() => ({
    get: jest.fn(() => Promise.resolve({ data: {} })),
    post: jest.fn(() => Promise.resolve({ data: {} })),
    interceptors: { response: { use: jest.fn() } },
  })),
}));
```

---

### STEP 3: TEST FILE MIGRATION

**Für JEDEN VALID Test aus Phase 2, erstelle Jest Test:**

Create: `rn-expo-project/src/features/<FEATURE>/__tests__/<FeatureName>.test.ts`

```typescript
/**
 * TRACE: TEST_SUITE_<FeatureName>
 * PHASE: 4 – RN Test Migration
 * SOURCE: 22_test_execution_report.md (Phase 2)
 * 
 * Migrated from:
 * - Android: <File>.java (JUnit4)
 * - iOS: <File>.swift (XCTest)
 */

import AsyncStorage from '@react-native-async-storage/async-storage';
import apiService from '../../services/api';
import storageService from '../../services/storage';
import { <ComponentName> } from '../components/<ComponentName>';

// Mock all dependencies
jest.mock('../../services/storage');
jest.mock('../../services/api');

describe('<FeatureName> Component Tests', () => {
  
  beforeEach(() => {
    // Clear all mocks before each test
    jest.clearAllMocks();
    
    // Reset AsyncStorage mock
    (AsyncStorage.getItem as jest.Mock).mockResolvedValue(null);
    (AsyncStorage.setItem as jest.Mock).mockResolvedValue(undefined);
  });

  afterEach(() => {
    // Cleanup
    jest.restoreAllMocks();
  });

  /**
   * TEST-ID: TEST-SC-001 (aus Phase 2)
   * Type: State Change
   * Mapped from: Android JUnit4 @ <AndroidFile>.<TestMethod>()
   * Mapped from: iOS XCTest @ <iOSFile>.test_SC_001()
   */
  test('TEST-SC-001: Should store value in storage', async () => {
    // Precondition (aus 13_test_definition.md)
    expect(AsyncStorage.getItem).not.toHaveBeenCalled();

    // Action (aus 13_test_definition.md Entry Point)
    const result = await storageService.setItem('FEATURE_KEY_1', 'test_value');

    // Assertion (konkret, aus 13_test_definition.md Expected Output)
    expect(AsyncStorage.setItem).toHaveBeenCalledWith(
      'feature_key_1',
      'test_value'
    );
    expect(result).toBeUndefined(); // setItem returns void
  });

  /**
   * TEST-ID: TEST-SC-002
   * Type: State Change – Retrieve from Storage
   * Mapped from: Android JUnit4 @ ...
   * Mapped from: iOS XCTest @ ...
   */
  test('TEST-SC-002: Should retrieve value from storage', async () => {
    // Mock storage return value
    (AsyncStorage.getItem as jest.Mock).mockResolvedValue('stored_value');

    // Action
    const result = await storageService.getItem('FEATURE_KEY_1');

    // Assertion
    expect(AsyncStorage.getItem).toHaveBeenCalledWith('feature_key_1');
    expect(result).toBe('stored_value');
  });

  /**
   * TEST-ID: TEST-EB-001
   * Type: Error Branch
   * Mapped from: Android @ ...
   * Mapped from: iOS @ ...
   */
  test('TEST-EB-001: Should handle storage error gracefully', async () => {
    // Precondition: Mock error
    const storageError = new Error('Storage access denied');
    (AsyncStorage.getItem as jest.Mock).mockRejectedValue(storageError);

    // Action & Assertion
    await expect(storageService.getItem('FEATURE_KEY_1')).rejects.toThrow(
      'Storage access denied'
    );
  });

  /**
   * TEST-ID: TEST-EP-002
   * Type: Entry Point
   * Mapped from: Android @ ...
   * Mapped from: iOS @ ...
   */
  test('TEST-EP-002: Component should initialize on mount', async () => {
    // Component initialization test
    // TODO: Implement based on 12_code_facts.md O-1302
  });
});
```

**Jest Assertions Mapping (Phase 2 → Phase 4):**

| Phase 2 (Android JUnit4) | Phase 2 (iOS XCTest) | Phase 4 (Jest) |
|-------------------------|------------------|----------------|
| assertEquals(true, x) | XCTAssertEqual(true, x) | expect(x).toBe(true) |
| assertTrue(x) | XCTAssertTrue(x) | expect(x).toBe(true) |
| assertNull(x) | XCTAssertNil(x) | expect(x).toBeNull() |
| assertThrows | XCTAssertThrows | expect().toThrow() |

---

### STEP 4: HOOK TESTS

**Für Custom Hooks (falls vorhanden):**

Create: `rn-expo-project/src/features/<FEATURE>/__tests__/hooks.test.ts`

```typescript
/**
 * TRACE: HOOK_TESTS_<Feature>
 * PHASE: 4 – RN Test Migration
 * SOURCE: 12_code_facts.md O-1305 (State Management)
 */

import { renderHook, act } from '@testing-library/react-native';
import { use<FeatureName> } from '../hooks/use<FeatureName>';

describe('use<FeatureName> Hook', () => {
  
  beforeEach(() => {
    jest.clearAllMocks();
  });

  test('should initialize with default state', () => {
    const { result } = renderHook(() => use<FeatureName>());

    expect(result.current.state).toBeNull();
    expect(result.current.isLoading).toBe(false);
    expect(result.current.error).toBeNull();
  });

  test('should update state', async () => {
    const { result } = renderHook(() => use<FeatureName>());

    act(() => {
      result.current.updateState({ data: 'test' });
    });

    expect(result.current.state).toEqual({ data: 'test' });
  });

  // Additional hook tests mapping Phase 2 tests
});
```

---

### STEP 5: UTILITY TESTS

**Für Helper Functions (falls vorhanden):**

Create: `rn-expo-project/src/features/<FEATURE>/__tests__/utils.test.ts`

```typescript
/**
 * TRACE: UTILS_TESTS_<Feature>
 * PHASE: 4 – RN Test Migration
 * SOURCE: 12_code_facts.md O-1310 (Utility Functions)
 */

import {
  transformDataForDisplay,
  validateInput,
} from '../utils/helpers';

describe('Utility Functions', () => {
  
  test('transformDataForDisplay should transform data correctly', () => {
    const input = { /* test data */ };
    const output = transformDataForDisplay(input);
    
    // Assertion based on O-1310
    expect(output).toEqual({ /* expected */ });
  });

  test('validateInput should validate input correctly', () => {
    const validInput = { /* valid data */ };
    expect(validateInput(validInput)).toBe(true);

    const invalidInput = { /* invalid data */ };
    expect(validateInput(invalidInput)).toBe(false);
  });
});
```

---

### STEP 6: OUTPUT – test_migration_mapping.md

[Siehe STEP 1 oben – wird dort bereits erzeugt]

---

### STEP 7: OUTPUT – rn_test_implementation.md

**Erstelle: 42_rn_test_implementation.md**

```markdown
# RN Test Implementation Summary

## Test Files Generated
- src/features/<FEATURE>/__tests__/<FeatureName>.test.ts ✅
- src/features/<FEATURE>/__tests__/hooks.test.ts [YES/NO]
- src/features/<FEATURE>/__tests__/utils.test.ts [YES/NO]

## Test Migration Statistics
- Total Tests from Phase 2: <N>
- VALID Tests (migrated): <N>
- WEAK Tests (migrated with flags): <N>
- INVALID Tests (skipped): <N>

## Test-by-Test Implementation Status
| TEST-ID | Status | File | Notes |
|---------|--------|------|-------|
| TEST-SC-001 | ✅ MIGRATED | __tests__/<Feature>.test.ts | Line XX |
| TEST-SC-002 | ✅ MIGRATED | __tests__/<Feature>.test.ts | Line YY |
| TEST-EP-005 | ❌ SKIPPED | - | Entry Point unavailable |

## Jest Configuration
- jest.config.js: ✅ CONFIGURED
- jest.setup.js: ✅ CONFIGURED
- Mock Dependencies: ✅ CONFIGURED
  - AsyncStorage ✅
  - axios ✅
  - [Other] ✅
```

---

### STEP 8: BUILD & COMPILE

**Schritt 8a – TypeScript Check:**
```bash
cd rn-expo-project
npm run type-check
```

Falls Errors → Dokumentiere in 43_test_execution_report_rn.md

**Schritt 8b – Test Compilation:**
```bash
npm test -- --listTests
```

Falls Errors → STOP (E-0402)

---

### STEP 9: TEST EXECUTION

**Schritt 9a – Run all tests:**
```bash
cd rn-expo-project
npm test -- --verbose --coverage
```

**Schritt 9b – Collect Results:**

```
Dokumentiere:
- Total tests run
- Passed
- Failed
- Skipped
- Coverage %

Für JEDEN Failed Test:
  - TEST-ID
  - Error Message
  - Line where failed
  - Root cause
```

---

### STEP 10: OUTPUT – test_execution_report_rn.md

**Erstelle: 43_test_execution_report_rn.md**

```markdown
# RN Test Execution Report

## Execution Environment
- Node Version: <V>
- Jest Version: <V>
- React Native Version: <V>
- Execution Date: YYYY-MM-DD HH:MM

## Test Results Summary
- Total Tests: <N>
- Passed: <N> (X%)
- Failed: <N> (X%)
- Skipped: <N>

## Failed Tests Detail
| TEST-ID | Error | Root Cause |
|---------|-------|-----------|
| TEST-SC-001 | AssertionError: expected X to be Y | Mock not configured |
| TEST-EB-001 | TypeError: Cannot read property | Missing implementation |

## Code Coverage
- Statements: X%
- Branches: X%
- Functions: X%
- Lines: X%

### Uncovered Code
[Liste von Dateien/Funktionen ohne Test Coverage]

## Comparison: Phase 2 vs Phase 4
| Metric | Phase 2 (Legacy) | Phase 4 (RN) | Delta |
|--------|-----------------|-------------|-------|
| Total Tests | N | N | 0 (1:1 mapping) |
| Passed % | X% | Y% | [+/-] |
| Coverage | X% | Y% | [+/-] |

## Summary
- Phase 4 Status: COMPLETE / PARTIAL / FAILED
- All VALID tests migrated: YES / NO
- Ready for Phase 5: YES / NO
- Blockers: [Falls vorhanden]
```

---

## REGELN

### Jest Implementation
- JEDEN Legacy Test 1:1 zu Jest migrieren (VALID Tests)
- Mocks für AsyncStorage, API, Storage Service MÜSSEN korrekt konfiguriert sein
- Assertions MÜSSEN identisch zu Phase 2 sein
- Test-IDs MÜSSEN referenziert werden

### Skipping Tests
- INVALID Tests: NOT MIGRATED (dokumentiere Grund)
- WEAK Tests: MIGRATED MIT FLAG (mit Kommentar)
- Wenn Legacy Test nicht auf RN mappbar: Dokumentiere explizit

### Error Handling
- Jest error messages MÜSSEN aussagekräftig sein
- Failed tests MÜSSEN Root Cause analysiert sein
- KEINE Interpretation, nur Fakten

---

## VALIDATION (BLOCKING)

| Regel | Prüfung | Fehler |
|------|---------|--------|
| V-0901 | Alle VALID Tests aus Phase 2 MÜSSEN migriert sein | E-0401 |
| V-0902 | TypeScript muss kompilieren | E-0401 |
| V-0903 | Jest Tests müssen kompilierbar sein | E-0401 |
| V-0904 | Kein Test ohne SOURCE Referenz (TEST-ID) | E-0401 |
| V-0905 | Jeder Mock korrekt konfiguriert | E-0402 |

---

## FEHLERFALL

| Fehler Code | Situation | Behandlung |
|-------------|-----------|-----------|
| E-0401 | Test Migration Failed (Compilation Error) | STOP. Details in Report |
| E-0402 | Too Many Test Failures (>20% Failed) | WARNUNG, Dokumentiere, fortsetzen zu Phase 5 |

---
