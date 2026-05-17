# OUTPUT RULES

---

# CORE PRINCIPLE

* Erstelle alle Dateien im Ordner features/<FEATURE_NAME>/
* Dateiname = <FILE_NAME>

---

# 1. STRUCTURED OUTPUT
## O-0001 STRUCTURED LIST
* Erstelle in <FILE_NAME> folgende strukturierte Tabelle:

| ID | Plattform | Path | Datei | Methode | Zeilen | Beobachtung |
|----|-----------|------|-------|---------|--------|-------------|
|    |           |      |       |         |        |             |

## O-0002 DISCOVERY METRICS
* Dateien gesamt: X
* Relevante Dateien: X
* Ignorierte Dateien: X

## O-0003 DISCOVERY QUESTIONS
* Welches Problem löst das Feature <FEATURE_NAME>? 
* Wer nutzt das Feature <FEATURE_NAME> (User, System, Admin)?
* Was passiert wenn das Feature fehlen würde?
* Welche Use Cases hat das Feature?
* Welche Schritte laufen in welcher Reihenfolge ab?
* Welche Bedingungen und Verzweigungen existieren?
* Welche Daten werden gelesen / geschrieben?
* Wie sehen die Datenstrukturen aus?
* Gibt es Transformationen (Mapping, Encoding)?
* Wer ruft das Feature auf?
* Welche Inputs bekommt es?
* Was gibt es zurück oder verändert es?
* Welche Zustände existieren?
* Wie wird Validität bestimmt?
* Welche Flags steuern das Verhalten?

## O-0004 TECHNICAL REALISATION
* Welche Klassen / Methoden sind beteiligt?
* Gibt es Unterschiede zwischen iOS und Android?
* Gibt es Workarounds oder Hacks?
* Gibt es inkonsistenzen zwischen iOS und Android?
* Gibt es technische Schulden oder veraltete Patterns?

## O-0005 LEGACY ERRORHANDLING
* Was passiert bei ungültigen Eingaben?
* Netzwerkfehler?
* Fehlende Daten?
* Race Conditions / Timing-Probleme?
* Wie wird der Fehler behandelt (Retry, Abbruch, Default-Werte)?

## O-0006 SECURITY AND RISKS
* Werden sensible Daten verarbeitet?
* Gibt es Verschlüsselung oder nur Encoding?
* Gibt es potenzielle Angriffsflächen?

## O-0007 LIFECYCLE AND TIMING
* Wann wird das Feature <FEATURE_NAME> initialisiert?
* Läuft es einmalig oder dauerhaft?
* Läuft es synchron oder asynchron?

## O-0008 DISCOVERY DEPENDENCIES
* Welche anderen Komponenten werden verwendet?
* Externe Systeme (Server, APIs)?
* Frameworks oder Plattform-APIs?

## O-0009 DATA FLOW
* Wo entstehen Daten (Quelle)?
* Welche Transformationen durchlaufen sie?
* Wo werden sie gespeichert?
* Wann und wo werden sie wieder geladen?
* Welche Komponenten greifen auf dieselben Daten zu?

## O-0010 SIDE EFFECTS
* Welche globalen Zustände werden verändert?
* Welche Flags beeinflussen nachgelagerte Logik?
* Welche Aktionen haben indirekte Auswirkungen auf andere Features?
* Gibt es versteckte Abhängigkeiten oder implizite Zustandsänderungen?

---

# 2. BEHAVIOUR SPEC OUTPUT
## O-0101 BEHAVIOUR SPEC
* <FILE_NAME> = behaviour_spec.md
* Alle Tabellen müssen vollständig befüllt werden.
* Erstelle in <FILE_NAME> folgende strukturierte Tabellen und Listen:

### 1. INPUTS
| Name | Typ | Pflicht | Validierung | Source |
|------|-----|---------|-------------|--------|
|      |     |         |             |        |

### 2. OUTPUTS
| Zustand | Beschreibung | Source |
|---------|--------------|--------|
|         |              |        |

### 3. STATES
| State | Beschreibung | Source |
|-------|--------------|--------|
|       |              |        |

### 4. TRANSITIONS
| Von | Event | Nach | Source |
|-----|-------|------|--------|
|     |       |      |        |

