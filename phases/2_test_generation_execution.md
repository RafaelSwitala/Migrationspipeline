# Phase 2: Legacy Unit Test Generation And Execution

## Ziel

Erzeuge und führe für `<FEATURE_NAME>` Unit Tests in den bestehenden iOS- und Android-Codebasen aus. Die Tests müssen aus Phase 1 ableitbar sein und eine möglichst hohe sinnvolle Coverage erreichen.

## Input

Runtime-Parameter:

| Parameter | Bedeutung |
|---|---|
| `FEATURE_NAME` | Feature-Bezeichnung aus dem Nutzerprompt |
| `FEATURE_SLUG` | identisch zum Phase-1-Run |
| `AGENT_ID` | identisch zum Phase-1-Run |
| `RUN_ID` | vorhandener Run; falls nicht genannt, den passenden reviewed Run wählen und dokumentieren |

Arbeitsquellen:

- Phase 1: `artifacts/<feature-slug>/<agent-id>/<run-id>/phase_1/`
- Legacy iOS: `../ios-mobilebrowser/`
- Legacy Android: `../android-mobilebrowser/`
- Regeln: `rules/*.md`
- Base: `base/testing.md`, `base/validation_check.md`, `base/evaluation_framework.md`
- Templates: `templates/21_legacy_test_plan.template.md` bis `templates/24_legacy_test_quality.template.md`

Legacy-Code darf in Phase 2 nur für Testplatzierung, Imports, Buildmechanik und Fehlersuche beim Testlauf geöffnet werden. Neue fachliche Ableitungen sind verboten.

## Output

Erzeuge folgende Dateien in `artifacts/<feature-slug>/<agent-id>/<run-id>/phase_2/`:

| Artifact ID | Datei | Pflichtinhalt | Vollständig wenn |
|---|---|---|---|
| P2-A21 | `21_legacy_test_plan.md` | alle `LT-*` Tests aus Phase 1 mit Plattform, Given/When/Then, Quellen, Priorität | jeder Test referenziert Phase-1-IDs |
| P2-A22 | `22_legacy_test_implementation.md` | erzeugte/geänderte Testdateien, Frameworks, Mocks, Test-ID zu Datei | jede Codeänderung ist dokumentiert |
| P2-A23 | `23_legacy_test_results.md` | ausgeführte Commands, Testresultate, Failure Details, Coverage je Plattform | jeder valide Test hat `PASS`, `FAIL`, `SKIP`, `NOT_RUN` oder `INVALID` |
| P2-A24 | `24_legacy_test_quality.md` | Bewertung nach `TEST-006`, Coverage-Gaps, schwache Tests, Failure-Sensitivität | jeder Test ist qualitativ bewertet |

Erzeuge oder aktualisiere Unit-Testdateien in:

- `../ios-mobilebrowser/`
- `../android-mobilebrowser/`

Keine produktiven Legacy-Implementierungen ändern, außer eine minimale testtechnische Sichtbarkeit oder Testkonfiguration ist zwingend notwendig und dokumentiert.

## Regelbindungen

- `PC-001` bis `PC-009`
- `MC-001`, `MC-003`, `MC-004`, `MC-006`
- `GR-001`, `GR-003`, `GR-006`, `GR-007`
- `REF-002`, `REF-003`, `REF-005`
- `TEST-001` bis `TEST-006`
- `OUT-001`, `OUT-003`, `OUT-004`, `OUT-005`, `OUT-007`, `OUT-008`, `OUT-009`
- `VAL-P2-01` bis `VAL-P2-04`
- `ERR-P2-01`, `ERR-P2-02`, `ERR-P2-03`
- `STOP-001` bis `STOP-004`

## Execution Steps

1. Pre-flight prüfen.
   - Stelle sicher, dass alle Phase-1-Artefakte im Run vorhanden sind.
   - Lies `P1-A13` und `P1-A15` für Testfälle, Frameworks, Mocks und Commands.
   - Lege `phase_2/` an.
   - Kopiere die Phase-2-Templates in `phase_2/` und entferne `.template` aus dem Dateinamen.

2. Testplan erstellen.
   - Übertrage alle validen `LT-*` Testideen in `21_legacy_test_plan.md`.
   - Jeder Test bekommt Given/When/Then, Plattform, Quelle und erwartetes Ergebnis.

3. Testumgebung prüfen.
   - Android: vorhandene JUnit-Struktur bevorzugen, sonst minimales Unit-Test-Setup erstellen.
   - iOS: vorhandenes XCTest Target bevorzugen, sonst minimales Unit-Test-Setup erstellen.
   - Jede Recovery wegen fehlender Testumgebung als `ERR-P2-01` dokumentieren.

4. Unit Tests implementieren.
   - Schreibe Tests in die Legacy-Repos.
   - Nutze Test Doubles/Mocks nur für externe Systeme.
   - Keine Tests, die nur Klassenexistenz oder Snapshots ohne Behavior prüfen.

5. Tests und Coverage ausführen.
   - Führe die passenden Android- und iOS-Unit-Testcommands aus.
   - Erfasse Pass/Fail/Skip/Invalid nach `OUT-004`.
   - Erfasse Coverage nach `OUT-005`, wenn verfügbar.

6. Testqualität bewerten.
   - Prüfe jeden Test gegen `TEST-006`.
   - Markiere schwache Tests und erkläre, ob sie verbessert wurden oder bewusst bleiben.

7. Ergebnisse dokumentieren.
   - Füll alle vier Phase-2-Artefakte.
   - Aktualisiere `run_metadata.md` mit Commands, Dauer und offenen Risiken.

## Validationsregeln

| ID | Check | Fehler |
|---|---|---|
| VAL-P2-01 | Jeder Test referenziert Phase-1-IDs | ERR-P2-02 |
| VAL-P2-02 | iOS und Android getestet oder `N/A` belegt | ERR-P2-02 |
| VAL-P2-03 | Alle validen Tests ausgeführt oder Ausführungsfehler dokumentiert | ERR-P2-03 |
| VAL-P2-04 | Coverage erfasst oder `N/A` begründet | ERR-P2-03 |
| VAL-GEN-03 | Keine Platzhalter in `COMPLETE` Artefakten | ERR-P2-02 |

## Fehlerälle

| Fehler | Behandlung |
|---|---|
| ERR-P2-01 | Minimales Unit-Test-Setup erstellen, dokumentieren und fortsetzen |
| ERR-P2-02 | STOP, Test ist nicht aus Phase 1 ableitbar |
| ERR-P2-03 | STOP nach Dokumentation von Testcommand, Output, Failure und vermuteter Ursache |
