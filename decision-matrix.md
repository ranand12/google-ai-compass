# Google AI Products — Decision Matrix (When to Use Which)

**Research date: July 15, 2026.** Companion to `product-comparison.md` (which has full citations and uncertainty flags).

---

## 1. Quick decision table

| If you want to… | Use | Why not the others |
|---|---|---|
| Understand, question, and synthesize a **specific set of documents** (papers, contracts, transcripts, specs) with cited answers | **NotebookLM** | Gemini app can read files but isn't strictly source-grounded; Gemini Enterprise is overkill unless it's org-wide data |
| Turn documents into **podcasts, videos, quizzes, flashcards, slide decks, infographics** | **NotebookLM** | Unique Studio outputs; nothing else generates Audio/Video Overviews |
| **Try Gemini models / prompts**, get an API key, prototype an AI feature or demo app fast | **AI Studio** | Free, zero setup; but free tier trains on your data — no confidential material |
| Ship a **production app on the Gemini API** with enterprise controls (IAM, regions, compliance) | **Vertex AI enterprise API** (a developer platform, separate from the Gemini Enterprise app) — prototype in AI Studio, then migrate (same SDK, client-init change) | AI Studio has no governance |
| **Code interactively** with AI assist in a full editor (completions, inline edits, agent panel) | **Antigravity IDE** | CLI has no editor UI; Manager is for supervising, not typing |
| **Delegate whole coding tasks** — run several agents in parallel, review plans/walkthroughs, schedule recurring jobs, browser-verified testing | **Antigravity 2.0 desktop app (Agent Manager)** | IDE is single-focus synchronous; supervision + artifacts are the Manager's core |
| Agentic coding **in the terminal / over SSH / scripted** | **Antigravity CLI (`agy`)** | Only terminal surface; note Gemini CLI is retired for individuals (June 18, 2026) |
| Give the **whole company** AI search over enterprise data (M365, Salesforce, ServiceNow…) + governed custom agents | **Gemini Enterprise** | Workspace Gemini only reaches Workspace data; NotebookLM is per-notebook, not org-wide |
| Everyday **knowledge-worker AI**: draft email/docs, analyze Sheets, Meet notes/translation, chat, Deep Research — inside tools people already use | **Gemini app in Workspace** | Already bundled in Business/Enterprise plans — no extra purchase; enterprise data protections included |
| **Deep research on the open web** with a cited report | **Gemini app (Deep Research)**; use **NotebookLM Deep Research** if results should land in a grounded notebook | |
| Build **no-code business agents/automations** | Simple/personal: **Gems + Workspace Studio**. Cross-system, governed, shareable: **Gemini Enterprise Agent Designer** | Antigravity agents are coding-specific |
| Connect an agent to **MCP tools while coding** (local + remote servers, one-click store) | **Antigravity** (IDE/Manager/CLI share one MCP config; MCP Store in the IDE) | NotebookLM and the Gemini app have no MCP at all |
| Call **MCP servers from your own app/agent code** | **Gemini API SDK** (`tools=[mcp_session]`) or Interactions API remote MCP | AI Studio Build mode has no in-UI MCP attachment |
| **Govern MCP access org-wide** (IAM, egress policies, catalog) | **Gemini Enterprise Agent Registry + Agent Gateway** | The direct Custom MCP Server connector bypasses Gateway governance — avoid for regulated data |
| Reuse **Claude Code / Cursor skills** (open SKILL.md format) | **Antigravity** — same standard, skills work unchanged (`~/.gemini/config/skills/` global, `.agents/skills/` per project) | No other Google product reads SKILL.md |

## 2. Decide by axis

**Who is the user?**
- Non-technical knowledge worker → Gemini in Workspace (default), NotebookLM (document-heavy work)
- Developer, individual → AI Studio (API/prototyping), Antigravity IDE/CLI/Manager (coding)
- Developer, enterprise/production → Vertex AI enterprise API (separate developer platform — not the Gemini Enterprise app)
- IT / entire org rollout → Gemini Enterprise (+ Workspace Gemini already bundled)

**How sensitive is the data?**
- Confidential/regulated → never AI Studio free tier (Google trains on it). Use Workspace Gemini, NotebookLM (Workspace/Enterprise), Gemini Enterprise, or paid API — all DPA-covered, no training use.
- Antigravity collects interaction data by default — opt out in settings before using on proprietary code; enterprises should go through the Gemini Enterprise Agent Platform.

**Grounding scope?**
- A curated set of sources → NotebookLM
- Your mailbox/Drive/company Workspace data → Gemini in Workspace
- All enterprise systems incl. non-Google (SharePoint, Salesforce, SAP…) → Gemini Enterprise
- A codebase → Antigravity
- Whatever you wire up yourself → AI Studio / Gemini API

**What can you spend?**
- **$0 — free tools only** → NotebookLM free tier, AI Studio, Antigravity free tier (limited quotas), CLI public preview
- **$0 extra — already paying for Workspace Business/Enterprise** → the Gemini app + embedded features are included in your plan; start there
- **~$20/mo per developer** → Google AI Pro covers all three Antigravity surfaces
- **$21–50/mo per employee, org-wide** → Gemini Enterprise (Business $21 / Standard $30 / Plus $50)

