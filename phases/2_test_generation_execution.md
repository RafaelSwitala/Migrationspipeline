# PHASE 2 – TEST GENERATION EXECUTION

## ZIEL
Erzeuge deterministische, ausführbare Testklassen für Android und iOS basierend auf test_definition.md und führe diese vollständig aus. Dokumentiere ausschließlich reale Ergebnisse.

---

## INPUT

### Aus Phase 1 erforderlich:
* features/<FEATURE_NAME>/12_code_facts.md → für reale Klassen + Methoden
* features/<FEATURE_NAME>/13_test_definition.md → für Test IDs + Entry Points
* features/<FEATURE_NAME>/15_execution_contract.md → für Test Reihenfolge + Restrictions

### Legacy Code (physisch erforderlich):
* Android: android-mobilebrowser/app/src (für reale Klassen Import)
* iOS: ios-mobilebrowser/Source (für reale Klassen Import)

Zusätzliche Regelwerke müssen beachtet werden:
* base/output_rules.md
* base/validation_rules.md
* base/error_rules.md
* base/testing.md (falls vorhanden)
* base/naming_rules.md

---

## OUTPUT

Es müssen folgende Dateien vollständig erzeugt werden:

* features/<FEATURE_NAME>/21_test_implementation.md
* features/<FEATURE_NAME>/22_test_execution_report.md
* features/<FEATURE_NAME>/23_test_quality_report.md
* Testklassen für Android: android-mobilebrowser/app/src/test/java/.../
* Testklassen für iOS: ios-mobilebrowser/SourceTests/

---

## EXECUTION STEPS

---

### STEP 0: ENVIRONMENT CHECK & SETUP

**Android:**
* Prüfe: VC-0204
* Falls etwas fehlt: E-0203

Führe aus:
cd android-mobilebrowser
./gradlew clean --build-cache

**iOS:**
* Prüfe: VC-0205
* Falls etwas fehlt: E-0204

Führe aus:
cd ios-mobilebrowser
pod install falls erforderlich

---

### STEP 1: TEST SPECIFICATION EXTRACTION

Aus 13_test_definition.md:

**Für JEDEN Test extrahiere:**

| Feld | Quelle | Beispiel |
|------|--------|---------|
| TEST-ID | O-1401 col1 | TEST-SC-001 |
| Type | O-1401 col2 | State Change / Entry Point / Edge Branch |
| Entry Point | O-1401 col3 | feature.init() |
| Precondition | O-1401 col4 | storage.isEmpty() |
| Action | O-1401 col5 | feature.setValue("key", "value") |
| Expected Output | O-1401 col6 | return true |
| Platform | O-1402 col1 | iOS / Android / Both |
| O-130x Ref | O-1401 col7 | O-1302, O-1306 |

**Validierung:** Kein Test ohne alle Felder → STOP (V-0701)

---

### STEP 2: CODE FACTS RESOLUTION

Für JEDEN Test:

**Schritt 2a – Entry Point Lookup:**
```
1. Suche Entry Point (z.B. "feature.init()") in 12_code_facts.md
2. Finde Quelldatei + Zeilennummern
3. Bestätige Klasse existiert in Legacy Code
   Android: Suche in app/src/main/java
   iOS: Suche in Source
4. Falls nicht gefunden → BLOCKER (E-0201)
```

**Schritt 2b – Precondition Resolution:**
```
1. Wenn Precondition = "storage.isEmpty()", suche in code_facts.md:
   - Wie wird Storage initialisiert?
   - Android: SharedPreferences Instanz
   - iOS: UserDefaults Instanz
2. Bestimme Setup-Code für Test
3. Falls Setup unmöglich → Flag als WEAK in Quality Report
```

**Schritt 2c – Assertion Mapping:**
```
1. Expected Output: "return true"
2. Suche in Code:
   - Welche Methode ruft das zurück?
   - Welcher Wert wird tatsächlich returned?
3. Konkretisiere Assertion:
   - NICHT: assertTrue(result) 
   - SONDERN: assertEquals(true, feature.getValue("key"))
```

