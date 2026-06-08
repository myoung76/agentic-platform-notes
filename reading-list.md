# Reading List

Annotated resources on MCP architecture, agent systems, and developer platform strategy. Organized by topic. Each entry includes why I think it's worth reading, not just what it is.

Last updated: June 2026

---

## MCP and agentic protocols

**[MCP Specification](https://modelcontextprotocol.io/specification/2025-11-25)**
Read the primitives section and the trust model section closely. The primitives section reveals the design philosophy -- why tools, resources, and prompts are the right three abstractions. The trust model section is underread and directly relevant to anyone building enterprise agent products. The authorization model for agents acting on behalf of users is still being worked out at the protocol level; this is where the spec is most honest about what's unsolved.

**[Why MCP Won -- Latent Space](https://www.latent.space/p/why-mcp-won)**
The best single piece on why MCP achieved ecosystem escape velocity when other standards didn't. The network effects argument is sound. Read it for the competitive dynamics analysis, not just the technical explanation.

**[github.com/modelcontextprotocol](https://github.com/modelcontextprotocol)**
The reference implementations are worth reading as product artifacts, not just code. How Anthropic chose to structure the example servers reveals their opinions about what good tool schema design looks like. The filesystem server and GitHub server are the clearest examples.

**[Anthropic's Model Specification](https://www.anthropic.com/research/model-specification)**
Understanding how the model is designed shapes how you design the agent. The sections on corrigibility, harm avoidance, and epistemic humility directly affect how agents behave when given ambiguous instructions or tool schemas. Product managers who build on top of Claude without reading this are missing context that affects their product decisions.

---

## Agent architecture

**[LangChain Blog](https://blog.langchain.dev)**
Uneven in quality but consistently early on practical agent architecture patterns. The posts on agent memory, tool reliability, and evaluation frameworks are worth reading. Skip the hype; focus on the posts that describe specific failure modes they've seen in production.

**[Building Effective Agents -- Anthropic](https://www.anthropic.com/research/building-effective-agents)**
The most honest piece Anthropic has published on when to use agents and when not to. The section on when simpler solutions are better is directly useful for product managers who are deciding whether a given use case actually needs an agent. Required reading before designing any agentic workflow.

**[AWS Agent Core Documentation](https://docs.aws.amazon.com/bedrock/latest/userguide/agents.html)**
Useful not as a product to use but as a reference for how a major cloud provider is thinking about agent infrastructure -- memory management, action groups, guardrails. The design decisions here will become industry defaults for enterprise buyers.

**[LangGraph Conceptual Guide](https://langchain-ai.github.io/langgraph/concepts/)**
The clearest explanation of stateful agent orchestration I've found. The sections on the orchestrator pattern, checkpointing, and human-in-the-loop are directly applicable to any multi-agent system design. If you're thinking about agent workflow state management, start here.

---

## Developer platform strategy

**[Working in Public -- Nadia Eghbal](https://www.amazon.com/Working-Public-Making-Maintenance-Software/dp/0578675862)**
The best thing I've read on developer community dynamics and the economics of open source maintenance. Relevant for anyone building a developer platform that depends on community contribution. The framing of maintainers vs. contributors vs. users maps well to how agent platform ecosystems actually stratify.

**[Stratechery -- Aggregation Theory](https://stratechery.com/2015/aggregation-theory/)**
Ben Thompson's framework for understanding platform power. Still the clearest mental model for why some platforms capture enormous value while others don't. The agent platform layer is playing out these dynamics right now -- who controls the user relationship, who controls the tool ecosystem, and which layer ends up with pricing power.

**[The Cold Start Problem -- Andrew Chen](https://www.coldstart.com)**
The best book on network effects and marketplace growth. The sections on atomic networks and the cold start problem are directly applicable to agent platform tool ecosystems. How do you get the first 100 high-quality tool servers before you have the developer community to sustain them?

**[Platform Revolution -- Parker, Van Alstyne, Choudary](https://www.amazon.com/Platform-Revolution-Networked-Markets-Transforming/dp/0393354350)**
The academic foundation for platform thinking. Dense but useful for the governance and design frameworks. The chapter on trust and safety in two-sided markets maps well to the tool verification problem in agent platforms.

---

## Observability and reliability

**[Site Reliability Engineering -- Google](https://sre.google/sre-book/table-of-contents/)**
The SRE book is directly applicable to agent platform operations in ways that most agent platform teams haven't absorbed yet. Agents are distributed systems. The SLO framework, error budget concept, and toil reduction principles apply. The chapter on being on-call is unexpectedly relevant to designing human-in-the-loop escalation paths for agent failures.

**[Honeycomb: Observability Engineering](https://www.oreilly.com/library/view/observability-engineering/9781492076438/)**
Charity Majors' framing of observability as asking arbitrary questions of your system in production is the right mental model for agent observability. The agent equivalent: can you trace a specific wrong output back to the exact tool call, context retrieval, or model response that caused it? Most current platforms cannot. This book explains why that matters and what the architecture looks like when you get it right.

---

## On AI and product

**[Prediction Machines -- Agrawal, Gans, Goldfarb](https://www.amazon.com/Prediction-Machines-Simple-Economics-Artificial/dp/1633695670)**
The clearest economic framework for thinking about where AI creates value: AI reduces the cost of prediction, which changes the value of everything that complements prediction (judgment, data, action). Useful for product strategy conversations about where AI actually fits in a workflow vs. where it's being used as a buzzword.

**[The Alignment Problem -- Brian Christian](https://www.amazon.com/Alignment-Problem-Machine-Learning-Values/dp/0393635821)**
Not a product book but directly relevant to anyone designing agent guardrails. The chapters on specification gaming and reward hacking are the clearest explanation I've found of why "just tell the agent what you want" is insufficient. Shapes how I think about tool schema design and guardrail architecture.

---

## My own thinking

**[agent-patterns.md](./agent-patterns.md)** -- Production patterns for multi-agent systems: orchestrator routing, shared context, tool reliability, guardrailed actions.

**[platform-strategy.md](./platform-strategy.md)** -- The extensibility-reliability tradeoff, cold start problem, and how to measure agent platform success.

**[mcp-architecture.md](./mcp-architecture.md)** -- MCP deep dive: the three primitives, tool schema design, why MCP won.
