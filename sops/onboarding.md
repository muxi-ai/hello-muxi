---
type: sop
name: MUXI Onboarding
description: Interactive walkthrough that introduces new users to MUXI by demonstrating multi-agent orchestration and MCP tools in action
mode: template
tags: onboard, get started, getting started, walk me through, hello muxi, how do I get started, new here, first time, introduction
bypass_approval: true
---

# MUXI Onboarding

Welcome new users to MUXI by demonstrating the formation's capabilities interactively.

## Steps

1. **Welcome & Collect Name** [critical]
   Greet the user warmly and ask for their name or handle.
   Explain briefly that this is a multi-agent formation running on MUXI, and you're about to walk them through what that means — live.
   Wait for the user to respond with their name before proceeding.

2. **Introduce MUXI** [agent:muxi-expert]
   Give the user a concise introduction to MUXI:
   - What MUXI is (open-source AI agent infrastructure platform)
   - What a formation is (a team of agents declared in YAML)
   - What they're inside right now (the Hello World formation: 2 agents, 2 MCPs, 1 SOP)
   Use embedded knowledge and Firecrawl to crawl https://muxi.org/docs if needed for additional detail. Cite source URLs when available.
   Keep it short — three to four sentences max. This is a demo, not a lecture.

3. **Post Community Greeting** [agent:community-greeter] [critical]
   Tell the user: "Let me show you an agent taking a real action."
   Post a comment on issue #50 ("Hello MUXI: Community Guestbook") in the `muxi-ai/muxi` repository on GitHub.
   The comment should include:
   - A clever greeting
   - A one-liner: "Posted by the Hello World formation — a MUXI demo."
   Return the comment URL to the user as proof.
   If the post fails, explain the error clearly and move on.

4. **Recap & Next Steps** [critical]
   Summarize what just happened:
   - "You talked to a formation with two specialist agents and two MCP tools."
   - "One agent explained MUXI using its knowledge base and live documentation tools."
   - "Another agent posted a real comment on GitHub using the GitHub MCP."
   - "All of this was orchestrated by an SOP — the procedure you just experienced."
   Then point the user to next steps:
   - Read the docs: https://muxi.org/docs
   - Explore formations: https://github.com/muxi-ai/muxi
   - Build their own: https://github.com/muxi-ai/sdks

## Expected Outcome

The user has:
- Learned what MUXI is in 60 seconds
- Seen a real MCP tool call happen (GitHub comment with live URL)
- Understood the core concepts: agents, formations, MCPs, SOPs
- Received clear next steps to go deeper
