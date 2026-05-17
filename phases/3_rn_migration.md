# PHASE 3 – REACT NATIVE MIGRATION (FEATURE IMPLEMENTATION)

## ZIEL
Implementiere das Feature von Grund auf in React Native/Expo auf Basis aller Informationen aus Phase 1, OHNE auf Legacy-Code zurückzugreifen.

---

## INPUT

### Aus Phase 1 erforderlich:
* features/<FEATURE_NAME>/11_feature_analysis.md → Feature-Beschreibung, Entry Points
* features/<FEATURE_NAME>/12_code_facts.md → Reale Implementierungsdetails (Klassen, Methoden, Storage, APIs)
* features/<FEATURE_NAME>/14_migration_mapping.md → Component Mapping, Storage Mapping, API Mapping
* features/<FEATURE_NAME>/15_execution_contract.md → Ausführungs-Regeln, Abhängigkeiten

### Aus Phase 2 (optional, für Referenz):
* features/<FEATURE_NAME>/21_test_implementation.md → Test-Struktur (kann helfen beim Design)

### RN Projekt (bereits initialisiert):
* rn-expo-project/ (Basis-Struktur vorhanden, kein Legacy Code)

### Regelwerke:
* base/architecture.md → RN Projektstruktur
* base/output_rules.md
* base/validation_rules.md
* base/error_rules.md

---

## OUTPUT

### Dateien zu erzeugen:
* features/<FEATURE_NAME>/31_rn_architecture_decisions.md
* features/<FEATURE_NAME>/32_rn_implementation_report.md
* features/<FEATURE_NAME>/33_rn_dependency_mapping.md

### Code zu erzeugen:
* rn-expo-project/src/features/<FEATURE>/
  - index.ts
  - types.ts
  - constants.ts
  - services/ (API, Storage, etc.)
  - components/ (UI Components)
  - hooks/ (Custom Hooks)
  - utils/ (Helper Functions)
  - __tests__/ (Später in Phase 4)

---

## EXECUTION STEPS (VERKÜRZT HIER; SIEHE DETAILS UNTEN)

Folge den Schritten STEP 0 bis STEP 10 in exakter Reihenfolge.

---

## REGELN

### Code Generation
- KEINE neue Funktionalität, nur Umsetzung der Legacy Behavior
- Alle Dateien MÜSSEN auf Phase 1 O-XXX Referenzen haben
- KEINE Annahmen über Verhalten – alles muss aus Code Facts ableitbar sein
- KEINE TODOs außer `// TODO: Implement exact [X] from Legacy Code`

### Architecture Choices
- AsyncStorage für nicht-sensitive Daten
- SecureStore für sensitive Daten (nur wenn Legacy Code Verschlüsselung nutzte)
- axios für API calls (bereits Standard in RN)
- Custom hooks für State Management (kein Redux/MobX außer legacy Code nutzte es)

### TypeScript Standards
- Alle Props und State MÜSSEN typisiert sein
- Keine `any` Types außer wo absolut notwendig (mit Kommentar)
- Alle Exports MÜSSEN typisiert sein

### Error Handling
- MUSS basierend auf O-1308 (Legacy Error Handling) implementiert sein
- Try/catch für alle async Operations
- Error state in Components / Hooks

### Platform Divergences
- Falls Feature nur auf iOS existiert → SKIP Android-Implementation
- Falls Feature nur auf Android existiert → SKIP iOS-Implementation
- Falls unterschiedliche Implementierung → Mit Kommentar dokumentieren, warum

---

## VALIDATION (BLOCKING)

| Regel | Prüfung | Fehler |
|------|---------|--------|
| V-0801 | Alle Dateien aus O-1501 Components MÜSSEN implementiert sein | E-0301 |
| V-0802 | Storage Service MUSS alle Keys aus O-1306 implementieren | E-0301 |
| V-0803 | API Service MUSS alle Endpoints aus O-1307 implementieren | E-0301 |
| V-0804 | Alle Components MÜSSEN TypeScript compilieren | E-0301 |
| V-0805 | Keine `any` Types außer mit Kommentar | E-0301 |
| V-0806 | Jede Funktion MUSS auf O-1302 oder O-1310 Referenz haben | E-0301 |
| V-0807 | Error Handling MUSS pro O-1308 implementiert sein | E-0301 |

---

## FEHLERFALL

| Fehler Code | Situation | Behandlung |
|-------------|-----------|-----------|
| E-0301 | RN Migration Failed (Compile Error, Mapping Incomplete) | STOP. Detail im Report. |
| E-0302 | Missing Dependency | STOP. Dokumentiere welche. |
| E-0303 | Behavior nicht mappar (z.B. Platform-specific) | Dokumentiere in Report, FLAG als Partial |

---

## DETAILLIERTE EXECUTION STEPS

[Weitere Sections folgen wie oben in create_file definiert]