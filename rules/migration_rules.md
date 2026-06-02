# Migration Rules

## MIG-001 Behavior Parity

RN-Code muss das in Phase 1 belegte Verhalten abbilden. Verbesserungen, UI-Modernisierung oder neue Business-Logik sind außerhalb des Scopes.

## MIG-002 No Legacy Rediscovery

Phase 3 bis 5 ürfen Legacy-Code nicht zur fachlichen Interpretation öffnen. Fehlende Informationen führen zu `ERR-REF-01`.

## MIG-003 Platform Divergence

Unterschiede zwischen iOS und Android werden nicht gegättet. Sie werden als Divergenz dokumentiert und im RN-Zielverhalten bewusst entschieden.

## MIG-004 Dependency Reuse

Bestehende RN-Services, Hooks und Utilities werden wiederverwendet, wenn sie das benötigte Verhalten bereits anbieten. Doppelte Implementierungen sind verboten.

## MIG-005 Security Preservation

Sensitive Daten müssen mindestens so geschützt werden wie in Legacy. Mapping-Beispiele:

- unkritische Persistenz: `AsyncStorage`
- sensitive Tokens/Secrets: `expo-secure-store` oder vorhandener sicherer RN-Service

## MIG-006 Test Parity

RN-Tests aus Phase 4 müssen die validen Legacy-Tests aus Phase 2 abbilden. Ein Test darf nur übersprungen werden, wenn Phase 2 ihn als invalid oder nicht migrierbar markiert.

## MIG-007 No Runtime Code In ai-context

`ai-context/artifacts/<feature-slug>/<agent-id>/<run-id>/` enthält nur Dokumentation und Reports. Runtime-Code und Tests liegen in den App-Repositories.
