# Artifacts

Hier landen die ausgefuellten Ergebnisse einzelner KI-Laeufe. Dieser Ordner ist bewusst von `templates/` getrennt, damit Vorlagen leer bleiben und mehrere Agenten dasselbe Feature vergleichbar bearbeiten koennen.

## Layout

```text
artifacts/
  _comparison/
    <feature-slug>_comparison.md
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

## Run-ID

Empfohlenes Format:

```text
YYYYMMDD-HHMM-<agent-id>-<feature-slug>
```

Wenn der Agent keine sichere Uhrzeit ermitteln kann, verwendet er `unknown-time-<agent-id>-<feature-slug>` und dokumentiert den Grund in `run_metadata.md`.

## Vergleich

`_comparison/` ist fuer spaetere manuelle oder KI-gestuetzte Auswertung gedacht. Die Rohdaten bleiben in den Run-Ordnern; Vergleichsdateien duerfen nur daraus zitieren.
