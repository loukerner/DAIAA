# Documentation

## 2026 Agent Compliance & Implementation Guide

**[Read the guide](2026-agent-compliance-implementation-guide.md)**

The guide maps agentic AI governance obligations to practical evidence controls for autonomous systems that retrieve data, invoke tools, delegate work, and operate across regulated environments.

It is written for compliance officers, CISOs, developers, auditors, legal teams, procurement teams, and strategic advisors preparing for EU AI Act, DORA, ISO 42001, ISO 27001, SOC 2, privacy, and sector-specific obligations.

It focuses on a core requirement for agentic AI systems: compliance evidence should be generated automatically, bound to the policy in force at the time, protected against alteration, and independently checkable by a party other than the one whose conduct is being assessed.

> [!NOTE]
> This guide is a structured compliance and technical reference, not legal advice. Where it conflicts with primary legislation, official regulatory guidance, or binding standards, those primary sources control.

### Contents

1. [Executive Summary](2026-agent-compliance-implementation-guide.md#1-executive-summary)
2. [Who Should Use This Guide](2026-agent-compliance-implementation-guide.md#2-who-should-use-this-guide)
3. [Core Concepts](2026-agent-compliance-implementation-guide.md#3-core-concepts)
4. [The Compliance Problem](2026-agent-compliance-implementation-guide.md#4-the-compliance-problem)
5. [Regulatory and Audit Obligation Map](2026-agent-compliance-implementation-guide.md#5-regulatory-and-audit-obligation-map)
6. [Evidence Maturity Model](2026-agent-compliance-implementation-guide.md#6-evidence-maturity-model)
7. [The Nine Control Areas](2026-agent-compliance-implementation-guide.md#7-the-nine-control-areas)
    - [01 — AI inventory and shadow-AI discovery](2026-agent-compliance-implementation-guide.md#72-control-area-01--ai-inventory-and-shadow-ai-discovery)
    - [02 — Use-case classification and risk assessment](2026-agent-compliance-implementation-guide.md#73-control-area-02--use-case-classification-and-risk-assessment)
    - [03 — Model and data provenance](2026-agent-compliance-implementation-guide.md#74-control-area-03--model-and-data-provenance)
    - [04 — Sanctioned-application control](2026-agent-compliance-implementation-guide.md#75-control-area-04--sanctioned-application-control)
    - [05 — Prompt and output governance](2026-agent-compliance-implementation-guide.md#76-control-area-05--prompt-and-output-governance)
    - [06 — Identity and access control for AI](2026-agent-compliance-implementation-guide.md#77-control-area-06--identity-and-access-control-for-ai)
    - [07 — Logging, telemetry and auditability](2026-agent-compliance-implementation-guide.md#78-control-area-07--logging-telemetry-and-auditability)
    - [08 — Incident, drift and escalation response](2026-agent-compliance-implementation-guide.md#79-control-area-08--incident-drift-and-escalation-response)
    - [09 — Aggregate and trajectory governance](2026-agent-compliance-implementation-guide.md#710-control-area-09--aggregate-and-trajectory-governance)
8. [Reference Architecture for Verifiable Agent Governance](2026-agent-compliance-implementation-guide.md#8-reference-architecture-for-verifiable-agent-governance)
9. [Implementation Checklist](2026-agent-compliance-implementation-guide.md#9-implementation-checklist)
10. [Standards Proposals](2026-agent-compliance-implementation-guide.md#10-standards-proposals)
11. [What This Guide Does Not Claim](2026-agent-compliance-implementation-guide.md#11-what-this-guide-does-not-claim)
12. [Appendix A — Authoritative Sources](2026-agent-compliance-implementation-guide.md#appendix-a--authoritative-sources)
13. [Appendix B — EU AI Act Timeline](2026-agent-compliance-implementation-guide.md#appendix-b--eu-ai-act-timeline)
14. [Appendix C — Technical Standards and Cryptography Background](2026-agent-compliance-implementation-guide.md#appendix-c--technical-standards-and-cryptography-background)
15. [Appendix D — Adversary Model](2026-agent-compliance-implementation-guide.md#appendix-d--adversary-model)
16. [Appendix E — Global Jurisdiction Map](2026-agent-compliance-implementation-guide.md#appendix-e--global-jurisdiction-map)
17. [Appendix F — Role Inventory and Reader Map](2026-agent-compliance-implementation-guide.md#appendix-f--role-inventory-and-reader-map)

### Standards proposals arising from the guide

[§10](2026-agent-compliance-implementation-guide.md#10-standards-proposals) sketches proposals that the [AAIP track](../standards/) is turning into submittable documents. AAIP-001 and AAIP-002 are reserved against §10.3 and §10.4.
