# MUXI - The AI Application Server

> No one builds their own Nginx to deploy a website. No one should reinvent infrastructure to build AI.

MUXI is open-source AI application server for running AI agents in production. Not a framework. Not a wrapper. A complete server stack.

## What is MUXI?

MUXI (Multiplexed eXtensible Intelligence, pronounced /ˈmʌk.siː/) is production infrastructure purpose-built for AI agents. Unlike frameworks that you import as libraries, MUXI is a complete server stack that runs, orchestrates, and manages multi-agent systems at scale.

**The mental model:**

How it runs — like a web application:
| Layer | Web World | MUXI |
|-------|-----------|------|
| Server | Nginx | MUXI Server (Go) |
| Runtime | Node / Python | MUXI Runtime (Python) |
| Application | Your code | Formation (.afs) |

How you ship it — like Docker:
| Concept | Docker | MUXI |
|---------|--------|------|
| Engine | Docker Engine | Server + Runtime |
| Definition | Dockerfile | Formation |
| Registry | Docker Hub | MUXI Registry |
| CLI | `docker` | `muxi` |

**The key insight:** You build applications ON TOP of MUXI using SDKs. Your frontend, mobile app, or backend talks to MUXI via API. MUXI handles orchestration, memory, multi-tenancy, and observability. That's what makes it infrastructure, not a framework.

**Core Philosophy:** Agents are native primitives – declared in portable `.afs` files, orchestrated at the infrastructure layer, scaled like containers. No frameworks to import. No infrastructure to build. Just declare and deploy.

## Who Is MUXI For?

**Platform Builders**: Building a SaaS with AI features? MUXI handles orchestration, memory, and multi-tenancy so you can focus on your product.

**Internal Tool Builders**: Deploying AI assistants for your team? MUXI gives you RBAC, observability, and enterprise-grade infrastructure out of the box.

**Developers Tired of Framework Hell**: Spent months on LangChain orchestration code? MUXI replaces it with YAML configuration and a single deploy command.

You could build the next OpenClaw on MUXI. That's the point.

## Key Differentiators

- **Infrastructure, not a framework**: Deploy with `muxi deploy` – agents go live instantly
- **API-first architecture**: REST, WebSocket, gRPC + SDKs for Python, TypeScript, Go, Swift, Java
- **Formation-based deployment**: Complete AI systems defined in the Agent Formation Standard
- **LLM-agnostic**: Use any provider (OpenAI, Anthropic, Google, AWS, Azure, local models)
- **Multi-tenant by design**: Built-in user isolation with per-user credentials and enterprise RBAC
- **Self-hosted**: Complete data sovereignty, runs anywhere (on-prem, cloud, air-gapped)
- **Open source**: Elastic License 2.0 (ELv2) and Apache 2.0 – free for commercial use, forever

## Core Concepts

### Formations

