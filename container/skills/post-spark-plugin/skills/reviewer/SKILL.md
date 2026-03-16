---
name: reviewer
description: >
  Use this skill to validate and quality-check researched tech topics before writing posts.
  Trigger when the user says "review these topics", "validate the ideas", "check the sources",
  "run the reviewer", "verify these topics", or after the tech-researcher skill has surfaced
  a list of post ideas. Also trigger when the user asks to confirm topics are recent, in-scope,
  or not duplicates of previously published posts.
version: 0.1.0
---

# Reviewer

Validate a list of 5–7 tech post ideas before passing them to the writer. Confirm every topic is recent, credible, scoped to the user's interests, and not a repeat of previously published content.

## Validation Criteria

Check each topic against all four criteria:

1. **Recency** — Source published within the last 7 days. Flag any topic with no clear publish date or a date older than 7 days.
2. **Source credibility** — The source is a real, verifiable article or announcement. Reject hallucinated or unresolvable URLs. Prefer official engineering blogs, major tech outlets (Hacker News, The Verge, InfoQ), or well-sourced community posts.
3. **Scope fit** — Topic falls within the user's interest areas: AI/LLMs/agents, React/Next.js/Node.js, full-stack architecture, DevOps, or developer tooling. Flag anything outside this scope.
4. **Duplicate check** — If the user has provided a list of past post topics, check whether any idea substantially overlaps with previously covered content (same product, same feature, same angle).

## Validation Workflow

### Step 1: Review each idea

Go through each topic from the researcher's list. For each one:
- Assess the publish date against the 7-day window
- Evaluate whether the source URL appears real and credible
- Check scope alignment
- Cross-reference against any past-topics list provided by the user

### Step 2: Present the review table

Show a structured validation result:

```
| # | Title                        | Recency      | Source  | Scope | Duplicate | Decision  |
|---|------------------------------|--------------|---------|-------|-----------|-----------|
| 1 | [Title]                      | ✅ Mar 12    | ✅      | ✅    | ✅ No     | ✓ Keep    |
| 2 | [Title]                      | ⚠️ No date   | ✅      | ✅    | ✅ No     | ✗ Replace |
| 3 | [Title]                      | ✅ Mar 14    | ⚠️ Weak | ✅    | ✅ No     | ⚠️ Verify |
```

### Step 3: Make a decision

**If 5 or more topics pass all criteria:**
Present the validated list and ask: "Which of these would you like me to turn into posts? Pick one or several."

**If fewer than 5 topics pass:**
Note the issues clearly, then instruct the researcher to replace the failing topics with specific guidance (e.g., "Replace #2 — no publish date found; find a different AI tooling release from this week"). Track the iteration count.

**If iteration limit (5) is reached:**
Present the best available list with all caveats noted. Let the user decide whether to proceed or swap topics manually.

## Loop Protocol

When sending topics back to the researcher, always include:
- Which topics need replacement and the specific reason (recency, bad source, out of scope, duplicate)
- What to search for instead
- Current iteration number: "Iteration [N] of 5"

Example handoff instruction:
> "Sending back to researcher (Iteration 2 of 5). Please replace #3 (source URL unverifiable) and #5 (duplicate of previous post on Next.js 15 release). Look for: a different React/Next.js update from this week, or a new AI tooling release."

## Handoff to Writer

Once the validated list is confirmed and the user has selected their topics:

> "Topics locked in. Hand these to the post writer — just say 'write the posts' or pass the selected topics directly to the post-writer skill."
