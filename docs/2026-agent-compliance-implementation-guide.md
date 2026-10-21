# DAIAA Agent Compliance and Implementation Guide

*A practical reference for regulatory compliance, security implementation, audit assurance, and legal strategy in autonomous AI systems.*

> **Warning:** This guide is a structured compliance and technical reference, not legal advice. Where this document conflicts with primary legislation, official regulatory guidance, or binding standards, those primary sources control.
> 

# 1. Executive Summary

Autonomous AI agents create a compliance problem that traditional governance frameworks were not designed to handle. They can retrieve data, invoke tools, delegate tasks, call external systems, and make decisions faster than human reviewers can inspect each step.

Existing regulations and standards already require many of the right outcomes: logging, monitoring, risk classification, access control, human oversight, incident response, and protection of records. The unresolved question is whether the evidence produced by an autonomous system can be checked by a relying party without trusting the system operator that produced it.

This guide maps agentic AI obligations to eight evidence control areas and explains how organizations can move from documented controls to operational and independently verifiable controls. It is written for compliance officers, CISOs, developers, auditors, legal teams, and strategic advisors preparing for EU AI Act, DORA, ISO 42001, ISO 27001, SOC 2, privacy, and sector-specific obligations.

Zero-Knowledge Boundary Compliance (ZKBC) is presented as one implementation architecture for producing privacy-preserving, verifiable evidence. The broader requirement is technology-neutral: agentic AI systems should produce evidence that is tamper-evident, policy-bound, and independently replayable.

## The core problem

Every major framework requires some form of record, log, assessment, report, or retained evidence. But most frameworks do not require that anyone outside the record holder can independently check that evidence.

That creates a structural weakness:

- A provider may generate the evidence.
- The same provider may store the evidence.
- The same provider may define the reference values.
- The same provider may verify whether the evidence passes.
- A regulator, customer, auditor, or relying party may only receive an assertion.

For ordinary systems, this may be acceptable. For autonomous systems acting at machine speed across data stores, tools, identities, vendors, and jurisdictions, it is not enough.

The target state is verifiable governance:

> Evidence should be generated automatically, bound to the policy in force at the time, protected against alteration, and independently checkable by a party other than the one whose conduct is being assessed.
> 

## The practical goal

This guide helps teams answer four questions:

1. **What obligations apply?**
2. **What evidence should the system produce?**
3. **Who needs to verify that evidence?**
4. **Can the verification happen without relying on the claimant’s own assertion?**

---

# 2. Who Should Use This Guide

This document is intended for four primary user categories. Each group reads the guide differently, but all four need a shared vocabulary for agentic AI compliance evidence.

## 2.1 Governance & Compliance Architects

*"I need to understand what regulations apply and how to build a compliant program."*

**Primary roles**

- Compliance officers
- CISOs operating from a governance and risk perspective
- Chief risk officers
- Chief compliance officers
- AI ethics officers
- Privacy officers and data protection officers
- Regulatory affairs managers
- Policy analysts
- Board and audit committee members

**How they use this guide**

- Map EU AI Act, DORA, ISO 42001, ISO 27001, SOC 2, and privacy obligations to practical control areas.
- Build internal AI governance programs around the eight control areas.
- Use the maturity model to move from paper compliance to operational evidence.
- Prepare board-level reporting on agentic AI risk.
- Understand cross-border compliance where privacy, financial resilience, AI governance, and operational security overlap.

**Most relevant sections**

- Section 3 — Core Concepts
- Section 4 — The Compliance Problem
- Section 5 — Regulatory and Audit Obligation Map
- Section 6 — Evidence Maturity Model
- Section 7 — The Eight Control Areas
- Appendix A — Authoritative Sources
- Appendix B — EU AI Act Timeline
- Appendix F — Role Inventory and Reader Map

## 2.2 Technical Security Implementers

*"I need to build systems that satisfy compliance and cryptographic evidence requirements."*

**Primary roles**

- Security architects
- Developers and software engineers
- ML engineers and AI engineers
- DevSecOps engineers
- Site reliability engineers
- Infrastructure engineers
- Cryptographers and security researchers
- Technical implementers building compliance tooling

**How they use this guide**

- Translate governance requirements into enforcement points, logs, receipts, schemas, and verification flows.
- Understand how ZKBC, MPC, threshold cryptography, attestation, signed receipts, and transparency mechanisms can support evidence generation.
- Identify what is standardized and what is still implementation-specific.
- Design systems that bind actions to identity, delegation scope, policy version, and evidence artifacts.
- Prepare technical evidence that auditors and customers can actually evaluate.

**Most relevant sections**

- Section 7 — The Eight Control Areas
- Section 8 — Reference Architecture
- Section 9 — Implementation Checklist
- Appendix C — Technical Standards and Cryptography Background
- Appendix D — Adversary Model
- Appendix E — Global Jurisdiction Map

## 2.3 Audit & Assurance Professionals

*"I need to verify compliance claims and assess evidence quality."*

**Primary roles**

- Internal auditors
- External auditors
- Big 4 and specialized compliance firms
- Audit preparation teams
- Third-party risk managers
- SOC 2 lead auditors
- ISO 27001 and ISO 42001 lead auditors
- Vendor due diligence teams

**How they use this guide**

- Distinguish evidence from assurance.
- Assess whether a control is merely documented, actually operational, or adversarial-ready.
- Test whether logs, receipts, and attestations are independently checkable.
- Evaluate whether the verifier is independent from the attester.
- Design audit procedures for agentic AI systems where traditional sampling may be insufficient.

**Most relevant sections**

- Section 4 — The Compliance Problem
- Section 6 — Evidence Maturity Model
- Section 7 — The Eight Control Areas
- Section 9 — Implementation Checklist
- Section 10 — Standards Proposals
- Appendix A — Authoritative Sources
- Appendix D — Adversary Model
- Appendix F — Role Inventory and Reader Map

## 2.4 Legal & Strategic Advisors

*"I need to advise on liability, vendor contracts, procurement, and strategic risk."*

**Primary roles**

- General counsel and chief legal officers
- In-house and external legal counsel
- Privacy lawyers
- Technology transaction lawyers
- Insurance and risk advisors
- Management consultants
- Procurement officers evaluating AI vendors
- Business leaders responsible for regulated AI deployment

**How they use this guide**

