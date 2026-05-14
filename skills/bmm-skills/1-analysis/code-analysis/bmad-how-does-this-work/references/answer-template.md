# How Does This Work - Answer Template

## 1. Question

- Request:
- Product or application in scope:
- Business mode in scope:

## 2. Short Answer

State the answer first in 2 to 4 sentences. Write for a PM-level reader: clear, direct, and specific about what actually drives the behavior.

## 3. How It Works

Use this section as the main logic outline. Explain the behavior in functional terms first. Keep code-path detail out of this section unless it is necessary to explain the business behavior. Prefer 2 parts:

- Functional explanation: what the system is trying to decide and how the decision works
- Exact logic: the full rule set, branch list, or fallback matrix covered by the code

Prefer 5 to 9 ordered steps when the behavior has multiple branches or layers.

Functional explanation:

1. What decision is being made:
2. What inputs matter to that decision:
3. How the main branch or fallback works:
4. What overrides or restrictions apply:
5. Final functional outcome:

Exact logic:

1. Full rule set, branch list, or fallback matrix:

## 4. Conditions and Variants

- Condition:
- Variant:
- Hidden blocker or fallback:
- Scope note:

## 5. Evidence

- `path/to/file`: what it proves
- `path/to/test`: what it confirms
- `path/to/config`: which variant or override it drives

Keep evidence concise. This section is where code references belong.

## 6. Confidence

- Level:
- Why:

## 7. Unknowns or Next Checks

- Unknown:
- Next file or dependency to inspect:
