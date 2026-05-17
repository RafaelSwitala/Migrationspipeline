# VALIDATION RULES

---

# CORE PRINCIPLE

Validation ist:

* binär (PASS / FAIL)
* deterministisch
* niemals interpretativ

---

# 1. STRUCTURAL VALIDATION

## V-0001 TABLE COMPLETENESS

if any(table.has_empty_fields):
    STOP

---

## V-0002 OUTPUT COMPLETENESS

if output_missing:
    STOP

---

# 2. REFERENCE & TRACEABILITY

## V-0101 MISSING REFERENCES

if missing_references:
    STOP

---

## V-0102 BEHAVIOR WITHOUT SOURCE

if behavior_without_source_reference:
    STOP

---

## V-0103 TEST WITHOUT SOURCE

if test_without_source_reference:
    STOP

---

# 3. DERIVATION CONSISTENCY

## V-0201 NON-DERIVABLE INFORMATION

if non_derivable_information_detected:
    STOP

---

# 4. DISCOVERY VALIDATION

## V-0301 NO FILES FOUND

Prüfe Tabelle O-0001 in feature_analysis.md:

Wenn:
* Tabelle O-0001 existiert NICHT
ODER
* Tabelle O-0001 enthält 0 Datenzeilen (nur Header)

Dann:
→ STOP

---

## V-0302 NO RELEVANT FILES

Prüfe Spalte "Relevante Dateien" in DISCOVERY METRICS:

Wenn:
* keine Datei als RELEVANT markiert ist

Dann:
→ STOP

---

## V-0303 INVALID FILE STRUCTURE

Für jede Zeile in O-0001:

Wenn eines der folgenden Felder fehlt oder leer ist:
* Plattform
* Datei
* Methode
* Zeilen

→ STOP

Wenn Plattform nicht exakt einer der folgenden Werte ist:
* iOS
* Android

→ STOP

---

## V-0304 OUTPUT COMPLETENESS

Prüfe feature_analysis.md und code_facts.md:

Für feature_analysis.md: Wenn einer der folgenden Abschnitte fehlt:
* O-0001
* O-0002
* O-0003
* O-0004
* O-0005
* O-0006
* O-0007
* O-0008
* O-0009
* O-0010

Für feature_analysis.md: Wenn einer der folgenden Abschnitte fehlt:
* O-1301
* O-1302
* O-1303
* O-1304
* O-1305
* O-1306
* O-1307
* O-1308
* O-1309
* O-1310

→ STOP

Für jeden Abschnitt:

Wenn Inhalt leer ist
ODER nur Platzhalter enthält
ODER "NOT FOUND" in ALLEN Feldern verwendet wird

→ STOP

---

## V-0305 REFERENCE INTEGRITY

Für jede Aussage in feature_analysis.md und code_facts.md:

Wenn KEINE Referenz vorhanden ist im Format:
(Datei + Methode + Zeile)

→ STOP

Wenn Referenz unvollständig ist (z.B. Zeile fehlt):
→ STOP

---

## V-0306 NO INTERPRETATION IN CODE FACTS
Prüfe alle Inhalte in code_facts.md:

Wenn:
* Texte abstrahiert sind (z. B. „Login erfolgreich“, „User wird weitergeleitet“)
ODER

* Begriffe verwendet werden, die nicht im Code vorkommen
ODER

* mehrere Codepfade zusammengefasst wurden
ODER

* Bedingungen umformuliert wurden (nicht 1:1 Code)

→ STOP

Erlaubt sind nur:
* originale Bezeichner (Variablen, Methoden, Klassen)
* originale Bedingungen (if, switch, etc.)
* originale Werte und Literale

---

## V-0307 MISSING RAW CONDITIONS

Prüfe Abschnitt O-1306 (LOGIC CONDITIONS):

Wenn:

* keine einzige Bedingung extrahiert wurde

→ STOP

Für jede Zeile:

Wenn:

* Feld „Bedingung“ leer ist
ODER

* Bedingung nicht im Original-Codeformat vorliegt
→ STOP


---

## V-0308 MISSING API DETAILS