- Understand where accountability gaps arise between providers, deployers, vendors, verifiers, and relying parties.
- Translate evidence requirements into contracts, vendor due diligence, procurement criteria, and audit rights.
- Evaluate whether vendor claims about “attestation,” “compliance,” or “verification” are meaningful.
- Plan for future obligations under the EU AI Act and adjacent frameworks.
- Prepare for disputes where proof quality, not only policy wording, determines evidentiary weight.

**Most relevant sections**

- Section 4 — The Compliance Problem
- Section 5 — Regulatory and Audit Obligation Map
- Section 10 — Standards Proposals
- Appendix A — Authoritative Sources
- Appendix B — EU AI Act Timeline
- Appendix F — Role Inventory and Reader Map

---

# 3. Core Concepts

| Term | Plain-English meaning |
| --- | --- |
| **Agentic AI system** | An AI system that can take actions through tools, APIs, memory, retrieval, delegation, or external services. |
| **Compliance evidence** | Records, logs, receipts, attestations, proofs, or artifacts showing what happened and why it was permitted. |
| **Assurance** | A statement that a control worked. |
| **Evidence** | The underlying artifact that lets someone check whether the control worked. |
| **Attestation** | A signed claim about a system, environment, execution state, measurement, or evidence result. |
| **Attester** | The party or system producing evidence about itself. |
| **Verifier** | The party or system checking evidence against policies, reference values, or expected properties. |
| **Relying party** | The person or organization that depends on the verification result. |
| **Reference value** | The expected measurement, policy, configuration, or baseline against which evidence is checked. |
| **Policy version binding** | Recording which policy authorized an action at the time it occurred. |
| **Delegation scope** | The authority, limits, and conditions that travel when one agent, service, or user delegates work to another. |
| **Independent replayability** | The ability for another party to re-check a result without trusting the original producer. |
| **Tamper-evidence** | The ability to detect alteration, rollback, truncation, or inconsistency in records. |
| **ZKBC** | Zero-Knowledge Boundary Compliance: an implementation pattern using gateways, policy commitments, and cryptographic proofs to verify agent boundaries without exposing sensitive data. |
| **MPC** | Multi-party computation: a method for computing over inputs distributed across parties without each party revealing its raw input. |
| **ZK proof** | A cryptographic proof that a statement is true without revealing the underlying private data. |
| **Transparency log** | An append-only log that supports public or third-party consistency checking. |
| **Canonical serialization** | A fixed way to turn a record into bytes so different parties can independently hash and verify the same facts. |

---

# 4. The Compliance Problem

## 4.1 What frameworks already require

The relevant frameworks do not start from zero. Most already require one or more of the following:

- Logs
- Monitoring
- Risk assessments
- Technical documentation
- Audit trails
- Access controls
- Human oversight
- Incident response
- Data protection records
- Business continuity controls
- Third-party risk management
- Evidence for internal or external audit

The problem is not that compliance frameworks ignore records. The problem is that they usually assume the record holder is an acceptable custodian of the record.

## 4.2 Why agentic AI changes the evidence problem

Autonomous agents can:

- Act continuously rather than at discrete human-approved moments.
- Chain actions across tools and services.
- Retrieve data from multiple repositories.
- Delegate work to other agents or services.
- Use third-party model endpoints.
- Combine data across purposes and jurisdictions.
- Trigger financial, legal, operational, or security consequences.
- Produce high-volume evidence that manual sampling cannot meaningfully cover.

This creates three key gaps:

1. **Boundary gap** — Did the agent stay within authorized data, tool, purpose, and jurisdictional boundaries?
2. **Delegation gap** — Did the original authority and scope survive across hops?
3. **Verification gap** — Can a relying party check the evidence without trusting the system operator?

## 4.3 The evidence principle

For agentic systems, a compliance record is stronger when it has these properties:

| Property | Why it matters |
| --- | --- |
| **Generated automatically** | Reduces after-the-fact reconstruction and selective reporting. |
| **Policy-bound** | Shows what rule authorized the action at the time. |
| **Identity-bound** | Shows which user, agent, service, or delegated authority acted. |
| **Tamper-evident** | Makes alteration detectable. |
| **Replayable** | Lets another party re-check the result. |
| **Minimally revealing** | Protects sensitive data while preserving verifiability. |
| **Independently verifiable** | Reduces reliance on the party whose conduct is being assessed. |

## 4.4 What this means for you

> **Governance & Compliance Architects:** Build programs around evidence properties, not only policy statements. Ask what proof each obligation produces.
> 

> **Technical Security Implementers:** Instrument enforcement points. Every tool call, retrieval, delegation, and policy decision should produce structured evidence.
> 

> **Audit & Assurance Professionals:** Test whether evidence can be checked independently. A dashboard showing “pass” is not the same as replayable evidence.
> 

> **Legal & Strategic Advisors:** Translate evidence properties into contracts, procurement requirements, audit rights, liability allocation, and dispute readiness.
> 

---

# 5. Regulatory and Audit Obligation Map

This section summarizes common obligations across major frameworks. It is an interpretive mapping, not a legal determination.

| Framework | Main obligation | Agentic AI concern | Evidence needed | Relevant control areas |
| --- | --- | --- | --- | --- |
| **EU AI Act** | Logging, transparency, risk management, human oversight, technical documentation | Agents may qualify as high-risk systems and generate high-volume autonomous activity | Event logs, risk classification, policy versions, human escalation records, post-market monitoring evidence | 02, 05, 07, 08 |
| **DORA** | ICT risk management, resilience testing, incident reporting, third-party risk | Agents operate across ICT dependencies, vendors, and decentralized infrastructure | Resilience test evidence, incident records, third-party evidence, continuity records | 03, 04, 07, 08 |
| **GDPR** | Privacy by design, records of processing, lawful basis, data minimization | Agents can combine data across purposes, systems, and contexts | Purpose binding, access records, processing records, minimization evidence | 05, 06, 07 |
| **CCPA / CPRA** | Consumer rights, automated decision-making disclosures, deletion and opt-out rights | Persistent agent memory and opaque decision trails complicate explainability and revocation | Consent state, deletion records, decision records, context access logs | 05, 06, 07 |
| **HIPAA** | PHI access control, audit trails, minimum necessary standard | Agents may retrieve more health information than needed unless constrained at retrieval time | Access logs, minimum-necessary checks, user identity, data segment evidence | 04, 05, 06, 07 |
| **PCI DSS v4.0** | Cardholder data isolation, access logging, tokenization, security controls | Financial tool calls and logs may leak CHD into prompts, memory, or downstream systems | Tool argument sanitization, redaction records, access logs, data-flow records | 04, 05, 06, 07 |
| **ISO/IEC 42001** | AI management system, monitoring, evaluation, improvement | Governance must be operationalized across lifecycle and deployment | AI inventory, risk assessments, monitoring evidence, improvement records | 01, 02, 07, 08 |
| **ISO/IEC 27001** | ISMS controls, access control, logging, monitoring, record protection | Agents expand the attack surface across prompts, tools, memory, and identities | Access evidence, log protection, monitoring records, privileged activity records | 04, 06, 07, 08 |
| **SOC 2 Type II** | Security, confidentiality, processing integrity over an audit period | Sampling may be weak for high-volume autonomous activity | Continuous control evidence, exceptions, change records, processing integrity evidence | 04, 05, 07, 08 |
| **NIST AI RMF** | Govern, Map, Measure, Manage AI risks | Risk measurement must occur during dynamic tool use and deployment | Risk metrics, impact assessments, monitoring records, mitigation evidence | 01, 02, 07, 08 |

