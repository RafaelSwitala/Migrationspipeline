# PHASE 2 – TEST GENERATION EXECUTION

## ZIEL
Erzeuge eine vollständig deterministische test_spec.md basierend auf behavior_spec.md und intake.md.
Erzeuge deterministische, ausführbare Testklassen für Android und iOS basierend auf test_definition.md und führe diese vollständig aus. Dokumentiere ausschließlich reale Ergebnisse.

---

## INPUT

* Legacy Code:
  - Android: android-mobilebrowser/app/src
  - iOS: ios-mobilebrowser/Source

* base\output_rules.md
* base\validation_rules.md
* base\validation_check.md
* base\error_rules.md
* code_facts.md
* execution_contracts.md
* traceability_matrix.md

* Output 1: O-0501

---

## OUTPUT
Es müssen folgende Dateien vollständig erzeugt werden:

* features/<FEATURE_NAME>/21_test_implementation.md
* features/<FEATURE_NAME>/22_test_execution_report.md
features/<FEATURE_NAME>/23_test_quality_report.md
* Testklassen für Android
* Testklassen für iOS

---

## EXECUTION STEPS

### 1. TEST FILE GENERATION

Für JEDEN Test aus 13_test_definition.md:

#### Android
Erzeuge Datei: android-mobilebrowser/app/src/test/java/.../<TestClassName>.java

*Regeln*
* Framework: JUnit4
* Naming:
  - Klasse: <Feature><Component>Test
  - Methode: test_<TEST-ID>()
* Jede Testmethode mappt EXACT 1:1 auf Test-ID aus 13_test_definition.md

*Pflicht*
* Verwende reale Klassen aus code_facts.md
* Verwende echte Methoden (KEINE mocks außer notwendig)
* SharedPreferences MUSS real oder via Instrumentation sein
* Reihenfolge MUSS execution_contracts.md entsprechen

#### iOS
Erzeuge Datei: ios-mobilebrowser/SourceTests/<TestClassName>.swift

*Regeln*
* Framework: XCTest
* Naming:
    - Klasse: <Feature><Component>Tests
    - Methode: test_TEST_ID()

*Pflicht*
* Verwende reale Klassen (z.B. QRCodeSettings)
* Wenn Implementierung fehlt: Test MUSS fehlschlagen (kein Mocking der Logik!)

---

### 2. TRACEABILITY ENFORCEMENT

Jeder Test MUSS enthalten:
* TRACE, 
* TEST-ID: TEST-XXXX
* *SOURCE: O-130X / SC-X / ST-X / EP-X

Wenn keine Quelle vorhanden → BLOCKER (V-0102)

---

### 3. ASSERTION REGELN

Jede Assertion MUSS:
* deterministisch sein
* konkreten Wert prüfen
* KEIN:
    - "not null" ohne Kontext
    - "should work"

---

### 4. EDGE CASE TESTS

Für jeden EB-* Test:
* MUSS explizit Fehlerzustand erzeugen
* MUSS Zustand VOR und NACH prüfen

---

### 5. STATE TESTS

Für jeden SC-* Test:
* MUSS Zustand ändern
* MUSS Transition validieren

---

### 6. IMPLEMENTATION OUTPUT

*Output*: test_implementation.md
*Struktur*: TEST IMPLEMENTATION SUMMARY

*Android*:
* Anzahl Tests
* Dateien erstellt
* Mapping TEST-ID → Datei

*iOS*:
* Anzahl Tests
* Fehlende Implementierungen
* Mapping TEST-ID → Datei

---

### 7. TEST EXECUTION (REAL RUN)

#### ANDROID EXECUTION
cd android-mobilebrowser
./gradlew test

*Pflicht*
* KEIN Stop bei Fehlern
* Sammle:
    - Anzahl Tests
    - Passed
    - Failed
    - Stacktraces

#### iOS EXECUTION
cd ios-mobilebrowser
xcodebuild test -scheme MobileBrowserV2 \
-destination 'platform=iOS Simulator,name=iPhone 14'

*Pflicht*
* Sammle:
    - Anzahl Tests
    - Passed
    - Failed
    - Build Errors

#### COVERAGE EXTRACTION

Wenn verfügbar:
* Android: JaCoCo Report aus build/reports/jacoco/
* iOS: xccov oder xcodebuild coverage

*Extrahiere*
* % Coverage
* nicht getestete Klassen

---

### 8. TEST QUALITY VALIDATION (POST EXECUTION)

*Ziel*
Prüfe ob die generierten Tests tatsächlich valide sind und Fehler im Code erkennen würden. Verwende V-1001 bis V1021.

*Output*
* features/<FEATURE_NAME>/23_test_quality_report.md

Für jeden Test:

* Analysiere:
   - Input
   - Action
   - Assertion

* Simuliere Code-Manipulationen

* Entscheide:
   - VALID
   - WEAK
   - INVALID

* Dokumentiere im test_quality_report.md

---

### 9. RESULT COLLECTION
* Output: test_execution_report.md

*Struktur*
* Tests total:
* Passed:
* Failed:
* Failed Tests:
    - TEST-ID:
    - Error:
    - Stacktrace:
* Build Errors:
    - Datei:
    - Fehler:

*Coverage*
* Android: %
* iOS: %

*Traceability Coverage*
Anzahl Tests vs:
* EP:
* SC:
* ST:
* EB:

Nicht abgedeckt:
* Liste

*Raw Logs*
* ungefiltert
* Regeln
    - KEINE Interpretation
    - KEINE Optimierung
    - KEIN Fixing von Code
* Sondern:
    - Generieren
    - Ausführen
    - Dokumentieren

---

## REGELN

* Kein generischer Text
* Keine unkonkreten Assertions
* Kein „should work“

* Jede Action MUSS reale Methode sein  
* Jeder Expected Output MUSS deterministisch sein  
* Jeder Test MUSS aus Code ableitbar sein

---

## VALIDATION (BLOCKING)

Angewendete Regeln:

* V-0102 – Behaviour Without Source
* V-0701 – Missing Tests
* V-0702 – Missing Expected Output
* V-0703 – Ambiguous Tests
* V-0704 – State Coverage
* V-0710
* V-0711
* V-0712
* V-0713
* V-0714
* V-0715
* V-0716
* V-0717
* V-0718

* VC-0203 Test Completion Criteria

---

## FEHLERFALL

Angewendete Regeln:

* E-0201 – Test Invalid

---