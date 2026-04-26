# START HERE – MIGRATION EXECUTION SPEC

## OVERVIEW

Diese Datei ist die **einzige Ausführungsdefinition** für die Migration.

* Alle Phasen sind **verpflichtend**
* Reihenfolge ist **fix**
* Keine Interpretation erlaubt

---

# PHASE MODEL

| Phase | Name                | Output               | Fehler          |
| ----- | ------------------- | -------------------- | --------------- |
| 1     | Code Discovery      | Dateiliste           | STOP            |
| 2     | Intake Extraktion   | Validierung          | STOP            |
| 2.5   | Feature Dependency  | Metrik-Struktur      | STOP            |
| 3     | Context derivation  | intake.md            | STOP            |
| 4     | Test definition     | 6 Dateien            | STOP            |
| 5     | Test Implementation | test_spec.md         | STOP            |
| 6     | RN-Expo Migration   | iOS + Android Tests  | STOP (BLOCKING) |
| 7     | RN-Test Migration   | RN Code + mapping.md | STOP            |
| 8     | Final Validation    | RN Tests             | STOP            |

Hier ist Output und Fehler noch nicht korrekt.

---

# GLOBAL RULES

## 1. STRICT SCOPE

Nur `<FEATURE_NAME>` verarbeiten.

Andere Features:
→ IGNORE
→ Wenn notwendig → STOP

---

## 2. REFERENCE REQUIREMENT

Jede Aussage MUSS enthalten:

* Datei
* Methode
* Zeile

Format:
[iOS: File.swift:method():10-20]

Fehlt Referenz:
→ STOP

---

## 3. NO ASSUMPTIONS

Verboten:

* Raten
* Interpretieren
* Ergänzen

Fehlende Info:
→ STOP

---

## 4. SOURCE OF TRUTH

Nur erlaubt:

* ios-mobilebrowser/Source
* android-mobilebrowser/app/src
* features/<FEATURE_NAME>/

---

## 5. HARD STOP

Bei Fehler:

* Execution sofort stoppen
* Nur Fehler + Lösung ausgeben

---

# PHASE DETAILS

---

## PHASE 1 – CODE DISCOVERY

DISCOVERY METRICS

* Dateien gesamt: X
* Relevante Dateien: X
* Ignorierte Dateien: X

Durchsuche:

* ios-mobilebrowser/Source → .swift
* android-mobilebrowser/app/src → .kt/.java

Output:

* Pfad
* Plattform
* Relevanz
* Zeilen

Keine Dateien:
→ STOP

Validiere:

* Phasen stimmen
* Dateien definiert
* Regeln konsistent
* Pfade korrekt

Fehler:
→ STOP

---

## PHASE 2 – INTAKE EXTRACTION

Ziel:
Befülle `intake.md` vollständig durch **direktes Lesen des Legacy-Codes**.

---

## EXTRACTION QUALITY

* Unklare Stellen: X
* Fehlende Referenzen: X
* Mehrdeutige Logikstellen: X

---

## INPUT

* Dateien aus PHASE 1
* iOS: ios-mobilebrowser/Source
* Android: android-mobilebrowser/app/src

---

## AUFGABE

Öffne jede Datei aus der PRE-PHASE und extrahiere:

* FILES
* ENTRY POINTS
* API CALLS
* STORAGE
* NAVIGATION
* SCOPE

Trage alle Informationen in die bestehende ai-context/feature/<FEATURE_NAME>/intake.md ein.

---

## REGELN

KEINE Interpretation
KEINE Annahmen
KEINE fehlenden Werte schätzen

Jede Zeile MUSS enthalten:

* Datei
* Methode
* Zeile

Nur Informationen verwenden, die direkt im Code stehen

---

## PFLICHT

Alle Tabellen in intake.md müssen vollständig gefüllt sein:

* Keine leeren Felder
* Keine Platzhalter
* STATUS → COMPLETE setzen

---

## VALIDATION

* Alle gefundenen Dateien sind dokumentiert
* Alle Entry Points enthalten
* Alle Storage Keys enthalten
* Alle Navigation Flows enthalten

---

## FEHLERFALL

