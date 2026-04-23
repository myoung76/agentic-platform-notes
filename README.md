# Agent Platform Resources

A curated reference on MCP architecture, agentic workflow design, and developer platform thinking — maintained by Matt Young.

I'm a product leader focused on agent-based platforms, MCP infrastructure, and developer-facing tooling at scale. This repo is where I organize my thinking on the protocols, patterns, and platforms shaping how software gets built.

---

## What is MCP and why it matters

The Model Context Protocol (MCP) is an open standard — originally developed by Anthropic, now stewarded by the Linux Foundation — that solves the M×N integration problem for AI agents. Before MCP, every AI application needed a custom connector to every tool or data source. MCP standardizes that interface so agents can connect to any MCP-compatible server using the same protocol.

The USB-C analogy is apt: one plug, any device. One protocol, any tool.

**The three primitives:**
- **Tools** — executable actions an agent can invoke (e.g., `create_github_issue`, `query_database`)
- **Resources** — read-only data sources the agent can pull context from (files, repos, API data)
- **Prompts** — reusable templates that shape how the agent formulates requests

**Why this matters for developer platforms:** GitHub's Copilot agent extension model is built on exactly this pattern. MCP gives any developer the ability to expose their tool, API, or service to any AI agent that speaks the protocol. The platform that wins is the one with the deepest, most reliable, most extensible tool ecosystem — which is why Agent Platform architecture is the most important infrastructure bet in developer tooling right now.

---

## Core MCP resources

| Resource | What it is |
|---|---|
| [modelcontextprotocol.io](https://modelcontextprotocol.io) | Official spec, docs, and implementation guides |
| [github.com/modelcontextprotocol](https://github.com/modelcontextprotocol) | All official repos — spec, SDKs, reference servers |
| [MCP Registry](https://github.com/mcp) | Browse 5,000+ community-built MCP servers |
| [MCP Specification](https://modelcontextprotocol.io/specification/2025-11-25) | Protocol spec (JSON-RPC 2.0 over stdio or HTTP+SSE) |

---

## My MCP work

**[domotz-mcp-server](https://github.com/myoung76/domotz-mcp-server)** — MCP server connecting Claude AI to the Domotz network monitoring platform. Exposes 130+ Domotz API endpoints as MCP tools, enabling natural language control of infrastructure monitoring, device management, and network diagnostics across 500K+ managed endpoints.

At Domotz, I led the product architecture and delivery of this integration — including the tool schema design, agent orchestration patterns, and the go-to-market strategy for MCP-enabled agentic workflows.

---

## Agent platform patterns worth understanding

These are the architectural patterns that separate production-grade agent platforms from demos. I think about these constantly in my product work.

**Agent memory and context retrieval**
Agents without persistent memory restart from zero on every invocation. The meaningful question for platform PMs isn't "does the agent have memory" — it's "what's the retrieval architecture, what's the latency, and how do you prevent context poisoning?" Episodic memory (what happened), semantic memory (what things mean), and procedural memory (how to do things) need different storage and retrieval strategies.

**Tool invocation reliability**
An agent is only as reliable as its worst tool call. Platform-grade agent infrastructure needs circuit breakers, retry logic, graceful degradation, and observability at the tool level — not just at the agent level. This is where infrastructure agent patterns (like what we built at Puppet and Domotz) translate directly to developer-facing agent platforms.

**Context window economics**
Code understanding and code search are fundamentally context problems. Retrieving the right 10K tokens from a 10M token codebase is a harder problem than it looks — and it's the core infrastructure challenge underneath GitHub Copilot's agent capabilities.

**Extensibility vs. reliability tradeoff**
Every open platform faces this: the more extensible you make the tool ecosystem, the harder it is to guarantee reliability. The right answer is layered trust — first-party tools with SLAs, verified third-party tools with attestation, community tools with explicit risk acknowledgment.

---

## Developer platform reading list

**On MCP and agentic protocols**
- [MCP Specification](https://modelcontextprotocol.io/specification/2025-11-25) — read the primitives section closely; the design decisions reveal a lot about how Anthropic thinks about agent-tool interaction
- [Why MCP Won](https://www.latent.space/p/why-mcp-won) — Latent Space podcast, good on the network effects argument
- [MCP Security Considerations](https://modelcontextprotocol.io/specification/2025-11-25) — the trust model section is underread and important

**On developer platform product strategy**
- [Stratechery: Platforms, Ecosystems, and the Role of APIs](https://stratechery.com) — Ben Thompson's framework for thinking about platform leverage
- [Working in Public](https://www.amazon.com/Working-Public-Making-Maintenance-Software/dp/0578675862) — Nadia Eghbal's book on open source maintenance is the best thing I've read on developer community dynamics

**On agent architecture**
- [Anthropic's Model Specification](https://www.anthropic.com/research/model-specification) — understanding how the model is designed shapes how you design the agent
- [LangChain Blog](https://blog.langchain.dev) — practical agent architecture patterns, less hype than most

---

## What I'm thinking about

A few open questions I'm actively working through as a PM in this space:

1. **Agent identity and authorization** — When an agent acts on behalf of a developer, whose permissions apply? OAuth scopes were designed for humans. The agent authorization model is still being figured out at the protocol level.

2. **Code search as an agent primitive** — The jump from "search my codebase" to "understand the architectural intent of this codebase" requires something closer to semantic indexing than keyword search. How do you build a product around that distinction?

3. **The cold-start problem for enterprise agent platforms** — Enterprises won't give agents broad permissions on day one. How do you design an agent platform that's useful with narrow permissions and earns its way to broader access over time?

4. **Measuring agent platform success** — DAU/MAU don't map well to agent usage. What are the right leading indicators for a developer agent platform that's actually delivering value vs. just generating API calls?

---

*I'm [@myoung76](https://github.com/myoung76) on GitHub. Find me on [LinkedIn](https://www.linkedin.com/in/mattyoung/) or reach me at seamattyoung@gmail.com.*