---

### STEP 3: TEST FILE GENERATION

#### Android (JUnit4)

**Template für jede Testklasse:**

```java
package com.mobilebrowser.tests.<FEATURE>;

import static org.junit.Assert.*;
import org.junit.Before;
import org.junit.After;
import org.junit.Test;
import android.content.Context;
import android.content.SharedPreferences;
import androidx.test.core.app.ApplicationProvider;

/**
 * TRACE: TEST_FAMILY_<Feature><Component>
 * PHASE: 2 – Test Generation
 * SOURCE: 13_test_definition.md
 */
public class <Feature><Component>Test {
    
    private Context context;
    private SharedPreferences prefs;
    private <RealClass> instance;
    
    @Before
    public void setUp() throws Exception {
        // Aus Code Facts abgeleitet (O-1302, O-1306)
        context = ApplicationProvider.getApplicationContext();
        prefs = context.getSharedPreferences("test_prefs", Context.MODE_PRIVATE);
        prefs.edit().clear().commit();
        
        // Instanziiere reale Klasse
        instance = new <RealClass>(context);
    }
    
    @After
    public void tearDown() throws Exception {
        prefs.edit().clear().commit();
    }
    
    /**
     * TEST-ID: <ID>
     * TYPE: State Change
     * SOURCE: O-1303, O-1305
     */
    @Test
    public void test_<ID>() throws Exception {
        // Precondition
        assertTrue(prefs.getAll().isEmpty());
        
        // Action (exakte Methode aus Code Facts)
        boolean result = instance.setValue("key", "value");
        
        // Assertion (konkret, deterministisch)
        assertEquals(true, result);
        assertEquals("value", prefs.getString("key", null));
    }
}
```

**Pro Test Regeln:**
- Exakt 1 @Test Methode pro TEST-ID
- @Before/@After für State Reset
- SharedPreferences real (nicht gemockt)
- KEINE Interpretation von Expected Output
- Assertions müssen scheitern wenn Code sich ändert

#### iOS (XCTest)

**Template für jede Testklasse:**

```swift
import XCTest
@testable import MobileBrowserV2

/**
 TRACE: TEST_FAMILY_<Feature><Component>
 PHASE: 2 – Test Generation
 SOURCE: 13_test_definition.md
 */
class <Feature><Component>Tests: XCTestCase {
    
    var instance: <RealClass>?
    var userDefaults: UserDefaults?
    
    override func setUp() {
        super.setUp()
        // Aus Code Facts abgeleitet (O-1302, O-1306)
        userDefaults = UserDefaults(suiteName: "test_suite")
        userDefaults?.removePersistentDomain(forName: "test_suite")
        
        instance = <RealClass>(userDefaults: userDefaults!)
    }
    
    override func tearDown() {
        userDefaults?.removePersistentDomain(forName: "test_suite")
        super.tearDown()
    }
    
    /**
     TEST-ID: <ID>
     TYPE: State Change
     SOURCE: O-1303, O-1305
     */
    func test_<ID>() throws {
        // Precondition
        XCTAssertEqual(userDefaults?.dictionaryRepresentation().count, 0)
        
        // Action (exakte Methode aus Code Facts)
        let result = instance?.setValue(key: "key", value: "value")
        
        // Assertion (konkret, deterministisch)
        XCTAssertEqual(result, true)
        XCTAssertEqual(userDefaults?.string(forKey: "key"), "value")
    }
}
```

**Pro Test Regeln:**
- Exakt 1 func test_<ID> pro TEST-ID
- UserDefaults real (nicht gemockt)
- setUp/tearDown für State Reset
- KEINE Interpretation von Expected Output

---

### STEP 4: TRACEABILITY ENFORCEMENT

**Pro Test validiere:**