Wenn Code nicht eindeutig analysierbar:

→ STOP: INTAKE EXTRACTION FAILED

Aktion:
→ Code erneut prüfen
→ Fehlende Referenzen ergänzen


---

## PHASE 2.5 – FEATURE DEPENDENCY

AUSFÜHRUNGSBEDINGUNG

Diese Phase wird nur ausgeführt, wenn: migrated_features_count > 0

Andernfalls:

→ Phase überspringen
→ direkt zu PHASE 3

## INPUT
Aktuelles Feature:
intake.md
behavior_spec.md (falls vorhanden → nur aus Phase 2 ableitbar vorbereitend)
Bereits migrierte Features:
features/<FEATURE_X>/
mapping.md
behavior_spec.md
RN Code (src/)
test_spec.md

## OUTPUT

Erstelle: features/<FEATURE_NAME>/feature_dependencies.md

## AUFGABE
1. IDENTIFIZIERE ABHÄNGIGKEITEN

Vergleiche aktuelles Feature mit ALLEN bereits migrierten Features:

Für jedes Feature prüfen:

STORAGE Nutzung
API Nutzung
Navigation
Shared Logic
State Management
Konfiguration

## DEPENDENCY MATRIX (PFLICHT)
## DEPENDENCY MATRIX

| Current Feature | Depends On Feature | Type | Required | Source |
|----------------|------------------|------|----------|--------|
|                |                  |      |          |        |

## TYPE Definition
HARD → zwingend erforderlich
SOFT → optional / indirekt

## SOURCE (PFLICHT)

MUSS enthalten:

Datei
Methode
Zeile (aus intake.md)

## REUSE ANALYSIS

Identifiziere vorhandene Implementierungen aus RN Code:
## REUSE MAPPING

| Required Functionality | Existing Implementation | Location | Reuse Strategy | Source |
|----------------------|------------------------|----------|----------------|--------|
|                      |                        |          |                |        |

## REUSE STRATEGY
DIRECT → direkt verwenden
EXTEND → erweitern
WRAP → kapseln
NONE → nicht vorhanden

## KONFLIKT-ANALYSE (PFLICHT)

Prüfe:

doppelte Services
doppelte API Clients
widersprüchliche Logik
unterschiedliche Datenmodelle

## CONFLICTS

| Type | Beschreibung | Betroffene Features | Resolution | Source |
|------|-------------|---------------------|------------|--------|
|      |             |                     |            |        |

## RESOLUTION

MUSS eindeutig sein:

„verwende bestehenden Service“
„entferne neue Implementierung“
„merge erforderlich“

## INTEGRATION REQUIREMENTS

- 
- 
- 

## MUSS enthalten:

konkrete Services
konkrete Dateien
konkrete Regeln

## Beispiel:
- Muss src/services/storageService.ts verwenden
- Darf keinen neuen API Client erstellen
- Muss bestehenden Auth State nutzen

---

## PHASE 3 – CONTEXT DERIVATION (FROM INTAKE)

Ziel:
Leite alle weiteren Dateien **ausschließlich aus intake.md ab**.

## REGELN

KEINE Interpretation
KEINE neue Logik
KEINE Annahmen

Nur vergleichen:

intake.md
bestehender RN Code
bestehende mapping.md

## PFLICHT

Alle Tabellen müssen:

vollständig ausgefüllt sein
keine leeren Felder enthalten
referenzierbar sein

## VALIDATION (BLOCKING)
if dependency_detected and no_reuse_mapping:
    STOP

if duplicate_logic_detected and no_resolution_defined:
    STOP

if required_dependency_missing:
    STOP

if tables_incomplete:
    STOP

## INTEGRATIONSREGEL FÜR FOLGEPHASEN

Ab dieser Phase gilt: ALLE Abhängigkeiten aus feature_dependencies.md sind verpflichtend zu berücksichtigen

## WEITERGABE AN PHASE 6

Phase 6 MUSS:

REUSE MAPPING strikt einhalten
CONFLICT RESOLUTION umsetzen
INTEGRATION REQUIREMENTS vollständig erfüllen

## FEHLERFALL

