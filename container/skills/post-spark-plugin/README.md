# post-spark

Research, review, and write LinkedIn + Twitter/X tech posts — with a human in the loop at every key decision point.

## Overview

post-spark splits the social media content workflow into three focused, chainable skills:

1. **tech-researcher** — Finds 5–7 recent, post-worthy tech topics from the last 7 days
2. **topic-reviewer** — Validates topics for recency, source credibility, scope fit, and uniqueness (loops with researcher up to 5 times)
3. **post-writer** — Writes polished LinkedIn posts + tweets using a consistent senior full-stack developer persona

The workflow is human-in-the-loop: you select topics after research, review after validation, and approve posts before publishing.

## Skills

| Skill | Trigger phrases |
|-------|----------------|
| `tech-researcher` | "find tech topics", "what should I post about this week", "run research", "find ideas for posts" |
| `topic-reviewer` | "review these topics", "validate the ideas", "check the sources", "run the reviewer" |
| `post-writer` | "write the posts", "draft the LinkedIn post", "write a tweet about [topic]", "turn this into a post" |

## Typical Workflow

```
1. "Find tech topics for this week"
   → tech-researcher surfaces 5–7 ideas

2. "Review these topics"
   → topic-reviewer validates recency, sources, scope, and duplicates
   → loops back to researcher if topics need replacing (max 5 iterations)

3. You select 1–3 topics to write about

4. "Write the posts"
   → post-writer generates LinkedIn post + tweet + hashtags for each
```

## Standalone Usage

The post-writer works independently — skip the research pipeline and go straight to writing:

- "Write a LinkedIn post about [topic]"
- "Write a tweet based on this article: [URL]"
- "Turn these notes into a LinkedIn post: [paste notes]"

## Persona

Posts are written in the voice of a senior full-stack developer/architect (12+ years experience) specialising in React, Next.js, Node.js, and the AI ecosystem. The tone is peer-to-peer: curious, knowledgeable, personal, and accessible — not corporate or lecture-y.

## Setup

No external services or environment variables required. The plugin uses built-in web search for research.

## Duplicate Checking

To enable duplicate detection during review, paste a list of your previously published post topics when invoking the topic-reviewer. Example:

> "Review these topics. Here are topics I've already covered: Next.js 15 release, Claude 3.5 launch, Bun 1.0, React Server Components deep dive."
