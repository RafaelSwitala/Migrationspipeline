# Testing Baseline

## TEST-001 Scope

Nur Unit Tests sind Teil des Migrationsvergleichs.

## TEST-002 Legacy Android

- Bevorzugt: JUnit4
- Mocking: Mockito oder bereits vorhandene Projektkonvention
- Testpfad: vorhandene Unit-Teststruktur, sonst `app/src/test/`

## TEST-003 Legacy iOS

- Bevorzugt: XCTest
- Mocking: manuelle Test Doubles oder vorhandene Projektkonvention
- Testpfad: vorhandenes Test Target, sonst minimaler XCTest-Unit-Testpfad

## TEST-004 React Native

- Bevorzugt: Jest
- UI-nahe Tests: React Native Testing Library, wenn im Projekt vorhanden oder begründet installierbar
- Native/Expo APIs werden deterministisch gemockt

## TEST-005 Coverage

Coverage soll so hoch wie sinnvoll erreichbar sein. Qualität geht vor künstlicher Prozentoptimierung. Branches, Error Paths, State Transitions und Storage/API Side Effects haben Priorität.

## TEST-006 Valid Test

Ein Test ist valide, wenn er:

- auf Phase-1-Fakten oder Phase-2-Test-IDs referenziert,
- deterministische Inputs nutzt,
- mindestens eine fachliche Assertion enthält,
- bei gebrochenem Verhalten plausibel fehlschlagen würde.
