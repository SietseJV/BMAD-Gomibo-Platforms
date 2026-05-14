---
name: bmad-how-does-this-work
description: Answer targeted codebase questions by locating the relevant implementation and explaining how it works with explicit evidence and confidence handling. Use when the user asks a focused question such as how a rule, calculation, validation, permission check, flow step, or side effect works in code, especially when they do not know where the logic lives and need a trustworthy answer instead of a broad architecture map.
---

# How Does This Work

Answer specific implementation questions with evidence-first reasoning. This skill is for narrow questions, not whole-domain mapping. Its default mode is strict: if the evidence is weak, incomplete, or contradictory, do not state the behavior as a fact. Say what is certain, what is inferred, and what remains unknown.

Explain the code in product-friendly language by default. Assume the reader may be a PM, designer, or engineer who needs to understand the behavior, the business meaning of each branch, and where the answer is proven in code. Keep the main explanation focused on functional behavior, not a tour of implementation files. Do not stop at a terse example or shortest-path summary when the real logic has multiple branches, fallbacks, or layers. Walk the full relevant logic path end to end.

## Conventions

- Use `./references/answer-template.md` as the default output shape.
- Use `./references/confidence-rubric.md` when deciding whether something is certain enough to state as fact.
- When subagents are available or explicitly allowed, use the prompts in `./agents/` to split discovery, explanation, and certainty review. Otherwise do the same work locally.
- If application scope or business mode materially changes the answer, ask or state the ambiguity early.

## Inputs To Expect

Expect some combination of:

- a repository or folder to inspect
- a focused question such as `how does renewal eligibility work`, `why is this user blocked`, or `where is the discount calculated`
- optional identifiers such as route names, UI copy, field names, error messages, entity names, or ticket links
- optional application hints such as `store`, `Hub`, shared platform logic, reseller mode, or operator mode

## Workflow

### 1. Frame The Question And Certainty Mode

Restate the question in one sentence and decide what must be proven. Default to strict certainty:

- state `facts` only when backed by direct evidence
- label `inferences` as inferences
- keep `unknowns` explicit

If the user asks for an answer and the code is not enough to prove it, answer with the best verified partial explanation plus the remaining uncertainty.

### 2. Discover The Relevant Code

If the user does not know where the logic lives:

- search by domain terms, identifiers, UI copy, and error messages
- look for routes, handlers, services, validators, policies, config, and tests
- prefer business entry points over generic utilities
- stop expanding once you have the shortest evidence chain that answers the question

Use `./agents/code-path-finder.md` when you need a clean discovery pass.

### 3. Trace The Full Relevant Logic

Trace the full relevant logic needed to explain the behavior with confidence:

- trigger or entry point
- core decision logic
- meaningful branches and guards
- important dependencies
- returned outcome or side effect
- tests or config that confirm the behavior

Prefer the smallest complete explanation, not the shortest partial explanation. Include every branch, fallback, override, or validation step that materially changes what the user should believe about the behavior. Keep file-by-file implementation details out of the main explanation unless they are necessary to understand the business behavior. Do not pad the explanation with unrelated architecture.

### 4. Cross-Check For Hidden Conditions

Before answering, check for:

- feature flags or config overrides
- role or permission restrictions
- operator, market, or channel variants
- duplicated rules across frontend and backend
- tests that disagree with the first code reading
- fallback and error paths

Use `./agents/certainty-checker.md` when the answer could be brittle or when multiple layers may disagree.

### 5. Write The Answer

Produce a direct explanation using `./references/answer-template.md`:

- answer the question first
- explain the behavior in PM-friendly language without dumbing it down
- explain the full relevant logic path, not just one example branch
- keep section 3 focused on functional logic; put code-path detail in section 5 evidence
- when fallbacks or variants exist, enumerate the full rule set instead of giving only one example
- cite the exact artifacts that support the answer
- separate facts, inferences, and unknowns
- include a confidence level

Use `./agents/behavior-explainer.md` when you need a final pass that turns traced logic into a crisp answer.

## Confidence Rule

Prefer `no claim` over a weak claim.

- `High`: directly confirmed by code and reinforced by tests, config, or multiple artifacts
- `Medium`: directly visible in code, but some surrounding conditions remain partly hidden
- `Low`: plausible but under-evidenced; do not present as settled behavior

If the best answer is `Low`, either:

- provide only the confirmed partial facts and list the unknowns, or
- tell the user you cannot yet answer with confidence and state what would need to be checked next

## Output Standard

Default sections:

1. Question
2. Short answer
3. How it works
4. Conditions and variants
5. Evidence
6. Confidence
7. Unknowns or next checks

By default, section 3 should be a full outline of the relevant logic in execution order, written in functional terms. Prefer ordered steps with enough detail that a PM can follow what happens and why, without turning the section into a file walkthrough. Use examples only to clarify a branch, never as a substitute for the actual logic outline. When the logic is effectively a rule matrix, list the full matrix or rule set rather than one or two sample cases.

For very small questions, collapse sections 1 to 4 into a short prose answer, but keep evidence and confidence explicit.

## Quality Checks

- Do not answer a different question than the one asked.
- Do not over-summarize away the decisive branch or condition.
- Do not convert guesses into facts.
- Prefer the smallest complete explanation over the shortest traceable explanation.
- Explain the business meaning of branches and fallbacks in language a PM can reuse.
- Do not rely on one illustrative example when the actual code has broader logic to outline.
- Do not let section 3 collapse into a list of files or implementation hops.
- When defaults, fallbacks, or variants are table-like, enumerate the complete set covered by the code.
- Call out if the answer differs by `store` versus `Hub`, or by reseller versus operator logic.
- Flag likely rule drift when different layers appear inconsistent.

## References

- `./references/answer-template.md` - default answer structure
- `./references/confidence-rubric.md` - confidence rules and escalation guidance
- `./agents/code-path-finder.md` - prompt for locating the relevant implementation
- `./agents/behavior-explainer.md` - prompt for turning traced behavior into a direct explanation
- `./agents/certainty-checker.md` - prompt for checking whether the answer is strong enough to state as fact
