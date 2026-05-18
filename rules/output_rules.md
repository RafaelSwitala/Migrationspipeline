# Output Rules

## OUT-001 Artifact Header

Jedes Artefakt beginnt mit:

```text
# <Title>

| Field | Value |
|---|---|
| Feature | <feature-slug> |
| Phase | P<nr> |
| Artifact ID | <P*-A**> |
| Artifact Path | artifacts/<feature-slug>/<agent-id>/<run-id>/phase_<n>/<file>.md |
| Status | NOT_STARTED / IN_PROGRESS / READY_FOR_REVIEW / BLOCKED / FAILED / COMPLETE |
| Created by | <tool/model if known> |
| Last updated | <ISO timestamp or UNKNOWN> |
```

## OUT-002 Evidence Tables

Tabellen mit fachlichen Aussagen enthalten immer:

```text
| ID | Platform | Finding | Source | Confidence | Notes |
```

`Confidence` ist `HIGH`, `MEDIUM` oder `LOW`. `LOW` darf eine Phase nur passieren, wenn es nicht fachlich entscheidend ist.

## OUT-003 Changed Files And Commands

Phasen mit Code- oder Testaenderungen dokumentieren:

```text
| Type | Path/Command | Result | Notes |
```

## OUT-004 Test Result Format

Testergebnisse verwenden:

```text
| Test ID | Platform | File | Result | Duration | Failure Reason | Source |
```

`Result` ist `PASS`, `FAIL`, `SKIP`, `NOT_RUN` oder `INVALID`.

## OUT-005 Coverage Format

Coverage wird einheitlich dokumentiert:

```text
| Platform | Statements | Branches | Functions | Lines | Tool | Raw Report Path |
```

Wenn ein Tool keine Metrik liefert, wird `N/A` mit Begruendung eingetragen.

## OUT-006 Decision Log

Architektur- oder Testentscheidungen werden als Decision Log dokumentiert:

```text
| Decision ID | Decision | Reason | Source | Alternatives |
```

## OUT-007 Research Metrics

Jede Phase liefert, soweit messbar:

- Dauer
- Anzahl geaenderter Dateien
- Anzahl generierter Tests
- Test-Passrate
- Coverage
- Anzahl Fehler nach Error-ID
- Anzahl manueller Eingriffe
- offene Risiken

## OUT-008 No Placeholder Completion

Keine Tabelle darf mit Platzhaltern wie `TODO`, `TBD`, `...` oder leeren Pflichtfeldern als `COMPLETE` markiert werden.

## OUT-009 Artifact Content Contract

Jedes in einer Phase genannte Output-Artefakt muss die in der Phasendatei beschriebene Pflichtdokumentation enthalten. Der Dateiname allein reicht nie als Output-Definition.
