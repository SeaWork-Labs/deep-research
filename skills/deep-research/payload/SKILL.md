---
name: deep-research
description: Use this skill when a question needs multi-source investigation, primary-source analysis, competing explanations, uncertainty tracking, or a cited decision report rather than a quick lookup or an uncited summary.
---

# Deep Research

Turn an open question into an evidence-backed judgment. This skill owns the
research method and report structure; it does not own document persistence. Use
ordinary file and code tools for ordinary file and code work. When external
evidence is required, search for it, open the strongest original sources, and
verify what they actually support.

## When to use

Use this workflow when the user asks for deep research, due diligence,
comparative analysis, an evidence review, a landscape scan, or a recommendation
that depends on several sources. For a simple fact, a small deterministic edit,
or a known local file transformation, use the smallest direct tool path instead.

## Operating contract

- Default to Chinese output unless the user requests another language.
- Never invent sources, URLs, authors, dates, figures, quotations, study
  results, or search activity. If a claim cannot be verified, label it unknown.
- Prefer first-party and primary sources: official documentation, filings,
  standards, source datasets, original papers, transcripts, court records, and
  direct announcements. Use reputable secondary analysis to add context, not to
  replace primary evidence.
- Preserve the exact URL for every external source and include a short key
  excerpt or precise locator (page, section, table, timestamp, or paragraph).
- Separate **observed facts**, **interpretation**, **recommendation**, and
  **unknowns**. State confidence and what would change the conclusion.
- Search for disconfirming evidence and credible criticism before finalizing a
  thesis. Do not present source count as evidence quality.
- Keep sensitive or private local files inside the current Session workspace.
  Inspect supplied documents and structured data with available project
  libraries or small deterministic scripts. Preserve originals, note parser
  limitations, and do not assume a global parser installation.
- For external evidence, search broadly enough to map the field, then open and
  inspect the strongest original sources. Treat snippets as leads rather than
  verified evidence.
- Use ordinary file and code operations directly for code, files, local data,
  and deterministic transformations. Do not require a CLI wrapper or route
  normal work through another Skill.
- One final report is the default deliverable. If persistence is requested,
  write `research/<slug>/report.md` and any evidence table under the current
  Session workspace, preserving source files.
- You may parallelize up to 7 independent research threads. Sub-agents must
  not spawn more sub-agents; each returns sources, claims, and caveats to the
  lead researcher.

## Four-phase workflow

### Phase 0: Frame the question

Before searching, write a compact research brief:

1. Decision or question to answer.
2. Scope, audience, geography, and time window.
3. Definitions and hidden assumptions.
4. An analysis framework or comparison dimensions.
5. Two to five falsifiable hypotheses, including a plausible alternative.
6. Evidence threshold and stopping rule.

If key scope is missing, state the assumption and proceed with a bounded first
pass. Do not silently turn an ambiguous question into a confident conclusion.

### Phase 1: Find and read primary evidence

Search broadly enough to map the field, then read the strongest original sources
in full or at the relevant sections. For each source record:

| id | source type | publisher/author | date | URL | locator | key excerpt | claims supported | limitations |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

Capture publication dates and version numbers. Distinguish an original source
from a page that merely repeats it. For quantitative claims, record units,
denominator, population, and period before comparing numbers.

### Phase 2: Compare, challenge, and seek counter-evidence

Group evidence by hypothesis rather than by website. Compare methods, samples,
definitions, incentives, and time periods. Deliberately search for:

- well-supported counterexamples and null results;
- critical reviews, retractions, dissenting expert views, or competing standards;
- sources that use a different definition or measure the same outcome differently;
- base-rate, implementation, cost, legal, or operational constraints.

Record whether a disagreement is factual, methodological, definitional, or a
genuine unresolved debate. Update the hypothesis status as evidence arrives.

### Phase 3: Verify and synthesize

Cross-check every material claim against at least two independent sources when
feasible, with one primary source for claims about an organization, product,
policy, dataset, or study. Check dates, versions, arithmetic, quotations, and
whether a source actually supports the wording. Preserve conflicts instead of
averaging them away. Assign confidence as high, medium, or low with a reason.

Use a claim ledger:

| claim | evidence ids | status | confidence | unresolved issue / next check |
| --- | --- | --- | --- | --- |

Status values: `supported`, `partially supported`, `contested`, `not found`, or
`refuted`. A source that is only a search snippet is a lead, not verified
evidence.

## Final report format

Use an argument-driven report, adapting length to the request:

```markdown
# [Research question]
## Executive answer
[Direct answer, decision, or recommendation in 3-6 sentences.]

## Scope and method
- Scope, assumptions, date checked, and stopping rule
- Search limitations and evidence quality

## Findings by hypothesis
### H1: [hypothesis]
- **Finding:** ...
- **Evidence:** [S1], [S2]
- **Counter-evidence:** ...
- **Confidence:** High / Medium / Low — [reason]

## Alternatives, trade-offs, and risks
[What could make the answer wrong, including implementation constraints.]

## Recommendation and decision triggers
[Action, sequencing, owner, and observable signals that would change it.]

## Unknowns and follow-up checks
[Material gaps; do not fill them with guesses.]

## Sources
### [S1] [title]
- URL: https://...
- Locator: [section/page/table/timestamp]
- Key excerpt: "..."
- Source type and limitation: ...
```

Use inline source ids consistently. Do not append a long undigested link dump or
turn the report into one paragraph per source. If research was not actually
completed, title the output `Research plan` or `Evidence gap report` rather than
claiming results.

## Quality gate

Before delivery, verify that every material external claim has a reachable URL,
locator, and excerpt; facts are distinct from inference; counter-evidence is
represented; arithmetic and dates are checked; unknowns are explicit; and the
report answers the original decision. If a page is inaccessible, record the
failed retrieval and do not infer its contents.
