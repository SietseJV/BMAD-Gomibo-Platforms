# Confidence Rubric

Use this rubric when deciding whether an answer is strong enough to give.

## High

Use `High` when:

- the decisive behavior is directly visible in code
- at least one other artifact reinforces it, such as a test, config, or second layer
- no inspected artifact contradicts it

## Medium

Use `Medium` when:

- the core behavior is directly visible in code
- some surrounding conditions or dependencies are not fully visible
- the answer is still useful, but may vary with runtime data or another service

## Low

Use `Low` when:

- the behavior is mostly inferred
- the decisive branch depends on missing code, data, or environment
- inspected artifacts conflict

Do not give a settled answer at `Low`. Either provide only the confirmed partial facts or say the question cannot yet be answered with confidence.
