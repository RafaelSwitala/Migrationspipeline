## ZIEL

Identifiziere alle Abhängigkeiten zu bestehenden Features und definiere verbindliche Integrationsregeln.

---

## INPUT
* intake.md
* Alle bestehenden Features:
* mapping.md
* behavior_spec.md
* RN Code (src/)
* test_spec.md

* base\output_rules.md
* base\validation_rules.md
* base\validation_check.md
* base\error_rules.md

---

## OUTPUT
* Output 1: O-0301

---

## EXECUTION STEPS
### 1. DEPENDENCY DETECTION

→ Dependency erstellen

### 2. DEPENDENCY CLASSIFICATION

### 3. REUSE ANALYSIS

### 4. CONFLICT DETECTION

### 5. CONFLICT RESOLUTION (PFLICHT)

### 6. INTEGRATION REQUIREMENTS

---


## REGELN

Diese Phase wird nur ausgeführt, wenn: migrated_features_count > 0

Andernfalls:

→ Phase überspringen
→ direkt zu PHASE 3

---

## VALIDATION (BLOCKING)

Angewendete Regeln:

* V-0101 – Missing References
* V-0501 – Missing Reuse Mapping
* V-0502 – Missing Conflict Resolution
* V-0504 – Empty Integration Requirements

* VC-1001 Dependency Completion Criteria

---

## FEHLERFALL

Angewendete Regeln:

* E-0401 – Dependency Analysis Failed

---