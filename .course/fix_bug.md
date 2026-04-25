# Phase 2: Guided Debugging

Find and fix a pre-seeded bug in the FastAPI codebase.

## Step: Understand the issue

A real user reported that FastAPI returns the wrong HTTP status code when a request is missing required parameters.

- **Expected behavior** — a missing required query parameter returns a structured validation error response
- **Actual behavior** — the response has an unexpected status code
- **Hint** — the bug is in how FastAPI handles validation errors, not in any route or dependency
- **Related test** — `tests/test_validation_error_status_code.py`

> Take a moment to understand the *symptom* before diving into code. What does the HTTP specification say is the correct status code for a request that fails validation?

## Step: Explore the codebase

Orient yourself in the relevant code:

1. Open the failing test file and read what it expects
2. Understand what `RequestValidationError` is and how FastAPI handles it
3. Follow the path from a validation error being raised to a response being sent

```bash
# Find where validation errors are referenced in the framework
grep -rn "RequestValidationError" fastapi/
```

> **Tip:** FastAPI's architecture separates *raising* an exception from *handling* it. Think about which side of that boundary the bug is on.

## Step: Reproduce the problem

Run the specific failing tests to see the error firsthand:

```bash
uv run pytest tests/test_validation_error_status_code.py -v
```

Read the failure output carefully — it tells you exactly what status code was returned versus what was expected.

## Step: Plan your change

Before editing code, decide on the fix:

1. What is the **root cause** — not just the symptom?
2. What is the **minimal change** needed?
3. Will your fix break anything else?

> **Important:** Don't change the tests. The tests are correct — they describe expected behavior per the HTTP specification and FastAPI's own documentation. Your job is to fix the application code.

## Step: Implement and test

Make your fix, then verify:

```bash
# Run the full test suite
uv run bash scripts/test.sh

# Or run just the affected tests first for a faster feedback loop
uv run pytest tests/test_validation_error_status_code.py -v
```

Check that:
- [ ] All previously failing tests now pass
- [ ] All other tests still pass
- [ ] The fix is a minimal, focused change

> **Optional:** Can you find other test files that also cover validation error handling? Do they all pass now too? Try searching for `422` in `tests/`.

## Footer

- [FastAPI Contributing Guide](https://fastapi.tiangolo.com/contributing/)
- [FastAPI Exception Handling Docs](https://fastapi.tiangolo.com/tutorial/handling-errors/)
- [Architecture Overview](../CLAUDE.md)
