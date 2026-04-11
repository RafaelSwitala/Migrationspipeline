# Migration Protocol (verbindlicher Ablauf)

Dieses Dokument definiert den verbindlichen Ablauf für die Migration eines Features.

Alle Schritte sind strikt einzuhalten.

---

## 1. Feature-Analyse

- Analysiere iOS- und Android-Implementierung
- Identifiziere:
  - Gemeinsame Logik
  - Unterschiede
  - Abhängigkeiten
- Leite das funktionale Verhalten ab

---

## 2. Ableitung der Verhaltensspezifikation

- Extrahiere das erwartete Verhalten
- Nutze:
  - behavior_spec.md
  - vorhandenen Code
- Ziel:
  Plattformunabhängige Beschreibung des Features

---

## 3. Erstellung von Legacy-Tests

Für beide Plattformen separat:

### iOS (ios-mobilebrowser)
- Erstelle Unit-Tests basierend auf dem Verhalten

### Android (android-mobilebrowser)
- Erstelle Unit-Tests basierend auf dem Verhalten

Ziel:
- Tests definieren das Referenzverhalten („Ground Truth“)

---

## 4. Validierung der Legacy-Systeme

- Führe alle Tests aus
- Stelle sicher:
  - Alle Tests bestehen

Wenn Tests fehlschlagen:
→ Migration abbrechen

---

## 5. KI-gestützte Transformation

- Implementiere das Feature in:
  React Native (Expo, TypeScript)

Regeln:
- Funktionale Äquivalenz
- Keine zusätzlichen Features
- Architektur einhalten

---

## 6. Migration der Tests

- Übertrage die Testfälle nach React Native (Jest)

Ziel:
- Identisches Verhalten wird geprüft

---

## 7. Validierung der React-Native-Implementierung

- Führe alle Tests aus

Bewertung:
- Tests bestehen direkt → hohe Qualität
- Tests bestehen nach Anpassung → akzeptabel
- Tests schlagen fehl → fehlerhaft

---

## 8. Manuelle Prüfung

- Überprüfe:
  - Funktionalität
  - Edge Cases
  - Verhalten im UI

---

## 9. Dokumentation & Evaluation

- Dokumentiere: (Nutze migration_report.md)
  - Zeitaufwand
  - Probleme
  - Fehler
  - Lösungen
  - Qualität der KI-Ergebnisse

---

## Wichtige Regeln

- Keine Schritte überspringen
- Keine Annahmen außerhalb des Kontexts
- Tests sind die einzige Quelle der Wahrheit