## 5.1 DORA alignment example

| DORA theme | Agentic AI control need | Evidence pattern |
| --- | --- | --- |
| ICT risk management | Know what agents, tools, model endpoints, and infrastructure are in scope | Inventory, architecture map, access graph, policy records |
| Incident management | Detect and report agentic failures quickly | Tamper-evident incident records, policy breach receipts, escalation logs |
| Resilience testing | Prove the system can withstand failure or compromise | Adversarial exercises, chaos testing results, recovery evidence |
| Third-party risk | Evaluate external models, vendors, APIs, and data processors | Vendor attestations, independent verification records, contract evidence |
| Business continuity | Maintain operation under stress | Recovery plans, failover evidence, continuity tests |
| Reporting to authorities | Produce accurate, privacy-preserving reports | Policy-bound summaries, retained evidence, verification receipts |

## 5.2 ISO 27001 / ISO 27002 logging nuance

ISO 27001 and ISO 27002 require logs and records to be protected against alteration, deletion, and misuse, including by privileged users. However, they do not generally require that a relying party outside the custodian’s control be able to independently re-derive the record or detect alteration without the custodian’s cooperation.

That distinction matters for agentic AI. Internal log protection is necessary, but it is not the same as independently verifiable evidence.

## 5.3 What this means for you

> **Governance & Compliance Architects:** Use this map to connect regulatory obligations to control areas, owners, and evidence requirements.
> 

> **Technical Security Implementers:** Turn each “evidence needed” entry into concrete logs, receipts, schemas, policy checks, and retention rules.
> 

> **Audit & Assurance Professionals:** Treat framework mapping as an audit planning input. Confirm the legal basis, then test whether evidence exists and is reliable.
> 

> **Legal & Strategic Advisors:** Use this table to identify where contracts, vendor obligations, audit rights, indemnities, and regulatory representations may be needed.
> 

---

# 6. Evidence Maturity Model

Agentic AI compliance should not be measured by a single pass/fail label. A control that exists on paper is materially different from a control that is enforced in production and tested under adversarial conditions.

| Level | Meaning | Typical evidence | Reader takeaway |
| --- | --- | --- | --- |
| **Documented** | The control exists and is described. | Policies, procedures, architecture documents, responsibility matrices | Useful for governance design, weak for runtime assurance. |
| **Operational** | The control is enforced in the running system and produces evidence. | Logs, receipts, alerts, access records, approval records, policy decision records | Suitable for internal monitoring and ordinary audit. |
| **Adversarial-ready** | The control has been exercised against attempts to defeat it and survived with evidence. | Red-team reports, containment tests, replay tests, tamper-evidence tests, incident drills | Appropriate for high-risk systems, critical infrastructure, and contested evidence environments. |

The overall maturity of an agentic AI governance system should be treated as the minimum maturity across its weakest relevant control area. A system that is adversarial-ready on access control but merely documented on shadow-AI discovery still has a specific, addressable weakness.

## What this means for you

> **Governance & Compliance Architects:** Set target maturity by use case. Not every system needs adversarial-ready evidence, but high-risk systems should not rely on documented-only controls.
> 

> **Technical Security Implementers:** Design for operational and adversarial-ready evidence from the start. Retrofitting replayability and tamper-evidence is difficult.
> 

> **Audit & Assurance Professionals:** Report maturity per control area. A single overall pass hides which controls actually need remediation.
> 

> **Legal & Strategic Advisors:** Align contractual representations with maturity level. Do not let vendors describe documented controls as if they are independently verified controls.
> 

---

# 7. The Eight Control Areas

The eight control areas are the backbone of this guide. They are not new legal obligations. They are the evidence categories that existing obligations already imply for agentic systems.

## 7.1 Summary table

| # | Control area | Plain-English purpose |
| --- | --- | --- |
| **01** | AI inventory and shadow-AI discovery | Know what AI systems, agents, models, endpoints, and tools are actually running. |
| **02** | Use-case classification and risk assessment | Know which uses fall into which regulatory, safety, or business risk categories. |
| **03** | Model and data provenance | Know where models and data came from and whether that history can be reconstructed. |
| **04** | Sanctioned-application control | Know which tools, applications, APIs, and endpoints agents are allowed to use. |
| **05** | Prompt and output governance | Know what goes in, what comes out, and what must be retained or redacted. |
| **06** | Identity and access control for AI | Know which identity acts, what authority it carries, and how delegation is constrained. |
| **07** | Logging, telemetry and auditability | Know whether records exist and whether they can be independently re-derived. |
| **08** | Incident, drift and escalation response | Know what happens when behavior changes, boundaries fail, or escalation is required. |

---

## 7.2 Control Area 01 — AI Inventory and Shadow-AI Discovery

**Purpose**  

Know what AI systems, agents, models, endpoints, tools, data stores, and owners are actually in use.

**Why it matters**  

You cannot govern, secure, or audit systems you cannot list.

**Minimum evidence**

- Inventory of agents, models, endpoints, tools, and owners
- Production, staging, development, and experimental status
- Date added, changed, approved, deprecated, or removed
- Data categories accessible
- Business owner and technical owner
- Approval status and risk tier

**Implementation notes**

- Maintain a machine-readable registry.
- Block unregistered tools and model endpoints by default.
- Log discovery of new endpoints and unauthorized tool use.
- Tie inventory to CI/CD, runtime gateway telemetry, procurement, and vendor management.

**Maturity examples**

- **Documented:** Inventory spreadsheet or policy exists.
- **Operational:** Runtime systems enforce registration before use.
- **Adversarial-ready:** Shadow endpoints are deliberately introduced in tests and detected.

