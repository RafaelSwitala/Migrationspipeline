# PHASE 6 – REACT NATIVE MIGRATION (FEATURE IMPLEMENTATION)

## ZIEL
Implementiere vollständigen, produktionsreifen React Native Code basierend auf behavior_spec.md und mapping.md.

---

## INPUT

* mapping.md (RN Target teilweise oder TBD)
* behavior_spec.md
* test_spec.md
* intake.md
* feature_dependencies.md (falls vorhanden)

* base\output_rules.md
* base\validation_rules.md
* base\validation_check.md
* base\error_rules.md

---

## OUTPUT
* Output 1: O-0801
* Output 2: O-0902
* Output 3: O-1001

---

## EXECUTION STEPS

### 1. ARCHITECTURE SETUP

Verwende die Projektstruktur aus ./base/architecture.md

### 2. DEPENDENCY INTEGRATION (PFLICHT)

### 3. CODE GENERATION

Implementiere:

---

## REGELN

* Kein Pseudocode
* Keine TODOs
* Keine unimplementierten Funktionen
* Jeder Behavior MUSS implementiert sein  
* Jede Funktion MUSS aus Legacy Code ableitbar sein  
* Storage: AsyncStorage oder SecureStore verwenden
* Fehlerbehandlung: MUSS vorhanden sein

Wenn feature_dependencies.md existiert:

* REUSE MAPPING strikt einhalten
* EXISTIERENDE Services verwenden
* KEINE neuen Implementierungen bei vorhandener Lösung

---

## VALIDATION (BLOCKING)

Angewendete Regeln:

* V-0801 – Behaviour Not Implemented
* V-0802 – Mapping Incomplete
* V-0803 – Duplicate Services
* V-0804 – Dependency Rule Violation
* V-0805 – Code Integrity

* VC-0502 – Migration Completion Criteria

---

## FEHLERFALL

Angewendete Regeln:

* E-0301 – RN Migration Failed

---