```
[ ] TEST-ID vorhanden?
[ ] SOURCE: O-130x Referenz vorhanden?
[ ] Entry Point ist echte Methode aus Code?
[ ] Assertion konkret + deterministisch?
[ ] Precondition aufbaubar?

Falls EINES ausfällt → Test nicht generieren, BLOCKER E-0201
```

---

### STEP 5: EDGE CASE & STATE TESTS VALIDATION

**Für EB-* Tests (Edge Branches):**

```
Action MUSS Fehlersituation triggern:
  Beispiel: setValue mit null Wert
  
Assertion MUSS VOR + NACH checken:
  VOR: prefs.contains("key") == false
  NACH: exception thrown OR prefs.contains("key") == true
  
Falls nicht möglich → Quality Report: WEAK
```

**Für SC-* Tests (State Changes):**

```
Assertion MUSS State Transition prüfen:
  NICHT: "value was stored"
  SONDERN: 
    - VOR: storage.isEmpty() == true
    - NACH: storage.contains("key") == true
  
Falls nicht möglich → Quality Report: WEAK
```

---

### STEP 6: OUTPUT – test_implementation.md

**Struktur:**

```markdown
# Test Implementation Summary

## Android
- Tests generiert: <COUNT>
- Dateien: <FILE_PATHS>
- Mapping:
  TEST-SC-001 → src/test/java/com/mobilebrowser/tests/storage/StorageTest.java
  TEST-SC-002 → src/test/java/com/mobilebrowser/tests/storage/StorageTest.java

### Ungenerierbare Tests (mit Grund)
- TEST-EP-005: Entry Point "feature.deprecated()" existiert nicht mehr

## iOS
- Tests generiert: <COUNT>
- Dateien: <FILE_PATHS>
- Mapping:
  TEST-SC-001 → SourceTests/StorageTests.swift
  TEST-SC-002 → SourceTests/StorageTests.swift

### Ungenerierbare Tests (mit Grund)
- TEST-EP-005: Entry Point nicht in Code gefunden

## Statistics
- Total aus 13_test_definition.md: <N>
- Android generiert: <N>
- iOS generiert: <N>
- Fehlgeschlagen: <N> (mit Details)
```

---

### STEP 7: TEST EXECUTION (REAL RUN)

#### ANDROID EXECUTION

**Schritt 1: Build**
```bash
cd android-mobilebrowser
./gradlew clean test --continue
```

**Sammle nach Execution:**
```
- Total tests run: <N>
- Passed: <N>
- Failed: <N>
- Skipped: <N>

Für JEDEN Failed Test:
  - Test-ID
  - Error Message
  - Stacktrace (UNGEFILTERT)
  - Zeile im Code wo Fehler auftrat
```

**Coverage Extraction (wenn verfügbar):**
```
./gradlew jacocoTestReport
Aus: build/reports/jacoco/test/html/
Extrahiere:
- Line Coverage: X%
- Branch Coverage: X%
- Klassen ohne Coverage: [Liste]
```

#### iOS EXECUTION

**Schritt 1: Build & Test**
```bash
cd ios-mobilebrowser
xcodebuild test \
  -scheme MobileBrowserV2 \
  -configuration Debug \
  -destination 'platform=iOS Simulator,name=iPhone 14' \
  -enableCodeCoverage YES 2>&1
```

**Sammle nach Execution:**
```
- Total tests run: <N>
- Passed: <N>
- Failed: <N>

Für JEDEN Failed Test:
  - Test-ID  
  - Error Message
  - Stacktrace (UNGEFILTERT)
  - Zeile im Code wo Fehler auftrat
```

**Coverage Extraction (wenn verfügbar):**
```
Aus Xcode Build Log:
Extrahiere:
- Line Coverage: X%
- Klassen ohne Coverage: [Liste]
```

**Execution Mode:**
- KEIN Stop bei Failures
- Sammle ALLE Outputs
- Dokumentiere auch Build Errors (nicht nur Test Failures)

