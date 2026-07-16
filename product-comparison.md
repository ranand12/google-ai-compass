# Google AI Products — Feature Comparison

**Research date: July 15, 2026.** All facts below were verified against official Google sources (linked). Anything Google does not officially document is explicitly marked ⚠️ *unverified*. See `decision-matrix.md` for the when-to-use-which guide.

> **Naming:** this doc uses official names throughout. The item listed as "antigravity manager 2.0" in products.md is officially the **Agent Manager** — the standalone desktop orchestration app of the **Antigravity 2.0** platform (launched at Google I/O, May 19, 2026).

---

## 1. Product-at-a-glance

| Product | One-liner | Primary user | Cost model |
|---|---|---|---|
| **NotebookLM** | Source-grounded research assistant: answers only from *your* uploaded sources, with citations | Researchers, students, analysts, knowledge workers | Free tier; higher limits via Google AI Plus/Pro/Ultra subscriptions, Workspace, or NotebookLM Enterprise (GCP) |
| **AI Studio** | Free browser playground + API-key hub for the Gemini API, with prompt-to-app "Build mode" | Developers prototyping with Gemini | Free (Studio itself); Gemini API free tier + pay-as-you-go paid tier |
| **Antigravity 2.0 desktop app (Agent Manager)** | "Mission control" for spawning and supervising multiple async coding agents in parallel | Developers delegating task-level work to agents | Included with Google AI Pro ($20/mo); AI Ultra tiers for 5x/20x limits |
| **Antigravity CLI (`agy`)** | Terminal surface of Antigravity; successor to Gemini CLI (Go rewrite, launched I/O 2026) | Terminal-first devs, SSH/remote sessions | Free in public preview ⚠️ *pricing unverified* |
| **Antigravity IDE** | VS Code-style agentic editor: tab completion, inline commands, embedded agent panel, artifacts, browser sub-agent | Developers doing hands-on, interactive coding | Same Antigravity quota tiers as above |
| **Gemini Enterprise app (GCP)** | The end-user enterprise AI hub: permission-aware company-wide search, no-code agents, partner Agent Gallery; successor to Agentspace. (The developer-side "Agent Platform" is a separate product, out of scope here) | Whole organizations: knowledge workers + IT | Per-seat: Business $21, Standard $30, Plus $50/user/mo (annual); Frontline custom — confirm pricing with Google sales |
| **Gemini app in Workspace** | Gemini chat app + Gemini embedded in Gmail/Docs/Sheets/Slides/Meet/Chat, bundled into Workspace Business/Enterprise since Jan 2025 | Every Workspace knowledge worker | Included in Workspace Business/Enterprise editions (Starter gets limited features) |

---

## 2. What each product can do