Wenn Abhängigkeiten nicht eindeutig bestimmbar:

→ STOP: DEPENDENCY ANALYSIS FAILED

Aktion:

→ intake.md prüfen
→ vorherige Features prüfen
→ fehlende Referenzen ergänzen

---

## INPUT

* Vollständig ausgefülltes intake.md

---

## AUFGABE

Befülle folgende bestehende Dateien:

* legacy_analysis.md
* mapping.md (RN Target = TBD)
* behavior_spec.md
* feature_description.md
* test_spec.md
* context_status.md

---

## REGELN

KEIN Zugriff mehr auf Code
KEINE neuen Informationen
KEINE Interpretation

Alles MUSS aus intake.md ableitbar sein
Jede Aussage MUSS referenzierbar bleiben

---

## SPEZIALREGEL mapping.md

RN Target bleibt:

→ `TBD (Phase 6)`

---

## VALIDATION

Alle Dateien müssen:

* vollständig sein
* deterministisch sein
* keine Platzhalter enthalten
* referenzierbar sein

---

## CONTEXT DERIVATION ISSUES

- Nicht ableitbare Informationen: X
- STOP ausgelöst: JA/NEIN

---

## FEHLERFALL

Wenn Information nicht aus intake.md ableitbar:

→ STOP: CONTEXT INVALID

Aktion:
→ Zurück zu PHASE 2
→ intake.md ergänzen


---

## PHASE 4 – TEST DEFINITION

Ziel:
Erstelle eine vollständig ausgefüllte `test_spec.md` basierend auf:

* behavior_spec.md
* intake.md

---

## TEST QUALITY

- deterministische Tests: X%
- unklare Expected Outputs: X
- direkte Code-Referenzen: X%

---

## OUTPUT

Befülle die bestehende Datei:

→ features/<FEATURE_NAME>/test_spec.md

---

## ANFORDERUNGEN

Für jeden Behavior:

* Mindestens ein Testfall
* Referenz auf Behavior ID
* Referenz auf Source (Datei + Methode + Zeile)

---

## TESTSTRUKTUR

Jeder Test MUSS enthalten:

* ID (T001, T002, …)
* Behavior Ref (z.B. B005)
* Precondition
* Input
* Action (konkrete Methode aus Code)
* Expected Output
* State (falls relevant)
* Platform (Android / iOS / beide)
* Source (intake.md Referenz)

---

## REGELN

Kein generischer Text
Keine unkonkreten Assertions
Kein „should work“

Jede Action MUSS reale Methode sein
Jeder Expected Output MUSS deterministisch sein
Jeder Test MUSS aus Code ableitbar sein

---

## EDGE CASES

* Müssen explizit definiert werden
* Müssen aus behavior_spec ableitbar sein

---

## VALIDATION

* Jeder Behavior hat mindestens einen Test
* Jeder State ist abgedeckt
* Jeder Test ist eindeutig ausführbar

---

## FEHLERFALL

Wenn ein Test nicht eindeutig aus Code ableitbar ist:

→ STOP: TEST INVALID

Aktion:
→ behavior_spec.md oder intake.md ergänzen


---

## PHASE 5 – TEST IMPLEMENTATION & EXECUTION (BLOCKER)

Ziel:
Erzeuge ausführbare Tests für Android und iOS UND dokumentiere deren Ausführung.

---

## INPUT

* test_spec.md
* behavior_spec.md
* intake.md
* Legacy Code (Android + iOS)

---

## AUFGABE TEIL 1 – TEST IMPLEMENTATION

Erstelle echte Testdateien:

### ANDROID

Pfad:
android-mobilebrowser/app/src/test/java/.../Feature<FEATURE_NAME>Test.java

Framework:

* JUnit4

---

### iOS

Pfad:
ios-mobilebrowser/Tests/Feature<FEATURE_NAME>Tests.swift

Framework:

* XCTest

---

## REGELN

Jeder Test MUSS:

* test_spec.md referenzieren (Test ID)
* behavior_spec.md referenzieren (Behavior ID)
* intake.md referenzieren (Zeilenangaben)
* echte Methoden aus Code verwenden

