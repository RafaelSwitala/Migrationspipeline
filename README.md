# AI Context: Legacy iOS/Android to React Native Expo

Dieses Repository ist der gemeinsame Arbeitskontext fuer eine featureweise Migration von zwei Legacy-Codebasen nach React Native Expo. Es enthaelt Regeln, Phasenbeschreibungen, Contracts und Artefakt-Templates. Es enthaelt keinen Runtime-Code der Ziel-App.

## Ziel-Layout

Die Projekte sollen als Geschwisterordner liegen:

```text
parent/
  ai-context/
  ios-mobilebrowser/
  android-mobilebrowser/
  rn-e-mobilebrowser/
```

## Prompt-Workflow

Pro Feature wird jede Phase einzeln gestartet und danach manuell geprueft:

```text
Wende Phase 1 auf das Feature <FEATURE_NAME> an.
Wende Phase 2 auf das Feature <FEATURE_NAME> an.
Wende Phase 3 auf das Feature <FEATURE_NAME> an.
Wende Phase 4 auf das Feature <FEATURE_NAME> an.
Wende Phase 5 auf das Feature <FEATURE_NAME> an.
```

Die Schreibweise mit Phasendatei ist ebenfalls gueltig:

```text
Wende Phase 1 (1_context_build.md) auf das Feature <FEATURE_NAME> an.
```

`<FEATURE_NAME>` wird als slug in `artifacts/<feature-slug>/...` verwendet, zum Beispiel `storage-config` oder `login`.

Der Prompt ist nur der Ausloeser im Chat. Er ist kein Datei-Input. Die Phasendateien beschreiben stattdessen die Runtime-Parameter, Quellen, Templates und Zielartefakte.

## Wichtige Leitplanken

- Phase 1 ist der einzige fachliche Legacy-Discovery-Schritt.
- Phase 2 darf Legacy-Code nur fuer Testplatzierung, Imports und Buildmechanik oeffnen, nicht fuer neue fachliche Ableitungen.
- Phase 3 bis 5 duerfen fachliches Verhalten nur aus Phase-1-Artefakten ableiten.
- Phase 5 veraendert keinen Code. Sie validiert und erzeugt vergleichbare Ergebnisse fuer die Bachelorarbeit.
- Unit Tests sind der Scope. E2E-, UI-Automation- und manuelle Smoke-Tests sind ausserhalb dieses Kontexts.

## Zentrale Dateien

- `contracts/phase_contract.md`: Pflichtstruktur fuer jede Phase.
- `contracts/migration_contract.md`: End-to-end-Vertrag der Migration.
- `rules/id_registry.md`: ID-System, Artefaktliste und Statuswerte.
- `rules/*.md`: Wiederverwendbare Regeln.
- `base/*.md`: Zielarchitektur, Constraints, Testing und Evaluationsmetriken.
- `templates/*.template.md`: leere Vorlagen, die kopiert und im Artefaktordner ausgefuellt werden.
- `artifacts/`: Ergebnisse einzelner KI-Laeufe, getrennt nach Feature, Agent und Run.
- `phases/*.md`: Ausfuehrungsanweisungen fuer die fuenf Phasen.

Hinweis: Unnummerierte alte Feature-Artefakte in `features/` sind historisches Material. Fuer neue Migrationen gelten die nummerierten Artefakte aus `rules/id_registry.md` und der Ablagepfad unter `artifacts/`.

## Artefakt-Ablage

Jeder Agent schreibt in einen eigenen Run-Ordner:

```text
artifacts/
  <feature-slug>/
    <agent-id>/
      <run-id>/
        run_metadata.md
        phase_1/
        phase_2/
        phase_3/
        phase_4/
        phase_5/
```

`agent-id` ist zum Beispiel `codex`, `github-copilot`, `cursor`, `claude` oder `google-antigravity`. Wenn ein Agent keine ID kennt, verwendet er `unknown-agent` und dokumentiert das in `run_metadata.md`.