---

## 7.3 Control Area 02 — Use-Case Classification and Risk Assessment

**Purpose**  

Classify agentic AI use cases by regulatory, operational, privacy, safety, financial, and reputational risk.

**Why it matters**  

Most obligations depend on use case, impact, jurisdiction, sector, and affected population.

**Minimum evidence**

- Use-case description
- Regulatory classification
- Risk assessment rationale
- Impact assessment
- Human oversight requirements
- Jurisdictional scope
- Approval and review history

**Implementation notes**

- Classify at the workflow level, not only the model level.
- Reassess classification when tools, data access, autonomy, or deployment context changes.
- Bind classification to runtime policy enforcement.

**Maturity examples**

- **Documented:** Risk classification matrix exists.
- **Operational:** Deployment gates require classification before production.
- **Adversarial-ready:** Misclassified or unclassified workflows are tested and blocked.

---

## 7.4 Control Area 03 — Model and Data Provenance

**Purpose**  

Preserve evidence of where models, datasets, embeddings, prompts, policies, and reference values came from.

**Why it matters**  

Attestation can show what is running now, but it does not prove the pre-deployment history was trustworthy.

**Minimum evidence**

- Model source and version
- Dataset source and permitted use
- Training, fine-tuning, or retrieval source records
- Build provenance
- Reference value owner
- Integrity hashes and signing records
- Change history

**Implementation notes**

- Use software supply chain controls, signed artifacts, model cards, data lineage, and reproducible build records.
- Record who computed reference values and whether that party is independent from the provider.

**Maturity examples**

- **Documented:** Provenance records are manually maintained.
- **Operational:** Build and deployment pipelines produce signed provenance evidence.
- **Adversarial-ready:** Tampered artifacts and disputed reference values are tested.

---

## 7.5 Control Area 04 — Sanctioned-Application Control

**Purpose**  

Restrict agents to approved tools, applications, APIs, model endpoints, data sources, and execution environments.

**Why it matters**  

An agent can create compliance risk by using an unauthorized tool even if the model itself is approved.

**Minimum evidence**

- Approved application and tool list
- Tool authorization policy
- Denied tool-call records
- Exception approvals
- Vendor status
- Data categories permitted per tool

**Implementation notes**

- Enforce tool allowlists at the gateway or runtime layer.
- Treat tool use as a security boundary.
- Record tool arguments, sensitive field handling, redactions, and policy decision results.

**Maturity examples**

- **Documented:** Approved tool list exists.
- **Operational:** Unauthorized tools are blocked at runtime.
- **Adversarial-ready:** Attempts to bypass tool restrictions are tested and recorded.

---

## 7.6 Control Area 05 — Prompt and Output Governance

**Purpose**  

Govern what enters the model, what leaves the model, and what must be retained, redacted, minimized, or explained.

**Why it matters**  

Prompt and output records often contain the evidence needed to explain decisions, investigate incidents, and respond to legal requests.

**Minimum evidence**

- Prompt or prompt commitment
- Retrieved context or context commitment
- Output or output commitment
- Redaction records
- Policy version in force
- Data categories used
- Retention and deletion status
- Human review records where applicable

**Implementation notes**

- Avoid storing unnecessary sensitive plaintext.
- Use commitments, hashes, encryption, or ZK proofs where full plaintext retention is not appropriate.
- Bind prompt, context, output, and policy version together.

**Maturity examples**

- **Documented:** Prompt retention policy exists.
- **Operational:** Prompt and output governance runs at gateway level.
- **Adversarial-ready:** Prompt injection, data exfiltration, and redaction bypass attempts are tested.

---

## 7.7 Control Area 06 — Identity and Access Control for AI

**Purpose**  

Record which user, agent, service, or delegated authority acted, and what scope of authority traveled with the action.

**Why it matters**  

Agentic systems blur the distinction between who authorized an action and what system executed it.

**Minimum evidence**

- Acting identity
- Authorizing principal
- Delegation chain
- Scope and conditions of authority
- Token or credential boundaries
- Access decision records
- Revocation status

**Implementation notes**

- Do not let delegation carry only a task description. It must also carry scope.
- Preserve authority boundaries across agent-to-agent and agent-to-service hops.
- Bind identity, delegation, policy, and action together.

**Maturity examples**

- **Documented:** Identity and delegation policy exists.
- **Operational:** Runtime enforces delegated scope.
- **Adversarial-ready:** Scope confusion, privilege escalation, and cross-agent delegation failures are tested.

---

## 7.8 Control Area 07 — Logging, Telemetry and Auditability

**Purpose**  

Ensure records exist, are protected, and can be independently checked where required.

**Why it matters**  

A log that only the custodian can interpret or validate may be weak evidence when challenged.

**Minimum evidence**

- Event records
- Policy decision records
- Integrity hashes
- Append-only commitments
- External anchors or witnessed commitments where appropriate
- Verification receipts
- Retention records
- Access to audit evidence

**Implementation notes**

- Decide on canonical serialization before deployment.
- Use tamper-evident logs, signed receipts, transparency services, witness cosigning, or external anchoring where appropriate.
- Design for independent replayability.

**Maturity examples**

- **Documented:** Logging policy exists.
- **Operational:** Logs are generated, protected, monitored, and retained.
- **Adversarial-ready:** Alteration, rollback, truncation, and verifier disagreement are tested.

---

## 7.9 Control Area 08 — Incident, Drift and Escalation Response

**Purpose**  

Detect, escalate, investigate, and remediate agent behavior that changes, exceeds policy, or produces harmful outcomes.

**Why it matters**  

Autonomous systems can fail through drift, tool misuse, prompt injection, delegation errors, or policy boundary failures.

**Minimum evidence**

- Incident records
- Drift detection records
- Escalation rules
- Human intervention records
- Root-cause analysis
- Remediation actions
- Post-incident control updates
- Regulatory reporting records where required

**Implementation notes**

- Define what constitutes an agentic incident.
- Treat containment failures as reportable internal events even when no external harm occurred.
- Exercise escalation workflows before production incidents occur.

**Maturity examples**

- **Documented:** Incident response policy includes AI systems.
- **Operational:** Alerts and escalation workflows run in production.
- **Adversarial-ready:** Red-team and tabletop exercises test agent containment failures.

---

# 8. Reference Architecture for Verifiable Agent Governance

The architecture below is technology-neutral. ZKBC is one implementation profile for achieving the evidence properties described in this guide.

