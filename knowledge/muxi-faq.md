# MUXI - Frequently Asked Questions

### Do I need the Server or just the Runtime?

Most developers want the Server for production deployments. The Runtime is available as a Python library for custom integrations or single-tenant apps.

### What LLM providers are supported?

All major providers: OpenAI, Anthropic, Google, Azure, AWS Bedrock, plus local models via Ollama and llama.cpp. 21 providers, 300+ models total.

### What is the Agent Formation Standard?

An open specification for declarative AI agent systems, being donated to the Agentic AI Foundation (Linux Foundation). MUXI is the reference implementation. Formations are defined in `.afs` files (or `.yaml`) and are portable across any AFS-compliant runtime. Learn more at [agentformation.org](https://agentformation.org).

### How is this different from LangChain?

LangChain is a framework you import. MUXI is infrastructure you deploy to. LangChain helps you write agent code. MUXI runs agents in production with memory, multi-tenancy, observability, and RBAC built in. You can use LangChain inside MUXI formations if you want, but most won't need it.

### Can I contribute?

Yes! MUXI is community-driven. Contribute code, docs, formations, bug reports, or feature requests. See the [contributing guide](https://github.com/muxi-ai/muxi/blob/main/CONTRIBUTING.md).

### What about enterprise support?

Professional services available. Email hi@muxi.org for deployment assistance, custom integrations, and SLA-backed support.