### 5. SIDE EFFECTS
| Typ | Beschreibung | Source |
|-----|--------------|--------|
| Storage |          |        |
| Navigation |       |        |
| API |              |        |

### 6. EDGE CASES
| Case | Verhalten | Source |
|------|-----------|--------|
|      |           |        |

---

# 3. MAPPING OUTPUT
## O-0201 MAPPING
* <FILE_NAME> = mapping.md
* Die Tabelle muss vollständig befüllt werden.
* Erstelle in <FILE_NAME> folgende strukturierte Tabelle:

### 1. MAPPING
| Behavior | iOS Source | Android Source | RN Target | Funktion | Hook | Component |
|----------|------------|----------------|-----------|----------|------|-----------|
|          |            |                |           |          |      |           |

---

# 4. FEATURE DESCRIPTION OUTPUT
## O-0301 FEATURE DEPENDENCY
* <FILE_NAME> = feature_dependency.md
* Alle Tabellen müssen vollständig befüllt werden.
* Erstelle in <FILE_NAME> folgende strukturierte Tabellen und Listen:

### 1. DEPENDENCY MATRIX
| Current Feature | Depends On Feature | Type | Required | Source |
|-----------------|--------------------|------|----------|--------|
|                 |                    |      |          |        |

### 2. REUSE MAPPING
| Required Functionality | Existing Implementation | Location | Reuse Strategy | Source |
|------------------------|-------------------------|----------|----------------|--------|
|                        |                         |          |                |        |

### 3. CONFLICTS
| Type | Beschreibung | Betroffene Features | Resolution | Source |
|------|--------------|---------------------|------------|--------|
|      |              |                     |            |        |

### 4. INTEGRATION REQUIREMENTS
- 

### 5. DEPENDENCY CLASSIFICATION
Für jede Dependency:

HARD → zwingend erforderlich
SOFT → optional

### 6. REUSE ANALYSIS

Für jede benötigte Funktionalität:

Prüfe:

existiert bereits im RN Code?

Dann:

DIRECT
EXTEND
WRAP
NONE

### 7. CONFLICT DETECTION

Identifiziere:

doppelte Services
doppelte API Clients
widersprüchliche Logik
unterschiedliche Datenmodelle

### 8. CONFLICT RESOLUTION
Für jeden Konflikt MUSS definiert werden:

eindeutige Lösung

Erlaubte Werte:

USE_EXISTING
REMOVE_NEW
MERGE

### 9. INTEGRATION REQUIREMENTS

Erstelle konkrete Regeln:

konkrete Datei
konkreter Service
konkrete Einschränkung

## O-0302 FEATURE DESCRIPTION
* <FILE_NAME> = feature_description.md

### 1. Beantworte alle Fragen in <FILE_NAME>
* Was sind zentrale Aufgaben des Features <FEATURE_NAME>?
* Welche Workflows sind im Feature <FEATURE_NAME> enthalten?
* Welches Datenmodell nutzt das Feature <FEATURE_NAME>?
* Was sind die Integration Points im Feature <FEATURE_NAME>?
* Welche Android-Plattform-Spezifika hat das Feature <FEATURE_NAME>?
* Welche iOS-Plattform-Spezifika hat das Feature <FEATURE_NAME>?
* Welche Sicherheitsaspekte sind im Feature <FEATURE_NAME> enthalten?
* Wie wird die Fehlerbehandlung im Feature <FEATURE_NAME> realisiert?

---

# 5. CONTEXT STATUS OUTPUT
## O-0401 CREATE INTAKE

* <FILE_NAME> = intake.md
* Alle Tabellen müssen vollständig befüllt werden.
* Erstelle in <FILE_NAME> folgende strukturierte Tabellen und Listen:

### 1. FILES
#### iOS
| Datei | Zweck | Verwendet | Referenzen | Source |
|------|------|-----------|--------------|------- |
|      |      |           |              |        |

#### Android
| Datei | Zweck | Verwendet | Referenzen | Source |
|------|------|-----------|--------------| ------ |
|      |      |           |              | ------ |

### 2. ENTRY POINTS
| Plattform | Datei | Methode | Zeile | Trigger | Test Type | Source |
|-----------|-------|---------|-------|---------|-----------|--------|
|           |       |         |       |         |           |        |