```
[ USER / ENTERPRISE APPLICATION ]
              │
              ▼
[ POLICY ISSUER / GOVERNANCE LAYER ]
              │
              ▼
[ COMPLETION GATEWAY ]
  - prompt screening
  - output screening
  - sensitive data handling
  - policy checks
              │
              ▼
[ AGENT RUNTIME ]
  - planning
  - tool selection
  - delegation
  - retrieval
              │
              ▼
[ BOUNDARY COMPLIANCE GATEWAY ]
  - tool mediation
  - access control
  - jurisdiction checks
  - data minimization
  - evidence generation
              │
              ▼
[ EXTERNAL TOOLS / DATA STORES / MODEL ENDPOINTS ]
              │
              ▼
[ EVIDENCE JOURNAL / RECEIPT LAYER ]
  - event records
  - policy version commitments
  - identity and delegation records
  - integrity commitments
  - verification receipts
              │
              ▼
[ VERIFIER / RELYING PARTY ]
  - replays checks
  - validates evidence
  - evaluates independence
```

## 8.1 Core architecture components

| Component | Purpose |
| --- | --- |
| **Policy issuer** | Defines permitted actions, data access, escalation rules, jurisdictional limits, and evidence requirements. |
| **Completion gateway** | Screens prompts and outputs before the agent acts or responds. |
| **Agent runtime** | Executes tasks, calls tools, retrieves context, and delegates work. |
| **Boundary compliance gateway** | Mediates tool use, retrieval, external calls, data movement, and proof generation. |
| **Evidence journal** | Stores event records, commitments, hashes, receipts, policy versions, and retention state. |
| **Verifier** | Checks evidence against policy, reference values, and verification procedures. |
| **Relying party** | Uses the verification result for compliance, procurement, audit, legal, or operational decisions. |

## 8.2 ZKBC implementation profile

ZKBC can be used to implement this architecture by combining:

- Complete mediation of agent I/O channels
- Policy commitments
- Deterministic boundary checks
- Minimal public journals
- Zero-knowledge proofs
- Threshold cryptography
- MPC-based computation where multiple parties contribute sensitive inputs
- Recursive or cumulative receipts for high-volume activity

The compliance goal is not “use zero-knowledge everywhere.” The goal is to produce evidence that is privacy-preserving, tamper-evident, policy-bound, and independently verifiable.

## 8.3 What this means for you

> **Governance & Compliance Architects:** Use the architecture to assign owners, policies, evidence requirements, and escalation responsibilities.
> 

> **Technical Security Implementers:** Build enforcement at the gateway and runtime layers. Avoid relying on model behavior alone as a control.
> 

> **Audit & Assurance Professionals:** Ask whether each architecture component produces evidence and whether that evidence can be replayed or independently verified.
> 

> **Legal & Strategic Advisors:** Use the architecture to identify contract boundaries, vendor responsibilities, audit rights, data-processing roles, and liability allocation.
> 

---

# 9. Implementation Checklist

## 9.1 Eight questions to run this week

| # | Question | Primary owner | If the answer is no |
| --- | --- | --- | --- |
| **01** | Can we list every model endpoint and agent tool currently reachable, including those added recently? | CISO / engineering | Create an inventory, integrate it with runtime telemetry, and block unregistered endpoints. |
| **02** | For the riskiest agent action, can we name the regulatory class and show the reasoning? | Compliance / legal | Create a use-case classification process before further deployment. |
| **03** | For a production model, can we reconstruct which build produced it and who computed the reference value? | Engineering / security | Add provenance, build integrity, and reference-value ownership records. |
| **04** | Can an agent invoke a tool that is not on an approved list? | Security architecture / platform engineering | Enforce allowlists at the gateway or runtime layer. |
| **05** | For one output last Tuesday, can we retrieve the prompt, context, output, and policy version in force? | Compliance / engineering | Bind prompt, context, output, and policy version in the evidence record. |
| **06** | When Agent A delegates to Agent B, what carries the principal’s authorization scope? | Security architecture | Add delegation scope to identity and authorization records. |
| **07** | Could someone outside the organization detect if last month’s logs had been altered without relying on us? | CISO / audit | Add tamper-evidence, external commitments, receipts, or independent replayability. |
| **08** | Has anyone deliberately tried to make an agent leave its execution boundary, and is the attempt recorded? | Security / red team | Add adversarial containment tests and record the results. |

## 9.2 Design checklist

Build these properties in before deployment:

1. **Canonical serialization** — Decide exactly how records are serialized before hashing, signing, or proving them.
2. **Policy version binding** — Bind every action to the policy version that permitted it.
3. **Principal and delegation chain** — Record whose authority each hop used.
4. **Independent replayability** — Let another party re-derive the result from evidence and published checks.
5. **Evidence, not assurance** — Store the artifact that proves the control worked, not only the claim that it did.
6. **Adversarial exercise** — Test containment by attacking it.
7. **Evaluation-time containment** — Treat a boundary failure during testing as evidence, not as noise to be ignored.

---

# 10. Standards Proposals

The following proposals are small enough to be actionable and specific enough to be debated in standards or guidance work.

## 10.1 Verifier independence as a machine-checkable claim

**Target forums**  

IETF RATS, SCITT, ISO/IEC 17065-adjacent assurance models

**Problem**  

Current attestation architectures allow one organization to hold multiple roles. That may be valid, but independence is then an organizational claim rather than a machine-checkable property.

**Proposal**  

Evidence formats should disclose:

- Who operates the verifier
- Who owns the verifier policy
- Who supplies reference values
- Whether the verifier has a commercial, organizational, or control relationship with the attester
- Whether the relying party can independently re-check the result

## 10.2 Delegation scope as evidence

**Target forums**  

IETF RATS, SCITT, identity and authorization communities

**Problem**  

Authorization chaining exists, but agentic delegation often carries the task without carrying the principal’s authorized scope.

**Proposal**  

Evidence records should include:

- Principal
- Delegating party
- Acting party
- Scope granted
- Conditions and expiry
- Policy version
- Downstream delegation limits

## 10.3 Tamper-evidence for regulatory logs

**Target forums**  

EU AI Act guidance, ISO 42001, ISO 27001/27002 guidance, sector regulators

**Problem**  

Regulatory logs may be protected internally but not independently re-derivable by relying parties.

**Proposal**  

Logs generated for high-risk AI systems should be:

- Canonically serialized
- Integrity-protected
- Policy-bound
- Externally anchored or witnessed where appropriate
- Replayable by authorized third parties

