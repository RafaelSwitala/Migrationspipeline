# Zielarchitektur
- React Native (Expo)
- TypeScript

## Projektstruktur
* src/screens/
* src/services/
* src/hooks/
* src/components/
* src/types/
* src/utils/

## Verantwortlichkeiten

- components/ → reine UI
- hooks/ → State + Logik
- services/ → API + externe Systeme
- utils/ → pure functions

## Regeln
- Keine Business-Logik in components
- API nur über services

## FEATURE INTEGRATION RULE:

Neue Features dürfen NICHT als isolierter Ordner gebaut werden.

Sie müssen integriert werden in:

- screens/
- services/
- hooks/

Feature-Ordner existiert ausschließlich für Analyse- und Dokumentationszwecke.
Er darf NICHT für Runtime-Code verwendet werden.

Verstoß → STOP: ARCHITECTURE VIOLATION