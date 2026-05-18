# Feature Workspace

Dieses Verzeichnis enthaelt alte Referenzen und optionale globale Feature-Uebersichten. Neue Artefakte der fuenf Migrationsphasen liegen in `artifacts/<feature-slug>/<agent-id>/<run-id>/`.

Bestehende unnummerierte Artefakte wie `intake.md`, `behavior_spec.md`, `mapping.md` oder alte `_golden_example`-Dateien sind Legacy-Material. Neue Phasenlaeufe verwenden nur die nummerierten Artefakte aus `rules/id_registry.md`, ausser der Nutzer fordert explizit eine Altanalyse an.

## Neue Artefaktordner

```text
artifacts/
  <feature-slug>/
    <agent-id>/
      <run-id>/
        run_metadata.md
        phase_1/
          11_feature_analysis.md
          12_code_facts.md
          13_test_definition.md
          14_migration_mapping.md
          15_execution_contract.md
          16_traceability_matrix.md
        phase_2/
        phase_3/
        phase_4/
        phase_5/
```

## Workflow

Jede Phase wird einzeln gepromptet und danach reviewed:

```text
Wende Phase 1 auf das Feature <FEATURE_NAME> an.
Wende Phase 2 auf das Feature <FEATURE_NAME> an.
Wende Phase 3 auf das Feature <FEATURE_NAME> an.
Wende Phase 4 auf das Feature <FEATURE_NAME> an.
Wende Phase 5 auf das Feature <FEATURE_NAME> an.
```

Optional kann der Dateiname genannt werden, zum Beispiel:

```text
Wende Phase 1 (1_context_build.md) auf das Feature <FEATURE_NAME> an.
```

## Status

Erlaubte Statuswerte stehen in `rules/id_registry.md`:

- `NOT_STARTED`
- `IN_PROGRESS`
- `READY_FOR_REVIEW`
- `BLOCKED`
- `FAILED`
- `COMPLETE`

## Review-Regel

Die naechste Phase soll erst starten, wenn die vorherige Phase mindestens `READY_FOR_REVIEW` ist und keine blockierenden `UNKNOWN`-Werte offen sind.