## 10.4 Adversarial exercise as an attestation grade

**Target forums**  

NIST AI RMF, ISO 42001, audit and assurance standards

**Problem**  

A documented control and an adversarially tested control are materially different, but current assurance artifacts often collapse them into one status.

**Proposal**  

Control maturity should be separately reportable as:

- Documented
- Operational
- Adversarial-ready

---

# 11. What This Guide Does Not Claim

This document is intentionally careful about its boundaries.

## 11.1 It does not claim ZKBC is the only solution

ZKBC is one architecture for achieving privacy-preserving verification. Other valid approaches may use confidential computing, signed receipts, secure enclaves, transparency logs, third-party attestation, formal methods, or conventional audit evidence.

## 11.2 It does not claim zero-knowledge circuits are standardized

Many ZK systems are well studied and widely implemented, but ZK circuit schemes and ZK virtual machines are not standardized in the same way as AES, SHA-3, ECDSA, ML-KEM, or ML-DSA.

## 11.3 It does not claim attestation proves intent

Attestation can show what code, model, or environment was measured. It does not prove that the system’s goals were correct, benign, lawful, or aligned with human intent.

## 11.4 It does not claim multi-hop agentic verification is solved

Single-hop attestation, authorization chaining, and software provenance have mature components. General compound attestation across mutually distrusting parties running non-deterministic agents remains an open area.

## 11.5 It does not claim regulatory mapping is legal determination

The mappings are reasoned interpretations to support governance, implementation, and assurance planning. Qualified legal counsel should confirm binding obligations.

---

# Appendix A — Authoritative Sources

## A.1 Source hierarchy

When sources conflict, apply this hierarchy:

1. **Primary legislation** — Official Journal of the EU, Federal Register, statutory text.
2. **Delegated and implementing acts** — RTS, ITS, Commission regulations, binding technical rules.
3. **Official guidance** — Commission FAQs, supervisory authority guidance, ESMA/EBA/EIOPA guidance.
4. **Technical standards** — ISO, IEC, IETF RFCs, NIST publications.
5. **Industry research** — Security reports, whitepapers, academic literature, vendor analysis.

## A.2 Primary legislation and regulatory sources

| Source | Relevance |
| --- | --- |
| Regulation (EU) 2024/1689 — Artificial Intelligence Act | Risk-based AI governance, high-risk system obligations, logging, transparency, oversight. |
| Regulation (EU) 2026/1744 — Digital Omnibus on AI | Amended AI Act dates and transitional provisions. |
| Regulation (EU) 2022/2554 — DORA | ICT risk management, incident reporting, resilience testing, third-party risk for financial entities. |
| GDPR | Privacy by design, records of processing, lawful basis, data minimization, data subject rights. |
| NIS2 Directive | Network and information security obligations across essential and important sectors. |
| MiCA | Crypto-asset and stablecoin regulatory obligations where relevant. |

## A.3 Management and audit frameworks

| Framework | Relevance |
| --- | --- |
| ISO/IEC 42001:2023 | AI management system standard. |
| ISO/IEC 27001:2022 | Information security management system. |
| ISO/IEC 27002:2022 | Security control guidance, including logging and monitoring. |
| SOC 2 Type II | Trust Services Criteria over an operating period. |
| NIST AI RMF 1.0 | Govern, Map, Measure, Manage AI risks. |
| Singapore Model AI Governance Framework | Human-centric, operational AI governance model. |

## A.4 Technical and attestation sources

| Source | Relevance |
| --- | --- |
| RFC 9334 — RATS Architecture | Defines attestation roles and trust relationships. |
| RFC 9711 — Entity Attestation Token | EAT format for attestation evidence. |
| RFC 9393 — CoSWID | Software identification and supply-chain metadata. |
| RFC 9683 — Remote Integrity Verification | TPM-based network device attestation. |
| RFC 6962 and RFC 9162 | Certificate Transparency and transparency log concepts. |
| RFC 8785 | JSON Canonicalization Scheme. |
| RFC 8949 | CBOR and deterministic encoding guidance. |
| draft-ietf-scitt-architecture | Supply Chain Integrity, Transparency and Trust architecture. |
| draft-ietf-rats-ar4si | Attestation results for secure interactions. |
| draft-hillier-certisyn-ai-governance-verified | Individual submission on AI governance verification artifacts. |
| draft-hillier-certisyn-essential-eight-verified | Individual submission on cyber hygiene verification. |
| draft-hillier-scitt-arp | Individual submission on attestation reconciliation. |

---

# Appendix B — EU AI Act Timeline

> **Note:** Use the primary Official Journal text and competent authority guidance before relying on any operational date. This table reflects the guide’s working interpretation of the amended timeline.
> 

| Obligation area | Date | Notes |
| --- | --- | --- |
| Prohibited practices | 2 February 2025 | Article 5 prohibitions. |
| GPAI model obligations | 2 August 2025 | Core GPAI model obligations. |
| Article 50(2) GPAI transparency | 2 August 2026 | Transparency / watermarking obligations for new systems. |
| Article 50(2) grace period for certain pre-market systems | 2 December 2026 | Grace for systems already on market before 2 August 2026, subject to applicable rules. |
| Legacy GPAI models | 2 August 2027 | Transitional treatment under relevant provisions. |
| Annex III high-risk systems | 2 December 2027 | Use-case high-risk systems. |
| Annex I high-risk systems | 2 August 2028 | Product-regulated high-risk systems. |

## Why the timeline matters

The deferral of some high-risk obligations is not a removal of the requirement. It creates a build window for evidence infrastructure, governance processes, technical controls, and audit readiness.

---

# Appendix C — Technical Standards and Cryptography Background

## C.1 Standards bodies and ZK circuit status

| Standards body | Cryptographic standards issued | ZK circuit status |
| --- | --- | --- |
| **NIST** | Post-quantum algorithms, hash functions, block ciphers, digital signatures, key management | No general ZK circuit standard. |
| **ISO/IEC JTC 1/SC 27** | ISO 27001, ISO 42001, digital signatures, entity authentication | Anonymous credentials exist, but general ZK circuits are not standardized. |
| **IETF** | TLS, PKIX, RATS, SCITT, hash-to-curve, cryptographic message formats | Some ZK-adjacent work, but no general ZK circuit standard. |
| **IEEE** | Public key cryptography and related standards | No general ZK circuit standard. |
| **ETSI** | Quantum-safe cryptography and trust services | No general ZK circuit standard. |