### NotebookLM
- **Grounded Q&A with citations** — answers come only from sources you add; refuses when the answer isn't in them ([FAQ](https://support.google.com/notebooklm/answer/16269187)).
- **Sources:** PDF, docx, txt, md, csv, pptx, EPUB, audio, Google Docs/Sheets/Slides, websites (text only), public YouTube with captions. Cap: 500K words / 200 MB per source on **all** plans ([source types](https://support.google.com/notebooklm/answer/16215270)).
- **Studio outputs:** Audio Overviews, Video Overviews (Cinematic on paid tiers), Reports, Flashcards, Quizzes, Mind Maps, Data Tables, Infographics, Slide Decks, Deep Research ([upgrade page](https://support.google.com/notebooklm/answer/16213268)).
- **June 2026 agentic upgrade** ([blog](https://blog.google/innovation-and-ai/products/notebooklm/better-research-notebooklm/)): runs on Gemini 3.5 + Antigravity; per-notebook secure cloud computer that writes/executes code; can search the web and add sources itself; exports charts, docx/PDF/markdown, CSV/JSON/xlsx/pptx, images. Initially Ultra + Workspace business tiers.
- **Notebooks sync with the Gemini app** (July 14, 2026, [blog](https://blog.google/innovation-and-ai/products/gemini-app/notebooks-gemini-notebooklm/)).
- **Privacy:** consumer data not used to train models (unless feedback submitted); Workspace/Enterprise usage covered by Workspace/Cloud DPA terms, never human-reviewed ([privacy](https://support.google.com/notebooklm/answer/17004255)).
- **Limits by tier (per day unless noted):** Free 100 notebooks / 50 sources each / 50 chats / 3 audio-video overviews / Deep Research 10 per month → up to Ultra 30TB: 500 notebooks / 600 sources / 5K chats / 200 overviews / 200 Deep Research per day.

### Google AI Studio ([ai.google.dev/aistudio](https://ai.google.dev/aistudio))
- **Prompt playground:** try Gemini models, tune parameters/safety, tools (structured output, function calling, code execution, grounding), 1M-token context, "Get code" export.
- **Gemini API keys** self-serve — no GCP project setup.
- **Build mode ("vibe coding"):** prompt-to-app for web (full-stack Node.js runtime, secrets, npm) and native Android (Kotlin/Compose, in-browser emulator); deploy to Cloud Run; App Gallery ([docs](https://ai.google.dev/gemini-api/docs/aistudio-build-mode)).
- **Media generation via paid API tier:** Veo 3.1 video, Lyria 3 music, Nano Banana image models (Imagen 4 deprecated, shutdown Aug 2026) ([pricing](https://ai.google.dev/gemini-api/docs/pricing)).
- **No fine-tuning** — removed from the Gemini API since May 2025; supervised tuning only on the enterprise (Vertex-lineage) platform ([model tuning](https://ai.google.dev/gemini-api/docs/model-tuning)).
- **Critical caveat:** on the free tier Google **uses your prompts/outputs to improve products, including human review** (EEA/CH/UK excepted). Terms say don't submit sensitive/confidential data. Paid tier: no training use, DPA-covered ([terms](https://ai.google.dev/gemini-api/terms)).
- No IAM/service accounts/region control — that's what the enterprise platform (Vertex AI lineage) adds.

### Antigravity 2.0 desktop app — Agent Manager ([docs](https://antigravity.google/docs/agent-manager))
- Spawn, orchestrate, and observe **multiple agents working asynchronously** across Projects (repo/folder scopes with isolated settings).
- **Artifacts, not raw logs:** task lists, implementation plans, Walkthroughs (what changed + how to test), screenshots, browser recordings; comment on artifacts Google-Docs-style and agents incorporate feedback without stopping.
- **Browser use:** agents drive Chrome to test and verify end-to-end flows (requires Chrome).
- 2.0 additions: agent groups, dynamic subagents, parallel + **scheduled tasks**, voice commands, Local Mode vs New Worktree Mode, `/goal`, `/grill-me`, `/schedule`, unified permissions ([codelab](https://codelabs.developers.google.com/getting-started-google-antigravity), [TechCrunch](https://techcrunch.com/2026/05/19/google-launches-antigravity-2-0-with-an-updated-desktop-app-and-cli-tool-at-io-2026/)).
- **Models:** Gemini 3 Pro default; third-party model access announced but specifics not confirmed on official pages.
- **Pricing:** included with Google AI Pro $20/mo; AI Ultra $100/mo (5x) and $200/mo (20x); quotas based on agent "work done," refreshing ~every 5 hours.
- **Maturity caveats:** rocky 2.0 forced migration (config wipes reported), Interactions API still public beta, free-tier limits cut sharply in March 2026.

### Antigravity CLI (`agy`) ([docs](https://antigravity.google/docs/cli-overview), [GitHub](https://github.com/google-antigravity/antigravity-cli))
- Terminal (TUI) surface of Antigravity, launched **May 19, 2026** as the **official replacement for Gemini CLI** — Gemini CLI stopped serving free/AI Pro/Ultra individual users June 18, 2026 (Gemini Code Assist Standard/Enterprise orgs unaffected) ([transition blog](https://developers.googleblog.com/an-important-update-transitioning-gemini-cli-to-antigravity-cli/)).
- Go rewrite (fast startup, low memory); keyboard-first, built for SSH/remote; shares the same server-side agent harness as the desktop app.
- Multi-step reasoning, multi-file edits, tool calling, terminal execution, persistent history, **parallel background subagents**, slash commands, AGENTS.md project instructions, Agent Skills (Markdown files → slash commands), JSON lifecycle hooks; conversations exportable to the desktop app with bidirectional settings sync.
- Non-interactive mode `agy -p "…"` reported by tutorials ⚠️ *official CI/headless support unverified*.
- Free in public preview ⚠️ *unverified*; distributed as binaries, likely **not open source** (unlike Apache-2.0 gemini-cli); collects interaction data by default (opt-out in settings).

### Antigravity IDE ([launch post](https://developers.googleblog.com/build-with-google-antigravity-our-new-agentic-development-platform/), [codelab](https://codelabs.developers.google.com/getting-started-google-antigravity))
- VS Code-style agentic editor for **synchronous, hands-on** work: tab completions, inline commands, embedded Agent Panel, deep codebase understanding.
- Includes the Agent Manager, artifacts (rendered in an Auxiliary Pane), and a `/browser` Chrome-debugging sub-agent.
- Launched Nov 18, 2025 alongside Gemini 3 (macOS/Windows/Linux); built partly on Windsurf technology/team.
- Same model lineup and quota tiers as the desktop app.

### Gemini Enterprise app (GCP) ([Next 2026 blog](https://cloud.google.com/blog/products/ai-machine-learning/the-new-gemini-enterprise-one-platform-for-agent-development), [editions](https://docs.cloud.google.com/gemini/enterprise/docs/editions))
**Scope note:** this comparison covers the **Gemini Enterprise app** — the end-user hub. The developer-side **Gemini Enterprise Agent Platform** (ADK, Agent Studio, Model Armor; the evolution of Vertex AI) is a separate product and out of scope; it is mentioned below only to delineate the boundary.
- Launched Oct 9, 2025 as the successor to **Agentspace**; at Next 2026 Google split the brand into three pieces (only #2 is in scope here):
  1. **Gemini Enterprise Agent Platform** — the developer platform, officially the **evolution of Vertex AI**: ADK (incl. graph-based multi-agent framework), MCP + A2A protocols, low-code **Agent Studio**, Model Garden (200+ models), RAG Engine, Vector Search, Agent Runtime, Memory Bank, **Agent Identity / Agent Gateway / Model Armor** governance, Agent Simulation and Observability.
  2. **Gemini Enterprise app** (end-user hub): permission-aware search/grounding across company data, **Agent Designer** (no-code agent builder, preview), Inbox (agent monitoring), Projects (shared team memory), Canvas with Microsoft 365 export, Deep Research, **NotebookLM Enterprise**, image/video generation.
  3. **Agent Gallery / open ecosystem:** Google-validated partner agents (Oracle, Salesforce, ServiceNow, Adobe, Workday) with IT approval workflow.
- **Connectors (80+):** Workspace, BigQuery, Cloud Storage/SQL/Spanner/Firestore/AlloyDB; Microsoft 365 (SharePoint, OneDrive, Outlook, Entra ID), Salesforce, ServiceNow, Jira, Confluence, Box, Slack, SAP.
- **Editions:** Business $21 (1–500 users, 25 GiB/user), Standard $30 (full connectors, 30 GiB), Plus $50 (75 GiB) — annual, per user/mo; Frontline (consume-only, needs 150+ base seats) ⚠️ *Plus/flex figures partly third-party; official pricing page unavailable — verify with Google sales*. Custom ADK agents add usage-based Cloud consumption charges ⚠️ *third-party sourced*.

### Gemini app in Workspace ([pricing](https://workspace.google.com/pricing), [what's included](https://support.google.com/a/answer/15756885))
- **Bundled since Jan 2025** into Workspace Business/Enterprise (standalone Gemini add-ons discontinued; base prices rose ~15–20%). Education remains an add-on ("Google AI Pro for Education").
- **Gemini app:** Gemini 3 Pro chat (since Nov 2025), **Deep Research** (agentic web research, can also search your Gmail/Drive/Chat), **Gems** (custom assistants, also in Workspace side panels since July 2025), **Canvas** (interactive doc/code/app prototyping), connected Workspace apps as sources.
- **Embedded:** side panel in Gmail/Docs/Sheets/Slides/Drive/Chat; Help me write; Sheets analysis; Slides/Vids image + video creation; Meet "Take notes for me," real-time translated captions (~65+ languages); **enhanced NotebookLM included**; **Workspace Studio** automations; Gemini in AppSheet.
- **Editions:** Business Starter gets limited embedded Gemini (Gmail + Vids only) and basic app access; Standard/Plus/Enterprise get the full set; Enterprise adds DLP, AI Classification, data regions, per-feature admin controls.
- **Data protection:** customer data not used to train Gemini, not used for ads; respects existing access permissions; works with DLP/IRM/client-side encryption; ISO 42001, SOC 1/2/3, HIPAA-supportable, Cloud DPA ([solutions/ai](https://workspace.google.com/solutions/ai/)).
- Limitations: no admin off-switch for Deep Research/Gems in the app; conversation history required for Workspace-connected features; Deep Research report visuals gated to AI Ultra.

---

## 3. Cross-product feature matrix

| Capability | NotebookLM | AI Studio | Antigravity (Manager / IDE / CLI) | Gemini Enterprise | Gemini in Workspace |
|---|---|---|---|---|---|
| Grounded Q&A on your own documents | ✅ core (per-notebook sources) | ➖ (via API/RAG you build) | ➖ (codebase-grounded only) | ✅ company-wide, permission-aware | ✅ side panel + connected apps |
| Deep Research (agentic web research) | ✅ (tiered quotas) | ➖ | ➖ | ✅ | ✅ |
| Writes/edits code | ➖ (executes code internally for analysis, June 2026) | ✅ Build mode (generates apps) | ✅✅ core purpose | ➖ (not in the app — pro-code is the separate Agent Platform) | Canvas (light prototyping) |
| Multiple async/parallel agents | ➖ | ➖ | ✅ Manager + CLI subagents | ➖ (scheduled/trigger no-code agents only) | ➖ |
| Build custom AI agents | ➖ | Prototype only | For coding tasks | ✅ no-code (Agent Designer, preview) + Agent Gallery partner agents | Gems (simple), Workspace Studio |
| Enterprise connectors (M365, Salesforce…) | ➖ | ➖ | ➖ | ✅ 80+ | Workspace apps only |
| Gemini API access / keys | ➖ | ✅ core | ➖ (consumes models) | ➖ (not in the app — that is the separate Agent Platform) | ➖ |
| Audio/Video Overviews, podcasts | ✅ core | ➖ | ➖ | ✅ (via NotebookLM Enterprise) | ✅ (via bundled NotebookLM) |
| Media generation (image/video/music) | Images in outputs | ✅ Veo/Lyria/Nano Banana (paid API) | ➖ | ✅ image/video | ✅ Slides/Vids (+add-on for more) |
| Data NOT used for training | ✅ (consumer & enterprise) | ❌ free tier trains / ✅ paid | ⚠️ collects interaction data by default (opt-out) | ✅ Cloud DPA | ✅ Workspace terms |
| Governance (IAM, VPC-SC, DLP, audit) | Enterprise version only | ❌ | ❌ (enterprise via Gemini Enterprise Agent Platform) | ✅✅ core | ✅ (Enterprise editions) |
| Free tier | ✅ | ✅ | ✅ (shrinking) / CLI preview | ❌ (30-day Business trial) | ➖ (bundled with paid Workspace) |
| Connect to MCP servers/tools | ❌ (no API; third-party browser-automation bridges only) | ✅ SDK `tools=[mcp_session]` + Interactions API remote MCP | ✅✅ first-class: unified config, MCP Store, local + remote | ✅ Custom MCP Server connector, or governed via Agent Registry + Agent Gateway | ❌ consumer app (API Deep Research supports MCP, not exposed in-app) |
| Agent Skills (open SKILL.md format) | ➖ | ➖ | ✅ portable with Claude Code/Cursor skills | ➖ (ADK tools/connectors instead) | ➖ (Gems are prompt+files only) |

---

## 3.5 MCP connectors & skills compatibility (detail)

### Antigravity — the deepest MCP + skills integration
- **Unified MCP config across all three surfaces** (IDE, Agent Manager, CLI): central `~/.gemini/config/mcp_config.json`, per-surface dirs generated from it; per-project config in `<workspace>/.agents/mcp_config.json`. IDE UI: Settings → Customizations → "Open MCP Config", or agent panel → MCP Servers ([codelab](https://codelabs.developers.google.com/google-workspace-mcp-antigravity)). ⚠️ *Paths have shifted between releases — verify against live docs.*
- **Local (stdio) and remote (Streamable HTTP)** servers both supported; Google Workspace MCP servers (Docs, Sheets, Calendar) ship out of the box; an in-IDE **MCP Store** offers one-click installs.
- **Agent Skills use the open SKILL.md standard shared with Claude Code/Cursor** — skills written for other agents work unchanged. Global: `~/.gemini/config/skills/` (shared by all three surfaces); workspace: `.agents/skills/`. Skill frontmatter can gate MCP tools (`tools: mcp_<server>_*`) — skills teach the agent *how* to use MCP tools.
- **Plugins** (evolution of Gemini CLI extensions): bundles of `plugin.json` + optional `mcp_config.json`, `hooks.json`, `skills/`, `agents/`, `rules/`. Gemini CLI migration: skills carry over unchanged, MCP config moves to `mcp_config.json`, hooks keep the same format, extensions must be reinstalled as plugins.
- ⚠️ Practitioner-reported: MCP OAuth tokens are *not* centralized — re-authenticate per surface.

### Gemini API / AI Studio
- `google-genai` SDKs accept an **MCP client session directly in `tools=`** with automatic tool calling (Python; experimental) ([function calling docs](https://ai.google.dev/gemini-api/docs/function-calling)).
- **Interactions API** supports remote MCP servers natively (Streamable HTTP only; no-auth/bearer/OAuth; `allowed_tools` restriction), including for managed **Deep Research agents** ([blog](https://blog.google/innovation-and-ai/technology/developers-tools/expanding-managed-agents-gemini-api/)).
- AI Studio **Build mode has no in-studio MCP attachment** — MCP use is via the SDK code your app generates. ⚠️ *Treat as unsupported in the UI.*

### Gemini Enterprise app
- **Two connection paths in the app:** (a) Custom MCP Server connector — Streamable HTTP, public endpoint, tools disabled by default, requires an org-policy override and **bypasses Agent Gateway governance** ([docs](https://docs.cloud.google.com/gemini/enterprise/docs/connectors/custom-mcp-server/set-up-custom-mcp-server)); (b) the **governed path: Agent Registry + Agent Gateway (GA)** — a managed MCP gateway cataloging servers/agents with IAM and semantic egress policies. Prefer (b) for enterprise.
- (Developer-side MCP tooling — ADK McpToolset, MCP Toolbox for Databases, A2A — belongs to the separate Agent Platform, out of scope here.)
- **50+ Google-managed MCP servers** (Workspace Gmail/Drive/Calendar/Chat, etc.) GA/preview as of Next '26 — interoperable with Antigravity, Claude, ChatGPT, ADK ([blog](https://cloud.google.com/blog/products/ai-machine-learning/google-managed-mcp-servers-are-available-for-everyone)).
- No SKILL.md support — app extensibility is connectors and gallery agents.

### NotebookLM and Gemini app/Workspace — no MCP
- **NotebookLM:** no MCP, no plugins, no public API — the June 2026 agentic upgrade did not add any. Third-party browser-automation MCP bridges exist (e.g., notebooklm-mcp) but are unofficial.
- **Gemini app (consumer/Workspace):** no user-facing MCP and no announced ETA; Gems are prompt+file customization only. Extensibility = first-party Workspace connectors. Nuance: the *API's* Deep Research supports MCP, but that configuration is not exposed to app users.

---

## 3.6 Free vs GCP-linked: AI Studio and Antigravity tier ladders

### AI Studio / Gemini API — three levels

| | **Level 0: Free API key** | **Level 1: Paid API key (billing linked)** | **Level 2: Vertex / Gemini Enterprise Agent Platform** |
|---|---|---|---|
| Setup | API key from AI Studio; a GCP project backs it but **no billing account** | "Set up billing" in AI Studio links a **Cloud Billing account** to the key's project (~$10 prepay minimum for most new users) | Full GCP project: enable Vertex, `vertexai=True, project, location` in the same SDK |
| Auth | API key | API key | **IAM / service accounts** (no API keys) |
| Data terms | ⚠️ **Google trains on your prompts/outputs, incl. human review** (EEA/CH/UK excepted). Don't submit confidential data | Flips to Paid Services: **no training use, DPA-covered** | Google Cloud Terms / DPA |
| Rate limits | Free-tier caps | Automatic spend tiers: Tier 1 (billing linked, ~$250/mo cap) → Tier 2 ($100 spent + 3 days, $2K cap) → Tier 3 ($1K + 30 days, $20K–100K+, Postpay) | Provisioned Throughput available |
| Models/features | Flash-class + 2.5 Pro, embeddings, some Live API, Gemma. **No** Veo, Lyria, image-gen, Batch, most caching, Computer Use | Unlocks Veo, Lyria, image-gen, Batch API (−50%), context caching, Computer Use, Flex/Priority | Same models + **regions, VPC-SC, CMEK**, Provisioned Throughput |
| Gotcha | — | Prepay balance at $0 stops **all keys across all linked projects** | AI Studio-tuned models must be retrained |

Sources: [rate limits](https://ai.google.dev/gemini-api/docs/rate-limits), [billing](https://ai.google.dev/gemini-api/docs/billing), [terms](https://ai.google.dev/gemini-api/terms), [pricing](https://ai.google.dev/gemini-api/docs/pricing), [migrate](https://ai.google.dev/gemini-api/docs/migrate-to-cloud).

### Antigravity — three levels

| | **Level 1: Free Google account** | **Level 2: Google AI Pro / Ultra** | **Level 3: GCP project (Agent Platform)** |
|---|---|---|---|
| Setup | Google sign-in | Google AI Pro $20/mo; Ultra tiers available at higher price points | GCP project with billing; enable `aiplatform.googleapis.com`; users get `roles/aiplatform.user`; sign in via **Cloud OAuth** with project ID + region ([enterprise docs](https://antigravity.google/docs/enterprise)) |
| Surfaces | All three | All three | ⚠️ **Antigravity 2.0 desktop app + CLI only — the classic IDE is not supported for enterprise** |
| Quotas | Lowest; **weekly** refresh; metered by agent "work done" | Priority quotas, **5-hour** refresh; pooled Flash+Pro limit drawn down at API rates; AI credits = overage only | Billed to your GCP project; inference "runs within your secure cloud boundary" |
| Data terms | ⚠️ Interactions (incl. **source code and prompts**) used for training **unless you opt out in settings** | **Same individual terms as free** — a consumer subscription does NOT add enterprise data protection | **No training on your code/prompts** — carve-out applies automatically (GCP/Workspace access excluded from Interactions training); processing under Cloud DPA (Google as processor) |
| API keys? | ❌ Cannot plug an AI Studio/paid API key into Antigravity (auth is account/OAuth-based). Paid API keys keep **Gemini CLI** working instead | ❌ same | Auth is OAuth/ADC, not API keys |
| Indemnification | — | — | Check your Cloud gen-AI terms for indemnification coverage |

---

## 4. Items to verify with Google before customer commitments

1. Antigravity CLI pricing after public preview ends; official CI/headless support.
2. Gemini Enterprise Plus pricing and consumption-billing details for custom agents — confirm with Google sales.
3. Google AI subscription prices for NotebookLM tiers — not confirmed on a Google page.
4. Antigravity enterprise data handling beyond the training carve-out — verify the live terms at antigravity.google/docs/enterprise.
