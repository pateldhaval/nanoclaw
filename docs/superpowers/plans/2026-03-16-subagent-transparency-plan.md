# Subagent Transparency Implementation Plan

> **For agentic workers:** REQUIRED: Use superpowers:subagent-driven-development (if subagents available) or superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add transparency to agent teams by having main agent post prompts before spawning subagents, while subagents post their own responses.

**Architecture:** Pure documentation change - update CLAUDE.md files with explicit transparency instructions. No code changes needed as the IPC infrastructure already supports `send_message` with `sender` parameter.

**Tech Stack:** Markdown documentation (CLAUDE.md files)

---

## Overview

This implementation adds transparency instructions to group CLAUDE.md files so that:
1. Main agent posts "Asking {role}: {task}" before spawning teammates
2. Each subagent posts their own responses using `send_message` with sender identity
3. Group sees the full conversation flow

## Files to Modify

1. `groups/main/CLAUDE.md` - Add Agent Teams Transparency section
2. `groups/global/CLAUDE.md` - Update existing Agent Teams section

---

## Chunk 1: Update groups/main/CLAUDE.md

### Task 1: Add Agent Teams Transparency Section to Main Group

**Files:**
- Modify: `groups/main/CLAUDE.md`

- [ ] **Step 1: Read current groups/main/CLAUDE.md**

Read the file to find the exact location to insert the new section. Look for the "### Sub-agents and teammates" section around line 33-35.

- [ ] **Step 2: Add Agent Teams Transparency section**

Add the following after the existing "Sub-agents and teammates" section (around line 35):

```markdown
### Agent Teams Transparency

When creating a team of subagents using TeamCreate:

1. **Post the prompt before spawning** - Before calling TeamCreate, send a message announcing what you're asking teammates to do:
   - "Asking {role}: {task summary}"
   - Example: "Asking Researcher: Find information about X"

2. **Keep the group informed** - Brief status updates about team progress are welcome

3. **Subagents post their own responses** - Teammates will send their own messages; don't relay or summarize their work unless synthesizing at the end
```

- [ ] **Step 3: Commit the changes**

```bash
git add groups/main/CLAUDE.md
git commit -m "docs: add agent teams transparency section to main group"
```

---

## Chunk 2: Update groups/global/CLAUDE.md

### Task 2: Update Agent Teams Section in Global Memory

**Files:**
- Modify: `groups/global/CLAUDE.md`

- [ ] **Step 1: Read current groups/global/CLAUDE.md**

Read the file to find the existing "### Agent Teams (Creating Subagents)" section around lines 50-66.

- [ ] **Step 2: Update the Agent Teams section**

Replace or augment the existing section to add prompt posting requirement. The current section should be updated to include:

```markdown
### Agent Teams (Creating Subagents)

When you create a team of subagents using TeamCreate:

1. **Post your prompt first** - Before spawning teammates, send a message like:
   - "Asking {role}: {task}"
   - Example: "Asking Researcher: Look up the latest news on AI"

2. **Each teammate sends their own responses** - They will use send_message with their sender identity

3. **Include these instructions in EVERY teammate's prompt**:
   - Use mcp__nanoclaw__send_message with sender parameter
   - Always include a sender parameter with their role name (e.g., "Researcher", "Coder")
   - Keep messages short - 2-4 sentences max
   - Use proper formatting - single *asterisks* for bold, _underscores_ for italic, • for bullets
```

- [ ] **Step 3: Commit the changes**

```bash
git add groups/global/CLAUDE.md
git commit -m "docs: add prompt posting requirement to global agent teams instructions"
```

---

## Verification

After implementation, verify:

1. Main group CLAUDE.md has the new Agent Teams Transparency section
2. Global CLAUDE.md has updated Agent Teams section with prompt posting requirement
3. Both sections clearly instruct agents to post prompts before spawning subagents

No code tests needed - this is pure documentation.

---

## Summary

| Task | File | Change |
|------|------|--------|
| 1 | groups/main/CLAUDE.md | Add Agent Teams Transparency section |
| 2 | groups/global/CLAUDE.md | Update Agent Teams section with prompt posting |
