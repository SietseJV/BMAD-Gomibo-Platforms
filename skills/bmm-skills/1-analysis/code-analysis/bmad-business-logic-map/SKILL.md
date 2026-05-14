---
name: bmad-business-logic-map
description: Inspect a codebase and translate implemented behavior into a PM-readable map of business logic. Use when Codex needs to explain how a flow, service, domain object, page, or product area currently works in code, especially to extract rules, validations, calculations, exceptions, state transitions, permissions, feature-flag behavior, and operator or channel variants before documentation, requirements work, migrations, bug triage, or stakeholder alignment.
---

# Business Logic Map

Explain implemented product behavior from code without forcing PMs to reverse-engineer the system themselves. The goal is not a generic architecture tour. The goal is a traceable business-logic explanation that says what the software actually does, where it does it, and which rules or exceptions matter to product decisions.

## Conventions

- Treat `./references/template.md` as the default output structure.
- Use `./references/sample.md` as the target level of abstraction.
- Treat every claim as one of:
  - `Code fact`: directly visible in code, config, tests, or schema
  - `Inference`: likely product meaning inferred from implementation
  - `Unknown`: depends on runtime data, another system, or missing context
- When subagents are available or explicitly allowed, use the prompts in `./agents/` to split the work. Otherwise do the same work locally.

## Inputs To Expect

Expect some combination of:

- a repository or folder to inspect
- a target flow, page, service, object, or feature area
- bug reports, tickets, requirements, or stakeholder questions that define the scope
- optional hints about which application is in scope, such as `store` or `Hub`
- optional hints about whether the behavior should be understood for reseller-style reuse, operator-specific behavior, or both

If the scope is broad, narrow it to a product slice that can be explained coherently. Prefer one journey, object, rule area, or decision surface at a time over attempting to summarize an entire codebase.

## Workflow

### 1. Frame The Question

Turn the request into a concrete investigation target:

- what user or operator task is being explained
- which domain object or workflow is in scope
- which application is in scope if that matters
- whether the focus is storefront behavior, back-office behavior, or shared platform logic
- whether the question is about current behavior, hidden rules, bug-causing edge cases, or migration risk

If the user asks for repo-level explanation, do not scan everything equally. Identify likely business entry points first.

### 2. Find The Business Entry Points

Start from the code that initiates or resolves business outcomes, such as:

- routes, controllers, handlers, loaders, actions, or resolvers
- form submit handlers and validation layers
- domain services, orchestration services, policies, and rule engines
- state machines, lifecycle handlers, or status transition code
- pricing, discount, eligibility, and proposition logic
- config lookups, feature flags, experiment gates, or market or channel overrides
- tests that encode expected business behavior

When helpful, use `./agents/entry-point-finder.md` to identify the smallest artifact set that can explain the behavior.

### 3. Trace The Decision Path

Walk through the logic in execution order and capture:

- triggering inputs
- important conditions and branches
- data dependencies
- outputs or side effects
- where control jumps into another module or service

Follow the path that determines the outcome. Ignore low-value implementation detail unless it changes a business result.

### 4. Extract The Rule Ledger

Convert traced logic into explicit business rules. Look especially for:

- eligibility criteria
- required versus optional fields
- default values and prefills
- calculations, scoring, sorting, or ranking rules
- validation thresholds and rejection reasons
- state transitions and forbidden transitions
- override precedence, inheritance, or fallback behavior
- manual versus automated paths
- operator, market, locale, or channel variants
- permission checks and role-based restrictions
- date, time, stock, or lifecycle-driven behavior
- failure handling, retries, guardrails, and silent fallbacks

If a rule is scattered across multiple files, consolidate it into one human-readable statement with code references.

Use `./agents/rule-ledger-builder.md` when you need a clean pass that turns traced behavior into rule statements.

### 5. Separate Business Logic From Technical Mechanics

Not every branch is a business rule. Separate:

- `Business logic`: behavior that product, operations, legal, marketing, finance, or support would care about
- `Technical mechanism`: caching, serialization, framework plumbing, transport code, or pure formatting concerns

Keep technical notes only when they explain why the business behavior happens or why it may be brittle.

### 6. Capture Exceptions, Variants, And Drift

PMs usually need the non-obvious parts most. Explicitly call out:

- exceptions to the happy path
- special handling for legacy states or migrated data
- branches guarded by feature flags or configuration
- behavior that differs by channel, operator, market, locale, or customer type
- places where frontend and backend enforce different rules
- cases where the code appears to contradict product expectations or documentation
- status models and allowed transitions when the behavior changes over time

Use `./agents/variant-and-edge-case-checker.md` when you need a dedicated pass over flags, config, tests, or edge-case branches.

### 7. Write The PM-Readable Map

Produce a Markdown document using `./references/template.md`:

- start with the plain-language flow summary
- define the main actors, entities, and outcomes
- list the rules in concise statements
- attach evidence references to files, functions, tests, or config locations
- note confidence and open questions where behavior is partially inferred

Prefer statements like `If the customer already has X, the system blocks Y and shows Z` over implementation narration like `the code calls method A then mapper B`.

## Confidence Standard

Use:

- `High`: directly confirmed by code and reinforced by tests, config, or multiple artifacts
- `Medium`: directly confirmed in code, but surrounding behavior or runtime data is only partly visible
- `Low`: plausible interpretation, but key behavior depends on missing context

Do not present `Low` confidence items as settled rules. Move them into open questions or explicit inferences.

## Quality Checks

- Preserve traceability. Every important claim should point back to code, config, tests, or another inspected artifact.
- Distinguish code facts from inferred product meaning.
- Prefer PM-readable statements over raw code paraphrase.
- Do not stop at the happy path when edge cases are present.
- Note whether a rule is enforced in frontend code, backend code, shared logic, configuration, or multiple places.
- Call out duplication, drift, or contradiction when the same rule appears differently across layers.
- In this repo's domain, be explicit about channel, operator, contract, and back-office variants when they affect the rule.

## References

- `./references/template.md` - output template for the business logic map
- `./references/sample.md` - worked example showing the expected level of abstraction
- `./agents/entry-point-finder.md` - prompt for locating the most relevant artifacts
- `./agents/rule-ledger-builder.md` - prompt for converting traced behavior into rule statements
- `./agents/variant-and-edge-case-checker.md` - prompt for finding flags, variants, and drift
