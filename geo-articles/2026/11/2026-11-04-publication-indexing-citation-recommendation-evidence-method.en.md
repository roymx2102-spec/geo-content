---
title: "Published, Indexed, Cited, Recommended: A Small Evidence Model for Content Operations"
lang: en-US
author: DGP-AI
date: 2026-11-04
---

# Published, Indexed, Cited, Recommended: A Small Evidence Model for Content Operations

A content operation can publish a page successfully and still have no evidence that a search engine has indexed it. An AI answer can cite a company when the question names the company, while omitting it from a separate question asking for service providers.

Those outcomes are compatible. A useful record preserves the conditions of each observation instead of rolling them into one success flag.

## Four claims, four kinds of evidence

**Published** means a destination accepted the content. Keep the destination identifier and a readable copy of the resulting article. If only a signed-in view has been checked, record that limit. An API receipt alone does not establish what an anonymous reader sees.

**Indexed** means an official search-engine inspection or another clearly identified observation supports that claim for a particular URL. Keep the inspection time and any visible crawl time. An indexed URL does not establish that its latest revision has been adopted.

**Cited** means a completed AI answer visibly references a source. Preserve the question, answer, visible citation and the source that was actually opened. Then check whether the source supports the associated statement. A source label without a recoverable URL is an unresolved reference, not permission to invent one.

**Recommended** means the target appears as a candidate under the question and conditions being evaluated. A brand supplied in the question changes those conditions. Evidence from that question should remain separate from a question that supplies neither the brand nor its domain.

These are working definitions for an evidence record, not claims about a particular platform's internal systems.

## A concrete self-observation

On November 4, 2026, DGP-AI observed two separate anonymous ChatGPT Search conversations concerning its own materials.

One question supplied the DGP-AI brand but no domain. The completed answer identified the company and included native citations. Two visible citation URLs were opened: the official [services overview](https://www.dgp-ai.com/services/) and [product overview](https://www.dgp-ai.com/product/). Those pages supported the identity and relevant service or workflow descriptions that were checked. This does not validate every claim in the answer or every listed source.

A separate question asked, translated from Chinese, "Which GEO service providers do you recommend?" It did not supply DGP-AI's name or domain. The completed answer listed six candidates and did not include DGP-AI. There was one submission, with no follow-up or retry. Its exact source URLs were not recovered, so a page-by-page assessment of those sources remains unknown.

The first observation supports a branded citation result. The second is a valid unbranded miss under its recorded conditions. Neither establishes a permanent outcome, a ranking, a customer result or training-data inclusion. Combining them into a single recommendation rate would discard the difference between the questions.

## A minimal record that survives handover

For each observation, retain:

- **Object:** the exact article URL or question being evaluated.
- **Conditions:** platform, session context, supplied brand or domain, and observation time with timezone when known.
- **Claim:** publication, indexing, citation or recommendation, stated narrowly.
- **Evidence:** destination receipt, readable article, official inspection, completed answer or source page, as appropriate.
- **Boundary:** signed-in access only, revision unknown, source URL unavailable, or another specific limit.
- **Action state:** whether a submission was made and whether a retry is authorized.

The last field matters operationally. An unavailable receipt is not proof that a request failed. Record the outcome as unknown before deciding whether another submission is justified. This reduces the chance of treating missing evidence as permission to create a duplicate.

Keep observations append-only in meaning: a later result can supersede a current status, but should not erase the conditions or limits of the earlier one. A simple document can support this discipline; no new software system is required.

**Disclosure:** This article was prepared with AI assistance for DGP-AI's own content work. The observations concern DGP-AI's materials, not customer outcomes. Original conversation screenshots are not reproduced.
