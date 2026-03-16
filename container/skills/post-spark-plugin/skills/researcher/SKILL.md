---
name: researcher
description: >
  Use this skill to research recent tech news and find post-worthy topics for social media.
  Trigger when the user says "find tech topics", "research what's new in tech this week",
  "what should I post about", "run research", "start the post pipeline", "find ideas for posts",
  "look up tech news", or any request to discover recent developments in AI, React, Next.js,
  Node.js, or full-stack architecture for LinkedIn or Twitter/X posts.
  Also trigger at the start of the post-spark workflow when no specific topic has been provided yet.
version: 0.1.0
---

# Researcher

Research recent tech developments and surface 5–7 post-worthy ideas for a senior full-stack developer/architect audience.

## Scope

Cover these domains:
- AI ecosystem: new models, agent frameworks, tooling, API changes, open-source releases (OpenAI, Anthropic, Google DeepMind, Mistral, Hugging Face, LangChain, etc.)
- React / Next.js / Node.js: framework releases, new APIs/hooks, tooling changes, notable community discussions
- Full-stack architecture & DevOps: serverless, edge, containers, deployment patterns, infrastructure trends
- Developer experience improvements from major platforms (Vercel, Cloudflare, AWS, GitHub, etc.)

## Workflow

### Step 1: Check for user-provided context

If the user included specific topics, links, or focus areas in their message, note them — prioritize these. If the user said "only these topics," skip Step 2. Otherwise, supplement with web research.

### Step 2: Run web searches

Run 3–5 targeted searches covering the domains above. Focus on content published within the **last 7 days**. Look for:
- Official announcements, changelogs, and release notes
- Well-sourced articles from credible tech outlets (Hacker News top posts, The Verge, official engineering blogs, dev.to, InfoQ)
- Genuine developer community discussions with real engagement

Avoid: vague trend pieces with no concrete news, press releases without substance, repeat coverage of older announcements.

### Step 3: Present 5–7 ideas

Present exactly 5–7 ideas. For each:

```
[#] IDEA TITLE
Topic: [the specific update or development]
Source: [publication name + URL]
Date: [published date or "~[week of date]" if approximate]
Why it matters: [1–2 sentences on why developers should care]
Suggested angle: [e.g., "beginner explainer", "hot take", "personal experience with X", "comparison", "announcement breakdown", "what this means for your stack"]
```

If the user provided manual topics, always include those and reduce auto-researched ones to stay at 5–7 total.

### Step 4: Hand off

After presenting the ideas, say:

> "Ready to pass these to the reviewer for validation — or let me know if you'd like to swap any topics."

Do not generate posts. The topic-reviewer handles the next step.