TEST TYPE CLASSIFICATION 
* UNIT
* INTEGRATION
* UI
* SYSTEM
* NETWORK

### 3. API CALLS
| Endpoint | Methode | Datei | Zeile | Verwendung | Source |
|----------|---------|-------|-------|------------|------- |
|          |         |       |       |            |        |

### 4. STORAGE
| Key | Plattform | Zugriff | Datei | Zeile | Source |
|-----|-----------|---------|-------|-------|--------|
|     |           |         |       |       |        |

### 5. NAVIGATION
| Von | Nach | Trigger | Plattform | Quelle | Source |
|-----|------|---------|-----------|--------|--------|
|     |      |         |           |        |        |

### 6. SCOPE
#### in
- 

#### out
- 

Fülle zudem das: EXTRACTION QUALITY
- Unklare Stellen: X
- Fehlende Referenzen: X
- Mehrdeutige Logikstellen: X

### 7. LOGIC
| Datei | Methode | Bedingung | Ergebnis | Zeile | Source |
|-------|---------|-----------|----------|-------|--------|
|       |         |           |          |       |        |

### 8. STATES
| Zustand | Beschreibung | Eintritt | Austritt | Source |
|--------|---------------|----------|----------|--------|
|        |               |          |          |        |

### 9. DATA FLOW
| Quelle | Transformation | Ziel | Datei | Zeile | Source |
|--------|----------------|------|-------|-------|--------|
|        |                |      |       |       |        |

### 10. SIDE EFFECTS
| Aktion | Effekt | Betroffene Komponente | Datei | Zeile | Source |
|--------|--------|----------------------|-------|--------|--------|
|        |        |                      |       |        |        |

### 11. DEPENDENCIES
| Komponente | Typ | Verwendet von | Zweck | Source |
|------------|-----|---------------|-------|--------|
|            |     |               |       |        |

### 12. TEST SPECIFICATION
| Test Case | Input | Steps | Expected State | Expected Storage | Expected UI |
|-----------|------|--------|----------------|------------------|-------------|
|           |      |        |                |                  |             |

### 13. STATE MACHINE
| State | Trigger | Next State | Side Effects |
|-------|---------|------------|--------------|
|       |         |            |              |

### 14. CROSS PLATFORM MAPPING
| Feature | Android | iOS | Shared Logic |
|---------|---------|-----|--------------|
|         |         |     |              |

### 15. TEST HOOKS
| Component | Mockable | How | Risk |
|-----------|----------|-----|------|
|           |          |     |      |

### 16. FUNCTION CONTRACTS
| Method | Input | Output | Side Effects |
|--------|-------|--------|--------------|
|        |       |        |              |

## O-0402 CONTEXT STATUS
* <FILE_NAME> = context_status.md

### 1. Beantworte alle Fragen in <FILE_NAME>
* Wurde die Datei intake.md erstellt und sind alle Inhalte ausgefüllt?
* Wurde die Datei legacy_analysis.md erstellt und sind alle Inhalte ausgefüllt?
* Wurde die Datei feature_description.md erstellt und sind alle Inhalte ausgefüllt?
* Wurde die Datei behavior_spec.md erstellt und sind alle Inhalte ausgefüllt?
* Sind irgendwo Platzhalter enthalten? Wenn ja, wo?
* Sind alle Ausagen referenziert (Datei + Methode + Zeile)?
* Wurde an einer oder mehreren Stellen interpretiert? Wenn ja, welche?
* Gibt es Widersprüchliche Aussagen? Wenn ja, welche?
* Hat jeder Behaviour-Fall mindestens einen Test?
* Ist jeder State getestet?
* Ist jeder Edge Case getestet?
* Ist das Android Verhalten verifiziert (Code + Test)?
* Ist das iOS Verhalten verifiziert (Code + Test)?
* Ist das Verhalten vollständig nachvollziehbar?

## O-0403 CONTEXT DERIVATION ISSUES
* Nicht ableitbare Informationen: X
* STOP ausgelöst: JA/NEIN

---

