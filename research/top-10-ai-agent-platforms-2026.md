# Research: Top 10 AI Agent Platforms (as of 1 Sep 2026)

**Method:** Official product pages, docs, and pricing fetched 1 Sep 2026. Independent 2026 roundups used only as cross-checks. No invented products. Public list prices only where the vendor publishes them; otherwise "custom / contact sales."

**What "platform" means here:** something you can actually build, deploy, or govern agents on in production in 2026 — managed cloud, enterprise SaaS, or an OSS runtime with a commercial control plane. SDKs are included only when they are the vendor's current production path (OpenAI, Anthropic). This is **not** a quality scoreboard. Order is roughly "where production work is happening," hyperscalers and CRM/ITSM first, then OSS runtimes, then self-hosted conversational.

**Caveat:** vendor blogs score their own products. Treat those as marketing. This list prefers existence, public pricing, and documented production use over star counts.

---

## Executive take

The 2024 "autonomous agent" wave mostly died as products. What shipped in 2025-2026 is **orchestration + runtime + governance**: graph/state machines, identity, tool gateways, evals, and a control plane. AutoGen is in maintenance. OpenAI's Assistants API is sunset. Vertex AI's agent surface was absorbed into Gemini Enterprise Agent Platform. AutoGPT still has a GitHub repo; it is not how enterprises run agents.

If you pick one starting point:

| If you already run... | Start here |
| --- | --- |
| Microsoft 365 / Azure | Copilot Studio + Agent 365 |
| AWS | Bedrock AgentCore |
| Google Cloud | Gemini Enterprise Agent Platform |
| Salesforce CRM | Agentforce |
| ServiceNow ITSM / HR / CSM | ServiceNow AI Agents |
| Custom Python, multi-cloud | LangGraph + LangSmith |
| Fast role-based prototypes | CrewAI (OSS or AMP) |
| OpenAI-native apps | Agents SDK + Responses API |
| Coding / computer-use agents | Claude Agent SDK |
| Regulated, self-host / air-gap | Rasa |

Model cost is separate on almost every row. Platform fees are the smaller line until volume is high.

---

## Dead or replaced 2024 names (do not put these in a 2026 directory)

