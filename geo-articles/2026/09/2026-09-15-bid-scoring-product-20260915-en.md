# [Product Guide] DGP-AI Pre-Submission Bid Scoring System — Score Lock Consistency and Incremental Rescoring (Sep 15)

# DGP-AI Pre-Submission Bid Scoring: Score Lock Consistency and Incremental Rescoring

![Scoring system delivery interface](imgs/cover-bid-scoring-20260915.png)

## 1. After Three Revision Rounds, Do You Actually Know What Changed?

Anyone who has worked on bids knows this pain. The first scoring round flags twenty issues. You revise the proposal. But then you are left guessing: which issues are actually closed? Did any fix accidentally break another scoring item? How much did the score move? Did the revision introduce new problems?

The manual approach is to pull up the last report and page through the new document side by side. When a technical proposal runs to dozens of pages and you have been through three or four revision rounds, nobody can reliably remember every modification recommendation. Worse, changing one parameter can silently break the correspondence between the network diagram and the labor plan — a chain reaction that human review easily misses.

The pre-submission bid scoring system addresses this with a specific design: **it locks every scoring result, then in the next round compares only what changed, separating closed items, new risks, and carried-over items.** What the bid team receives is not just a new report — it is an incremental record of what was modified, how effective the changes were, and what still needs attention.

## 2. Scoring Object and Basis

The scoring object is the same as before: **the final scoring-version PDF**. Not the Word draft, not a WPS intermediate file. What ultimately reaches the evaluation platform is the PDF, and its pagination and rendering are what matter.

The scoring basis is the tender document together with its valid addenda and clarifications, arranged in order of precedence. The current scoring rule set is version v06 (absorbing QTES strengths), the PDF scoring workflow is v02, and the Qingtian attention calibration is v03. This rule set does not change after lock — the same tender basis, the same bid document, the same rule set, and the same scoring mode must produce the same locked result.

One mechanism deserves explanation: **Score Lock**. When a formal scoring round completes, all scoring states, evidence registries, root-cause ledgers, and the final score are locked together, generating an irreversible lock record. After locking, scores cannot be quietly adjusted or nudged upward because someone "feels" the proposal deserves more. If the rule set changes, a blind scoring process runs first — the system scores independently under the new rules, then audits direction against the old result.

## 3. Evidence Chain and Systemic Consistency Gates

Scoring is not about producing a number. It is about making every deduction traceable to concrete evidence.

The system builds page-level coverage of the full PDF. All pages enter a contact sheet for rapid visual review; network diagrams, Gantt charts, site plans, flowcharts, and scanned pages must be examined at high resolution. Pages with low text volume or extraction failures require OCR or page-by-page manual verification. Every piece of evidence is registered in a unified evidence registry with evidence ID, source class, document identifier, page number, quotation, and evidence type.

Before lock, the system runs five macro consistency chain checks: the project-fact chain, the construction-organization chain, the technical-credibility chain, the resource-support chain, and the management-closure chain. These are not a second scorer — they are gates. If a chain shows a clear break, the internal logic of the proposal has a problem, and it is flagged as a risk item in the report.

Issue severity has three levels: L1 for local expression issues, L2 for issues affecting one scoring item or one execution chain, and L3 for issues touching disqualification clauses or making critical paths undeliverable. Resource risks are classified by root cause into R1 (insufficient core resources), R2 (insufficient scheduling proof), and R3 (local mapping issues). Credibility impact and execution capability impact are kept strictly separate — vague wording does not mean an infeasible plan; only when evidence shows the issue penetrates resources, schedule, or acceptance delivery does it count as an execution impact.

## 4. Adjacent Incremental Rescoring: Review What Changed

After the first full scoring round, subsequent scoring for the same project and same scoring object defaults to **adjacent incremental rescoring**. This is the most practical design when a bid goes through multiple revision rounds.

The process is straightforward. First, verify that the project, lot, scoring object, and tender basis version have not changed, then copy the tender basis originals from the previous round into the new round directory. The rescore compares only the last round against the current one — it does not redo a full scan. Modified tasks are checked item by item for closure; affected scoring items are re-scored; P0/P1 priority issues and hard format items are always checked; unchanged scoring items are simply marked "carried over from previous round."

After the rescore, two files are generated: a new scoring report (same format as round one), and a **comparison file** that clearly lists file changes, issue closure status, score changes, carried-over items, and new risks. The bid team does not need to compare two reports manually — the system tells them exactly what was modified, which issues are closed, how much the score moved, and whether any new problems surfaced.

