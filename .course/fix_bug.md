# Phase 2: Fixing the bug

You have set up the environment, and tests are running, but some of them have failed. Our users are very attentive too
and
had already filed an issue. It's on GitHub, let's go and see.

The first goal here is to understand the main idea of the issue and find the questions
you already have when reading it for the first time.

[Open the issue]($issueLink)

## Step 1: Understand the issue

So you have read the issue. Now let's make sure the issue description is clear.

First, what exactly is the problem: is it wrong logic in production code, wrong tests, or something else?
What is expected behavior? What is actual? Write down your answers — even a
single sentence for each. You'll need them when you write your PR description later.

## Step 2: Reproduce the problem

Before diving into the code, let's see the failure with our own eyes. Run the specific failing tests:

```bash
uv run pytest tests/test_validation_error_status_code.py -v
```

Read the failure output carefully — it tells you exactly what status code was returned versus what was expected.
Look for lines starting with `AssertionError` or `assert` — they show the expected value on one side and the actual
value on
the other (e.g., `assert 401 == 422`).

## Step 3: Explore the codebase

Now that you've seen the failure, it's time to find the problematic code.

1. Open the failing test file and read what it expects. Look for `assert` statements — they
   tell you the expected status code and response body. Compare those to what the application actually returns.
2. Understand what `RequestValidationError` is and how FastAPI handles it.
3. Follow the path from a validation error being raised to a response being sent.

To trace this, look up `RequestValidationError` usages. In your IDE, navigate to the class, right-click on it, and
choose **Find Usages**. If your editor doesn't support that, you can search in the terminal:

```bash
# Find where validation errors are referenced in the framework
grep -rn "RequestValidationError" fastapi/
```

> **Tip:** FastAPI's architecture separates *raising* an exception from *handling* it. Think about which side of that
> boundary the bug is on.

## Step 4: Plan your change

Before editing code, decide on the fix:

1. What is the **root cause** — not just the symptom?
2. What is the **minimal change** needed?
3. Will your fix break anything else?

By now, your search should have shown you where `RequestValidationError` is handled. That handler is where the status
code gets set — and that's the file you need to edit.

> **Important:** Don't change the tests. The tests are correct — they describe expected behavior per the HTTP
> specification and FastAPI's own documentation. Your job is to fix the application code.

## Step 5: Implement and test

Make your fix, then verify:

```bash
# Run just the affected tests first for a faster feedback loop
uv run pytest tests/test_validation_error_status_code.py -v

# Then run the full test suite to make sure nothing else broke
uv run bash scripts/test.sh
```

Check that:

- All previously failing tests now pass
- All other tests still pass
- The fix is a minimal, focused change

> **If you're stuck:** Re-read the error output from pytest — it shows exactly which value was expected and which was
> actually returned. If that's not enough, try adding `print()` statements in the handler code to inspect what status code
> is being set and why. Run the targeted test again to see your debug output.

> **Optional:** Can you find other test files that also cover validation error handling? Do they all pass now too? Try
> searching for `422` in `tests/`.

## Useful links

- [FastAPI Contributing Guide](https://fastapi.tiangolo.com/contributing/)
- [FastAPI Exception Handling Docs](https://fastapi.tiangolo.com/tutorial/handling-errors/)
- [Architecture Overview](../CLAUDE.md)
