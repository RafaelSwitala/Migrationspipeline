# Migration Contract

Dieser Vertrag beschreibt den End-to-end-Ablauf für ein Feature.

## MC-001 Phase Dependency

| Phase | Darf starten wenn |
|---|---|
| P1 | Feature-Prompt und Legacy-Repos verfügbar sind |
| P2 | P1-Artefakte `READY_FOR_REVIEW` oder `COMPLETE` sind |
| P3 | P1-Artefakte `READY_FOR_REVIEW` oder `COMPLETE` sind und RN-Projekt existiert |
| P4 | P2-Artefakte und RN-Projekt existieren |
| P5 | P3-Code, P4-Tests und P2-Ergebnisse existieren |

## MC-002 Legacy Freeze

Phase 1 friert das fachliche Legacy-Verständnis ein. Spätere Phasen dürfen Defizite melden, aber keine neuen fachlichen Fakten stillschweigend ableiten.

## MC-003 Code Ownership

| Ort | Erlaubter Inhalt |
|---|---|
| `ai-context/artifacts/<feature-slug>/<agent-id>/<run-id>/` | Markdown-Artefakte, Reports, Metriken |
| `../ios-mobilebrowser/` | Legacy-iOS-Code und Phase-2-Unit-Tests |
| `../android-mobilebrowser/` | Legacy-Android-Code und Phase-2-Unit-Tests |
| `../rn-e-mobilebrowser/` | RN-Code aus Phase 3 und RN-Tests aus Phase 4 |

## MC-004 Research Integrity

Für den KI-Vergleich werden Fehlschläge nicht versteckt. Jeder Fehler, jede Recovery, jede manuelle Korrektur und jede nicht verfügbare Metrik wird dokumentiert.

## MC-005 No Cross-Agent Drift

Alle KI-Agenten müssen dieselben Phasen, Regeln, Inputs und Artefakt-Namen verwenden. Agent-spezifische Extras dürfen nur in `55_interpretation_notes.md` erläutert werden.

## MC-006 Run Isolation

Jeder Agent-Lauf bekommt einen eigenen Ordner. Ein Agent darf niemals Artefakte eines anderen Agenten oder Run-IDs überschreiben.
