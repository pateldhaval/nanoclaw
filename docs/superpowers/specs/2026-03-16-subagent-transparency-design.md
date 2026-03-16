# Subagent Transparency Design

**Date**: 2026-03-16
**Status**: Draft

## Overview

Add transparency to agent teams (subagent swarm) communication so the group sees:
1. What prompts are being sent to subagents (posted by main agent before spawning)
2. Subagent responses (posted by subagents themselves)
3. Activity indicators when work begins

## Goals

- Make subagent work visible to the group
- Maintain multi-channel support (Telegram, WhatsApp, Slack, Discord)
- Follow hybrid model: main agent posts prompts, subagents post own responses

## Current State

- Telegram swarm is configured with bot pool
- Subagents can send messages with `sender` parameter to appear as different bots
- Existing instructions in `groups/global/CLAUDE.md` for teammates to use `send_message` with `sender`
- Main agent has minimal instructions about transparency

## Design

### 1. Main Agent Transparency (groups/main/CLAUDE.md)

Add explicit instructions for the main agent to post prompts before spawning teammates:

```
### Agent Teams Transparency

When creating a team of subagents using TeamCreate:

1. **Post the prompt before spawning** - Before calling TeamCreate, send a message announcing what you're asking teammates to do:
   - "Asking {role}: {task summary}"
   - Example: "Asking Researcher: Find information about X"

2. **Keep the group informed** - Brief status updates about team progress are welcome

3. **Subagents post their own responses** - Teammates will send their own messages; don't relay or summarize their work unless synthesizing at the end
```

### 2. Global Instructions (groups/global/CLAUDE.md)

Update existing Agent Teams section to add transparency requirements:

```
### Agent Teams (Creating Subagents)

When you create a team of subagents using TeamCreate:

1. **Post your prompt first** - Before spawning teammates, send a message like:
   - "Asking {role}: {task}"
   - Example: "Asking Researcher: Look up the latest news on AI"

2. **Each teammate sends their own responses** - They will use send_message with their sender identity

3. **Include these instructions in EVERY teammate's prompt** (as currently exists):
   - Use mcp__nanoclaw__send_message with sender parameter
   - Keep messages short
   - Use proper formatting
```

### 3. Teammate Instructions (already exists, verify)

The existing instructions in global CLAUDE.md already cover:
- Using send_message with sender parameter
- Keeping messages short
- Proper formatting

This is already correct - no changes needed for teammates.

### 4. Multi-Channel Considerations

The `send_message` IPC mechanism routes to the correct channel based on the group's configuration:
- Telegram: Uses bot pool with sender → bot name mapping
- WhatsApp: Uses sender as display name prefix
- Slack: Uses sender as username
- Discord: Uses sender as display name

No code changes required - the IPC system handles routing.

## Implementation

### Files to Modify

1. `groups/main/CLAUDE.md` - Add Agent Teams Transparency section
2. `groups/global/CLAUDE.md` - Update Agent Teams section with prompt posting requirement

### No Code Changes Required

The existing IPC infrastructure already supports:
- `send_message` tool with `sender` parameter
- Channel-specific routing in the host
- Bot pool for Telegram swarm

## Testing

After implementation:
1. Create a team with multiple subagents
2. Verify main agent posts prompt announcements
3. Verify each subagent posts their own responses with correct sender identity
4. Verify messages appear correctly in all channels (Telegram, WhatsApp, etc.)
