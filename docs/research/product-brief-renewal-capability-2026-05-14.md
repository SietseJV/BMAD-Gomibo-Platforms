---
title: Product Brief - Renewal Capability
source_research: docs/research/market-renewal-flows-in-telco-ecommerce-research-2026-05-08.md
date: 2026-05-14
status: draft
---

# Product Brief: Configurable Renewal Capability

## Executive Summary

Gomibo Platforms has a clear opportunity to turn mobile contract renewal into a reusable product capability instead of treating it as a small variation on acquisition checkout. The market research shows that operators across the Netherlands, Germany, the UK, and the US already offer enough renewal mechanics. The bigger problem is execution: customers struggle to understand whether they are eligible, which path fits them, and what happens to their current contract, device balance, and bill when they renew.

This creates a strong product opening for a configurable renewal capability that serves both sides of the platform. In the Channel App Store, it should power a low-friction existing-customer renewal journey with early eligibility clarity, a clear split between `keep current device` and `get a new device`, and transparent consequence handling before deep shopping begins. In the Hub, it should support configuration, case continuity, and assisted recovery so broken self-service journeys do not become disconnected support incidents.

This matters now because renewal sits at the intersection of retention, support cost, channel consistency, and operator configurability. It is also well suited to Gomibo Platforms' dual business model: in reseller mode, the same capability can support multiple operator rule sets without duplicating journeys; in operator mode, teams can express channel-specific propositions on top of shared renewal primitives.

## The Problem

Existing-customer renewal is usually presented as simple, but in practice it behaves like an exception-heavy account journey. Customers often begin with high intent and then get blocked by unclear eligibility, failed verification, late explanation of financial consequences, or a mismatch between marketing promises and actual account state. When that happens, the experience feels less like normal ecommerce friction and more like a broken loyalty promise.

The current market gap is not lack of offers. It is lack of transparent renewal-state handling. Customers need early answers to four practical questions: `can I renew now`, `should I keep my phone or take a new one`, `what happens to my current contract and device payments`, and `what happens if self-service fails`. When those answers arrive too late, users fall into assisted channels, lose confidence, and start comparing switching instead of staying.

For Gomibo Platforms, the cost of the status quo is broader than conversion loss alone. Renewal friction increases support fallout, weakens channel consistency, makes parity harder across operators and countries, and encourages one-off channel logic instead of reusable platform capability.

## The Solution

Build a configurable renewal capability for the Channel App Store and Hub that treats renewal as a dedicated lifecycle flow. The customer-facing journey should start from authenticated recognition and explicit eligibility status, then branch early into `keep current device` and `get a new device`. Before users spend time in plan or device selection, the flow should make contract term, billing impact, trade-in or payoff consequences, and next-step rules explicit.

The supporting Hub layer should let operators and internal teams manage renewal rules, propositions, exception handling, and assisted continuation without rebuilding the journey per channel. When self-service breaks or the case is too complex, the same renewal case should continue into support with preserved context rather than forcing the customer to restart. The product should be built as configurable primitives: eligibility evaluation, branch logic, consequence messaging, offer orchestration, and cross-channel case continuity.

## What Makes This Different

The differentiation is not another upgrade mechanic. It is clearer orchestration of existing renewal mechanics. Most operators are already commercially capable, but few explain renewal state well inside the primary flow. Gomibo Platforms can differentiate by making renewal legible, recoverable, and reusable.

This is especially defensible for the platform because the value compounds across both business models. In reseller mode, shared primitives reduce repeated operator-specific journey work. In operator mode, teams still get room to vary proposition design and channel presentation without rebuilding the core renewal flow. The advantage is better execution, lower fragmentation, and faster rollout of renewal improvements across channels and tenants.

## Who This Serves

Primary users are existing mobile subscribers who are near contract end or otherwise eligible for renewal. Within that group, the most important segments are premium upgraders who want a new device, cost-sensitive customers who want to keep their current device, and assisted customers whose eligibility or financing state introduces complexity.

Secondary users are Hub-side operational users such as support, proposition, and channel teams. Support teams need continuity when self-service breaks. Product and proposition teams need configurable rule handling across operators, channels, and renewal propositions. Platform teams need a reusable capability that avoids channel-by-channel reinvention.

## Success Criteria

The product is successful when more existing customers can complete renewal digitally with confidence and when fewer renewal cases degrade into disconnected support journeys. Core KPIs should include digital renewal completion rate, drop-off between eligibility check and checkout, assisted fallback rate, offer-preservation rate after channel handoff, and satisfaction with the renewal journey.

Business success should also be measured through churn reduction at contract boundary, improved SIM-only versus device-upgrade guidance quality, lower renewal-related support contact volume, and reduced duplicate implementation effort across operators or channels.

## Scope

In scope for the first version are explicit eligibility states, early branching between `keep current device` and `get a new device`, clear visibility of contract and billing consequences, and preserved renewal context when a case moves from self-service into assisted handling. The first version should also define the minimum Hub configuration and operational tooling needed to support the storefront journey.

Out of scope for the first version are inventing new loyalty programs, building every possible early-upgrade proposition variant, or solving the full acquisition and renewal journey as one generic checkout system. The first release should focus on making renewal understandable and recoverable before broadening proposition complexity.

## Compliance and Operational Considerations

Because renewal is an account-based telecom journey, the capability must support operator-specific rules, verification needs, and regulated customer communication requirements. This includes clear handling of contract-end timing, billing implications, financed-device or payoff states, and auditable messaging across channels. The design should assume both country and operator variance rather than hardcoding one market model.

Operationally, the capability should expose renewal state in a way that is observable, testable, and usable by support. Error states need to be actionable, not generic, and handoff from digital to assisted channels should preserve both customer context and the current commercial offer where possible.

## Vision

If this succeeds, renewal becomes a shared lifecycle capability across Gomibo Platforms rather than a scattered set of operator-specific flows. In the Channel App Store, teams can launch clearer, more trustworthy renewal journeys faster across channels. In the Hub, internal and client teams gain one coherent model for configuring, monitoring, and recovering renewal cases.

Over time, this can expand into a broader retention and lifecycle foundation that covers proactive renewal prompts, loyalty treatment, channel parity monitoring, and support-assisted continuation across operators and markets. The long-term value is not just a better renewal page. It is a platform-level renewal system that improves retention, lowers support fallout, and scales across both reseller-style reuse and operator-specific depth.
