# Belsimpel / Gomibo Platforms

## Company Context

Gomibo Platforms is the omnichannel SaaS platform business that grew out of Belsimpel/Gomibo's in-house telco software. Historically, Belsimpel started as a telco reseller. Over time, the software capabilities built for that reseller business matured into a SaaS platform that can also be used by telco operators.

When reasoning about products, flows, architecture, or UI decisions, keep both business models in mind:

- `Belsimpel / reseller model`: one platform supports many operators, many contract types, many countries, and many channels with heavy reuse across channels.
- `Telco / operator model`: one operator is typically served per channel, with more separation in page content and less cross-channel reuse than the reseller case.

Agents should avoid solutions that only fit one of these worlds unless the task explicitly scopes itself to one of them.

## Domain Framing

This company operates in the telco commerce domain. Common concerns include:

- product assortments
- subscriptions and device bundles
- operator contracts and related sales flows
- pricing, promotions, and propositions
- channel-specific content and configuration
- back-office operations such as CRM, ERP, PIM, and CMS-like workflows

Expect many decisions to be driven by configurability, multi-channel support, reuse, operational correctness, and maintainability at scale.

## Main Applications

### 1. Channel App Store

Also referred to as `Channel App Store`, `channel apps`, or `store`.

This is the customer-facing web storefront application that powers websites/channels. It is designed to support configurable page rendering for multiple channel contexts.

Important architectural ideas:

- The storefront is not a traditional all-in-one CMS.
- A dedicated `Page Content Management System (PCMS)` is responsible for page structure and configuration, not for owning all content, layout concerns, or business logic.
- The broader Gomibo platform is service-oriented. Content and data can come from multiple services rather than a single source.
- "Bare" content such as texts, images, and files that do not come from other services is envisioned to live in a separate `Content Lake`.
- The page model is hierarchical:
  - base components
  - structured components
  - modules
  - page templates
  - page instances
- Components are defined in code and should follow single-responsibility and reuse principles where practical.

High-level render flow from the architecture document:

- A user requests a storefront URL.
- The Remix-based router/backend builds context for that request.
- Context may include product data and user data from platform services such as a channel product catalog and user service.
- The system resolves the page/template configuration via the PCMS.
- Settings come from a platform configuration service.
- Content can come from the content lake and other domain services.
- The frontend presents the rendered page to the end user.

When discussing or generating solutions for the store, optimize for:

- configurability over hardcoded channel behavior
- separation between page structure, settings, and content
- reuse across channels where appropriate
- room for tenant/channel variance without collapsing into duplicated implementations

### 2. The Hub

The `Hub` is the unified back-office application for Gomibo Platforms.

It is the place where colleagues should do their work and where operational and configuration-heavy workflows come together. It should be understood as a central workspace that combines responsibilities often associated with:

- CRM
- ERP
- PIM
- CMS
- Flow builder
- operational tooling
- internal administration and configuration

The Hub exists to replace fragmented standalone interfaces and help phase out legacy monolith-driven back-office experiences.

Core product vision:

- The Hub should be a single, user-friendly back-office application for telco operations.
- It should consolidate workflows that currently live across multiple services and interfaces.
- It should give both Gomibo employees and SaaS clients a coherent, intuitive experience.
- It should reduce duplicate UI work across teams by providing shared patterns, workflows, and components.
- It should allow custom interfaces where needed, but preserve usability and consistency.
- It should be intuitive enough that users can complete tasks with little or no prior training.

Key user groups include:

- Gomibo employees such as customer support, marketing, product management, and warehouse staff
- SaaS client employees using the same platform concepts with more indirect feedback loops
- development teams building and maintaining service-specific UIs
- product designers, Hub engineers, and product managers responsible for shared UX, components, and workflows

When discussing or generating solutions for the Hub, optimize for:

- a unified back-office experience instead of isolated feature UIs
- consistency in interaction patterns and terminology
- speed of implementation through shared building blocks
- workflows that match real user tasks
- low training burden
- maintainable standards that many teams can build on

## Working Assumptions For Future Agents

- Prefer configurable, platform-minded solutions over one-off channel logic.
- Check whether a change is meant for reseller-style multi-operator reuse, telco-style operator separation, or both.
- Treat the store and the Hub as distinct products with different user types, constraints, and success criteria.
- For storefront work, carefully separate page composition, configuration, domain data, and content storage concerns.
- For Hub work, prioritize clarity, workflow coherence, and shared patterns over isolated local optimizations.
- In this domain, "CMS" may be ambiguous. If precision matters, distinguish between `PCMS`, `Content Lake`, platform configuration, and the broader SaaS platform.

## Terminology

- `Belsimpel`: the reseller heritage/business context from which the platform evolved.
- `Gomibo Platforms`: the omnichannel SaaS solution for telcos built from that in-house software foundation.
- `Channel App Store / channel apps / store`: the customer-facing storefront application.
- `Hub`: the back-office application for internal users and SaaS clients.
- `PCMS`: Page Content Management System, focused on page structure/configuration.
- `Content Lake`: storage for bare content such as text, images, and files outside PCMS structure concerns.

## Agent Guidance

When helping with product, UX, architecture, or code in this ecosystem:

- ask which application is in scope if it is not clear
- ask which business mode is in scope if reseller vs telco changes the answer
- prefer language that reflects platform, channel, and configuration concepts accurately
- avoid assuming a single-country, single-operator, or single-channel setup by default

# Operating Philosophy — Pedagogic and Practical in Equal Measure

As much as this repo is for adding skills to your agent, it's equally tasked to help product managers become better at their craft — and to help them send the ladder down to others.

Skills here serve both goals simultaneously. The PM using a skill should finish knowing more than when they started — not just have a completed artifact. The reasoning embedded in a skill is what makes the output trustworthy, explainable, and transferable to the next person.

ABC — Always Be Coaching is a key governing principle.

This has direct implications for how you work in this repo as an agent:

- Do not optimize for brevity at the cost of explanation. Stripping learning scaffolding to tighten a skill is a defect, not an improvement.
- Examples show reasoning, not just outputs. A shorter example that hides the thinking is worse than a longer one that shows it.
- The dual audience is always both: the human PM building judgment and the AI agent executing the work. Never optimize for one at the expense of the other.
- If you are making efficiency improvements, tighten fluff — not lessons. If you are unsure which is which, leave it in.

# Rules

- Use Conventional Commits for every commit.
- Before pushing, run `npm ci && npm run quality` on `HEAD` in the exact checkout you are about to push.
  `quality` mirrors the checks in `.github/workflows/quality.yaml`.
- Skill validation rules are in `tools/skill-validator.md`.
- Deterministic skill checks run via `npm run validate:skills` (included in `quality`).
- AGENTS.md and every SKILLS.md are living documents — they evolve based on what works and what doesn't in practice. When a skill generates something that needs manual correction, that correction is a signal: update the relevant rule or skills/template section immediately so the same mistake doesn't happen again.
  - Do not apply a fix silently. Always ask for approval first. 
