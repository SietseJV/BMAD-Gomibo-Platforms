# Business Logic Map Template

## 1. Scope and Question

- Request:
- Product or application in scope:
- Business mode in scope:
- Target flow, object, or decision area:
- What this analysis is trying to explain:

## 2. Investigated Artifacts

| Artifact | Type | Why it matters |
| --- | --- | --- |
| `path/to/file` | route / service / validator / test / config | entry point for X |

## 3. Plain-Language Flow Summary

Write a short explanation of how the relevant behavior works end to end in PM-readable language.

## 4. Business Rule Ledger

| Rule ID | Rule statement | Why it matters | Inputs or conditions | Outcome | Exceptions or variants | Evidence refs | Confidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| R1 | | | | | | | |

## 5. Exceptions and Edge Cases

| ID | Scenario | What the system does | Why it matters | Evidence refs |
| --- | --- | --- | --- | --- |
| E1 | | | | |

## 6. Status and Transition Rules

Use this section only when the behavior depends on a meaningful status model or time-based progression. Skip it when the logic is just one-off validation with no real state changes.

| Current status | Trigger or condition | Next status or outcome | Allowed? | Notes | Evidence refs |
| --- | --- | --- | --- | --- | --- |
| Draft | Publish action and validation passes | Published | Yes | | |

## 7. Variants and Configuration Dependencies

| Variant type | Variant | Behavior difference | Source of variation | Evidence refs |
| --- | --- | --- | --- | --- |
| Market | NL vs BE | | config / code / data | |

## 8. Open Questions and Confidence Notes

- `Unknown`:
- `Possible inference`:
- `Likely drift or contradiction`:

## 9. Evidence Appendix

- `path/to/file`: what it contributes
- `path/to/test`: which rule it confirms
- `path/to/config`: which variant it drives