# 6. TEST SPEC OUTPUT
## O-0501 TEST SPEC
* <FILE_NAME> = test_spec.md
* Die Tabelle muss vollständig befüllt werden.
* Erstelle in <FILE_NAME> folgende strukturierte Tabelle:

### 1. TEST CASES
| ID | Behavior Ref | Precondition | Input | Action | Expected Output | State | Platform | Source |
|----|--------------|--------------|-------|--------|-----------------|-------|----------|--------|
|    |              |              |       |        |                 |       |          |        |

### 2. EDGE CASE TEST
| ID | Case | Expected | Source |
|----|------|----------|--------|
|    |      |          |        |

### 3. STATE COVERAGE
| State | Tested |
|-------|--------|
|       |        |

### 4. TEST QUALITY
- deterministische Tests: X%
- unklare Expected Outputs: X
- direkte Code-Referenzen: X%

---

# 7. TEST IMPLEMENTATION OUTPUT
## O-0601 TEST IMPLEMENTATION
Für jeden Test aus test_spec.md: 

### 1. Datei-Pfade
Erstelle für das Feature <FEATURE_NAME> Testdateien in den Pfaden:
* android-mobilebrowser/app/src/test/
* ios-mobilebrowser/MobileBrowserV2/Source/Test/

### 2. Framework
* JUnit 4 für Android
* XCTest für iOS

### 3. Implementations Regeln
Jeder Test MUSS:
* Test ID referenzieren
* Behavior ID referenzieren
* intake.md Referenzen enthalten
* echte Methoden aus Code verwenden

### 4. Mocking
* nur erlaubt, wenn aus Code ableitbar

### 5. Verboten
* Pseudocode
* TODOs
* leere Tests

---

# 8. TEST RESULT OUTPUT
## O-0701 TEST RESULT
* <FILE_NAME> = test_execution_report.md
* Alle Daten müssen vollständig befüllt werden.
* Erstelle in <FILE_NAME> folgende strukturierte Tabellen und Listen:

### 1. Erfasse folgende Daten nach dem Ausführen eines Android-Tests
* Executed: true/false
* Total Tests
* Passed
* Failed
* Raw Output

### 2. Erfasse folgende Daten nach dem Ausführen eines iOS-Tests
* Executed: true/false
* Total Tests
* Passed
* Failed
* Raw Output

### 3. Erfasse alle Failed Tests
| Test ID | Plattform | Fehler |
| ------- | --------- | ------ |
|         |           |        |

### 4. Beobachtungen der Test Implementation
* Mocking notwendig: JA/NEIN
* Mocking korrekt: JA/NEIN
* Probleme:
* Android: ...
* iOS: ...

### 5. EXECUTION HINWEIS
Wenn Ausführung nicht möglich:
* dokumentiere: "Execution not possible in environment – results not available"

---

# 9. RN CODE OUTPUT
## O-0801 RN-CODE

### 1. ALLGEMEIN
* Migriere alle Behaviours in rn-e-mobilebrowser/src/

### 2. SERVICES
* Storage
* API Calls
* Business Logic

### 3. HOOKS
* State Management
* Side Effects

### 4. SCREENS / COMPONENTS
* UI
* Navigation
* Event Handling

### 5. TYPES
* Interfaces
* Enums

### 6. UTILS
* Helper
* Constants

### 7. BEHAVIOR IMPLEMENTATION
Für JEDES Behavior:

* vollständige Implementierung
* referenzierbar zum Legacy Code
* deterministisch

## O-0802 RN-TEST GENERATION
* <FILE_NAME> = test_mapping.md
* Die Tabelle muss vollständig befüllt werden.
* Erstelle in <FILE_NAME> folgende strukturierte Tabelle:

### 1. TEST MAPPING
Für jeden Legacy Test:
* mappe auf genau einen RN Test
* ordne Behavior ID zu

| Legacy Test | Plattform | RN Test | Behavior |
|-------------|-----------|---------|----------|
|             |           |         |          |

## O-0803 RN-TEST RESULT COLLECTION
* <FILE_NAME> = rn_test_execution_report.md
* Die Tabelle muss vollständig befüllt werden.
* Erstelle in <FILE_NAME> folgende strukturierte Tabelle:

### 1. Erfasse:
* Total Tests
* Passed
* Failed
* Raw Output

### 2. Mapping Coverage
* Legacy Tests: X
* RN Tests: X
* Coverage: X%

### 3. Failed Tests (falls vorhanden)
| Test | Behavior | Fehler |
| ---- | -------- | ------ |
|      |          |        |

---

# 10. MIGRATION REPORT OUTPUT
## O-0901 MIGRATION REPORT
* <FILE_NAME> = migration_report.md
* Die Tabelle muss vollständig befüllt werden.
* Erstelle in <FILE_NAME> folgende strukturierte Tabelle:

### 1. DEPENDENCY INSTALLATION
* Erfolg / Fehler
* installierte Packages

### 2. EXECUTION LOGGING
* Start erfolgreich: true/false
* Raw Output
* Errors / Warnings

### 3. TEST EXECUTION

### 4. CODE GENERATION STATISTICS

| Metric | Count |
|--------|-------|
| Files Generated | |
| Lines of Code | |
| Test Files | |
| Test Cases | |
| Dependencies | |

### 5. GENERATED FILES
- 

### 6. Ready for Integration?

- [ ] YES – Ready for `npm install` + `npm start`
- [ ] NO – See notes below

Notes ( )

### 7. PHASE METRICS

| Phase | Status | Komplexität | Probleme | Fixes |
| ----- | ------ | ----------- | -------- | ----- |
|       |        |             |          |       |

### 8. ERROR TYPES

| Typ | Anzahl |
|-----|-------|
| Logikfehler | |
| Architekturfehler | |
| Kontextfehler | |
| Halluzination | |

### 9. ERRORS & FIXES

| Typ | Beschreibung | Fix angewendet |
| --- | ------------ | -------------- |
|     |              |                |

### 10. ERRORS & FIXES
Total
Passed
Failed

### 11. BUILD STATUS
npm install: SUCCESS / FAILED
npm start: SUCCESS / FAILED
npm test: SUCCESS / FAILED

### 12. ERRORS & FIXES
| Typ | Beschreibung | Fix |

## O-0902 RN MIGRATION QUALITY
Behaviors implementiert: X/X
Fehlende Behaviors: X
Abweichungen: X

---

# 11. ARCHITECTURE OUTPUT
## O-1001 ARCHITECTURE CONSISTENCY
Einheitlich: JA/NEIN
Probleme:
doppelte Services
Logik im UI

---

# 12. EXECUTION LOG OUTPUT
## O-1101 EXECUTION LOGS
npm install
<raw output>

npm start
<raw output>

npm test
<raw output>

---

# 13. FINAL STATUS OUTPUT

## O-1201 FINAL STATUS
Migration: SUCCESS / PARTIAL / FAILED
Tests: PASSING / PARTIAL / FAILING
Runtime: WORKING / BROKEN

---
# 14. CODE-FACTS

## O-1301 FILE REGISTRY

| ID | Plattform | Path | Datei | Typ | Zeilen | Source |
| -- | --------- | ---- | ----- | --- | ------ | ------ |
|    |           |      |       |     |        |        |

## O-1302 METHODS

| Datei | Klasse | Methode | Sichtbarkeit | Parameter | Rückgabe | Zeile | Source | Entry Point | YES/NO |
| ----- | ------ | ------- | ------------ | --------- | -------- | ----- | ------ | ----------- | ------ |
|       |        |         |              |           |          |       |        |             |        |

## O-1303 API CALL DETAILS

| Datei | Methode | Endpoint | HTTP Methode | Request Body | Response Felder | Status Handling | Zeile | Source |
| ----- | ------- | -------- | ------------ | ------------ | --------------- | --------------- | ----- | ------ |
|       |         |          |              |              |                 |                 |       |        |

Wenn nicht vorhanden: → NOT FOUND

## O-1304 STORAGE DETAILS

| Datei | Methode | Storage Typ | Key | Zugriff (read/write) | Default | Zeile | Source |
| ----- | ------- | ----------- | --- | -------------------- | ------- | ----- | ------ |
|       |         |             |     |                      |         |       |        |