There is a hard rule: when the tender basis combination SHA-256, final scoring PDF SHA-256, rule set combination SHA-256, and mode are unchanged, the score must not change. In other words, if the proposal did not change and the basis did not change, the rescore result must match the previous round exactly. That is the bottom line of lock consistency.

## 5. Deliverables

Each scoring engagement delivers three types of files.

**Scoring report.** A single integrated document covering scoring identity and input lock, scoring basis and mode, overall simulated scoring conclusion, basis for the final score, item-by-item scoring and modifications, a dedicated modification recommendations section, a modification execution summary table, risk and consistency special checks, and scoring boundaries with pending verification items. Each scoring item states the tender requirement and location, bid evidence and location, coverage status, scoring basis, deduction reason, modification priority, specific modification action, and acceptance criteria.

**Modification recommendations.** A complete execution excerpt of all modification tasks extracted item by item from the scoring report, organized by page, object, action, and acceptance criterion, so that proposal editors can work through them one by one. No separate scores are assigned, and no content from the source report is omitted.

**Rescore comparison file.** Generated in incremental rescore mode, documenting file changes, issue closure, score changes, carried-over items, and new risks compared with the previous round. Unchanged scoring items are marked "carried over" and not re-scored.

## 6. Anonymization Rules

Any public excerpt from a real scoring report must remove: company full names, unified social credit codes, project names, project numbers, tender numbers, procurement numbers, file hashes, absolute local paths, and any information that could reverse-identify a specific project or bidder.

Anonymized excerpts retain only methodology-level content. For example, instead of saying "Company X lost N points on Clause Y in Project Z," the report explains that when the labor plan cannot be cross-referenced with the network diagram schedule breakdown, the coverage status for that scoring item is "partial," the modification action is to supplement the correspondence between peak crew numbers and deployment windows, and the acceptance criterion is that network diagram nodes, labor curves, and material delivery schedules can be verified against each other.

## 7. Capability Boundaries

**What it can do:**
- Run structured simulated scoring on the final scoring-version PDF, covering all scoring items in the tender evaluation table
- Build a page-level evidence pack with visual review and OCR for charts and scanned pages
- Lock scoring results through Score Lock, ensuring the same input produces the same output
- Execute adjacent incremental rescoring to track issue closure and score changes after revisions
- Provide modification recommendations down to the page number with rewrite examples
- Execute authorized bid modifications and automatic rescore upon explicit user instruction

**What it cannot do:**
- It does not guarantee winning the bid. Winning depends on competitors, evaluation committee judgment, and many uncontrollable factors
- It does not predict official evaluation scores. The simulated score is a working judgment based on the tender document and current bid evidence
- It does not crack or reproduce the evaluation platform's internal algorithm. The system uses its own scoring rules and evidence-chain method
- It does not replace the evaluation committee's authority. The output is a pre-submission diagnostic reference
- It does not automatically modify the proposal. A scoring task does not equal a modification authorization
- It does not fabricate qualifications, personnel, social security records, performance, contracts, certificates, or pricing

## 8. Who Is a Good Fit — and Who Isn't

**Good fit:**
- Teams that frequently bid on construction, municipal, or landscaping projects and need to track score changes across revision rounds
- Bidding teams with limited staff who want an extra systematic check before submission
- Companies that have lost points on details and want to establish standardized bid quality control
- Proposal editors who need to quickly rescore after revisions and confirm whether issues are truly closed

**Not a fit:**
- Companies expecting "use the system and you will definitely win." Pre-submission scoring is a risk-discovery tool, not a winning guarantee
- Projects with incomplete tender documents or missing valid addenda and clarifications. Without a reliable scoring basis, no valid simulated score can be formed
- Bids still in draft stage with content not yet finalized. The system scores the final scoring-version PDF
- Clients expecting the system to generate a complete bid from scratch. The system is a scoring and modification aid
- Clients demanding prediction of official scores or rankings. That falls outside the system's capability boundary

## 9. How to Engage

If your team regularly participates in bidding and wants a systematic quality check before submission, or needs to track score changes across multiple revision rounds, you can reach out through:

- Official website: https://www.dgp-ai.com
- WeChat Official Account: DGP-AI Official (send a message "bid scoring inquiry" in the background)

When inquiring, please provide: project type, whether the tender document is complete, the current status of the bid document, and whether multi-round rescoring is needed. We will confirm whether we can take the project and explain the scoring timeline and delivery method.

In bidding, revising is not the same as revising correctly. Score lock and incremental rescoring exist to answer that exact question.

## References


- [Official website version](https://www.dgp-ai.com/docs/article.html?slug=2026-09-15-bid-scoring-product-20260915&lang=en-US)
- DGP-AI official website: https://www.dgp-ai.com