---

### STEP 8: TEST QUALITY VALIDATION (POST EXECUTION)

**Ziel:** Beurteile ob die generierten Tests tatsächlich robust sind.

**Für JEDEN Test analysiere:**

| Kriterium | Prüfung | Ergebnis |
|-----------|---------|---------|
| **Input Validity** | Precondition aufbaubar? | VALID / WEAK / INVALID |
| **Action Clarity** | Entry Point existiert? | VALID / WEAK / INVALID |
| **Assertion Strength** | Würde Test fehlschlagen wenn Code sich ändert? | VALID / WEAK / INVALID |
| **Determinism** | Läuft Test jedes Mal gleich? | VALID / WEAK / INVALID |
| **Platform Alignment** | Test läuft auf deklarierter Platform? | VALID / WEAK / INVALID |

**Entscheidungslogik:**

```
VALID:
  - Alle 5 Kriterien: VALID
  - Test schlägt fehl wenn Behavior sich ändert
  - Test determiniert ausführbar

WEAK:
  - 1-2 Kriterien: WEAK
  - Test läuft aber prüft nicht genug
  - z.B: "prefs.contains('key')" prüft nur Existenz, nicht Wert

INVALID:
  - 3+ Kriterien: WEAK
  - Test prüft nicht das gewünschte Verhalten
  - z.B: nur null-Checks ohne echte Assertions
```

---

### STEP 9: OUTPUT – test_execution_report.md

**Struktur:**

```markdown
# Test Execution Report

## Execution Environment
- Android Version: <V>
- iOS Version: <V>
- Build Date: YYYY-MM-DD HH:MM
- Gradle Version: <V>
- Xcode Version: <V>

## Android Results
- Total Tests: <N>
- Passed: <N>
- Failed: <N>
- Skipped: <N>
- **Success Rate: X%**

### Failed Tests Detail
| TEST-ID | Error | Stacktrace | Root Cause |
|---------|-------|-----------|-----------|
| TEST-SC-001 | NullPointerException | java.lang.NullPointerException at... | Storage nicht initialisiert |

### Code Coverage
- Line Coverage: X%
- Branch Coverage: X%
- Classes Missing Coverage: [Liste]

### Build Status
BUILD SUCCESS / BUILD FAILED

## iOS Results
[Identische Struktur wie Android]

## Traceability Audit
| Category | Count | Coverage |
|----------|-------|----------|
| Entry Points (EP-*) | 15 | 12/15 (80%) |
| State Changes (SC-*) | 20 | 20/20 (100%) |
| State Transitions (ST-*) | 8 | 7/8 (87%) |
| Error Branches (EB-*) | 10 | 9/10 (90%) |
| **TOTAL** | **53** | **48/53 (90%)** |

### Not Covered
- EP-002: Entry Point deprecated
- ST-005: Complex state transition impossible to trigger

## Summary
- Phase 2 Status: COMPLETE / PARTIAL / FAILED
- Tests Ready for Phase 4: YES / NO
- Blockers: [Falls vorhanden]
```

---

### STEP 10: OUTPUT – test_quality_report.md

**Struktur:**

```markdown
# Test Quality Report

## Summary Statistics
- Total Tests Analyzed: <N>
- VALID: <N> (X%)
- WEAK: <N> (X%)
- INVALID: <N> (X%)

## Detailed Analysis

### VALID Tests (ready for RN migration)
| TEST-ID | Reason | Migration Ready |
|---------|--------|-----------------|
| TEST-SC-001 | Deterministic, all assertions strong | YES |
| TEST-SC-002 | Precondition clear, assertion on return value | YES |

### WEAK Tests (need attention)
| TEST-ID | Issue | Recommendation | Migration Ready |
|---------|-------|-----------------|-----------------|
| TEST-EP-001 | Only checks null, not actual value | Strengthen assertion | PARTIAL |
| TEST-EB-003 | Precondition hard to setup | Document manual setup | PARTIAL |

### INVALID Tests (cannot use)
| TEST-ID | Issue | Reason | Migration Ready |
|---------|-------|--------|-----------------|
| TEST-ST-005 | State transition impossible to trigger | State machine too complex | NO |

## Recommendations
1. [Spezifische Empfehlung für jeden WEAK/INVALID Test]
2. [Patterns die wiederkehrend Probleme verursachen]

## Migration Status for Phase 4
- Tests VALID: <N> (ready)
- Tests WEAK: <N> (can migrate with flags)
- Tests INVALID: <N> (skip in Phase 4)
```

