## DEPENDENCY MATRIX

| Current Feature | Depends On | Type | Required | Source |
|----------------|----------|------|----------|--------|
| Settings       | Storage  | HARD | YES      | intake.md L45 |
| Settings       | Login    | SOFT | NO       | behavior B003 |

## REUSE MAPPING

| Needed Functionality | Existing Implementation | Location | Reuse Strategy |
|---------------------|------------------------|----------|----------------|
| Save Server Config  | storageService.save()  | src/services/storageService.ts | DIRECT |
| Get Token           | authService.getToken() | src/services/authService.ts    | DIRECT |

## CONFLICTS

- Storage wird aktuell in Feature 5 neu implementiert → KONFLIKT
- API Client doppelt vorhanden → KONFLIKT

Resolution:
→ Bestehenden Service verwenden

## INTEGRATION REQUIREMENTS

- Muss storageService verwenden
- Darf keinen neuen API Client erstellen
- Muss bestehende Navigation erweitern

## KRITISCHE REGEL

- KEINE neue Logik erfinden
- NUR vergleichen + referenzieren

## VALIDATIONS

if dependency_exists and no_reuse_defined:
    STOP

if duplicate_implementation_detected:
    STOP


## DEPENDENCY MATRIX

| Current Feature | Depends On Feature | Type | Required | Source |
|----------------|------------------|------|----------|--------|
|                |                  |      |          |        |

## REUSE ANALYSIS

Identifiziere vorhandene Implementierungen aus RN Code:
## REUSE MAPPING

| Required Functionality | Existing Implementation | Location | Reuse Strategy | Source |
|----------------------|------------------------|----------|----------------|--------|
|                      |                        |          |                |        |


## CONFLICTS

| Type | Beschreibung | Betroffene Features | Resolution | Source |
|------|-------------|---------------------|------------|--------|
|      |             |                     |            |        |


## INTEGRATION REQUIREMENTS

- 
- 
- 

## MUSS enthalten:

konkrete Services
konkrete Dateien
konkrete Regeln