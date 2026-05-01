---
type: sop
name: MUXI Onboarding
description: Interactive walkthrough that introduces new users to MUXI by demonstrating multi-agent orchestration and MCP tools in action
mode: template
tags: onboard, get started, getting started, walk me through, hello muxi, how do I get started, new here, first time, introduction
bypass_approval: true
---

# MUXI Onboarding

Run a single-turn live demo: introduce MUXI, take a real action against GitHub, and recap everything in one user-visible reply. **Do NOT pause for user input** — every step in this SOP runs in a single turn and the final reply is what the user sees.

## Steps

1. **Introduce MUXI** [agent:muxi-expert]
   Internal preparation step — produce a concise summary of MUXI for use in the recap. Do NOT address the user directly here; the recap step will weave this into the final reply.
   Cover:
   - What MUXI is (open-source AI agent infrastructure platform)
   - What a formation is (a team of agents declared in YAML)
   - What they're inside right now (the Hello World formation: 2 agents, 2 MCPs, 1 SOP)
   Use embedded knowledge and Firecrawl to crawl https://muxi.org/docs only if needed for accuracy. Cite source URLs when available.
   Keep it to three or four sentences. This is a demo, not a lecture.

2. **Post Community Greeting** [agent:community-greeter] [critical]
   Internal action step — post a comment on issue #50 ("Hello MUXI: Community Guestbook") in the `muxi-ai/muxi` repository on GitHub.
   The comment should include:
   - A clever, friendly greeting
   - A one-liner: "Posted by the Hello World formation — a MUXI demo."
   Capture the returned comment URL so the recap step can include it. Do NOT address the user directly here.
   If the post fails, capture the error so the recap step can mention it gracefully and continue.

3. **Welcome, Recap & Next Steps** [critical]
   This is the ONLY user-visible reply for this SOP. Produce a single warm message that:

   a. Greets the user with a brief "Welcome to MUXI! Glad you're here." opener (one or two sentences).

   b. Tells them what just happened, in the past tense, conversationally — something like: "While you were reading this, the formation already did a few things on your behalf. One agent prepared an introduction to MUXI for you, and another agent posted a real GitHub comment as a live demo of an MCP tool call." Use the actual MUXI summary from step 1 inline.

   c. Surfaces the GitHub comment URL from step 2 as proof: "You can see the comment here: <URL>". If step 2 failed, say so honestly: "The GitHub guestbook comment failed (<reason>), but here's what would have happened…"

   d. Points to next steps:
   - Read the docs: https://muxi.org/docs
   - Explore formations: https://github.com/muxi-ai/muxi
   - Build their own: https://github.com/muxi-ai/sdks

   e. Closes with a soft invitation: "Want to know more about any of this, or should I show you something else?"

   Keep the whole reply scannable — short paragraphs, a bullet list for next steps, no walls of text.

## Expected Outcome

The user has, in a single turn:
- Read a warm welcome that acknowledges what the formation did for them
- Seen a real MCP tool call land (GitHub comment with live URL in the reply)
- Learned the core concepts: agents, formations, MCPs, SOPs
- Received clear next steps to go deeper

## Implementation Notes

- The runtime's `mode: template` decomposes this SOP into sequential tasks in one turn — there is no pause-for-user-input between steps. Authoring instructions like "wait for the user to respond" will not work; design steps 1–2 as internal preparation and put all user-facing wording in the final step.
- Steps 1 and 2 have no data dependency on each other; they can run in parallel once the runtime supports parallel SOP-template execution.
