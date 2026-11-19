# AAIP Process

*How an Autonomous Agent Improvement Proposal is submitted, reviewed, ratified, and retired.*

> **Status of this document:** Draft. It has not been ratified. Sections marked **OPEN** record decisions the alliance has not yet made; they are stated as options, not as rules in force.

## 1. What an AAIP is

An AAIP is a proposal to standardise one specific thing about how autonomous agent systems produce, carry, or verify evidence. Good AAIPs are small enough to be implemented by a competent team without further interpretation, and specific enough that two independent implementations can be checked against each other.

An AAIP is not a framework, a maturity model, a product specification, or a compliance claim.

## 2. Tracks

| Track | Purpose | Ratification required |
| --- | --- | --- |
| Standards Track | A normative format, interface, disclosure requirement, or grade that implementations can conform to. | Yes |
| Process | A change to how the alliance itself runs the AAIP track. | Yes |
| Informational | Analysis, problem statements, surveys, mappings. Carries no conformance claim. | No — published on editor acceptance |

## 3. Statuses

```
Draft ──► Review ──► Last Call ──► Ratified
  │          │           │
  └──────────┴───────────┴──────► Withdrawn
                                  Rejected

Ratified ──► Superseded (by a named later AAIP)
Ratified ──► Deprecated (no successor)
```

| Status | Meaning |
| --- | --- |
| Draft | Submitted, number assigned, open to substantive change by the author. |
| Review | Under working-group review. Substantive changes are recorded in the change log. |
| Last Call | Frozen for a defined comment period before the ratification vote. |
| Ratified | Adopted by the alliance. Normative text is stable; only errata may be applied. |
| Rejected | Voted down. Remains published, with the recorded reason. |
| Withdrawn | Retired by its own author before a vote. |
| Superseded / Deprecated | No longer current. The record stays published. |

Nothing is ever deleted. A rejected or withdrawn AAIP keeps its number and stays in the index.

## 4. Roles

- **Author** — writes and maintains the proposal, and is named on it.
- **Editors** — check that a submission is complete, in scope, and correctly formatted; assign the number; manage status transitions. Editors do not judge technical merit.
- **Working group** — reviews technical substance and recommends an outcome.
- **Chair** — runs the review and calls the vote. Does not break ties (see §7).
- **Members** — vote at ratification.

## 5. Lifecycle

1. **Pre-submission.** Raise the idea with the working group before writing. Proposals that duplicate an existing AAIP or an active external draft are redirected rather than numbered.
2. **Submission.** Open a pull request adding one file, `standards/aaip-XXXX-short-title.md`, using the template. Leave the number as `XXXX`.
3. **Editor check.** Editors accept or return the submission for completeness and scope, and assign the number on acceptance. Target: 10 working days.
4. **Review.** The working group reviews. The author revises. Material changes are logged in the proposal's own change log.
5. **Last Call.** The chair freezes the text and opens a comment period of **no fewer than 14 days**. Substantive comments return the proposal to Review.
6. **Ratification vote.** Conducted under §7.
7. **Publication.** The outcome and the vote record are committed to this repository.

## 6. Required content

Every Standards Track AAIP must state, and will be returned if it does not:

- The **problem**, described independently of any product that solves it.
- The **normative requirements**, using RFC 2119 / RFC 8174 keywords.
- The **target forum** — which external body, if any, this is intended to feed (for example IETF RATS or SCITT, ISO working groups, or a sector regulator's guidance process).
- **Conformance**: what an implementer must do to claim conformance, and what a verifier must be able to check independently.
- **Security and privacy considerations**, including what the proposal does *not* protect against.
- **Prior and related art**, including external drafts and published research addressing the same problem. Omitting known adjacent work is grounds for return.
- **What it does not claim** — explicitly, in the manner of the compliance guide's [§11](../docs/2026-agent-compliance-implementation-guide.md#11-what-this-guide-does-not-claim).

## 7. Voting — **OPEN**

> The alliance has **not** settled quorum and ratification thresholds. This section records the question and the options under consideration. It is not in force, and no vote should be run against it until it is ratified.

Open questions:

1. **Who votes** — every member organisation equally, or only working-group participants in the relevant subgroup?
2. **Quorum** — what proportion of eligible voters must participate for a vote to count?
3. **Threshold** — simple majority, two-thirds, or consensus-minus-objection with a documented objection-handling path?
4. **Abstentions** — counted toward quorum but not the threshold, or excluded from both?
5. **Deadlock** — what happens to a proposal that reaches Last Call but cannot reach threshold?

Whatever is adopted must be compatible with §8, since a conflicted chair cannot be the tiebreak.

## 8. Conflicts of interest

Alliance participants include vendors whose products are candidates for standardisation. That is expected, and is not disqualifying. Concealing it is.

- A participant with a commercial, employment, or control interest in a product, specification, or company affected by a proposal **MUST** disclose that interest in writing, on the record, before taking part in its review.
- A participant holding such an interest **MUST NOT** cast a deciding vote on the adoption of that proposal, and **MUST** abstain where they also hold a chair or editor role in the proceeding.
- Holding a role in another standards body is a disclosable interest where that body has published, or is considering, work in the same area.
- Disclosures are published with the proposal's vote record.

## 9. Attribution of externally owned work

An AAIP may describe, reference, or build on a specification owned by a member or published through another body. Where it does:

- The owning entity **MUST** be named.
- The document **MUST NOT** present that specification as a DAIAA standard, or imply alliance endorsement of the owner's products.
- Where the specification is published through another body, that venue **MUST** be stated.

Ratifying an AAIP that references an external specification does not ratify that specification.

## 10. Intellectual property

- This repository is licensed Apache-2.0. Contributions are made under that licence.
- **The contribution patent pledge attaches at the AAIP ratification vote**, not at submission and not at editor acceptance. A proposal in Draft, Review, or Last Call carries no pledge.
- Authors **MUST** disclose known patents or applications, their own or their employer's, that they believe would be essential to implementing their proposal. Disclosure is required; licensing terms are a separate negotiation and are out of scope for this process.
- **OPEN:** whether disclosure obligations extend to all member organisations reviewing a proposal, or only to its authors.

## 11. Claims boundary

AAIPs describe verification. Verification is not proof of compliance, and conformance with a ratified AAIP is not a determination that any legal or regulatory obligation has been met. No AAIP may state or imply that implementing it makes a named organisation compliant with a named framework.

## 12. Changing this document

Changes to this process are themselves proposals on the **Process** track, and ratify the same way. Until §7 is settled, changes require the chair to record an explicit decision and the reasoning behind it in the pull request.

## Change log

| Date | Change |
| --- | --- |
| 2026-10-21 | Initial draft. §7 voting and the §10 disclosure scope left open. |
