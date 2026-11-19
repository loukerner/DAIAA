# ICO agentic AI call for evidence — DAIAA response (draft)

> [!WARNING]
> **Draft for DAIAA review. Not submitted or endorsed.** The subgroup should confirm its position, authority to respond on behalf of DAIAA, signatory, publication preference and supporting evidence. Legal review is needed before submission. This draft follows the ICO's published themes; the exact wording and field limits in the full survey still need to be checked.

**Consultation:** ICO call for evidence on agentic AI
**Deadline:** end of 20 November 2026
**Submission route:** [ICO Citizen Space survey](https://citizen-space.ico.org.uk/regulatory-risk/agentic-ai-call-for-evidence/)
**Proposed respondent:** Decentralized AI Agent Alliance (DAIAA), subject to approval
**Signatory and contact:** To be agreed

## Submission action items

- [ ] Provide confirmed organisation and respondent details, signatory and contact, and publication preference.
- [ ] relevant disclosures (all contributors)
- [ ] Lou, complete the survey's adoption, barriers, assurance and benefits questions using verified facts.
- [ ] Complete member and legal review; verify any examples.
- [ ] Check the live survey's exact questions and field limits, then submit by the end 20th Nov

## Proposed response

Dear ICO team,

Thank you for the opportunity to contribute to the call for evidence on agentic AI. DAIAA brings together people working on decentralised AI agents. Its Agent Privacy and Security subgroup examines practical approaches to privacy, security and accountability as agents use tools, access data and interact across organisations.

Our submission focuses on a practical question. When an agent takes an action involving personal information, how can the responsible organisation establish what happened, whether the action was authorised and what safeguards were applied? We offer the following as proposals for guidance and implementation, not as findings from a controlled study or a claim that all DAIAA members have adopted a common technical standard.

Our central recommendation is that the ICO give organisations practical, risk-based guidance on defining agent authority, enforcing controls at relevant boundaries and retaining evidence that can be reviewed without unnecessarily exposing personal information. These measures should be technology-neutral and proportionate to the processing and potential harm.

### 1. Data security

Agentic systems may move from reading a document to calling an external tool, writing a record or delegating a task. A model-level instruction is not, by itself, a sufficient control over those actions. Organisations need to identify the agent, its owner and purpose, the systems it can reach, the authority it is using and any limits on onward delegation.

We recommend that guidance address:

- **Inventory and isolation.** Register agents, models, tools and owners. Define session boundaries and test whether information from one user or task can be accessed by another without authorisation.
- **Access and tool permissions.** Grant the least access necessary for the task. Restrict tools, data sources and destinations, and require renewed approval when the proposed action exceeds the authorised scope.
- **Changing permissions.** Bind permissions to the task, duration and delegation context. Test revocation, expiry, changes in policy and what happens when an agent or tool is unavailable.
- **Testing and response.** Exercise prompt injection, unauthorised tool calls, credential misuse, cross-session leakage and attempts to bypass controls. Document escalation, containment, recovery and applicable breach-reporting decisions.
- **Legacy systems and vulnerabilities.** Include connected APIs, infrastructure and legacy tools in the inventory; identify owners, exposure and support status. Prioritise security updates and test compensating controls where a fix is unavailable or cannot be applied promptly. For previously unknown vulnerabilities, use layered controls such as segmentation, limited and short-lived credentials, monitoring, isolation and tested revocation. Prepare for rapid exploitation of known flaws after disclosure as well as for zero-day attacks.
- **Shadow and embedded AI.** Take proportionate steps to discover unapproved AI tools and agent integrations, as well as AI capabilities embedded in supplier products. Review their access, recipients, retention and data flows, and provide an accessible approved route for legitimate use. An unapproved tool and a compromised approved supplier are distinct risks and should be assessed separately.
- **Resilience and safe recovery.** Map critical dependencies, including shared providers and identity, policy-enforcement, logging and tool services. Test outages and recovery. When a critical control is unavailable, consequential actions should pause or move to an appropriately controlled human fallback rather than silently bypass authorisation. Review queued or partially completed actions before resuming, and protect relevant evidence.

For example, an agent instructed to summarise a customer's support history should not automatically be able to export the whole customer database or send it to a new external service. A boundary control can reject or escalate an attempted export outside the approved scope. The organisation should test that outcome and keep a proportionate record of the attempted action and control decision.

Recent incidents illustrate different parts of this problem. WorkOS reported that an agent escaped a researcher's test environment and accessed a legacy internal tool with weak credentials and inadequate monitoring. Cursor reported that a supplier-exposed key led to the copying of retained agent traces, some containing credentials, and ultimately to a tampered extension. These are distinct incidents, not evidence that all outages or breaches have the same cause. The primary incident reports are listed in the working references below.

### 2. Transparency

Transparency needs to work for both the person affected and the organisation responsible for the processing. People should receive a clear explanation of the purpose, relevant data sources, recipients, whether processing is local or remote, the actions an agent may take and how to obtain help or challenge an outcome. Where a material change occurs during a task, timely notice or an approval step may be more useful than a long initial notice alone.

Developers should provide deployers with practical information on tool use, data flows, retention, defaults and limitations. A post-task summary could identify the categories of information used, tools and recipients involved, actions taken and available correction or challenge routes. It should be accessible without disclosing another person's data or sensitive security details.

Tracing can support those explanations, but a technical log is not a substitute for a clear notice. Additional notice or approval does not, by itself, establish a lawful basis or amount to valid consent.

### 3. Accountability across the supply chain

Controller, joint-controller and processor roles should be assessed for each relevant processing activity according to who determines or influences its purposes and means. Contract labels and the fact that an agent acted autonomously do not resolve that assessment.

We recommend a documented responsibility map covering the deployer, model provider, tool and infrastructure providers, and any other relevant parties. It should identify who sets purposes and permissions, supplies and changes tools, handles rights requests, maintains evidence, manages incidents and provides information needed for oversight. Contracts should reflect the actual arrangements and support appropriate audit and incident cooperation.

For significant or high-risk workflows, the evidence should make it possible to reconstruct the authorised principal, acting agent, delegation scope, relevant policy version, tool or data boundary, decision and outcome. Evidence should be protected against alteration, subject to access and retention controls, and independently checkable where appropriate. Where proportionate, control decisions and relevant actions should be recorded outside the agent's sole control, rather than relying only on its account of what happened. A record or cryptographic proof establishes only the specific claim it covers. It does not establish that the underlying input was correct, that every action was captured or that the processing was lawful.

The DAIAA Agent Compliance and Implementation Guide offers a working, technology-neutral approach to assessing inventory, risk, provenance, application control, prompt and output governance, identity and access, auditability, and incident response. It distinguishes documented, operational and adversarially tested controls. It is a practical reference, not a statement of additional legal obligations or a substitute for legal advice.

### 4. Automated decision-making and human involvement

Organisations should assess the complete decision-making workflow rather than assuming that any human step takes the decision outside the applicable automated decision-making provisions. An agent's involvement does not automatically bring those provisions into scope either. The impact on the person and the actual role of human involvement matter.

Where human involvement is relied on, reviewers need sufficient information, time, training and authority to question or change the result. A routine click-through is not meaningful review. For consequential actions that require approval, the approval channel should be kept outside the agent's reach, so that the agent cannot approve its own action or retrieve the approval credential. Organisations should record the relevant decision stages, reasons for escalation, the reviewer's role and the outcome, while limiting personal information retained. Where applicable safeguards apply, people must have an effective route to exercise them, including human intervention and challenge where required.

We ask the ICO for examples covering multi-agent workflows and mixed human and automated stages, including how an organisation should evaluate meaningful involvement and explain its conclusion.

### 5. Fairness and purpose limitation

Agents may combine retrieved information, memory and behavioural data in ways that are unexpected or harmful. Organisations should assess the reasonable expectations of affected people, the sensitivity of the information and potential adverse effects across the whole workflow. They should test for unequal outcomes and provide a way to correct or challenge harmful decisions.

Purpose and access restrictions should carry through retrieval, memory, tool use and delegation. A new use identified by an agent is not automatically compatible with the original purpose. The organisation should assess compatibility or another applicable legal route before the new processing occurs. Controls should flag or stop a proposed action outside the approved purpose and direct it for review. Simply labelling product development as research does not automatically make the research provisions available.

### 6. Lawfulness of processing

A user's instruction or an agent's technical authority does not automatically establish a lawful basis for every subsequent processing activity. Organisations should identify and document the appropriate basis for each relevant activity and, where applicable, the additional condition for special-category data. Legitimate interests should be supported by the appropriate assessment. Consent, where relied upon, must meet the relevant legal standard and be capable of withdrawal.

Where an agent stores or accesses information on a user's device, the organisation should separately assess the applicable PECR requirements. It should also consider international transfers, retention, deletion and rights requests at each relevant stage. Technical permissions and evidence can help implement and demonstrate decisions, but cannot determine the legal basis on their own.

### Additional issues and request for guidance

We ask the ICO to publish worked examples and proportionate guidance for:

1. A multi-party agent that retrieves personal information and invokes an external tool, including role allocation and data flows.
2. A multi-stage decision involving both automated processing and human review, including how meaningful involvement is assessed.
3. A change of purpose or new data source during a task, including when to stop, reassess, inform or seek approval.
4. A privacy-preserving evidence record, including retention, access, verification and the risks of publishing personal information or linkable identifiers.
5. A supplier outage or newly disclosed vulnerability that disables a shared control during an agent workflow, including safe pause or fallback, recovery and reconciliation, preservation of evidence, supplier coordination and assessment of effects on individuals.

Useful safeguards have costs. Smaller organisations may lack engineering capacity, specialist reviewers or access to supplier information. Guidance should scale with risk, distinguish minimum documentation from stronger independent assurance, and encourage interoperable evidence rather than one prescribed vendor or cryptographic method.

We would welcome the opportunity to contribute further practical examples as this guidance develops.

Yours faithfully,

**For DAIAA**
[Name and role to be approved]

---

**Working references**

- [ICO call for evidence and deadline](https://ico.org.uk/about-the-ico/ico-and-stakeholder-consultations/2026/10/agentic-ai-call-for-evidence/)
- [ICO's six themes and evidence sought](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/the-ico-s-call-for-evidence-on-agentic-ai/)
- [ICO additional questions](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/the-ico-s-call-for-evidence-on-agentic-ai/additional-questions/)
- [DAIAA Agent Compliance and Implementation Guide](https://github.com/loukerner/DAIAA/blob/main/docs/2026-agent-compliance-implementation-guide.md)
- [WorkOS incident update: legacy tool and escaped research agent](https://workos.com/security/bulletins/update-for-october-30th-2026-data-security-incident)
- [Cursor incident update: supplier exposure and compromised extension](https://cursor.com/blog/security-incident-update)
- [Google Threat Intelligence: automated exploitation of disclosed vulnerabilities](https://cloud.google.com/blog/topics/threat-intelligence/agentic-threat-activity-crosses-a-significant-threshold)
- [I-HITL preprint: agent access to approval codes](https://arxiv.org/abs/2610.35835)
