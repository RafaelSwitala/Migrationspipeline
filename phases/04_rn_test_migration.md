# PHASE 7 – RN TEST MIGRATION & EXECUTION

## ZIEL
Migriere alle Legacy Tests nach React Native und führe sie aus.

---

## INPUT

* Legacy Tests (Android + iOS)
* test_spec.md
* behavior_spec.md
* RN Code (Phase 6)

* base\output_rules.md
* base\validation_rules.md
* base\validation_check.md
* base\error_rules.md

---

## OUTPUT
* Output 1: O-0802
* Output 2: O-0803

---

## EXECUTION STEPS

### 1. TEST MAPPING

### 2. TEST IMPLEMENTATION

Erstelle Tests in:

* src/**tests**/

Framework:

* Jest
* React Native Testing Library

### 3. TEST RULES

---

### 4. READINESS CHECK

### 5. EXECUTION

npm test

### 6. RESULT COLLECTION

---

## VALIDATION (BLOCKING)

Angewendete Regeln:

* V-0706 – RN Test Count Validation
* V-0709 – Test-Behaviour Mismatch
* V-0802 – Mapping Incomplete

* VC-0503 - Test Migration Completion Check
* VC-0601 - Readiness Check
* VC-0603 - Readiness Status

---

## REGELN
* Kein Stop bei Testfehlern
* Keine Interpretation
* Nur Rohoutput dokumentieren

Jeder Test MUSS:

* genau einen Legacy Test referenzieren
* eine Behavior ID referenzieren
* identische Inputs verwenden
* identische Expected Outputs prüfen

EXECUTION HINWEIS

Wenn Ausführung nicht möglich:

→ dokumentiere: "Execution not possible in environment – simulated result"

---

## FEHLERFALL

Angewendete Regeln:

* E-0302 – RN Test Migration Failed

---