## 3. Common scenarios

1. **"Summarize these 40 PDFs and make a briefing podcast for the team"** → NotebookLM.
2. **"Hackathon demo of an AI feature by Friday"** → AI Studio Build mode; deploy to Cloud Run.
3. **"That demo is now a product"** → link billing (data terms flip to DPA), then migrate to the Vertex AI enterprise API if IAM/regions are needed. (Developer-platform path — separate from the Gemini Enterprise app.)
4. **"Fix this bug while I keep working on the feature"** → Antigravity Agent Manager: agent on the bug in a worktree, you in the IDE.
5. **"Nightly dependency-update agent on a remote box"** → Antigravity CLI (scheduled/`agy -p` — verify headless support officially before relying on it in CI).
6. **"Employees keep pasting contracts into ChatGPT"** → roll out Gemini in Workspace (bundled, governed) and NotebookLM for document work; Gemini Enterprise if they also need M365/Salesforce/ServiceNow search.
7. **"HR wants an onboarding-answers agent over policies in SharePoint"** → Gemini Enterprise (connector + Agent Designer, no code).
8. **"Meeting notes + live translation for a global team"** → Gemini in Workspace (Meet).
9. **"Competitive analysis report by tomorrow"** → Gemini app Deep Research; move findings into NotebookLM if it becomes an ongoing research base.

## 3.5 MCP quick guide

- **Coding with MCP tools** → Antigravity: one config file (`~/.gemini/config/mcp_config.json`) serves the IDE, Agent Manager, and CLI; per-project overrides in `.agents/mcp_config.json`; Workspace MCP servers (Docs/Sheets/Calendar) built in; MCP Store for one-click installs. Caveat: OAuth re-auth per surface (practitioner-reported).
- **Your app needs MCP** → Gemini API: pass an MCP client session in `tools=` (SDK, experimental) or use the Interactions API's native remote-MCP support (Streamable HTTP; also powers Deep Research agents).
- **Enterprise MCP** → Gemini Enterprise app: register MCP servers in Agent Registry behind Agent Gateway (IAM + egress policies) for governed end-user access. Don't use the ungoverned Custom MCP Server connector for sensitive data.
- **Google-managed MCP servers** (50+, Next '26): Gmail, Drive, Calendar, Chat, etc. — usable from Antigravity and even non-Google agents (Claude, ChatGPT).
- **No MCP anywhere**: NotebookLM (no API at all — only unofficial browser-automation bridges) and the consumer/Workspace Gemini app (Gems can't attach tools).
- **Skills portability**: Antigravity reads the open SKILL.md format — your existing Claude Code/Cursor skill library carries over unchanged, and skills can gate MCP tools (`tools: mcp_<server>_*`).

## 3.6 Free vs GCP-linked (AI Studio & Antigravity)

**AI Studio / Gemini API:** stay on the free key only for throwaway experiments (Google trains on prompts, with human review). The moment data matters or you need Veo/Batch/caching, link a Cloud Billing account — data terms flip to DPA and spend-based tiers raise limits automatically. Go full Vertex/Agent Platform (IAM, regions, VPC-SC) only when enterprise controls are actually required; it's the same SDK, a client-init change.

**Antigravity:** free accounts get weekly-refresh quotas and — critically — **Google trains on your interactions including source code unless you opt out**; a Pro/Ultra subscription raises quotas (5-hour refresh) but does **not** change those data terms. For company code, use the GCP-project route (Cloud OAuth, `roles/aiplatform.user`, billed to the project, training carve-out automatic) — noting it supports only the desktop app and CLI, not the classic IDE, and API-key auth doesn't exist on any tier. Nuance for customer conversations: the GCP route means **no training on your code/prompts and Cloud-DPA processing**, but "no training" ≠ "no collection" — abuse-logging retention and telemetry specifics aren't documented on fetchable pages, so confirm against the live Antigravity enterprise terms before committing in writing.

## 4. Overlaps worth knowing

- **NotebookLM appears in three places:** standalone (consumer/Google AI subs), bundled enhanced in Workspace, and NotebookLM Enterprise inside Gemini Enterprise. Same product, different governance and limits — pick by where your data must live.
- **Deep Research exists in the Gemini app, NotebookLM, and Gemini Enterprise.** Choose by context: personal → app; source-grounded project → NotebookLM; enterprise-data-aware → Gemini Enterprise.
- **Three ways to "build an agent":** Gems (personal, minutes), Agent Designer/Studio (business, no/low-code, governed), ADK on the Agent Platform (pro-code, production). Escalate only as requirements demand.
- **AI Studio vs Antigravity:** AI Studio *builds apps that call Gemini*; Antigravity *is an agent that builds your software*. Different jobs despite both being "AI + code."
- **One migration path to remember:** AI Studio → Vertex AI enterprise API uses the same google-genai SDK; switching is mostly a client-initialization change. (That is a developer-platform path; the Gemini Enterprise *app* is the end-user hub and not part of it.)