## O-1305 NAVIGATION CALLS
| Datei | Methode | Navigation Call | Ziel | Parameter | Bedingung | Zeile | Source |
| ----- | ------- | --------------- | ---- | --------- | --------- | ----- | ------ |
|       |         |                 |      |           |           |       |        |

## O-1306 LOGIC CONDITIONS
| Datei | Methode | Bedingung (Original Code) | Kontext | Zeile | Source |
| ----- | ------- | ------------------------- | ------- | ----- | ------ |
|       |         |                           |         |       |        |

## O-1307 DATA STRUCTURES
| Datei | Struktur | Feld | Typ | Herkunft | Zeile | Source |
| ----- | -------- | ---- | --- | -------- | ----- | ------ |
|       |          |      |     |          |       |        |

## O-1308 FLAGS / VARIABLES
| Datei | Variable | Typ | Initialwert | Verwendung | Zeile | Source |
| ----- | -------- | --- | ----------- | ---------- | ----- | ------ |
|       |          |     |             |            |       |        |

## O-1309 DEPENDENCY CALLS
| Datei | Methode | Abhängigkeit | Typ | Aufruf | Zeile | Source |
| ----- | ------- | ------------ | --- | ------ | ----- | ------ |
|       |         |              |     |        |       |        |

## O-1310 ERROR HANDLING (RAW)
| Datei | Methode | Fehlerfall | Mechanismus | Code Referenz | Zeile | Source |
| ----- | ------- | ---------- | ----------- | ------------- | ----- | ------ |
|       |         |            |             |               |       |        |

## O-1311 EXECUTION FLOW

| Flow ID | Startpunkt | Schritte | Endpunkt | Datei | Source |
|--------|------------|----------|----------|-------|--------|
|        |            |          |          |       |        |

## O-1312 STATE TRANSITIONS

| State | Trigger | Neuer Zustand | Datei | Zeile | Source |
|------|--------|--------------|-------|-------|--------|
|      |        |              |       |       |        |

## O-1313 DATA FLOW LINKS

| Quelle | Ziel | Verbindung | Datei | Zeile | Source |
|--------|------|------------|-------|-------|--------|
|        |      |            |       |       |        |

## O-1314 DATA FLOW (RAW)

| Quelle | Transformation | Ziel | Datei | Zeile | Source |

## O-1315 STATE TRANSITIONS

| Zustand | Eintritt Methode | Austritt Methode | Datei | Source |


---

# 15. TEST_DEFINITION

## O-1401 TEST MAPPING
| Feature ID | Entry Point | Test Type | Input | Expected Output | Source |
| ---------- | ----------- | --------- | ----- | --------------- | ------ |


## O-1402 PLATFORM MIRROR TESTS 
| Test ID | Android Method | iOS Method | Shared Behavior | Source Android | Source iOS |
| ------- | -------------- | ---------- | --------------- | -------------- | ---------- |


## O-1403 STATE EXPECTATIONS
| State | Trigger | Expected Result | Source |
| ----- | ------- | --------------- | ------ |


## O-1404 STORAGE EXPECTATIONS
| Key | Before | After | Trigger | Source |
| --- | ------ | ----- | ------- | ------ |


## O-1405 FAILURE CASES
| Scenario | Input | Expected Error | Source |
| -------- | ----- | -------------- | ------ |

## O-1406 FLOW TESTS

Ziel:
Abbildung deterministischer Multi-Step Ausführungssequenzen basierend ausschließlich auf bestehenden Code Facts.

REGELN:
- Jeder Schritt MUSS auf O-1301 (Entry Point) oder O-1305 (State Change) referenzieren
- KEINE neuen Flows erfinden
- KEINE impliziten Übergänge
- Jeder Flow MUSS vollständig validierbar sein

FORMAT:

| Flow-ID | Steps (ordered) | Initial State (O-1305) | Final State (O-1305) | Validierung |
|--------|----------------|------------------------|----------------------|-------------|

DEFINITION:

Steps:
- Liste von IDs (EP-x, SC-x)
- Reihenfolge ist strikt

Initial State:
- MUSS exakt einem O-1305 Zustand entsprechen

Final State:
- MUSS exakt einem O-1305 Zustand entsprechen

Validierung:
- Muss referenzieren:
  - O-1305 (State Changes)
  - O-1310 (Storage)
  - ggf. O-1308 (Error)