Prüfe Abschnitt O-1303 (API CALL DETAILS):

Wenn:

* mindestens ein API Call in O-0001 (feature_analysis.md) existiert
UND

* O-1303 enthält keine entsprechenden Einträge

→ STOP

Für jede API-Zeile:

Wenn folgende Felder ALLE NOT FOUND sind:

* Endpoint
* HTTP Methode
* Request Body
* Response Felder

→ STOP

Wenn:

* API Call beschrieben ist, aber keine Datei/Methode/Zeile referenziert ist

→ STOP


---

## V-0309 MISSING STORAGE KEYS

Prüfe Abschnitt O-1304 (STORAGE DETAILS):

Wenn:

* Storage in feature_analysis.md erwähnt wird
UND

* keine Storage-Einträge in O-1304 existieren

→ STOP

Für jede Storage-Zeile:

Wenn:

* Feld „Key“ leer ist
ODER NOT FOUND
UND

* gleichzeitig Zugriff (read/write) vorhanden ist

→ STOP

Wenn:

* Storage-Zugriff existiert, aber keine Referenz (Datei + Methode + Zeile)

→ STOP

---

# 5. INTAKE COMPLETENESS

## V-0401 MISSING ENTRY POINTS

if missing_entry_points:
    STOP

---

## V-0402 MISSING STORAGE

if missing_storage_keys:
    STOP

---

## V-0403 MISSING NAVIGATION

if missing_navigation_flows:
    STOP

---

# 6. DEPENDENCY CONSISTENCY

## V-0501 MISSING REUSE MAPPING

if dependency_detected and no_reuse_mapping:
    STOP

---

## V-0502 MISSING CONFLICT RESOLUTION

if conflict_detected and no_resolution:
    STOP

---

## V-0503 MISSING REQUIRED DEPENDENCY

if required_dependency_missing:
    STOP

---

## V-0504 EMPTY INTEGRATION REQUIREMENTS

if integration_requirements_empty:
    STOP

---

# 7. LOGIC CONSISTENCY

## V-0601 DUPLICATE LOGIC

if duplicate_logic_detected and no_resolution_defined:
    STOP

---

# 8. TEST VALIDATION

## V-0701 MISSING TESTS

if any(behavior_without_test):
    STOP

---

## V-0702 MISSING EXPECTED OUTPUT

if any(test_without_expected_output):
    STOP

---

## V-0703 AMBIGUOUS TESTS

if ambiguous_tests_detected:
    STOP

---

## V-0704 STATE COVERAGE

if state_coverage_incomplete:
    STOP

---

## V-0705 LEGACY TEST COUNT VALIDATION

if android_tests_count == 0:
    STOP

if ios_tests_count == 0:
    STOP

---

## V-0706 RN TEST COUNT VALIDATION

if rn_tests_count == 0:
    STOP

---

## V-0707 TEST COUNT VALIDATION

if android_tests_count == 0:
    STOP

if ios_tests_count == 0:
    STOP

if rn_tests_count == 0:
    STOP

---

## V-0708 TEST COVERAGE GAP

if behaviors_not_covered:
    STOP

---

## V-0709 TEST-BEHAVIOR MISMATCH

if test_without_behavior_reference:
    STOP

if mismatched_expected_output:
    STOP

---

## V-0710 NO STRUCTURAL TESTS
if test_only_checks_class_existence OR
   test_only_checks_not_null_without_behavior:
    STOP

---

## V-0711 NO TEST WITHOUT TEST DEFINITION
if test_exists_without_test_definition_entry:
    STOP

---

## V-0712 EXPECTED OUTPUT NOT FROM CODE
if expected_output == result_of_called_method:
    STOP

---

## V-0713 WEAK TRACEABILITY
if source_reference != (file + method + line + condition):
    STOP

---

## V-0714 INVALID COVERAGE
coverage = tested_conditions / total_conditions

if coverage < required_threshold:
    STOP

---

## V-0715 NON-DETERMINISTIC INPUT
if input_not_covering_boundaries:
    STOP

---

## V-0716 EDGE CASE NOT EXECUTED
if edge_case_defined_but_not_tested:
    STOP

---

