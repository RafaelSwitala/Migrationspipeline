# Error Rules

Fehlercodes sind kurz, phasebezogen und eindeutig. Jeder Fehler wird mit `BLOCKING`, `RECOVERABLE` oder `WARNING` bewertet.

| ID | Severity | Bedeutung | Aktion |
|---|---|---|---|
| ERR-REF-01 | BLOCKING | Aussage ohne gültige Quelle | STOP, Quelle ergänzen |
| ERR-P1-01 | BLOCKING | Feature in Legacy-Code nicht auffindbar | STOP, Feature-Scope klären |
| ERR-P1-02 | BLOCKING | Phase-1-Artefakt unvollständig | STOP, fehlende Tabelle/ID ergänzen |
| ERR-P1-03 | BLOCKING | iOS/Android-Verhalten widerspricht sich ohne Mapping | STOP, Divergenz dokumentieren |
| ERR-P2-01 | RECOVERABLE | Legacy-Testumgebung fehlt | Minimales Unit-Test-Setup anlegen, dokumentieren |
| ERR-P2-02 | BLOCKING | Testfall nicht aus Phase 1 ableitbar | STOP, Test entfernen oder Phase 1 ergänzen |
| ERR-P2-03 | BLOCKING | Legacy-Tests schlagen fachlich fehl | STOP nach Dokumentation der Failure Details |
| ERR-P3-01 | BLOCKING | RN-Code kann Mapping aus Phase 1 nicht umsetzen | STOP, Mapping-Lücke dokumentieren |
| ERR-P3-02 | BLOCKING | RN-Projekt oder Dependency fehlt | STOP, fehlende Voraussetzung dokumentieren |
| ERR-P3-03 | BLOCKING | TypeScript/Import-Fehler im RN-Code | STOP, Fehler im Report erfassen |
| ERR-P4-01 | BLOCKING | Legacy-Test ohne RN-Test-Mapping | STOP, Mapping ergänzen |
| ERR-P4-02 | BLOCKING | RN-Test nicht kompilierbar | STOP, Fehler dokumentieren |
| ERR-P5-01 | BLOCKING | RN-Tests önnen nicht ausgeführt werden | STOP, Ausführungsfehler dokumentieren |
| ERR-P5-02 | BLOCKING | Paritätsvergleich unvollständig | STOP, fehlende Messdaten dokumentieren |
| ERR-P5-03 | WARNING | RN-Verhalten weicht dokumentiert ab | Fortsetzen, wenn als bewusste Divergenz markiert |
