# Zielarchitektur
- React Native (Expo)
- TypeScript

## Projektstruktur
- components/
- screens/
- hooks/
- services/
- navigation/
- utils/

## Verantwortlichkeiten

- components/ → reine UI
- hooks/ → State + Logik
- services/ → API + externe Systeme
- utils/ → pure functions

## Regeln
- Keine Business-Logik in components
- API nur über services