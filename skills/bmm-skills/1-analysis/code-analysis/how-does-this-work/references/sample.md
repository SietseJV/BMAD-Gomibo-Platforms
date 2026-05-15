# Sample Output

## 1. Question

- Request: How does the store decide whether to show a SIM-only renewal path instead of a device-upgrade path?
- Product or application in scope: Channel App Store
- Business mode in scope: Reseller model with operator-specific propositions

## 2. Short Answer

The store does not choose SIM-only renewal with one simple UI flag. It first establishes that the customer is in a renewal flow, then evaluates whether the current proposition and eligibility state allow the device-upgrade branch. If the upgrade branch is unavailable, blocked, or the proposition is explicitly keep-device, the flow exposes the SIM-only renewal path instead.

## 3. How It Works

Functional explanation:

1. What decision is being made: The store is deciding whether this renewal flow should offer a device-upgrade path or only a SIM-only renewal path.
2. What inputs matter to that decision: The decision depends on renewal context, proposition metadata, eligibility state, and any operator-specific override.
3. How the main branch or fallback works: The system prefers the device-upgrade branch only when that branch exists for the proposition and the customer is eligible for it. If either of those is missing, the flow falls back to SIM-only renewal.
4. What overrides or restrictions apply: A keep-device marker or operator-specific rule can still force the SIM-only branch even when an upgrade path exists in principle.
5. Final functional outcome: The user sees the branch that remains valid after proposition support, eligibility, and override rules are all applied.

Exact logic:

1. Full rule set, branch list, or fallback matrix:
   - If the user is not in a renewal context, this logic does not apply.
   - If the proposition has no device-upgrade branch, show SIM-only renewal.
   - If the proposition has a device-upgrade branch but the customer is not eligible, show SIM-only renewal.
   - If the proposition has a device-upgrade branch and the customer is eligible, check for keep-device or operator-specific override rules.
   - If a keep-device or operator-specific rule blocks upgrade, show SIM-only renewal.
   - Only show the device-upgrade path when the proposition supports it, the customer is eligible, and no override blocks it.

## 4. Conditions and Variants

- Condition: If the customer is not in a renewal context, this branch logic does not apply.
- Variant: Some operators may expose SIM-only renewal more broadly than device-upgrade renewal.
- Hidden blocker or fallback: Missing eligibility data may force a fallback state rather than a clean branch decision.
- Scope note: This answer should describe the full relevant branch logic, not just one happy-path example.

## 5. Evidence

- `apps/store/routes/renewal.tsx`: shows where renewal context is loaded.
- `services/renewal/branching-service.ts`: contains the keep-device versus new-device decision.
- `tests/renewal/branching.spec.ts`: confirms the blocked and keep-device paths.
- `config/operators/nl/kpn.json`: shows an operator-specific override.

## 6. Confidence

- Level: Medium
- Why: The branch logic is visible in code and tests, but operator data outside the inspected files may add more exceptions.

## 7. Unknowns or Next Checks

- Unknown: Whether assisted-channel renewals reuse the same branch decision service.
- Next file or dependency to inspect: Hub-side continuation or support orchestration code.
