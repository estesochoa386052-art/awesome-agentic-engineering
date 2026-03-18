<div align="center">

# Awesome Agentic Engineering

A curated collection of agent harnesses, frameworks, case studies, and resources from companies shipping production-grade agentic coding systems.

**The model is a commodity — the harness is the moat.**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

[Website](https://Parvej2017.github.io/awesome-agentic-engineering/) · [Contributing](CONTRIBUTING.md) · [Submit Resource](https://github.com/Parvej2017/awesome-agentic-engineering/issues/new)

</div>

---

## What is Harness Engineering?

**Harness engineering** is the practice of building the constraints, tools, documentation, and feedback loops that make AI coding agents productive in production. The term was popularized by [OpenAI's February 2026 post](https://openai.com/index/harness-engineering/), but the concept exists across every major engineering organization deploying agents at scale.

A harness encompasses: **context engineering** (what the agent knows), **architectural constraints** (what the agent can and cannot do), **execution environments** (isolated devboxes, VMs), **feedback loops** (linting, CI, review), and **tooling** (curated MCP servers, APIs, file access).

> "The real magic is the infrastructure. The AI agent itself is almost a commodity." — Stripe Engineering

---

## Contents

- [Company Deployments](#company-deployments)
- [Core Patterns](#core-patterns)
- [Agent Frameworks & Harnesses](#agent-frameworks--harnesses)
- [Engineering Blogs](#engineering-blogs)
- [Papers & Research](#papers--research)
- [Talks & Podcasts](#talks--podcasts)
- [Tools & Repos](#tools--repos)
- [Guides & Tutorials](#guides--tutorials)

---

## Company Deployments

Real-world production deployments of agentic coding systems at scale.

### OpenAI — Codex + AGENTS.md

The team that defined "harness engineering." Built **1M+ lines of code** over 5 months using zero manually-written code, with 88 AGENTS.md files across ~1,500 PRs. Three pillars: context engineering via structured `docs/` directories, architectural constraints enforced by custom linters, and "garbage collection" background agents.

| Metric | Value |
|---|---|
| Engineers using Codex weekly | 95% |
| More PRs by adopters vs peers | +70% |
| Avg PR review time | 2–3 min (down from 10–15 min) |
| Parallel Codex threads per engineer | 10–20 |

- [Harness Engineering: Leveraging Codex in an Agent-First World](https://openai.com/index/harness-engineering/) — OpenAI, Feb 2026
- [How Codex is Built](https://newsletter.pragmaticengineer.com/p/how-codex-is-built) — Pragmatic Engineer

### Stripe — Minions + Blueprint Architecture

Fully unattended, fire-and-forget agents that take a task description (via Slack) and produce complete, CI-passing PRs. **1,300+ PRs merged per week** with zero human-written code. Runs on isolated devboxes with a 500-tool MCP server ("Toolshed") — each agent gets only ~15 relevant tools. Blueprint architecture alternates deterministic and agentic nodes. Built on a fork of Block's open-source Goose agent.

| Metric | Value |
|---|---|
| PRs merged per week | 1,300+ |
| Human-written code per PR | 0 |
| Devbox spin-up time | ~10 seconds |
| Internal tools available | ~500 (via Toolshed MCP) |

- [Minions: Stripe's One-Shot, End-to-End Coding Agents](https://www.engineering.fyi/article/minions-stripe-s-one-shot-end-to-end-coding-agents) — Stripe Eng, Feb 2026
- [How Stripe's Minions Ship 1,300 PRs/wk](https://blog.bytebytego.com/p/how-stripes-minions-ship-1300-prs) — ByteByteGo

### Anthropic — Claude Code

Claude Code built itself — **~90% of its codebase is AI-generated**. ~12-person team ships 60–100 internal releases per day. Published definitive guide to harnesses for long-running agents: two-agent architecture (initializer + coder), incremental commits, progress files in JSON. Nicholas Carlini's 16-agent C compiler project: 100,000 lines of Rust, passes 99% of GCC's torture suite.

| Metric | Value |
|---|---|
| Engineers using daily | 80%+ |
| PR throughput increase | +67% |
| Self-reported productivity boost | +50% |
| AI assists in daily work | 60% |

- [Effective Harnesses for Long-Running Agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) — Anthropic, Nov 2025
- [Building a C Compiler with Parallel Claudes](https://www.anthropic.com/engineering/building-c-compiler) — Anthropic, 2026
- [How AI is Transforming Work at Anthropic](https://www.anthropic.com/research/how-ai-is-transforming-work-at-anthropic) — Anthropic Research, Dec 2025

### Uber — MCP Gateway + AIFX

Four-layer agentic platform across **5,000 engineers** and 6 monorepos (Go, Java, Android, iOS, TypeScript, Python). MCP Gateway exposes internal endpoints as MCP servers. Five named tools: uReview (90% of diffs, 4-min median), AutoCover (5,000+ tests/month), Shepherd (4.3M lines migrated), Validator, Code Inbox.

| Metric | Value |
|---|---|
| Agent code changes per week | ~1,800 |
| Engineers using AI monthly | 92–95% |
| Code that is AI-generated (IDE) | 65–72% |
| Dev hours saved | 21,000+ |

- [uReview: Scalable, Trustworthy GenAI for Code Review](https://www.uber.com/blog/ureview/) — Uber Eng
- [How Uber Uses AI for Development](https://newsletter.pragmaticengineer.com/p/how-uber-uses-ai-for-development) — Pragmatic Engineer

### Google / DeepMind — DIDACT + AlphaEvolve

DIDACT trains on the full development process — edits, builds, reviews, not just finished code. **30%+ of new code is AI-generated** (37% acceptance rate). AlphaEvolve (evolutionary coding agent) recovered **0.7% of Google's worldwide compute** through Borg scheduling improvements. Big Sleep (Project Zero × DeepMind) discovered first AI-found exploitable vulnerability in widely-used software (SQLite).

| Metric | Value |
|---|---|
| New code AI-generated | 30%+ |
| Code completion acceptance rate | 37% |
| Jules beta code improvements | 140,000+ |
| Compute recovered by AlphaEvolve | 0.7% of worldwide |

- [AI in Software Engineering at Google](https://research.google/blog/ai-in-software-engineering-at-google-progress-and-the-path-ahead/) — Google Research
- [AlphaEvolve: Gemini-Powered Coding Agent](https://deepmind.google/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/) — DeepMind, May 2025

### Meta — REA + JiTTests + Confucius

Ranking Engineer Agent (REA) drives end-to-end ML lifecycle for ads ranking: **2x model accuracy, 5x engineering productivity**. JiTTests generate disposable tests per code change — zero maintenance cost, only surface when a bug is caught. Confucius SDK (open-sourced Dec 2025) features a meta-agent that builds and refines other agents, hitting 74.6% SWE-Bench-Verified.

| Metric | Value |
|---|---|
| Model accuracy via REA | 2x |
| Engineering productivity | 5x |
| SWE-Bench via Confucius | 74.6% |
| 2025 AI infrastructure capex | $60–65B |

- [REA: Autonomous AI for Ads Ranking](https://engineering.fb.com/2026/03/17/developer-tools/ranking-engineer-agent-rea-autonomous-ai-system-accelerating-meta-ads-ranking-innovation/) — Meta Eng, Mar 2026
- [JiTTests: The Death of Traditional Testing](https://engineering.fb.com/2026/02/11/developer-tools/the-death-of-traditional-testing-agentic-development-jit-testing-revival/) — Meta Eng, Feb 2026

### Shopify — Roast Framework

CEO mandated AI as a baseline expectation. Open-sourced **Roast**: Ruby-based framework for structured AI workflows mixing deterministic and agentic nodes with YAML+Markdown config. Engineering director candidates are expected to be "90–95% AI, 5–10% manual" in coding interviews. Revenue grew 20–40% annually while headcount declined from 11,600 to 8,100.

- [Introducing Roast: Structured AI Workflows](https://shopify.engineering/introducing-roast) — Shopify Eng
- [How AI is Changing SE at Shopify](https://newsletter.pragmaticengineer.com/p/how-ai-is-changing-software-engineering) — Pragmatic Engineer

### Amazon / AWS — Q Developer + Kiro

**30,000 production Java applications** upgraded from Java 8/11 to Java 17, saving **4,500 developer-years** and $260M. Kiro: spec-driven agentic IDE with persistent context across sessions. Cautionary tale: an autonomous agent caused a 13-hour AWS Cost Explorer outage, triggering a 90-day safety reset across 335 critical systems.

- [AI Assistants Will Overwhelm Your Pipeline](https://aws.amazon.com/blogs/enterprise-strategy/your-ai-coding-assistants-will-overwhelm-your-delivery-pipeline-heres-how-to-prepare/) — AWS Enterprise Strategy
- [Measuring Impact of AI Assistants](https://aws.amazon.com/blogs/enterprise-strategy/measuring-the-impact-of-ai-assistants-on-software-development/) — AWS

### LinkedIn — MCP-First Architecture

Foreground agents (IDE-based) and background agents (migrations, upgrades, test coverage) unified through MCP protocol connecting to code search, static analysis, documentation, observability, and semantic indexes. Engineers push code to production in **17 minutes**. Engineers with strong soft skills promoted **13% faster** — orchestration is fundamentally a communication and judgment task.

- [Platform Engineering for AI: MCP at LinkedIn](https://www.infoq.com/podcasts/platform-engineering-scaling-agents/) — InfoQ
- [AI Transformation at LinkedIn](https://linearb.io/blog/ai-transformation-software-development-linkedin) — LinearB

---

## Core Patterns

Six patterns that converged independently across every major engineering org deploying agents at scale.

### 1. Deterministic–Agentic Hybrid

Alternate fixed logic nodes (linting, CI, git) with LLM nodes (generation, interpretation). The model does not run the system — the system runs the model.

> Seen in: Stripe Blueprints, Uber Validator, Meta Confucius

### 2. Isolated Execution Environments

Agents run in sandboxes identical to human developer machines — devboxes, VMs, containers. Isolation *is* the permission system. No complex auth needed.

> Seen in: Stripe devboxes, Google Cloud VMs (Jules), Anthropic local exec

### 3. Context Engineering (not prompt engineering)

Curated, structured, contextually relevant information delivered per task. AGENTS.md files, directory-scoped rules, semantic indexes. Over-contextualization is as harmful as under-contextualization.

> Seen in: OpenAI AGENTS.md (~100 lines each), Stripe Toolshed (~15 of 500 tools per task), Uber MCP Gateway

### 4. Tiered Review Gates

Risk-classified review: documentation gets AI-only review; billing logic, security, and data migrations demand full human scrutiny. Cap CI retries at 2–3 rounds.

> Seen in: OpenAI (tiered review system), Stripe (2 CI rounds max), Amazon (senior sign-off for junior AI code)

### 5. Background / Async Agent Workflows

The biggest productivity gains come from fire-and-forget background agents, not interactive copilots. Engineers launch 10–20 parallel tasks and review output, not generate it.

> Seen in: Stripe Minions, Uber background agents (grew from <1% to 8% of changes), OpenAI parallel Codex threads

### 6. Failure as Infrastructure Signal

When an agent struggles, the fix is never "try harder." Identify what capability or constraint is missing and feed it back into the repository as permanent infrastructure.

> Seen in: OpenAI's core principle, Stripe's rule files, Anthropic's two-agent architecture

---

## Agent Frameworks & Harnesses

| Framework | Org | Language | Type | Key Feature |
|---|---|---|---|---|
| [Roast](https://shopify.engineering/introducing-roast) | Shopify | Ruby | OSS | YAML+Markdown config, deterministic ↔ agentic node alternation |
| [LangGraph](https://blog.langchain.com/improving-deep-agents-with-harness-engineering/) | LangChain | Python/JS | OSS | Graph-based orchestration; +13.7 points on TerminalBench from harness-only improvements |
| [Goose](https://github.com/block/goose) | Block (Square) | Python | OSS | Foundation of Stripe's Minions; extensible MCP integration |
| [Claude Code](https://code.claude.com/docs/en/overview) | Anthropic | TypeScript | Product | CLI agent, Agent SDK for multi-agent composition, CLAUDE.md context |
| [Confucius SDK](https://engineering.fb.com) | Meta | Python | OSS | Meta-agent that builds other agents; 74.6% SWE-Bench-Verified |
| [Amazon Q / Kiro](https://aws.amazon.com/q/developer/) | AWS | Cloud | Product | Spec-driven development, persistent context, 10 parallel instances |

---

## Engineering Blogs

*First-party engineering posts describing production agent deployments.*

- [Harness Engineering: Leveraging Codex in an Agent-First World](https://openai.com/index/harness-engineering/) — OpenAI `[2026]` `[harness]`
- [Effective Harnesses for Long-Running Agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) — Anthropic `[2025]` `[architecture]`
- [Building a C Compiler with a Team of Parallel Claudes](https://www.anthropic.com/engineering/building-c-compiler) — Anthropic `[2026]` `[multi-agent]`
- [Minions: Stripe's One-Shot, End-to-End Coding Agents](https://www.engineering.fyi/article/minions-stripe-s-one-shot-end-to-end-coding-agents) — Stripe `[2026]` `[production]`
- [Introducing Roast: Structured AI Workflows](https://shopify.engineering/introducing-roast) — Shopify `[2025]` `[framework]`
- [uReview: Scalable, Trustworthy GenAI for Code Review at Uber](https://www.uber.com/blog/ureview/) — Uber `[2025]` `[code-review]`
- [REA: Autonomous AI Accelerating Meta's Ads Ranking](https://engineering.fb.com/2026/03/17/developer-tools/ranking-engineer-agent-rea-autonomous-ai-system-accelerating-meta-ads-ranking-innovation/) — Meta `[2026]` `[autonomous-agent]`
- [The Death of Traditional Testing: JiTTests](https://engineering.fb.com/2026/02/11/developer-tools/the-death-of-traditional-testing-agentic-development-jit-testing-revival/) — Meta `[2026]` `[testing]`
- [AI in Software Engineering at Google: Progress and the Path Ahead](https://research.google/blog/ai-in-software-engineering-at-google-progress-and-the-path-ahead/) — Google Research `[2025]`
- [AlphaEvolve: A Gemini-Powered Coding Agent](https://deepmind.google/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/) — DeepMind `[2025]`
- [AI Assistants Will Overwhelm Your Delivery Pipeline](https://aws.amazon.com/blogs/enterprise-strategy/your-ai-coding-assistants-will-overwhelm-your-delivery-pipeline-heres-how-to-prepare/) — AWS `[2025]` `[warning]`
- [How AI is Transforming Work at Anthropic](https://www.anthropic.com/research/how-ai-is-transforming-work-at-anthropic) — Anthropic Research `[2025]` `[internal-study]`

---

## Papers & Research

- [AlphaEvolve: A Coding Agent for Scientific and Algorithmic Discovery](https://arxiv.org/abs/2506.13131) — DeepMind `[2025]`
- [Mutation-Guided LLM-based Test Generation at Meta](https://arxiv.org/abs/2501.12862) — Meta `[2025]`
- [Large Sequence Models for Software Development Activities (DIDACT)](https://research.google/blog/large-sequence-models-for-software-development-activities/) — Google Research `[2023]`
- [CodeCompose: Large-Scale Industrial Deployment of AI-assisted Code Authoring](https://huggingface.co/papers/2305.12050) — Meta `[2023]`
- [From Naptime to Big Sleep: LLMs to Catch Vulnerabilities in Real-World Code](https://projectzero.google/2024/10/from-naptime-to-big-sleep.html) — Google Project Zero `[2024]`
- [State of AI vs Human Code Generation: AI Code Produces 1.7x More Issues](https://www.businesswire.com/news/home/20251217666881/en/CodeRabbits-State-of-AI-vs-Human-Code-Generation-Report-Finds-That-AI-Written-Code-Produces-1.7x-More-Issues-Than-Human-Code) — CodeRabbit `[2025]`

---

## Talks & Podcasts

- [Platform Engineering for AI: Scaling Agents and MCP at LinkedIn](https://www.infoq.com/podcasts/platform-engineering-scaling-agents/) — InfoQ `[2026]`
- [How Uber Uses AI for Development](https://newsletter.pragmaticengineer.com/p/how-uber-uses-ai-for-development) — Pragmatic Engineer `[2026]`
- [How Codex is Built](https://newsletter.pragmaticengineer.com/p/how-codex-is-built) — Pragmatic Engineer `[2026]`
- [How Claude Code is Built](https://newsletter.pragmaticengineer.com/p/how-claude-code-is-built) — Pragmatic Engineer `[2026]`
- [How AI is Changing SE at Shopify](https://newsletter.pragmaticengineer.com/p/how-ai-is-changing-software-engineering) — Pragmatic Engineer `[2025]`

---

## Tools & Repos

- [Roast](https://shopify.engineering/introducing-roast) — Shopify's open-source structured AI workflow framework (Ruby) `[OSS]`
- [AGENTS.md](https://agents.md/) — Community standard for agent context files `[Standard]`
- [Claude Agent SDK](https://www.anthropic.com/engineering/building-agents-with-the-claude-agent-sdk) — Build agents with multi-turn tool use (Python) `[SDK]`
- [LangGraph](https://blog.langchain.com/improving-deep-agents-with-harness-engineering/) — Graph-based agent orchestration with harness engineering `[Framework]`
- [Goose](https://github.com/block/goose) — Block's open-source coding agent (foundation of Stripe's Minions) `[OSS]`
- [Jules](https://blog.google/technology/google-labs/jules-now-available/) — Google's async AI coding agent running in Cloud VMs `[Product]`
- [Amazon Q Developer](https://aws.amazon.com/blogs/devops/accelerate-application-upgrades-with-amazon-q-developer-agent-for-code-transformation/) — Code transformation agents for large-scale migrations `[Product]`
- [Claude Code Docs](https://code.claude.com/docs/en/overview) — CLI agent documentation `[Docs]`

---

## Guides & Tutorials

- [Harness Engineering](https://martinfowler.com/articles/exploring-gen-ai/harness-engineering.html) — Martin Fowler's analysis `[2026]`
- [The Agent Harness is the Architecture](https://dev.to/epappas/the-agent-harness-is-the-architecture-and-your-model-is-not-the-bottleneck-3bjd) — DEV Community `[2026]`
- [Harness Engineering: The Complete Guide](https://www.nxcode.io/resources/news/harness-engineering-complete-guide-ai-agent-codex-2026) — NxCode `[2026]`
- [The Emerging "Harness Engineering" Playbook](https://www.ignorance.ai/p/the-emerging-harness-engineering) — Artificial Ignorance `[2026]`
- [Stripe's Coding Agents: The Walls Matter More Than the Model](https://www.anup.io/stripes-coding-agents-the-walls-matter-more-than-the-model/) — Anup Jadhav `[2026]`
- [Agentic Engineering Roadmap: Skills, Tools & Resources](https://towardsagenticai.com/agentic-engineering-roadmap-skills-tools-resources-2026/) — Towards Agentic AI `[2026]`

---

## Contributing

Contributions welcome! Please read the [contributing guidelines](CONTRIBUTING.md) first.

The bar for inclusion: published by an engineering org (not a vendor), describes a real production deployment or provides concrete architectural detail, and includes at least one metric or verifiable claim.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the contributors have waived all copyright and related or neighboring rights to this work.
