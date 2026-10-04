# Tests

Golden-output tests (every report change ships with one), unsafe-prompt tests and the semantic-layer schema linter, run with pytest. The schema linter fails the build on a missing view or field or a unit mismatch. A failing golden-output or unsafe-prompt test stops the change from being merged or released.