## C.2 What is standardized

| Component | Example standard |
| --- | --- |
| Hash functions | SHA-2, SHA-3, FIPS 202 |
| Post-quantum KEM | ML-KEM, FIPS 203 |
| Post-quantum signatures | ML-DSA, FIPS 204 |
| JSON canonicalization | RFC 8785 |
| CBOR deterministic encoding | RFC 8949 |
| Attestation architecture | RFC 9334 |
| Entity attestation token | RFC 9711 |
| Software identifiers | RFC 9393 |
| Some ZK-friendly curve parameters | IETF curve-related RFCs |

## C.3 What is not standardized

| Component | Status |
| --- | --- |
| Groth16, PLONK, STARKs as compliance standards | Not standardized as general regulatory compliance mechanisms. |
| ZK circuits for AI governance | Not standardized. |
| ZK virtual machines such as RISC0 or Cairo | Implementation-specific. |
| ZKBC evidence schema | Requires definition by implementer or standards work. |

## C.4 Compliance implications of non-standardized ZK

| Consideration | Implication | Mitigation |
| --- | --- | --- |
| Regulatory acceptance | Some regulators or auditors may question non-standard cryptography. | Document scheme choice, threat model, assumptions, and security proofs. |
| Audit readiness | Many auditors lack deep ZK expertise. | Engage specialized cryptographic auditors where needed. |
| Scheme agility | ZK systems evolve quickly. | Design systems to migrate schemes over time. |
| Evidence interpretation | A proof alone may not explain the control. | Pair proofs with clear evidence schemas and human-readable control mappings. |

---

# Appendix D — Adversary Model

This appendix defines what the evidence model can and cannot protect against.

| Adversary | In scope? | Capability and limit |
| --- | --- | --- |
| **A0 — Network** | Yes | Can intercept, reorder, replay, drop, or forge traffic in transit. |
| **A1 — Storage** | Partly | Can read or write the record store after the fact. Alteration is detectable if commitments exist. Rollback and truncation require external anchors or witnesses. |
| **A2 — Custodian** | Partly | The record holder may alter or selectively present records. Integrity can be checked only relative to commitments outside unilateral custodian control. |
| **A3 — Verifier** | Partly | The verifier may be captured, wrong, or colluding. Independent replayability allows another verifier to detect disagreement. |
| **A4 — Generation-time host** | No | A compromised kernel, hypervisor, or equivalent host may emit a faithful record of a false event before first commitment. Hardware roots of trust are needed for this layer. |
| **A5 — Signing environment** | No | If the signing environment or key is compromised, forged records may appear valid. |
| **A6a — Signature scheme break** | No | Future signature forgeries may become possible. Re-anchoring under a new scheme can help for future claims. |
| **A6b — Hash function break** | No | Collision or second-preimage breaks can undermine historic commitments. Re-anchoring cannot fully repair this retroactively. |

## D.1 Omission, time, and ground truth

| Issue | Limit |
| --- | --- |
| **Reconciliation** | Detects disagreement between records that exist. |
| **Ordering** | Strong only when anchored outside the custodian’s unilateral control. |
| **Ground truth** | Evidence shows what records say and whether they agree; it does not prove a real-world event occurred. |
| **Omission** | An event that produced no record may be invisible unless another independent signal implies a record should exist. |

---

# Appendix E — Global Jurisdiction Map

This appendix preserves broader jurisdictional considerations without overloading the main guide.

| Jurisdiction / framework | Main concern for agentic AI | Evidence focus |
| --- | --- | --- |
| **India DPDPA** | Consent, purpose limitation, breach notification, log retention | Purpose binding, consent state, breach detection records. |
| **Brazil LGPD** | Automated decision explanation and human review | Decision records, logic documentation, review evidence. |
| **China PIPL** | Sensitive personal information, cross-border transfer, localization | Geographic policy enforcement, transfer records, localization evidence. |
| **Canada AIDA** | High-impact AI systems, impact assessments, accountability | Impact assessment, classification, monitoring evidence. |
| **Korea PIPA** | Pseudonymization, breach notification, purpose limitation | Data minimization, pseudonymization evidence, breach records. |
| **Japan APPI** | Anonymization and third-party transfer rules | Anonymization evidence, transfer records. |
| **Australia Privacy Act reforms** | Fair and reasonable processing, breach notification, emerging AI obligations | Policy enforcement, fairness rationale, incident records. |
| **UK AI framework** | Contextual, sector-specific, risk-based governance | Sector-specific classification and control mapping. |
| **Thailand PDPA** | Consent withdrawal, purpose limitation, breach notification | Consent revocation, purpose binding, deletion evidence. |
| **Vietnam cybersecurity and data rules** | Local storage and important data controls | Classification, localization, transfer evidence. |

---

# Appendix F — Role Inventory and Reader Map

This appendix expands the target audience into a complete role inventory and maps those roles back to the four primary user categories used throughout the guide.

## F.1 Complete role inventory

### C-suite and executive leadership

| Role | Primary concern |
| --- | --- |
| **Chief Information Security Officers (CISOs)** | Security strategy, risk appetite, containment, incident response, and technical assurance. |
| **Chief Technology Officers (CTOs)** | Technical architecture, implementation feasibility, platform decisions, and engineering roadmap. |
| **Chief Information Officers (CIOs)** | IT governance, systems integration, enterprise operations, and control adoption. |
| **Chief Risk Officers (CROs)** | Enterprise risk management, operational resilience, cross-functional risk reporting. |
| **Chief Data Officers (CDOs)** | Data governance, data lineage, AI data strategy, and permitted use. |
| **Chief Compliance Officers (CCOs)** | Regulatory adherence across jurisdictions and evidence of control operation. |
| **Chief Legal Officers / General Counsel** | Legal risk, liability, contracts, regulatory exposure, and dispute readiness. |
| **Board Members / Audit Committee Members** | Oversight, fiduciary duty, risk appetite, governance maturity, and assurance reporting. |

### Governance and compliance specialists

| Role | Primary concern |
| --- | --- |
| **Compliance Officers** | Regulatory interpretation and implementation. |
| **AI Ethics Officers** | Responsible AI governance, oversight, and harm prevention. |
| **Privacy Officers / Data Protection Officers (DPOs)** | GDPR, privacy, lawful basis, data subject rights, and data minimization. |
| **Regulatory Affairs Managers** | Policy monitoring, regulatory response, and external engagement. |
| **Risk Managers** | Operational risk assessment and control monitoring. |
| **Policy Analysts** | Internal policy development, control mapping, and governance documentation. |

