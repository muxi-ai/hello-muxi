# Hello Muxi

A multi-agent formation that introduces you to MUXI by explaining itself, crawling its own docs, generating files, and posting a real comment on GitHub.

## What It Does

Two specialist agents coordinated by an Overlord:

| Agent | Role | Tools |
|-------|------|-------|
| **Muxi Expert** | Explains MUXI using embedded knowledge and live docs. Can generate PDFs, charts, and other files. | Firecrawl, generate_file |
| **Community Greeter** | Posts a greeting on the MUXI GitHub repo as proof of real-world action | GitHub |

## Things to Try

| What to say | What happens |
|-------------|--------------|
| **"hi"** | The Overlord introduces itself and the formation |
| **"what is muxi?"** | The Expert answers using embedded knowledge |
| **"tell me about the overlord. use docs at muxi.org"** | The Expert scrapes muxi.org via Firecrawl, then answers |
| **"onboard me"** or **"get started"** | Triggers the onboarding SOP: asks your name, explains MUXI, posts a hello on GitHub, recaps what happened |
| **"create a one-page pdf about muxi"** | The Expert generates an actual PDF file and attaches it to the response using the artifacts module |
| **"create a bar chart showing pretend quarterly sales of acme corp"** | Generates a chart image using the artifacts module |


## Prerequisites

You need API keys for the LLM and the MCP tools. The formation uses Anthropic (Claude Haiku 4.5) as its LLM.

| Secret | What | Where to get it |
|--------|------|-----------------|
| `ANTHROPIC_API_KEY` | Anthropic API key (required) | [console.anthropic.com](https://console.anthropic.com) |
| `FIRECRAWL_API_KEY` | Firecrawl web scraping | [firecrawl.dev](https://firecrawl.dev) (free tier available) |
| `GITHUB_PAT` | GitHub Personal Access Token | [github.com/settings/tokens](https://github.com/settings/tokens) -- needs `public_repo` scope |

The `FORMATION_ADMIN_API_KEY` and `FORMATION_CLIENT_API_KEY` are auto-generated during setup for API authentication.

## Quick Start

### 1. Pull from registry

```bash
muxi pull @muxi/hello-muxi
cd hello-muxi
```

### 2. Set up secrets

```bash
muxi secrets setup
```

You'll be prompted for the API keys listed above.

### 3. Run locally

```bash
muxi up
```

### 4. Try it

Enter the CLI chat
```
muxi chat
```

Prompt away :)
```
> onboard me
```

The formation will ask your name, explain MUXI, post a greeting on GitHub, and show you the live comment URL.

## What the Onboarding SOP Does

1. The Overlord greets you and asks for your name
2. The **Muxi Expert** gives a concise intro to MUXI (using embedded knowledge + Firecrawl)
3. The **Community Greeter** posts "Hello from [your name]!" on [github.com/muxi-ai/muxi/issues/50](https://github.com/muxi-ai/muxi/issues/50) and returns the comment URL
4. The Overlord recaps: two agents, two MCPs, one SOP

## Formation Structure

```
hello-muxi/
├── formation.afs              # Formation config (Overlord, LLM, server)
├── SOUL.md                    # Overlord personality and behavior
├── agents/
│   ├── muxi-expert.afs        # MUXI explainer (Firecrawl + file generation)
│   └── community-greeter.afs  # GitHub commenter (GitHub MCP)
├── sops/
│   └── onboarding.md          # Guided onboarding walkthrough
├── knowledge/                 # Embedded docs (overview, FAQ, manifesto)
├── secrets.enc                # Encrypted secrets
└── .key                       # Encryption key (never commit)
```

## Concepts Demonstrated

- **Multi-agent orchestration** -- Overlord routing to specialist agents
- **MCP integration** -- live tool connections (Firecrawl, GitHub)
- **File generation** -- agents create PDFs, charts, and documents using sandboxed Python
- **SOPs** -- structured procedures triggered by user intent
- **Embedded knowledge** -- agent-specific knowledge base
- **Real-world side effects** -- a public GitHub comment as proof of action

## Links

- [MUXI Documentation](https://muxi.org/docs)
- [MUXI GitHub](https://github.com/muxi-ai/muxi)
- [Agent Formation Standard](https://agentformation.org)
