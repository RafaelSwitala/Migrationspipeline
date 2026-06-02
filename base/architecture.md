# Target Architecture

## ARCH-001 Platform

Zielplattform ist React Native mit Expo und TypeScript.

## ARCH-002 Preferred Project Structure

Wenn das RN-Projekt keine andere etablierte Struktur vorgibt, gilt:

```text
src/
  components/
  hooks/
  screens/
  services/
  types/
  utils/
```

## ARCH-003 Responsibilities

| Layer | Verantwortung |
|---|---|
| `components/` | Reine UI und Props, keine Business-Logik |
| `screens/` | Screen-Komposition, Navigation, Hook-Nutzung |
| `hooks/` | State, Lifecycle, Feature-Orchestrierung |
| `services/` | API, Storage, externe Systeme |
| `types/` | Gemeinsame TypeScript-Typen |
| `utils/` | Pure Functions ohne Side Effects |

## ARCH-004 Feature Integration

`ai-context/artifacts/<feature-slug>/<agent-id>/<run-id>/` ist nur Dokumentation. Runtime-Code wird in die Struktur von `../rn-e-mobilebrowser/` integriert.

Ein isolierter `src/features/<feature-slug>/`-Ordner ist nur erlaubt, wenn das RN-Projekt dieses Pattern bereits nutzt.

## ARCH-005 Dependency Direction

UI darf Hooks nutzen. Hooks dürfen Services und Utils nutzen. Services dürfen keine UI importieren.

## ARCH-006 Minimalism

Keine neue State-Management-, API- oder Styling-Bibliothek einführen, wenn das Feature mit vorhandenen Mitteln umgesetzt werden kann.