A formation is a complete AI system packaged as a single deployable unit. MUXI is the reference implementation of the [Agent Formation Standard](https://agentformation.org) – an open spec for declarative AI agents, heading to the Linux Foundation.

Like a Dockerfile for containers, but for AI agents. Formations include:

- Agent definitions and configurations
- Domain knowledge (files, URLs, documents)
- MCP (Model Context Protocol) tool connections
- Standard Operating Procedures (SOPs)
- Triggers (schedules, webhooks)
- Settings and environment variables

All defined in `.afs` files (or `.yaml` – both work). Version-controlled, portable, and deployable with one command.

### The MUXI Stack

Four architectural layers:

1. **SDKs** - Python, JavaScript, Go, Swift, Java clients for programmatic interaction
2. **APIs** - REST endpoints for deployments, chat, streaming, observability
3. **Runtime** - Core orchestration: agents, memory, tools, task execution
4. **Server** - Self-hosted infrastructure for production deployments

Developers build ON TOP of MUXI. Your app calls MUXI's API. MUXI handles everything else.

### Agent-Native Infrastructure

Agents aren't bolted on – they're native primitives. State persistence, task orchestration, and resource management happen at the infrastructure layer. Agents are declared, deployed, and scaled like containers.

## Key Features

### Deployment & Operations

- **One-command deployment**: `muxi deploy` and you're live
- **GitOps workflow**: Version-controlled formations, CI/CD integration, instant rollbacks
- **Hot updates**: Zero downtime deployments with automatic restarts
- **Single binary**: No runtime dependencies, runs anywhere

### Intelligence & Execution

- **Overlord orchestration engine**: ~10,000-line core that powers multi-agent coordination, task routing, and workflow execution
- **Intelligent task decomposition**: Complex requests automatically broken into executable subtasks
- **Adaptive workflow creation**: Non-deterministic workflows generated based on context
- **Agent collaboration**: Multi-agent coordination via A2A protocol
- **Multimodal support**: Images, PDFs, audio, video processing out-of-the-box

### Memory & Context

- **Three-tier memory**: Buffer (immediate), persistent (long-term), vector (semantic)
- **User synopsis caching**: LLM-synthesized profiles reduce costs by 85%+
- **Intelligent context management**: Automatic FIFO cleanup with relevance scoring
- **Domain knowledge system**: Pre-load agents with files, docs, policies via RAG

### Integration & Tools

- **MCP Protocol native**: Access 1,000+ tools (GitHub, Slack, Postgres, Stripe, etc.)
- **Multi-user MCP access**: Per-user OAuth tokens and API keys with encryption
- **Agent Skills**: Native support for the open SKILL.md specification
- **LLM provider agnostic**: 21 providers, 300+ models via OneLLM
- **Automatic failover**: Provider switching when services fail

### MCP Without the Bloat

Traditional MCP implementations dump entire tool schemas into every conversation – often 10-30k tokens before your agent does anything useful. MUXI takes a different approach:

- **Load once**: Tool definitions fetched at startup and stored in a lightweight Python registry
- **Query on demand**: Subagents access only the tools they need at runtime
- **Minimal overhead**: Total context cost under 1k tokens, regardless of how many MCP servers you connect

Connect 10+ MCP servers simultaneously without context degradation.

### Production Features

- **Multi-tenancy**: Complete session isolation with per-user credentials
- **Enterprise RBAC**: Role-based access control (only AI agent platform with this)
- **Real-time streaming**: WebSocket and SSE support for live updates
- **Built-in observability**: 349 event types, stream to 10+ systems (Datadog, Splunk, Elastic, etc.)
- **Enterprise resilience**: Circuit breakers, exponential backoff, graceful degradation
- **70%+ LLM cost savings**: Semantic caching reduces costs dramatically

### Triggers & Automation

- **Natural language scheduling**: "Check email every hour" or "remind me tomorrow at 2pm"
- **Webhook triggers**: External systems activate agents via HTTP endpoints
- **Event-driven architecture**: Unified orchestration for schedules, webhooks, user interactions
- **Dynamic async execution**: Smart sync/async switching with complexity detection

### Developer Experience

- **Standard Operating Procedures**: Define organizational knowledge agents reason over (not rigid workflows)
- **Artifact generation**: Create documents, spreadsheets, presentations, code files
- **Type-safe SDKs**: Full IDE autocomplete and type checking
- **88.9% test coverage**: Production-ready from day one

## Quick Start

```bash
# Install (macOS)
brew install muxi-ai/tap/muxi

# Install (Linux)
curl -fsSL https://muxi.org/install | sudo bash

# Install (Windows)
powershell -c "irm https://muxi.org/install | iex"

# Deploy your first formation
muxi pull @muxi/bookkeeping
muxi secrets set OPENAI_API_KEY ••••••••••
muxi deploy --profile production
```

Then build on top:

```python
from muxi import MuxiClient

client = MuxiClient("http://localhost:3000")
response = client.chat(
    formation="bookkeeping",
    message="What's my current balance?",
    user_id="user_123"
)
```

Your app talks to MUXI. MUXI handles everything else.

## Documentation

Our documentation is available in markdown format for easier parsing:

- Add `.md` to any doc URL: `https://muxi.org/docs/[page].md`
- Full markdown sitemap: https://muxi.org/llms-sitemap.txt
- Most HTML pages include `<link rel="alternate" type="text/markdown">` tags for easier parsing by AI assistants.

## Architecture

MUXI implements the Agent Formation Standard (being donated to the Agentic AI Foundation under the Linux Foundation), where complete AI systems are packaged as `.afs` files.

**Go + Python split**: The Server is written in Go (single binary, excellent concurrency, low memory). The Runtime is Python (ML ecosystem, async-first). Go handles the hot path (orchestration, routing, auth). Python handles AI workloads where async I/O is sufficient for LLM-bound operations.

The server manages:

- Formation lifecycle (deploy, update, rollback)
- Multi-tenant isolation and RBAC
- Agent orchestration and task execution
- Memory management across three tiers
- Tool access via MCP protocol
- Event streaming and observability

**Registry**: The MUXI Registry is Docker Hub for agents – push, pull, and share formations with version management and access control.

## Use Cases

- **SaaS AI features**: Embed AI capabilities in your application via SDKs
- **Customer support systems**: Multi-agent teams handling tickets, refunds, inquiries
- **Internal tooling**: Automating workflows across GitHub, Slack, Jira, etc.
- **Document processing**: Extract, analyze, and generate reports from files
- **Data analysis platforms**: Query databases, generate visualizations, create reports
- **Booking and scheduling**: Coordinate calendars, send notifications, manage reservations

## Licensing

- **MUXI Server & Runtime**: Elastic License 2.0 (ELv2)
- **Formations, CLI, SDKs**: Apache 2.0
- **Agent Formation Standard**: Apache 2.0 (independent open standard)

**You CAN:**
- Use for internal projects and products
- Build and sell products that use MUXI
- Deploy for clients and customers
- Self-host on your infrastructure

**You CANNOT:**
- Offer MUXI itself as a hosted service (SaaS)

## Technical Details

- **Response time**: <100ms average
- **Test coverage**: 88.9% across 63,000+ test lines
- **Observability events**: 349 distinct event types
- **LLM cost savings**: 70%+ via semantic caching
- **Deployment**: Single binary or Docker container
- **Supported platforms**: Linux, macOS, Windows
- **Protocol support**: HTTP/REST, WebSocket, Server-Sent Events, gRPC

## Comparison with Alternatives

### vs. Frameworks (LangChain, CrewAI, AutoGen)

MUXI makes frameworks obsolete for 90% of use cases.

| | MUXI | Frameworks |
|---|---|---|
| **Type** | Server infrastructure | Python library |
| **Deployment** | `muxi deploy` | Write deployment code |
| **Configuration** | Declarative `.afs` files | Imperative code |
| **Multi-tenancy** | Built-in isolation | Build yourself |
| **Memory** | 3-tier with synopsis caching | Build yourself |
| **Observability** | 349 events included | Add external tools |
| **RBAC** | Enterprise-grade included | Build yourself ($100K+) |

Think: Flask is a framework. Nginx is infrastructure. You don't import Nginx — you deploy to it.

### vs. AI Assistants (OpenClaw, ChatGPT, Claude)

Different layer entirely. OpenClaw is a personal AI assistant (single-user product). MUXI is infrastructure to build products like OpenClaw — with multi-tenancy, proper memory, and SDKs for integration.

You could build OpenClaw on MUXI. That's the point.

### vs. Cloud AI (Bedrock, Vertex, Azure AI)

Cloud AI = model hosting + APIs + some orchestration primitives.
MUXI = agent-specific runtime with memory, orchestration, multi-tenancy.

We're complementary, not competitive. MUXI supports 21 providers, 300+ models.

## Business Model

Open-source with sustainable revenue from support services, not paywalls:

- Core stack is free and self-hostable forever
- GitHub Sponsors for priority support
- Professional services for enterprise deployments
- No feature restrictions or bait-and-switch licensing

**Track record**: Built by a developer whose other open-source libraries receive 20M+ monthly downloads – MUXI is production-grade from day one.

## Community & Support

- **Documentation**: https://muxi.org/docs
- **GitHub**: https://github.com/muxi-ai
- **Discussions**: https://muxi.org/community
- **Registry**: https://registry.muxi.org
- **Roadmap**: https://github.com/orgs/muxi-ai/projects/1
- **Sponsors**: https://github.com/sponsors/muxi-ai
- **Email**: hi@muxi.org
- **Twitter**: @muxi_ai

## Who Built This?

Created by Ran Aroussi (x.com/@aroussi), a 35+ year tech veteran whose open-source libraries, excluding MUXI, receive 20M+ monthly downloads. Author of "Production-Grade Agentic AI" (650+ page technical book). No VC funding, no exit timeline – built for long-term sustainability.

## Quick Links

- [Quickstart Guide](https://muxi.org/docs/quickstart)
- [Installation](https://muxi.org/docs/install)
- [Formation Spec](https://agentformation.org)
- [API Reference](https://muxi.org/docs/reference/api)
- [Examples](https://muxi.org/docs/examples)
- [Contributing Guide](https://muxi.org/contributing)
- [Changelog](https://muxi.org/changelog)
