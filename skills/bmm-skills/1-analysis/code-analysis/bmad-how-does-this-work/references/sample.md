# Sample Output

## 1. Question

- Request: How does the store decide whether to show a SIM-only renewal path instead of a device-upgrade path?
- Product or application in scope: Channel App Store
- Business mode in scope: Reseller model with operator-specific propositions

## 2. Short Answer

The store first confirms that the customer is in a renewal context, then checks whether the current proposition and eligibility state permit a device-upgrade path. If device upgrade is not allowed or the offer is explicitly marked as keep-device, the customer is routed into the SIM-only renewal path instead. This appears to be driven by both proposition metadata and eligibility checks, not by one UI toggle alone.

## 3. How It Works

1. Entry point or trigger: The renewal route loads the existing-customer context and proposition type.
2. Core decision logic: The flow checks whether the proposition supports device upgrade and whether the customer is eligible for that branch.
3. Important dependencies: Proposition metadata, eligibility service response, and any operator-specific override.
4. Outcome or side effect: The UI exposes the SIM-only renewal branch when device upgrade is blocked or absent.

## 4. Conditions and Variants

- Condition: If the customer is not in a renewal context, this branch logic does not apply.
- Variant: Some operators may expose SIM-only renewal more broadly than device-upgrade renewal.
- Hidden blocker or fallback: Missing eligibility data may force a fallback state rather than a clean branch decision.

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