---

# 16. MIGRATION_MAPPING

## O-1501 COMPONENT MAPPING
| Android | iOS | React Native | Behavior Contract |
| ------- | --- | ------------ | ----------------- |


## O-1502 STORAGE MAPPING

| SharedPreferences | UserDefaults | AsyncStorage / SecureStore | Access Type | Behavior |
| ----------------- | ------------ | -------------------------- | ----------- | -------- |


## O-1503 API MAPPING
| UrlUtils | Alamofire | fetch/axios | Behavior |
| -------- | --------- | ----------- | -------- |


## O-1504 UI MAPPING
| ViewController | UIView | React Component | Behavior |
| -------------- | ------ | --------------- | -------- |


## O-1505 STATE MAPPING
| State | Android Source | iOS Source | RN Target State | Trigger Behavior |
| ----- | -------------- | ---------- | --------------- | ---------------- |

## O-1506 CONFLICT RESOLUTION
* Android-only → übernehmen?
* iOS-only → ignorieren?
* Divergent → Feature Flag?

## O-1507 SECURITY TRANSFORMATION RULES

Ziel:
Definition von notwendigen Sicherheitsanpassungen basierend auf bestehenden Code Facts.

REGELN:
- MUSS auf O-1310 referenzieren
- KEINE Annahmen
- Nur wenn Risiko explizit in Code Facts sichtbar ist

FORMAT:

| ID | Source Code Fact | Risiko | Bestehende Implementierung | RN Target | Pflicht |
|----|------------------|--------|----------------------------|-----------|--------|

---

# 17. EXECUTION_CONTRACT

## O-1601 TEST EXECUTION RULES
* Jest / JUnit / XCTest Mapping
* no interpretation
* no fallback logic
* No execution without Source trace validation
* No test without Entry Point mapping
* No RN test without Behavior Contract

## O-1602 RUN ORDER
* Android Tests
* iOS Tests
* RN Tests
* Comparison
* Validation step after each platform

## O-1603 OUTPUT CONTRACT
| Output | Meaning         |
| ------ | --------------- |
| O-0601 | Android Results |
| O-0701 | iOS Results     |
| O-080x | RN Migration    |
| O-090x | Validation      |

- Async Consistency Rules
- Rehydration Rules
- Partial State Handling


## O-1604 COMPARISON RULES
* same input
* same expected output
* difference = defect
* Difference must be traceable to Source or marked as UNRESOLVED
* No semantic interpretation allowed during comparison

---

# 18. TRACEABILITY MATRIX
## O-1701 TRACEABILITY MATRIX

Ziel:
Zentrale Referenz aller Beziehungen zwischen Code, Tests, Migration und Execution.

---

## TRACE TABLE

| Type | ID | Referenziert von | Referenziert zu |
|------|----|------------------|-----------------|

Beispiele:

| EP | EP-1 | T-EP-1, T-FLOW-1 | CS-5, API-4 |
| SC | SC-3 | T-SC-3, T-FLOW-1 | ST-8 |
| ST | ST-1 | T-ST-1 | SM-1 |
| PP | PP-1 | T-PP-1 | CM-3, CM-4 |
| EB | EB-1 | T-EB-1 | AM-1 |

---

# 19. TEST QUALITY REPORT
## O-1801 TEST QUALITY REPORT
* <FILE_NAME> = test_quality_report.md

### 1. SUMMARY
| Metric | Value |
|--------|------|
| Total Tests | |
| Valid Tests | |
| Invalid Tests | |
| Weak Tests | |
| Mutation Resistant Tests | % |

---

### 2. INVALID TESTS (BLOCKER)
| Test-ID | Reason | Rule |
|--------|--------|------|

---

### 3. WEAK TESTS (WARNING)
| Test-ID | Issue | Rule |
|--------|-------|------|

---

### 4. COVERAGE QUALITY
| Type | Coverage |
|------|----------|
| Condition Coverage | % |
| State Coverage | % |
| Error Coverage | % |

---

### 5. FAILURE SENSITIVITY
| Test-ID | Would Fail If | Result |
|--------|---------------|--------|

---

### 6. FINAL RESULT
PASS / FAIL