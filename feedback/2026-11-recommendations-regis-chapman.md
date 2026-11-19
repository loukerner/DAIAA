# Recommendations for the DAIAA Agent Compliance and Implementation Guide

**Disclosure.** I'm Regis Chapman (Polymathie.xyz). I build the Dimensional Frame Harness, a runtime harness that reads an agent's whole run. I also write the open standards in the Integrity Suite, which I am adapting to agent settings. I'm a member of DAIAA. Nothing below depends on adopting any of it. I'm reading the guide at commit 2af450e.

## Summary

The guide's core is strong and correct: evidence a relying party can check without trusting the operator, evidence rather than assurance, and records that are tamper-evident, policy-bound, and independently replayable. Its adversary model, with explicit in-scope, partly-in-scope, and out-of-scope calls, and its "What This Guide Does Not Claim" section are unusually honest for this space. The recommendations below strengthen it along two dimensions it does not yet fully carry, coordination-level coverage and temporal integrity, and sharpen its strongest single proposal, verifier independence. They are ranked by impact.

## 1. Add a coordination-level (aggregate) evidence class

The guide names three gaps (Section 4.2): boundary, delegation, and verification. All three are per-action or single-chain. A gateway that clears each action as on-policy is structurally blind to harm that emerges across a sequence of individually-authorized actions, where every step is compliant and the composition is the harm. This is the failure class autonomous agents most produce, because they chain actions faster than any per-step review.

Recommendation: add a ninth control area, or extend Control Area 08, for aggregate or trajectory evidence: a record and an independent check over the sequence of actions, not only the step. The object to evaluate is the reachability of an inadmissible aggregate state across a run, not a sum over a per-action log. Without this, the architecture catches the anticipated boundary violation and misses the coordination-level failure.

## 2. Add temporal integrity to the evidence model

The guide has strong spatial integrity (tamper-evidence) and it binds the policy version in force at the time of an action. It does not yet address decay in time: a reference value, attestation, or reading that was correct when produced and is consumed after it has gone stale. Rollback and truncation are covered in the adversary model (Appendix D); staleness of still-valid-looking data is not, and none of the eight control areas reach it. Proposal 10.2 already carries expiry for delegation scope; the same property is needed for reference values and attestations.

Recommendation: add temporal properties to the evidence record: a validity window and a freshness measure on reference values and attestations, and a correction-window property, whether there was time to detect and correct a boundary breach before the irreversible consequence committed. Treat a correction path as effective only when it is shown to close before the consequence it must catch. This is the temporal half of tamper-evidence, and it is where agentic systems, acting at machine speed, are most exposed.

## 3. Deepen verifier independence, and add a shared-origin check

Making verifier independence a machine-checkable disclosure (proposal 10.1) is the guide's strongest idea. Two refinements make it hold under pressure.

First, independence is two coupled constraints, not one. A verifier must be both decorrelated from the attester and competent to actually check the thing it judges, and pushing one to the maximum starves the other: a verifier chosen for maximal distance from the attester may be incompetent to evaluate the evidence. The disclosure should carry both the independence relationship and the competence basis.

Second, disclosed-as-separate is not the same as independently-originated. Two verifiers, or two reference-value sources, that share a hidden common origin will agree because they must, which reads as corroboration but is not. Add a shared-origin check to the independence disclosure: when two apparently distinct chains converge on the same origin, the evidence should record the convergence. Without it, correlated sources pass as independent ones.

## 4. Make omission partially detectable

The adversary model (Appendix D.1) honestly states that an event which produced no record is invisible unless another signal implies a record should exist. That limit can be partly closed. Publish an expected-evidence manifest: a declaration, per action class, of which records must exist. A missing expected record then becomes a detectable gap rather than a silent absence. This does not solve omission in general, but it moves it from an acknowledged blind spot to a bounded one, and it pairs naturally with the default-deny posture the guide already recommends for tools and endpoints.

## 5. Make independence a maturity cross-cut, not a separate section

The maturity model (Section 6 and proposal 10.4: documented, operational, adversarial-ready) and the verifier-independence proposal (10.1) currently sit apart. That allows a control to be claimed adversarial-ready when the operator ran and graded its own red-team, which is the self-adjudication the guide's own thesis warns against. Cross the two: a control should not be reportable as adversarial-ready unless the adversarial exercise was gradable by a party the operator does not control. Independence of verification is not only a property of the evidence; it is a condition on the maturity claim itself.

## 6. Sharpen two definitions

Two terms would benefit from operational definitions an outside reader can apply without the author's intent. "Adversarial-ready" needs a stated "survived" criterion: against what threat set, judged by whom, with what recorded result. "Independent verifier" needs the two-constraint definition from recommendation 3, independence and competence, so that a reader can determine independence from the disclosure alone.

## 7. Consider whether the eight control areas are configurations of a smaller set

Offered as a design question, not a required change. The eight control areas read as a taxonomy, and a taxonomy is often a sign that a smaller generating set has not yet been found. They may all be instances of one primitive: bind X to the action and make X independently checkable, for X in identity, policy, tool, data, time, and provenance. Testing whether the eight fall out of that primitive would make the framework generative rather than enumerative, and would make it easier to show the set is complete rather than merely current.