---

## REGELN

### Code Generation
- Jede Testmethode = exakt 1 Test aus 13_test_definition.md
- Klasse = reale Klasse aus code_facts.md (KEINE Mocks für Logik)
- Precondition = testable (setUp ermöglicht es)
- Action = echte Methode aus Code Facts
- Assertion = konkret, auf Wert nicht auf Existenz

### Assertion Standards
**NICHT erlaubt:**
```java
assertTrue(result);           // Viel zu generisch
assertNotNull(prefs);         // Existenz ist nicht aussagekräftig
assertTrue(value.length() > 0);  // Implizite Logik
```

**ERLAUBT:**
```java
assertEquals(true, result);   // Expliziter Wert
assertEquals("stored_value", prefs.getString("key", null));
assertEquals(1, prefs.getInt("count", 0));
```

### Test Reihenfolge
- MUSS execution_contract.md von Phase 1 respektieren
- Wenn Test A Precondition für Test B ist → klar dokumentieren

### Platform Spezifität
- Wenn Test nur auf Android läuft (aus 13_test_definition.md) → NICHT in iOS erstellen
- Wenn Test nur auf iOS läuft → NICHT in Android erstellen
- Wenn "Both Plattformen" → BEIDE Versionen mit ggf. plattformspezifischen Setup

### Storage Handling
- Android: SharedPreferences REAL (nicht gemockt)
- iOS: UserDefaults REAL (nicht gemockt)
- setUp(): Storage zurücksetzen
- tearDown(): Storage aufräumen

---

## VALIDATION (BLOCKING)

| Regel | Prüfung | Fehler |
|------|---------|--------|
| V-0701 | Für JEDEN Test in 13_test_definition.md MUSS eine Testmethode existieren | E-0201 |
| V-0702 | Jede Testmethode MUSS eine Expected Output Assertion haben | E-0201 |
| V-0703 | Jede Assertion MUSS konkret sein (nicht "not null") | E-0201 |
| V-0704 | Jeder SC-* Test MUSS State VOR NACH prüfen | E-0201 |
| V-0705 | Kein Test ohne SOURCE: O-130x Referenz | E-0201 |
| V-0706 | Android Tests MÜSSEN ausführbar sein (kompilierbar) | E-0202 |
| V-0707 | iOS Tests MÜSSEN ausführbar sein (kompilierbar) | E-0202 |
| V-0708 | Execution Report MUSS Rohdaten (nicht interpretiert) enthalten | E-0203 |
| V-0709 | Test Quality Report MUSS für JEDEN Test eine Klassifikation haben (VALID/WEAK/INVALID) | E-0201 |
| V-0710 | VALID Tests: >= 80% der Tests nach Ausführung | E-0203 |

---

## FEHLERFALL

| Fehler Code | Situation | Behandlung |
|-------------|-----------|-----------|
| E-0201 | Test nicht generierbar (Entry Point nicht gefunden, Assertion nicht konkret) | Dokumentiere in test_implementation.md, Flag als SKIPPED |
| E-0202 | Android/iOS Build fehlgeschlagen | STOP. Zeige Build Errors, gib nicht weiter |
| E-0203 | Zu viele Invalid Tests (< 80% VALID) | Warnung in Report, aber fortsetzen zu Phase 4 |

---
