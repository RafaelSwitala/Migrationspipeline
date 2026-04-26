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
