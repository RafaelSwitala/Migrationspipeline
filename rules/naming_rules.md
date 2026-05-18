# Naming Rules

## NAM-001 Feature Slugs

Feature-Ordner verwenden lowercase kebab-case:

```text
features/storage-config/
features/login/
```

Keine Leerzeichen, Umlaute, Nummern-Prefixes oder Synonyme pro KI-Lauf.

## NAM-002 Artifact Names

Artefakte verwenden das Nummernschema aus `rules/id_registry.md`, zum Beispiel:

```text
11_feature_analysis.md
23_legacy_test_results.md
51_final_validation_report.md
```

## NAM-003 React Native Files

- Components: `PascalCase.tsx`
- Hooks: `useName.ts`
- Services: `nameService.ts`
- Types: `name.types.ts`
- Constants: `name.constants.ts`
- Tests: `Name.test.ts` oder `Name.test.tsx`

## NAM-004 Symbols

- Classes and components: `PascalCase`
- Functions, variables, methods: `camelCase`
- Constants: `UPPER_SNAKE_CASE`
- Boolean values: `isEnabled`, `hasPermission`, `canNavigate`

## NAM-005 ID Names

IDs sind stabil und werden nie umbenannt, sobald ein Artefakt reviewed wurde. Neue IDs werden angehaengt, nicht zwischen bestehende IDs geschoben.
