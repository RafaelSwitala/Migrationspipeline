# Templates

Diese Dateien sind leere Vorlagen. Ein Agent darf sie lesen und in einen Run-Ordner unter `artifacts/<feature-slug>/<agent-id>/<run-id>/phase_<n>/` kopieren. Templates selbst duerfen nie ausgefuellt oder ueberschrieben werden.

Pflicht:

- Header nach `OUT-001`
- stabile IDs nach `rules/id_registry.md`
- Quellen nach `REF-002`
- keine leeren Pflichtfelder

## Copy Rule

Beim Start einer Phase werden die passenden `.template.md` Dateien in den Run-Ordner kopiert:

```text
templates/11_feature_analysis.template.md
-> artifacts/<feature-slug>/<agent-id>/<run-id>/phase_1/11_feature_analysis.md
```

Erst die kopierte Datei wird ausgefuellt.