| 2024 name | Status on 1 Sep 2026 | Use instead |
| --- | --- | --- |
| **Microsoft AutoGen** | Maintenance mode. GitHub README: no new features; community-managed. Microsoft Agent Framework 1.0 GA 2 Apr 2026 is the successor (also absorbs Semantic Kernel). | [Microsoft Agent Framework](https://learn.microsoft.com/en-us/agent-framework/overview/) / Copilot Studio |
| **Semantic Kernel** (as the agent SDK) | Folded into Microsoft Agent Framework. | Same |
| **Power Virtual Agents** | Product renamed/absorbed into Copilot Studio. Microsoft FAQ confirms PVA is now part of Copilot Studio. | Copilot Studio |
| **OpenAI Assistants API** | Deprecated 26 Aug 2025; **sunset 26 Aug 2026**. `/v1/assistants`, `/v1/threads`, `/v1/runs` no longer serve traffic. | [Responses API](https://developers.openai.com/api/docs/assistants/migration) + [Agents SDK](https://openai.github.io/openai-agents-python/) |
| **OpenAI Swarm** | Experimental 2024 SDK; replaced by Agents SDK (Mar 2025). | Agents SDK |
| **Vertex AI Agent Builder** (as a standalone product name) | 22 Apr 2026: Vertex AI agent/build surfaces moved into **Gemini Enterprise Agent Platform**. Console no longer treats Vertex AI as the top-level agent product. | [Gemini Enterprise Agent Platform](https://cloud.google.com/blog/products/ai-machine-learning/introducing-gemini-enterprise-agent-platform) |
| **AutoGPT (2023 autonomous loop)** | Repo still active as "AutoGPT Platform" beta (v0.7.x, Aug 2026). The original "one agent that does everything from a prompt" is not a production platform. Independent 2026 write-ups treat it as a harder, thinner alternative to the list below. Not included. | LangGraph, CrewAI, or a cloud runtime |
| **BabyAGI / Adept ACT-1-era demos** | Research toys / company pivots. Not shippable platforms. | — |

---

## The 10 (verified live)

### 1. Microsoft Copilot Studio + Agent 365

- **URL:** https://www.microsoft.com/en-us/microsoft-365-copilot/microsoft-copilot-studio · Agent 365: https://www.microsoft.com/en-us/microsoft-agent-365
- **What it does:** Low-code / natural-language builder for conversational and autonomous agents, published into Microsoft 365 (Teams, SharePoint, Copilot Chat) or external channels. Agent 365 (GA 1 May 2026) is the IT/security control plane: discover, govern, and secure agents — including third-party ones — via Entra, Defender, Purview, and the M365 admin center. Code-first path is **Microsoft Agent Framework** (Python/.NET), not AutoGen.
- **Who it's for:** Microsoft 365 tenants that want agents inside existing identity, data (Graph, SharePoint, Dataverse), and IT process. Fortune-500-heavy. Pfizer, Dow, Amgen, Virgin Money cited on the product page.
- **Pricing (public):** Microsoft 365 Copilot **$30/user/month** (yearly), includes Copilot Chat + standard Copilot Studio harness for *internal* Copilot agents. Copilot Studio itself: prepaid **$200/pack/month for 25,000 Copilot Credits**, or pay-as-you-go meter (Azure subscription required). Agent 365 standalone **$15/user/month**; included in Microsoft 365 E7 (**$99/user/month** list). No consumption meter on Agent 365 yet (Microsoft licensing FAQ).
- **Why it matters:** Largest installed base of any agent *control plane*. If the buyer already pays for M365, this is usually the default — not because it is the best runtime, but because identity and admin already exist.
- **Sources:** Copilot Studio product + pricing FAQ; Microsoft Agent 365 product page; Microsoft Security Blog 1 May 2026; licensing FAQ.

### 2. Amazon Bedrock AgentCore

- **URL:** https://aws.amazon.com/bedrock/agentcore/ · Docs: https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/what-is-bedrock-agentcore.html · Pricing: https://aws.amazon.com/bedrock/agentcore/pricing/
- **What it does:** Modular agent *platform* on AWS: Runtime (serverless microVMs or managed EC2 instances), Harness (managed agent loop), Memory, Gateway (MCP tools), Identity, Browser, Code Interpreter, Observability (CloudWatch/OTEL), Evaluations, Optimization, Policy (Cedar), Registry, Payments. Framework-agnostic: LangGraph, CrewAI, LlamaIndex, Strands, OpenAI Agents SDK, Google ADK, Claude Agent SDK. GA of the platform since Oct 2025; Harness public preview/GA wave Apr-Jun 2026.
- **Who it's for:** AWS-native engineering teams that already built a prototype in an OSS framework and need session isolation, IAM-grade policy, and serverless scale without rewriting the agent loop. Cox Automotive, Druva, Thomson Reuters on the product page.
- **Pricing (public):** Consumption, no minimum. Runtime microVMs: **$0.0895 / vCPU-hour** and **$0.00945 / GB-hour**, billed per second on *active* CPU (I/O wait is free if nothing else is running). Memory 128 MB minimum. Gateway **$0.005 / 1,000 API invocations**. Web Search **$7 / 1,000 queries**. Short-term memory **$0.25 / 1,000 events**. Harness itself has no extra fee — you pay underlying resources. New AWS accounts: up to $200 Free Tier credits. Model tokens billed separately (Bedrock / OpenAI / Gemini).
- **Why it matters:** The "bring any framework, we run it" answer on AWS. Closest thing to an infrastructure-layer agent OS rather than a chatbot builder.
- **Sources:** AWS product page, AgentCore Developer Guide, AgentCore pricing page (fetched 1 Sep 2026).

### 3. Gemini Enterprise Agent Platform (Google Cloud)

- **URL:** https://cloud.google.com/blog/products/ai-machine-learning/introducing-gemini-enterprise-agent-platform (22 Apr 2026) · Docs: https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/overview · ADK: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/adk
- **What it does:** Google's end-to-end agent environment — the evolution of Vertex AI, not a new island. **Agent Studio** (low-code) + **Agent Development Kit (ADK)** (open-source, Python/TypeScript/Go/Java) + **Agent Runtime** (managed, long-running, sub-second cold start) + Memory Bank, Agent Sandbox, Agent Identity, Registry, Gateway, evaluation/observability. Model Garden: 200+ models including Gemini 3.1, Gemma 4, Claude. Employee delivery via the Gemini Enterprise app. Existing Vertex workloads keep running; *new* agent features ship only here.
- **Who it's for:** GCP shops and teams that want ADK locally then a governed runtime. Named customers on the launch post: Comcast (Xfinity Assistant), L'Oréal, PayPal, Color Health, Geotab, Burns & McDonnell.
- **Pricing (public):** ADK is Apache 2.0 / free to run yourself. Managed Runtime, Memory Bank, sandboxes, and model calls are **Google Cloud consumption** (Vertex/Gemini SKUs). Gemini Enterprise (workplace app + admin) is a **licensed** Google Cloud product; Google does not publish a simple public seat card on the Agent Platform launch post. Confirm with Cloud billing / sales. Do not treat "free ADK" as "free production."
- **Why it matters:** If you are already on GCP, this is the supported path. ADK is one of the few hyperscaler kits that is actually open-source and multi-language.
- **Sources:** Google Cloud Blog 22 Apr 2026; Agent Platform docs; ADK docs.

### 4. LangGraph + LangSmith (LangChain)

- **URL:** https://www.langchain.com/langgraph · Pricing: https://www.langchain.com/pricing
- **What it does:** LangGraph is an MIT-licensed graph/state runtime (checkpointing, human-in-the-loop interrupts, streaming, durable execution). LangSmith is the commercial platform: traces/evals, **Deployment** (formerly "LangGraph Platform"), sandboxes, LLM gateway, Engine (failure clustering / fix suggestions), Fleet (NL agent builder). Default production choice in most independent 2026 framework comparisons for *custom* multi-step agents. Vendor cites production use at companies such as Klarna, Uber, LinkedIn, Replit (treat as vendor-claimed; widely repeated in 2026 comparison posts).
- **Who it's for:** Python engineering teams that need explicit control flow, crash recovery, and model-agnostic orchestration. Not a business-user chatbot builder.
- **Pricing (public):** LangGraph OSS: **free (MIT)**. LangSmith Developer: **$0/seat**, 1 seat, 5k base traces/month then usage. Plus: **$39/seat/month**, 10k base traces, 1 free small serverless deployment. Enterprise: custom (self-host / hybrid, SSO, SLA). Usage meters: **LCU $1.50**, **LSU $1.00**. Deployment compute examples on the pricing page: runtime 0.045 LCU/vCPU-hr, memory 0.006 LCU/GiB-hr. LLM tokens extra unless you buy Fleet (Fleet includes model cost in LCUs).
- **Why it matters:** Closest thing to a vendor-neutral production standard for "agent as a state machine." If a 2024 tutorial still says "just use LangChain agents," that API is not the 2026 path — LangGraph is.
- **Sources:** langchain.com/langgraph; langchain.com/pricing (fetched 1 Sep 2026); LangChain "best AI agent frameworks 2026" resource page.

### 5. Salesforce Agentforce

- **URL:** https://www.salesforce.com/agentforce/ · Pricing: https://www.salesforce.com/agentforce/pricing/
- **What it does:** CRM-native autonomous agents (sales, service, marketing, field service, back-office "Operations" GA 29 Apr 2026). Low-code Agent Builder on existing Flows, Prompts, Apex, MuleSoft. Atlas reasoning engine. Voice, Slackbot, employee "coworker" agents. Data 360 (ex-Data Cloud) is the context layer. This is not a general-purpose multi-agent framework; it is Salesforce acting on Salesforce (and connected) data.
- **Who it's for:** Companies whose system of record is Salesforce and who want agents that update records, not just chat.
- **Pricing (public):** Foundations **$0** (builder, limited). Flex Credits **$500 / 100k credits**. Conversations **$2 / conversation** (customer-facing; cannot mix with Flex in the same org). Employee add-ons **$125/user/month** (unmetered employee usage) or Industries **$150/user/month**. Agentforce 1 Editions **from $550/user/month** (includes add-on + 2.5M Flex Credits/org/year). User license **$5/user/month** (requires Flex Credits). Help Agent resolutions **$2**. Unused Flex Credits do not roll over.
- **Why it matters:** If revenue ops live in Salesforce, buying a generic agent runtime and wiring CRM yourself is usually more expensive than Agentforce's credit bill.
- **Sources:** salesforce.com/agentforce and /pricing (fetched 1 Sep 2026); Salesforce Agentforce Operations announcement 29 Apr 2026.

### 6. ServiceNow AI Agents

- **URL:** https://www.servicenow.com/products/ai-agents.html · ITSM packaging: https://www.servicenow.com/products/itsm/pricing.html
- **What it does:** Agents embedded in the Now Platform (ITSM, CSM, HR, etc.): out-of-box specialists, natural-language **AI Agent Studio**, **AI Agent Fabric** (bring third-party agents), **AI Control Tower** (govern / kill-switch). Otto is the end-user router. 2026 packaging shift (9 Apr 2026): legacy five-tier SKUs replaced by AI-native **Foundation / Advanced / Prime**; AI is in the tier, usage is metered (assists). Prime is the tier for building/customizing autonomous agents.
- **Who it's for:** Enterprises that already run ServiceNow as the system of action for tickets, changes, HR cases. Not a greenfield agent framework.
- **Pricing (public):** No public dollar list for agents. Sold as platform tiers + assist consumption. Legacy SKUs end of sale **1 Jul 2026**. Get a quote. Third-party community posts describe assist pools and overage; treat those as unofficial.
- **Why it matters:** Highest-leverage place to put agents if the work is already a ServiceNow workflow. Control Tower is the governance story competitors sell as a separate product.
- **Sources:** ServiceNow AI Agents product page; ITSM pricing page; ServiceNow Community AI-native licensing 2026 (9 Apr 2026).

### 7. CrewAI (OSS + AMP)

- **URL:** https://www.crewai.com/ · Pricing: https://www.crewai.com/pricing
- **What it does:** Role/goal/task multi-agent framework (crews, flows). Fastest common path to a working multi-agent prototype in Python. **AMP** (Agent Management Platform) adds a visual studio, tracing, connectors, SSO/RBAC, cloud or VPC deploy. Vendor claims 65% of Fortune 500 and 450M+ workflow runs/month — **vendor marketing, not independently audited.** Independent 2026 comparisons still put CrewAI as the prototype default and LangGraph as the production-state default.
- **Who it's for:** Teams that think in job roles (researcher / writer / reviewer) and want something running this week. Enterprise if they outgrow 50 executions/month and need SSO.
- **Pricing (public):** OSS framework **free (MIT)**. AMP Basic **$0**, 50 workflow executions/month. Enterprise **custom** (SSO, RBAC, PII redaction, VPC/on-prem, 45-day onboarding, FDE). No public mid-tier or per-seat rate as of Aug/Sep 2026. LLM tokens extra.
- **Why it matters:** The role-based mental model is how non-ML teams describe work. That is why it shows up in every 2026 roundup even though the production ceiling is lower than LangGraph's graph runtime.
- **Sources:** crewai.com and /pricing (fetched 1 Sep 2026).

### 8. OpenAI Agents SDK

- **URL:** https://openai.github.io/openai-agents-python/
- **Also:** https://github.com/openai/openai-agents-python
- **Product note (15 Apr 2026):** https://openai.com/index/the-next-evolution-of-the-agents-sdk/
- **What it does:** Open-source Python (and JS/TS) SDK for multi-agent workflows: agents, runner loop, handoffs, guardrails, tracing, MCP, sessions. April 2026 update added native sandbox execution, Manifest workspaces (S3, GCS, Azure Blob, R2), and filesystem tools for long-horizon work. Provider-agnostic in principle (Responses API plus Chat Completions-compatible endpoints); strongest on OpenAI models. This is the supported replacement for the Assistants API, which shut down 26 Aug 2026.
- **Who it's for:** Product teams already on OpenAI, or anyone migrating off Assistants. Not a multi-cloud control plane.
- **Pricing (public):** SDK is free. Runtime billed at standard OpenAI API token and tool rates (Responses API). Sandbox compute billed by the sandbox provider you attach. No separate Agents SKU on the Apr 2026 post.
- **Why it matters:** After the Assistants sunset, this is OpenAI's agent platform for builders. Skipping it in a 2026 directory is how you ship a brief that is already wrong.
- **Sources:** OpenAI Agents SDK docs and GitHub; OpenAI "next evolution of the Agents SDK" (15 Apr 2026); Assistants migration guide sunset banner.

### 9. Anthropic Claude Agent SDK

- **URL:** https://code.claude.com/docs/en/agent-sdk/overview
- **What it does:** Official Python and TypeScript library that exposes the same agent loop used by Claude Code: planning, tools, MCP, subagents, hooks, and permissions. Previously called the Claude Code SDK. It is a coding and research harness, not a CRM or ITSM builder. Traffic can go through the Anthropic API, Amazon Bedrock, or Google Cloud.
- **Who it's for:** Engineering teams building repo, research, or long-horizon tool-using agents.
- **Pricing (public):** The library is free. Usage is billed at Anthropic API token rates, or at Bedrock/Vertex Claude rates if routed that way. Subscription-bundled Agent SDK credits also exist; third-party write-ups describe a 15 Jun 2026 split between interactive Claude Code quota and programmatic credits. Re-check Anthropic pricing before quoting a dollar figure.
- **Why it matters:** This is the production path for coding agents from Anthropic. Copilot Studio and Agentforce solve a different job.
- **Sources:** Claude Agent SDK overview (code.claude.com docs); Python SDK repo under anthropics on GitHub.

### 10. Rasa

- **URL:** https://rasa.com/ · Pricing: https://rasa.com/pricing
- **What it does:** Developer platform for conversational agents (chat + voice/IVR) with explicit business logic (CALM), on-prem / private cloud / air-gap, MCP tools, multi-agent handoff, OpenTelemetry. Forrester Wave conversational AI customer service Q2 2026: Strong Performer (vendor-cited). This is the self-host answer when data cannot leave the estate.
- **Who it's for:** Banks, health, government, telco with engineering teams. Named customers on site: N26, Providence, ERGO, Albert Heijn, Orange, nib.
- **Pricing (public):** **Free Developer Edition** — one bot per company, up to **1,000 external** or **100 internal** conversations/month, usable in production, community support. **Enterprise** — full Rasa Platform (Pro + optional Studio), custom quote. Official page does **not** list a dollar amount for paid tiers. Older Rasa forum post and 2026 third-party reviews still mention a Growth package around **$35k/year**; treat as unverified until sales confirms. LLM and infra extra.
- **Why it matters:** Only name on this list whose default is **you run it**. That is a real requirement in regulated deployments, not a preference.
- **Sources:** rasa.com and rasa.com/pricing (fetched 1 Sep 2026).

---

## Compact comparison

| # | Platform | Category | OSS core? | Public starting price | Default buyer |
| --- | --- | --- | --- | --- | --- |
| 1 | Copilot Studio + Agent 365 | Enterprise low-code + control plane | Partial (Agent Framework MIT) | Copilot $30/user/mo; Studio credits $200/25k; Agent 365 $15/user/mo | M365 IT |
| 2 | Bedrock AgentCore | Cloud agent runtime | Bring-your-own | $0.0895/vCPU-hr + $0.00945/GB-hr | AWS engineering |
| 3 | Gemini Enterprise Agent Platform | Cloud agent platform | ADK Apache 2.0 | ADK free; runtime/models metered; workplace license custom | GCP / Gemini Enterprise |
| 4 | LangGraph + LangSmith | OSS runtime + agent ops | Yes (MIT) | OSS $0; LangSmith Plus $39/seat/mo | Python platform teams |
| 5 | Salesforce Agentforce | CRM agents | No | Foundations $0; Flex $500/100k credits; $2/conversation | Salesforce shops |
| 6 | ServiceNow AI Agents | ITSM / workflow agents | No | Custom (Foundation/Advanced/Prime) | Now Platform customers |
| 7 | CrewAI | Role-based multi-agent | Yes (MIT) | OSS $0; AMP Basic $0 / 50 runs; Enterprise custom | Prototype + some F500 |
| 8 | OpenAI Agents SDK | Model-lab SDK | Yes | API tokens | OpenAI-native apps |
| 9 | Claude Agent SDK | Coding / research SDK | Client libs | API tokens | Eng / research agents |
| 10 | Rasa | Self-hosted conversational | Roots + commercial Pro | Free up to 1k conv/mo; Enterprise custom | Regulated CX / voice |

---

## Notes a buyer will regret skipping

1. **Stack first, framework second.** Copilot Studio on a non-M365 estate, or Agentforce without Salesforce, is usually a waste. The inverse is also true: LangGraph inside a shop that only wants a Teams bot is overkill.
2. **Assistants API code is dead.** Anything still calling the Assistants endpoints after 26 Aug 2026 is broken. Migrate to Responses + Agents SDK (OpenAI) or Foundry Agent Service (Azure).
3. **Do not start new work on AutoGen.** Microsoft said so.
4. **OSS is not free in production.** LangGraph, CrewAI, and ADK are free libraries. LangSmith, AMP, AgentCore Runtime, and model tokens are the bill.
5. **Governance is the 2026 product.** Agent 365, ServiceNow Control Tower, AgentCore Policy, and Google Agent Gateway/Identity exist because "we deployed 40 agents and lost track" is the actual incident.
6. **Voice is a different shortlist.** Rasa, Copilot Studio, Agentforce Voice, Cognigy/NICE, and Decagon are the CX/voice set. This brief is general agent platforms, not a contact-center bake-off. Cognigy and Decagon are real 2026 products; they were left off to keep the list to ten and avoid a CX-only skew.

---

## Sources (primary)

Fetched 1 Sep 2026. Prices and SKUs move; re-check vendor pages before a purchase memo.

- Microsoft Copilot Studio: https://www.microsoft.com/en-us/microsoft-365-copilot/microsoft-copilot-studio
- Microsoft Agent 365: https://www.microsoft.com/en-us/microsoft-agent-365
- Microsoft Agent 365 GA (1 May 2026): https://www.microsoft.com/en-us/security/blog/2026/05/01/microsoft-agent-365-now-generally-available-expands-capabilities-and-integrations/
- Microsoft Agent Framework: https://learn.microsoft.com/en-us/agent-framework/overview/
- AutoGen maintenance: https://github.com/microsoft/autogen
- AWS AgentCore: https://aws.amazon.com/bedrock/agentcore/
- AWS AgentCore docs: https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/what-is-bedrock-agentcore.html
- AWS AgentCore pricing: https://aws.amazon.com/bedrock/agentcore/pricing/
- Gemini Enterprise Agent Platform launch (22 Apr 2026): https://cloud.google.com/blog/products/ai-machine-learning/introducing-gemini-enterprise-agent-platform
- Agent Platform docs: https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/overview
- LangGraph: https://www.langchain.com/langgraph
- LangSmith pricing: https://www.langchain.com/pricing
- Salesforce Agentforce: https://www.salesforce.com/agentforce/
- Salesforce Agentforce pricing: https://www.salesforce.com/agentforce/pricing/
- ServiceNow AI Agents: https://www.servicenow.com/products/ai-agents.html
- CrewAI: https://www.crewai.com/ and https://www.crewai.com/pricing
- OpenAI Agents SDK: https://openai.github.io/openai-agents-python/
- OpenAI Agents SDK evolution (15 Apr 2026): https://openai.com/index/the-next-evolution-of-the-agents-sdk/
- Assistants API sunset: https://developers.openai.com/api/docs/assistants/migration
- Claude Agent SDK: https://code.claude.com/docs/en/agent-sdk/overview
- Rasa: https://rasa.com/ and https://rasa.com/pricing

---

## JSON (name, url, category)

```json
[
  {
    "name": "Microsoft Copilot Studio + Agent 365",
    "url": "https://www.microsoft.com/en-us/microsoft-365-copilot/microsoft-copilot-studio",
    "category": "enterprise-low-code"
  },
  {
    "name": "Amazon Bedrock AgentCore",
    "url": "https://aws.amazon.com/bedrock/agentcore/",
    "category": "cloud-runtime"
  },
  {
    "name": "Gemini Enterprise Agent Platform",
    "url": "https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/overview",
    "category": "cloud-platform"
  },
  {
    "name": "LangGraph / LangSmith",
    "url": "https://www.langchain.com/langgraph",
    "category": "oss-runtime"
  },
  {
    "name": "Salesforce Agentforce",
    "url": "https://www.salesforce.com/agentforce/",
    "category": "crm-agents"
  },
  {
    "name": "ServiceNow AI Agents",
    "url": "https://www.servicenow.com/products/ai-agents.html",
    "category": "itsm-workflow"
  },
  {
    "name": "CrewAI",
    "url": "https://www.crewai.com/",
    "category": "oss-multi-agent"
  },
  {
    "name": "OpenAI Agents SDK",
    "url": "https://openai.github.io/openai-agents-python/",
    "category": "model-lab-sdk"
  },
  {
    "name": "Anthropic Claude Agent SDK",
    "url": "https://code.claude.com/docs/en/agent-sdk/overview",
    "category": "coding-research"
  },
  {
    "name": "Rasa",
    "url": "https://rasa.com/",
    "category": "self-hosted-conversational"
  }
]
```

---

Optional Lightning tips: `rylyguy@strike.me` (Strike). Optional on-chain: `3M5R7D5UwtT6NuGUH6GVunZQZQ3p9DTePg`.