## V-0717 NO STATE TRANSITIONS
if no_test_changes_state_and_validates_transition:
    STOP

---

## V-0718 NO FAILURE PROOF
if test_would_still_pass_after_code_change:
    STOP

---

# 9. IMPLEMENTATION VALIDATION

## V-0801 BEHAVIOR NOT IMPLEMENTED

if any(behavior_not_implemented):
    STOP

---

## V-0802 MAPPING INCOMPLETE

if mapping_incomplete:
    STOP

---

## V-0803 DUPLICATE SERVICES

if duplicate_services_detected:
    STOP

---

## V-0804 DEPENDENCY RULE VIOLATION

if dependency_rules_violated:
    STOP

---

## V-0805 CODE INTEGRITY

if missing_imports:
    STOP

if invalid_types:
    STOP

---

# 10. EXECUTION VALIDATION

## V-0901 INSTALLATION FAILURE

if npm_install_failed:
    STOP

---

## V-0902 TYPESCRIPT ERRORS

if critical_typescript_errors:
    STOP

---

## V-0903 APPLICATION FAILURE

if app_not_starting:
    STOP

---

## V-1001  NO STRUCTURAL TESTS
if test_only_checks:
    - class existence
    - method existence
    - assertNotNull without context
then:
    mark test as INVALID

---

## V-1002 NO BEHAVIOR ASSERTION
if test_does_not_assert_behavior_change:
    mark test as INVALID

---

## V-1003 EXPECTED OUTPUT NOT DEFINED
if expected_output_missing OR vague:
    mark test as INVALID

---

## V-1004 ASSERTION NOT DETERMINISTIC
if assertion_can_pass_with_multiple_outputs:
    mark test as INVALID

---

## V-1005 NO FAILURE DETECTION
simulate:
    invert_condition
    change_constant
    remove_required_field

if test_still_passes:
    mark test as INVALID

---

## V-1006 IMPLEMENTATION MIRRORING
if expected_output == method_output_without_independent_logic:
    mark test as INVALID

---

## V-1007 NO INPUT VARIATION
if test_has_only_one_input_case:
    mark as WEAK

---

## V-1008 NO EDGE CASE EXECUTION
if edge_case_defined AND not tested:
    mark as INVALID

---

## V-1009 NO STATE TRANSITION
if test_does_not:
    capture_state_before AND
    trigger_change AND
    validate_state_after:
        mark as INVALID

---

## V-1010 WEAK TRACEABILITY
if source_reference_not_linked_to:
    - exact condition
    - exact code path
then:
    mark as INVALID

---

## V-1011 UNUSED CODE PATHS
if condition_in_O-1306_not_tested:
    mark coverage as INCOMPLETE

---

## V-1012 ASSERTION WITHOUT CAUSE
if assertion_not_linked_to_input:
    mark as WEAK

---

## V-1013 MULTIPLE BEHAVIORS IN ONE TEST
if test_validates_more_than_one_behavior:
    mark as INVALID

---

## V-1014 NO ERROR PATH VALIDATION
if error_condition_exists AND no failing test:
    mark as INVALID

---

## V-1015 TEST DOES NOT FAIL ON BROKEN CODE
simulate:
    method_returns_true_always

if test_still_passes:
    mark as INVALID

---

## V-1016 HARDCODED PASS CONDITION
if assertion_always_true_independent_of_logic:
    mark as INVALID

---

## V-1017 MISSING PLATFORM PARITY
if test_exists_only_on_one_platform:
    mark as INVALID

---

## V-1018 NO REAL METHOD USAGE
if test_does_not_call_real_method_from_code_facts:
    mark as INVALID

---

## V-1019 MOCK ABUSE
if mock_used_for_core_logic:
    mark as INVALID

---

## V-1020 COVERAGE IS FAKE
if test_only_executes_code_but_not_asserts_effect:
    mark coverage as INVALID

---

## V-1021 FAILURE SENSITIVITY CHECK
simulate_changes:
    1. invert_if_condition
    2. change_constant_value
    3. remove_required_field
    4. return_fixed_value

if test_does_not_fail:
    mark test as INVALID

---