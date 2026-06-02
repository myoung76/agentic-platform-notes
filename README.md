# Agent Platform Resources

A working reference on MCP architecture, agentic workflow design, and developer platform thinking — maintained by Matt Young.

I'm a product leader who's spent the last few years in agent-based platforms, MCP infrastructure, and developer tooling. This repo is where I keep my thinking organized on the protocols, patterns, and platforms that actually matter right now.

---

## What is MCP and why it matters

The Model Context Protocol (MCP) is an open standard — originally from Anthropic, now under the Linux Foundation — that solves the M×N integration problem for AI agents. Before MCP, every AI application needed a custom connector to every tool or data source. MCP standardizes that interface so agents can connect to any MCP-compatible server using the same protocol.

The USB-C analogy holds: one plug, any device. One protocol, any tool.

**The three primitives:**

- **Tools** — executable actions an agent can invoke (e.g., `create_github_issue`, `query_database`)
- **Resources** — read-only data sources the agent can pull context from (files, repos, API data)
- **Prompts** — reusable templates that shape how the agent formulates requests

For developer platforms, this matters because GitHub's Copilot agent extension model runs on exactly this pattern. Any developer can expose their tool, API, or service to any MCP-speaking agent. Which makes the tool ecosystem — depth, reliability, extensibility — the real competition surface in agent infrastructure right now.

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

**[domotz-mcp-server](https://github.com/myoung76/domotz-mcp-server)** — MCP server connecting Claude to the Domotz network monitoring platform. Exposes 130+ Domotz API endpoints as MCP tools for natural language control of infrastructure monitoring, device management, and network diagnostics across 500K+ managed endpoints.

I led the product architecture and delivery of this integration — tool schema design, agent orchestration patterns, and the go-to-market strategy for MCP-enabled agentic workflows.

---

## Agent platform patterns worth understanding

These are the architectural patterns that separate real agent platforms from demos. I think about them constantly.

**Agent memory and context retrieval**
Agents without persistent memory restart from zero on every invocation. The question that actually matters for platform PMs isn't "does the agent have memory" — it's "what's the retrieval architecture, what's the latency, and how do you prevent context poisoning?" Episodic memory (what happened), semantic memory (what things mean), and procedural memory (how to do things) need different storage and retrieval strategies.

**Tool invocation reliability**
An agent is only as reliable as its worst tool call. Real agent infrastructure needs circuit breakers, retry logic, graceful degradation, and observability at the tool level — not just at the agent level. This is where my time at Puppet and Domotz translates: infrastructure agent patterns and developer-facing agent platforms have more in common than people expect.

**Context window economics**
Code understanding and code search are fundamentally context problems. Retrieving the right 10K tokens from a 10M token codebase is harder than it looks — and it's the core infrastructure challenge underneath GitHub Copilot's agent capabilities.

**Extensibility vs. reliability**
Every open platform faces this tradeoff. The more extensible you make the tool ecosystem, the harder it is to guarantee reliability. The right answer is layered trust: first-party tools with SLAs, verified third-party tools with attestation, community tools with explicit risk acknowledgment.

---

## Developer platform reading list

**On MCP and agentic protocols**
- [MCP Specification](https://modelcontextprotocol.io/specification/2025-11-25) — read the primitives section closely; the design decisions reveal how Anthropic thinks about agent-tool interaction
- [Why MCP Won](https://www.latent.space/p/why-mcp-won) — Latent Space podcast, good on the network effects argument
- [MCP Security Considerations](https://modelcontextprotocol.io/specification/2025-11-25) — the trust model section is underread

**On developer platform product strategy**
- [Stratechery: Platforms, Ecosystems, and the Role of APIs](https://stratechery.com) — Ben Thompson's framework for thinking about platform leverage
- [Working in Public](https://www.amazon.com/Working-Public-Making-Maintenance-Software/dp/0578675862) — Nadia Eghbal on open source maintenance; the best thing I've read on developer community dynamics

**On agent architecture**
- [Anthropic's Model Specification](https://www.anthropic.com/research/model-specification) — understanding how the model is designed shapes how you design the agent
- [LangChain Blog](https://blog.langchain.dev) — practical agent architecture patterns, less hype than most

---

## What I'm thinking about

A few open questions I'm actively working through:

1. **Agent identity and authorization** — When an agent acts on a developer's behalf, whose permissions apply? OAuth scopes were designed for humans. The agent authorization model is still being worked out at the protocol level.

2. **Code search as an agent primitive** — The jump from "search my codebase" to "understand the architectural intent of this codebase" requires something closer to semantic indexing than keyword search. How do you build a product around that distinction?

3. **The cold-start problem for enterprise agent platforms** — Enterprises won't give agents broad permissions on day one. How do you design a platform that's useful with narrow permissions and earns its way to broader access over time?

4. **Measuring agent platform success** — DAU/MAU don't map well to agent usage. What are the right leading indicators for a developer agent platform that's actually delivering value vs. just generating API calls?

---