Mocking:

* erlaubt, aber nur wenn aus Code ableitbar

Kein Pseudocode
Keine leeren Tests
Keine TODOs

---

## TEST IMPLEMENTATION OBSERVATIONS

- Mocking notwendig: JA/NEIN
- Mocking korrekt ableitbar: JA/NEIN
- Probleme bei:
  - Android: ...
  - iOS: ...

---

## AUFGABE TEIL 2 – TEST EXECUTION

Führe die Tests tatsächlich aus:

### Android:

```bash
cd android-mobilebrowser
./gradlew test
```

### iOS:

```bash
cd ios-mobilebrowser
xcodebuild test -scheme MobileBrowserV2 -destination 'platform=iOS Simulator,name=iPhone 14'
```

---

## AUFGABE TEIL 3 – TEST RESULT DOCUMENTATION

Erstelle Datei:

features/<FEATURE_NAME>/test_execution_report.md

---

## FORMAT

# Test Execution Report – <FEATURE_NAME>

## Android Tests

* Executed: true/false
* Total Tests: X
* Passed: X
* Failed: X

### Output

```
<roher Konsolenoutput>
```

---

## iOS Tests

* Executed: true/false
* Total Tests: X
* Passed: X
* Failed: X

### Output

```
<roher Konsolenoutput>
```

---

## FAILED TESTS (falls vorhanden)

| Test ID | Plattform | Fehler |
| ------- | --------- | ------ |

---

## REGELN

KEIN Stop bei Testfehlern
KEINE Interpretation

Nur dokumentieren
Rohdaten beibehalten

---

## VALIDATION (BLOCKING)

```python
if android_tests_count == 0:
    STOP

if ios_tests_count == 0:
    STOP

if behaviors_not_covered:
    STOP
```

---

## WICHTIG

Test-Ausführung ist:

* REAL
* SONST dokumentiert als:

"Execution not possible in environment – results not available"

---

## FEHLERFALL

Wenn Tests nicht generiert werden können:

→ STOP: TEST IMPLEMENTATION FAILED

Aktion:
→ zurück zu Phase 4


---

## PHASE 6 – REACT NATIVE MIGRATION (FEATURE IMPLEMENTATION)

Ziel:
Migration des Legacy-Feature-Codes in vollständigen, produktiven React Native Code.

---

Wenn feature_dependencies.md existiert:

→ MUSS vollständig berücksichtigt werden
→ KEINE neuen Services, wenn bereits vorhanden

---

## INPUT

* mapping.md (RN Target aktuell noch TBD)
* behavior_spec.md
* test_spec.md
* intake.md

---

## AUFGABE

### 1. ARCHITEKTUR DEFINIEREN

Erstelle eine klare RN-Struktur:

* src/screens/
* src/services/
* src/hooks/
* src/components/
* src/types/
* src/utils/

---

### 2. MAPPING VERVOLLSTÄNDIGEN

Fülle mapping.md vollständig:

| Behavior ID | iOS Source | Android Source | RN Target |
| ----------- | ---------- | -------------- | --------- |

RN Target MUSS konkret sein, z.B.:

* src/services/storageService.ts
* src/hooks/useStorage.ts
* src/screens/SettingsScreen.tsx

---

### 3. CODE GENERIEREN

Erzeuge vollständigen TypeScript Code:

#### Services

* Storage
* API Calls
* Business Logic

#### Hooks

* State Management
* Side Effects

#### Screens / Components

* UI
* Event Handling
* Navigation

#### Types

* Interfaces
* Enums

#### Utils

* Constants
* Helper

---

## REGELN

Kein Pseudocode
Keine TODOs
Keine unimplementierten Funktionen

Jeder Behavior aus behavior_spec MUSS implementiert sein
Jede Funktion MUSS nachvollziehbar aus Legacy Code stammen
Fehlerbehandlung MUSS vorhanden sein
AsyncStorage / SecureStore verwenden für Storage

---

## MIGRATION QUALITY

- Behaviors implementiert: X/X
- Fehlende Behaviors: X
- Abweichungen: X

## ARCHITECTURE CONSISTENCY

- Einheitlich: JA/NEIN
- Probleme:
  - doppelte Services
  - Logik im UI

---

## VALIDATION

* mapping.md vollständig
* Alle Behaviors implementiert
* Kein fehlender Code
* Imports korrekt

---

## FEHLERFALL

Wenn ein Behavior nicht implementierbar ist:

→ STOP: RN MIGRATION FAILED

Aktion:
→ behavior_spec oder mapping prüfen


---

## PHASE 7 – RN TEST MIGRATION & EXECUTION

Ziel:
Migration aller Legacy Tests nach React Native UND Ausführung der Tests mit Ergebnisdokumentation.

---

## INPUT

* Legacy Tests (Android + iOS)
* test_spec.md
* behavior_spec.md
* RN Code (Phase 6)

---

## AUFGABE TEIL 1 – TEST MIGRATION

Erstelle React Native Tests:

Pfad:

* src/**tests**/

Framework:

* Jest
* React Native Testing Library

---

## TEST MIGRATION QUALITY

- 1:1 Mapping korrekt: X%
- Abweichungen: X
- Nicht migrierbar: X

---

## REGELN

Jeder RN Test MUSS:

* genau einen Legacy Test referenzieren
* eine Behavior ID referenzieren
* identische Inputs verwenden
* identische Expected Outputs prüfen

---

## TEST MAPPING

Erstelle Mapping:

| Legacy Test | Plattform | RN Test | Behavior |
| ----------- | --------- | ------- | -------- |

---

## AUFGABE TEIL 2 – TEST READINESS CHECK

Bewerte:

* Jest vorhanden
* Expo kompatibel
* AsyncStorage gemockt
* SecureStore gemockt

---

## STATUS

* ✅ HIGH LIKELIHOOD
* ⚠️ CONFIG REQUIRED
* ❌ HIGH RISK

---

## AUFGABE TEIL 3 – TEST EXECUTION

Führe RN Tests aus:

```bash
npm test
```

---

## AUFGABE TEIL 4 – TEST RESULT DOCUMENTATION

Erstelle Datei:

features/<FEATURE_NAME>/rn_test_execution_report.md

---

## FORMAT

# RN Test Execution Report – <FEATURE_NAME>

## Execution

* Executed: true/false
* Environment: local / simulated

---

## Results

* Total Tests: X
* Passed: X
* Failed: X

---

## Output

```
<raw console output>
```

---

## Mapping Coverage

* Legacy Tests: X
* RN Tests: X
* Coverage: X%

---

## Failed Tests (falls vorhanden)

| Test | Behavior | Fehler |
| ---- | -------- | ------ |

---

## READINESS STATUS

* Jest Setup: OK / MISSING
* Expo Compatibility: OK / ISSUE
* Mocks: OK / MISSING

---

## REGELN

Kein Stop bei Testfehlern
Keine Interpretation

Nur dokumentieren
Rohoutput beibehalten

---

## VALIDATION

```python
if rn_tests_count == 0:
    STOP

if mapping_incomplete:
    STOP
```

---

## EXECUTION HINWEIS

Wenn Testausführung nicht möglich:

→ Dokumentiere:

"Execution not possible in environment – simulated result"

---

## FEHLERFALL

Wenn Tests nicht migriert werden können:

→ STOP: RN TEST MIGRATION FAILED

Aktion:
→ test_spec prüfen


---

## PHASE 8 – FINAL VALIDATION, AUTO-FIX & EXECUTION

Ziel:
Validiere den generierten React Native Code, behebe automatisch lösbare Probleme, führe die Anwendung und Tests aus und dokumentiere ALLE Ergebnisse.

---

# TEIL 1 – STATIC VALIDATION

Prüfe:

* TypeScript Fehler
* Fehlende Imports
* Falsche Pfade
* Ungültige Types
* Zirkuläre Dependencies

---

## CONFIG VALIDATION

Prüfe:

* package.json vollständig
* Dependencies installiert
* Expo / React Native kompatibel
* Jest Setup vorhanden

---

## FEHLERBEHANDLUNG

Wenn Fehler gefunden:

→ Versuche automatische Behebung:

Beispiele:

* fehlende Dependencies → `npm install`
* falsche Imports → korrigieren
* fehlende Types → ergänzen
* Config-Probleme → fixen

---

## REGELN

Keine manuellen Annahmen
Keine unbestätigten Fixes

Nur Probleme beheben, die eindeutig identifizierbar sind

---

# TEIL 2 – DEPENDENCY INSTALLATION

Führe aus:

```bash id="y6bq3o"
npm install
```

Dokumentiere:

* Erfolg / Fehler
* Installierte Packages

---

# TEIL 3 – APPLICATION EXECUTION

Führe aus:

```bash id="qk7y8m"
npm start
```

Optional:

```bash id="t6u6kq"
npm run web
```

---

## ERFASSE

* Start erfolgreich: true/false
* Console Output (RAW)
* Errors / Warnings

---

## REGELN

Keine Interpretation
Nur beobachten und dokumentieren

---

# TEIL 4 – TEST EXECUTION (RN)

Führe aus:

```bash id="g4gq1n"
npm test
```

---

## ERFASSE

* Total Tests
* Passed
* Failed
* Raw Output

---

# TEIL 5 – EXECUTION REPORT

Erstelle:

→ features/<FEATURE_NAME>/execution_metrics.md

---

# INHALT

## PHASE METRICS

| Phase | Status | Komplexität | Probleme | Fixes | Dauer (geschätzt) |
| ----- | ------ | ----------- | -------- | ----- | ----------------- |

---

## CONTEXT EFFECTIVENESS

- behavior_spec ausreichend: JA/NEIN
- intake ausreichend: JA/NEIN
- fehlende Infos: ...

---

## AI BEHAVIOR

- deterministisch: JA/NEIN
- inkonsistent: JA/NEIN
- stark variierend: JA/NEIN

---

## ERROR TYPES

| Typ | Anzahl |
|-----|-------|
| Logikfehler | X |
| Architekturfehler | X |
| Kontextfehler | X |
| Halluzination | X |

---

## EFFORT

- automatische Fixes: X
- manuelle Eingriffe nötig: JA/NEIN
- Neugenerierung nötig: JA/NEIN

---

## TEST METRICS

### Legacy

* Android Tests: X
* iOS Tests: X

### React Native

* Total: X
* Passed: X
* Failed: X

---

## BUILD STATUS

* npm install: SUCCESS / FAILED
* npm start: SUCCESS / FAILED
* npm test: SUCCESS / FAILED

---

## ERRORS & FIXES

| Typ | Beschreibung | Fix angewendet |
| --- | ------------ | -------------- |

---

## GENERATED CODE STATS

* Dateien: X
* Zeilen Code: X
* Tests: X

---

## EXECUTION LOGS

### npm install

```id="cq31tw"
<raw output>
```

### npm start

```id="5q2u0z"
<raw output>
```

### npm test

```id="0o4g8o"
<raw output>
```

---

## FINAL STATUS

* Migration: SUCCESS / PARTIAL / FAILED
* Tests: PASSING / PARTIAL / FAILING
* Runtime: WORKING / BROKEN

---

# REGELN

Keine Beschönigung
Keine Interpretation ohne Logs

Alles muss belegbar sein
Rohdaten müssen enthalten sein

---

# FEHLERFALL

Wenn kritische Fehler nicht behebbar:

→ STOP: FINAL VALIDATION FAILED

Dokumentiere:

* Fehler
* betroffene Dateien
* mögliche Ursachen


---

# FILE RULES

## intake.md

* Vollständig
* Referenziert

## behavior_spec.md

* deterministisch
* vollständig

## mapping.md

* alle Behaviors gemappt

## test_spec.md

* exakt ableitbar

## context_status.md

* alles TRUE

---

# MIGRATION CONTRACT

* behavior_spec = Wahrheit
* mapping = Implementierung
* keine neue Logik

---

# FAILURE HANDLING

Bei Fehler:

Erstelle:
features/<FEATURE_NAME>/failure_report.md

Inhalt:

* Phase
* Ursache
* Fehlende Daten
* Fix-Anweisung