### Technical implementation teams

| Role | Primary concern |
| --- | --- |
| **Security Architects** | Secure AI infrastructure and boundary design. |
| **Developers / Software Engineers** | Building compliant agentic systems and evidence-generating workflows. |
| **ML Engineers / AI Engineers** | Model deployment, evaluation, monitoring, and integration with controls. |
| **DevSecOps Engineers** | Secure CI/CD for AI pipelines and runtime enforcement. |
| **Site Reliability Engineers (SREs)** | Production reliability, observability, incident response, and resilience. |
| **Infrastructure Engineers** | Cloud, on-premise, network, and execution environment controls. |
| **Cryptographers / Security Researchers** | ZK proof, MPC, threshold cryptography, and protocol design. |
| **Technical Implementers** | Hands-on compliance tooling, integrations, and automation. |

### Legal and risk advisory

| Role | Primary concern |
| --- | --- |
| **Legal Counsel** | Contract review, liability assessment, regulatory interpretation, and dispute preparation. |
| **Privacy Lawyers** | Data protection law, transfer restrictions, consent, and data subject rights. |
| **Technology Transaction Lawyers** | AI vendor agreements, warranties, audit rights, and evidence obligations. |
| **Insurance / Risk Advisors** | Cyber liability, E&O coverage, exclusions, and risk transfer. |

### Audit and assurance functions

| Role | Primary concern |
| --- | --- |
| **Internal Auditors** | Internal readiness, control testing, evidence collection, and remediation. |
| **External Auditors** | Independent assurance, certification, and evidence evaluation. |
| **Audit Preparation Teams** | Evidence collection, documentation, walkthroughs, and control narratives. |
| **Third-Party Risk Managers** | Vendor due diligence and ongoing monitoring. |
| **SOC 2 / ISO 27001 Lead Auditors** | Certification audit and control effectiveness assessment. |

### Product and business teams

| Role | Primary concern |
| --- | --- |
| **Product Managers (AI/ML)** | Feature development within compliance constraints. |
| **Procurement Officers** | Evaluating AI vendor compliance claims, warranties, and audit rights. |
| **Business Unit Leaders** | Operationalizing AI while staying within approved risk boundaries. |
| **Sales Engineers** | Demonstrating compliance evidence to enterprise customers. |

### External advisors and service providers

| Role | Primary concern |
| --- | --- |
| **Management Consultants** | Strategy, operating model, and implementation support. |
| **Compliance Consultants** | Specialized regulatory guidance and control design. |
| **Security Consultants** | Technical security architecture and adversarial testing. |
| **Systems Integrators** | End-to-end deployment, integration, and implementation. |

## F.2 Four primary reader categories

### Category 1 — The Governance & Compliance Architect

*"I need to understand what regulations apply and how to build a compliant program."*

**Primary roles**

- Compliance officers
- CISOs from a governance perspective
- Chief risk officers
- Chief compliance officers
- AI ethics officers
- Regulatory affairs managers
- Privacy officers and DPOs
- Board and audit committee members

**How they use this guide**

- As a primary reference for EU AI Act timeline and obligation mapping.
- For framework comparison across ISO 42001, NIST AI RMF, EU AI Act, DORA, ISO 27001, and SOC 2.
- For policy development using the eight control areas and three maturity levels.
- For board reporting using clear evidence and risk language.
- For cross-border compliance planning where DORA, EU AI Act, privacy, and sector rules intersect.

**Key sections**

- Section 5 — Regulatory and Audit Obligation Map
- Section 6 — Evidence Maturity Model
- Section 7 — The Eight Control Areas
- Appendix B — EU AI Act Timeline
- Appendix E — Global Jurisdiction Map

### Category 2 — The Technical Security Implementer

*"I need to build systems that satisfy compliance and cryptographic evidence requirements."*

**Primary roles**

- Security architects
- Developers and software engineers
- ML engineers and AI engineers
- DevSecOps engineers
- Infrastructure engineers
- SREs
- Cryptographers and security researchers
- Technical implementers

**How they use this guide**

- As an implementation roadmap for evidence-generating agentic AI architecture.
- As a technical reference for what is standardized and what is not.
- For risk assessment of non-standardized cryptography such as ZK circuits and ZK virtual machines.
- For audit preparation by understanding what evidence auditors will need.
- For vendor evaluation criteria for ZK, MPC, attestation, logging, and agent governance solutions.

**Key sections**

- Section 7 — The Eight Control Areas
- Section 8 — Reference Architecture
- Section 9 — Implementation Checklist
- Appendix C — Technical Standards and Cryptography Background
- Appendix D — Adversary Model

### Category 3 — The Audit & Assurance Professional

*"I need to verify compliance claims and assess evidence quality."*

**Primary roles**

- Internal auditors
- External auditors
- Third-party risk managers
- Audit preparation teams
- SOC 2 lead auditors
- ISO 27001 and ISO 42001 lead auditors

**How they use this guide**

- As an audit methodology for agentic AI systems.
- To distinguish evidence from assurance.
- To assess maturity using the Documented → Operational → Adversarial-ready model.
- To verify claims against primary source references.
- To design red-team and adversarial exercise requirements.

**Key sections**

- Section 4 — The Compliance Problem
- Section 6 — Evidence Maturity Model
- Section 7 — The Eight Control Areas
- Section 9 — Implementation Checklist
- Appendix A — Authoritative Sources
- Appendix D — Adversary Model

### Category 4 — The Legal & Strategic Advisor

*"I need to advise on liability, vendor contracts, and strategic risk."*

**Primary roles**

- Legal counsel
- Chief legal officers
- General counsel
- Technology transaction lawyers
- Privacy officers and DPOs
- Management consultants
- Procurement officers evaluating AI vendors
- Insurance and risk advisors

**How they use this guide**

- For liability assessment where accountability gaps exist between providers, deployers, vendors, and verifiers.
- For contract negotiation around technical compliance requirements and audit rights.
- For due diligence when evaluating AI vendor claims about attestation, verification, and compliance.
- For strategic planning during the EU AI Act high-risk build window.
- For dispute preparation where evidence quality may determine the strength of a claim.

**Key sections**

- Section 4 — The Compliance Problem
- Section 5 — Regulatory and Audit Obligation Map
- Section 10 — Standards Proposals
- Appendix A — Authoritative Sources
- Appendix B — EU AI Act Timeline
- Appendix F — Role Inventory and Reader Map