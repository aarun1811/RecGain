# Agentic AI: Transforming GRU for the Next Decade

## A Vision for AI-Powered Global Reconciliation

**Citi | Global Reconciliation Utility | 2026**

---

## 1. Executive Summary

The Global Reconciliation Utility (GRU) is the backbone of Citi's operational integrity — managing approximately 4,000 reconciliation processes across every asset class, every region, and every business line. Today, this operation relies on 500+ team members working across a fragmented landscape of internal and third-party tools, with processes that are largely manual, knowledge-dependent, and time-intensive.

This proposal presents a vision for an **Agentic AI Platform** — a unified, intelligent layer that sits across the entire GRU ecosystem. Rather than replacing existing tools, it connects them through standardized protocols (MCP and A2A), deploys specialized AI agents for each domain, and delivers a single conversational interface with Generative UI capabilities to every team member.

The result: reconciliation builds that take hours instead of weeks, breaks that are pre-classified before a human sees them, production failures that auto-remediate, and institutional knowledge that never walks out the door.

This is not incremental automation. This is a fundamental rethinking of how reconciliation operations work — designed to position Citi as the industry leader in AI-driven operations for the next 5-10 years.

---

## 2. The Challenge: Why Now

### 2.1 Scale and Complexity

GRU manages ~4,000 reconciliation processes globally, spanning trade reconciliation, cash and nostro reconciliation, position reconciliation, intercompany reconciliation, GL and ledger reconciliation, fees and commission reconciliation, collateral and margin reconciliation, client money segregation, and tax reconciliation. Each type carries its own rules, data sources, and regulatory requirements.

### 2.2 The Human Cost

The current operation is labor-intensive:

- **Build Team (~250 people):** Manually configuring recon processes from BRDs — analyzing source files, mapping columns, setting up matching rules, enrichments, and scheduling. Each new recon takes 2-12 weeks.
- **Ops / Break Management (150+ people):** Investigating breaks by manually switching between multiple tools, following category-specific playbooks, and cross-referencing data across systems.
- **Production Support (40-100+ people):** Triaging and resolving production incidents — job failures, data issues, infrastructure problems — with 40-70% being repetitive patterns.
- **Business Analysts (40+ people):** Gathering requirements through meetings, writing BRDs through iterative review cycles, and handing off to the Build Team.
- **Supporting functions (ETL, RCM, Infra, Reporting, Regulatory):** Additional teams maintaining the technical and compliance infrastructure.

### 2.3 The Fragmented Tool Landscape

Teams operate across a fragmented ecosystem:

- **Core Platforms:** OneRec (internal, with 5 modules), SmartStream TLM (external, being phased out)
- **Lifecycle Tracing:** RecTrace (internal, to be onboarded to OneRec)
- **Visualization:** RecViz (internal, future replacement for Tableau/QlikView)
- **Data Engineering:** Talend (ETL), Vanguard (future consolidated data source)
- **Service Management:** ServiceNow, Jira
- **Data Sources:** SFTP, Kafka, API feeds, manual uploads

Each tool serves a purpose, but they don't talk to each other intelligently. An ops analyst investigating a single break might need to open 5 different systems to get the full picture.

### 2.4 The Knowledge Risk

Critical institutional knowledge — how specific recons are built, why certain matching rules exist, how to resolve specific break patterns — lives primarily in people's heads and scattered email threads. Some failure-related information exists in ServiceNow incidents and Jira tickets. Recon configurations exist in the OneRec database. But there is no unified, searchable, learnable knowledge layer. When experienced team members leave, their knowledge leaves with them.

### 2.5 The Opportunity

The AI landscape has matured to a point where this transformation is not just possible — it's practical. Foundation models (Claude, Gemini) are capable of understanding complex domain logic. Standardized protocols (MCP, A2A) enable AI agents to interact with any tool. Citi's R2D2 gateway provides the security infrastructure to deploy AI safely within the bank's perimeter.

The question is not whether AI will transform reconciliation operations. The question is whether Citi will lead that transformation or follow.

---

## 3. GRU Today: The Current State

### 3.1 Organizational Structure

| Team | Headcount | Primary Function |
|------|-----------|-----------------|
| Build Team | ~250 | Configure and deploy new reconciliation processes |
| Ops / Break Management | 150+ | Investigate and resolve reconciliation breaks |
| Production Support | 40-100+ | Monitor, triage, and resolve production incidents |
| Business Analysts | 40+ | Gather requirements, write BRDs, sign off on recons |
| ETL Team | TBD | Heavy-duty data transformations in Talend |
| RCM (App Development) | TBD | Build and maintain OneRec platform and tools |
| Infrastructure | TBD | Server, database, and environment management |
| Reporting & Analytics | TBD | Dashboard design and management |
| Regulatory & Compliance | TBD | Audit evidence, control monitoring, regulatory readiness |
| PMO | 1 | Program management |
| Operations Managers | TBD | People management, capacity planning |

### 3.2 OneRec: The Central Platform

OneRec is GRU's primary internal reconciliation platform, developed and maintained by the RCM team. It consists of five modules:

1. **ETL Layer Builder** — Allows the Build Team to configure lightweight data transformations directly, without needing the ETL team. Used for recon enrichments when a full Talend job isn't required.
2. **Recon Builder (including Scheduling)** — The core module where reconciliation processes are configured: matching rules, tolerances, key fields, break categorizations, and job scheduling.
3. **Report Scheduler** — Configures and schedules the generation and distribution of reconciliation reports.
4. **Health Monitor** — Monitors the operational health of recon jobs — status, failures, performance metrics.
5. **Source Maintenance** — Manages source file configurations, connection details, and format specifications.

**Key technical detail:** The Build Team works through OneRec's web UI to configure recons, but the end product is **JSON configuration files on the server plus SQL commands** that run against the database. The JSON configs are mostly standardized across recon types with some type-specific variations. This is critical for the AI vision — it means an AI agent can generate these JSON configs and SQL commands directly, bypassing the manual UI workflow entirely.

**Existing config library:** There are ~4,000 existing recon configurations in the database. These serve as an invaluable training/reference dataset for the AI.

**Deployment:** Completed configurations go through a validation step and, post-approval, a CI/CD pipeline promotes them to production.

### 3.3 Supporting Tools

- **SmartStream TLM** — External reconciliation engine, currently used alongside OneRec. Eventually, everything will be migrated to OneRec.
- **RecTrace** — Internal tool for tracing the lifecycle of trades/files through the GRU system. Planned to be onboarded into OneRec.
- **RecViz** — Internal visualization tool being developed to replace Tableau/QlikView for reconciliation analytics.
- **Talend** — Enterprise ETL tool used by the dedicated ETL team for complex data transformations.
- **Vanguard** — Future consolidated data source platform. Currently, source data arrives via SFTP, API, Kafka, and manual uploads. Vanguard is expected to consolidate these in 2-3 years.
- **ServiceNow** — Incident management and IT service management.
- **Jira** — Project tracking and work management.

### 3.4 Regional Architecture

GRU operates globally. The same tools are deployed across regions, but **each region's data sits in separate data centers**. This means the AI platform must be region-aware — routing requests and data operations to the correct data center based on context.

### 3.5 Current Workflow: Building a New Recon

1. Business stakeholder identifies a reconciliation need.
2. BA conducts meetings with the business to understand requirements.
3. BA writes a Business Requirements Document (BRD) — iterates through review cycles.
4. BRD is handed to the Build Team.
5. Build analyst examines source files, manually maps columns to OneRec's schema.
6. If heavy ETL is needed, a Jira is raised for the ETL team (adds wait time).
7. Build analyst configures matching rules, tolerances, enrichments, scheduling in OneRec.
8. Recon is tested — run in lower environments, output reviewed.
9. Iterations happen — rule tuning, mapping adjustments, BA feedback.
10. BA signs off on the configuration.
11. Configuration is promoted through CI/CD pipeline to production.

**Timeline: 2-12 weeks.** Build team members have a mix of specializations (some focus on certain recon types) but can cross over.

### 3.6 Current Workflow: Break Investigation

1. Recon runs and produces breaks (unmatched items).
2. Ops analyst picks up the break from the queue.
3. Analyst opens OneRec to view break details.
4. Analyst opens RecTrace to trace the transaction lifecycle.
5. Analyst cross-references with source systems.
6. Analyst follows category-specific playbooks — different break types have different investigation procedures.
7. Analyst determines root cause: timing difference, missing trade, format mismatch, genuine discrepancy, etc.
8. Analyst takes action: contact counterparty, raise adjustment, rebook, or escalate.
9. Resolution is documented.

**Pain points:** Too many tools to check, overwhelming volume, lack of unified context. 150+ people doing this across regions.

### 3.7 Current Workflow: Production Support

1. Recon job fails or an alert fires from Health Monitor.
2. PS analyst picks up the incident.
3. Analyst checks Health Monitor, application logs, runs DB queries, checks ServiceNow for similar past incidents, sometimes checks source system status.
4. Analyst diagnoses root cause: job failure, data issue (missing/late/malformed files), infrastructure issue (DB connection, disk space, memory).
5. Analyst follows a runbook if one exists, or investigates from scratch.
6. Fix is applied or issue is escalated.
7. ServiceNow incident is created/updated.

**Key insight:** 40-70% of incidents are variations of known patterns. The same types of failures recur regularly.

### 3.8 AI and Automation Baseline

**There is currently no AI or automation in place.** No auto-matching intelligence, no auto-categorization of breaks, no predictive capabilities. This is a greenfield opportunity — the entire AI journey starts from zero, which means the phased roadmap must account for foundational infrastructure before advanced capabilities.

---

## 4. The Vision: An Agentic AI Platform for GRU

### 4.1 Core Concept

A unified Agentic AI platform that:

- **Understands reconciliation** — not a generic chatbot, but specialized AI agents with deep domain knowledge of recon operations.
- **Speaks to every tool** — through standardized MCP (Model Context Protocol) adapters, the AI can read from and write to every system in the GRU ecosystem.
- **Amplifies every team member** — a single conversational interface with Generative UI that adapts dynamically to the user's role and current task.
- **Learns continuously** — every interaction, every resolved break, every configured recon feeds back into the knowledge layer, making the system smarter over time.

### 4.2 Design Principles

1. **Augment, Don't Replace Tools** — OneRec, RecTrace, Vanguard, and other investments are preserved. The AI layer sits on top, connecting them through MCP adapters. No rip-and-replace.
2. **Human-in-the-Loop** — AI proposes, humans approve. Critical actions (recon deployment, break resolution, system changes) always have a human approval gate.
3. **Secure by Design** — All LLM traffic routes through Citi's R2D2 gateway. Sensitive data never leaves the bank's perimeter.
4. **Region-Aware** — The platform understands which data center to target based on the region and recon context.
5. **Decoupled Architecture** — Each tool integration is an independent MCP adapter. If Vanguard isn't ready, individual source adapters fill the gap. If a tool gets replaced, only its adapter changes.

---

## 5. Platform Architecture

### 5.1 Six-Layer Architecture

The platform is organized into six layers, each with a distinct responsibility:

#### Layer 1: Generative UI (The Interface Layer)

A single conversational interface that serves every persona in GRU:

- **Role-Aware Views** — An ops analyst sees break investigation tools. A build team member sees config generation views. A manager sees dashboards and KPIs.
- **Natural Language Input** — Users describe what they need in plain English. No need to navigate complex tool UIs.
- **Dynamic Visualizations** — The UI doesn't render pre-built screens. It dynamically generates the right visualization based on context: a lifecycle trace for a break investigation, a column mapping canvas for a new recon build, a dependency graph for a production failure.

Built as a web application, integrated within Citi's internal portal ecosystem.

#### Layer 2: AI Orchestration (The Brain)

The central intelligence that receives user intent and orchestrates the response:

- **Intent Understanding** — Determines what the user is trying to accomplish.
- **Task Decomposition** — Breaks complex requests into subtasks and delegates to the appropriate specialized agents.
- **Multi-Step Workflow Management** — Manages workflows that span multiple agents and tools, maintaining context across steps.
- **A2A Coordination** — Uses the Agent-to-Agent protocol to enable specialized agents to collaborate on complex tasks.

All LLM inference is routed through Citi's R2D2 gateway.

#### Layer 3: Specialized AI Agents (The Workers)

Six domain-specific agents, each with tailored system prompts, tool access, and knowledge:

1. **Build Agent** — Generates reconciliation configurations (JSON + SQL) from natural language requirements. References the library of 4,000+ existing configs to find similar patterns. Understands OneRec's configuration schema.

2. **Data Agent** — Understands source file structures and schemas. Profiles data quality. Suggests column mappings. Interfaces with Vanguard (when available) or direct source systems. Generates ETL Layer Builder configurations for lightweight transformations.

3. **PS/Reliability Agent** — Monitors Health Monitor alerts, reads application logs, correlates with recent changes and upstream system status, searches ServiceNow for similar past incidents. Auto-remediates known failure patterns. Provides full diagnosis context for novel issues.

4. **Break/Ops Agent** — Automatically runs category-specific investigation playbooks. Traces transaction lifecycles through RecTrace. Cross-references source data. Pre-classifies breaks (timing, missing trade, genuine discrepancy). Recommends resolution actions.

5. **Compliance Agent** — Continuously monitors reconciliation completeness and control effectiveness. Generates audit evidence packages on demand. Proactively flags control gaps. Maintains regulatory-ready audit trails.

6. **Analytics Agent** — Powers natural language querying across all recon data. Generates dynamic visualizations through RecViz. Answers ad-hoc analytical questions instantly without requiring dashboard development.

#### Layer 4: MCP Integration Layer (The Hands)

Standardized MCP (Model Context Protocol) adapters for every tool in the ecosystem:

- **OneRec Adapters** — Separate adapters for each module: Recon Builder, ETL Layer Builder, Report Scheduler, Health Monitor, Source Maintenance. These may need to be built or adapted from existing APIs (new APIs may be required where existing ones are insufficient).
- **RecTrace Adapter** — Transaction lifecycle tracing.
- **RecViz Adapter** — Visualization and analytics rendering.
- **SmartStream TLM Adapter** — Legacy recon engine interaction (until full migration to OneRec).
- **ServiceNow Adapter** — Incident management, knowledge base access.
- **Jira Adapter** — Work item management, project tracking.
- **Talend Adapter** — ETL job management and monitoring.
- **Vanguard Adapter** — Consolidated data source access (when available).
- **Source System Adapters** — SFTP, Kafka, API endpoints for direct source access.
- **Database Adapters** — Direct access to OneRec configuration DB and operational databases.

**Key architectural principle:** Each adapter is independent. If Vanguard isn't delivered on time, individual source system adapters fill the gap. If OneRec's existing APIs are insufficient, new ones are built. The agent layer doesn't care — it just talks to whatever adapter is available through the standardized MCP protocol.

**Region-aware routing:** All adapters are region-aware, pointing to the correct data center based on the reconciliation's regional context.

#### Layer 5: Knowledge Layer (The Memory)

The institutional memory that makes the AI genuinely intelligent about GRU's specific operations:

- **Config Pattern Library (4,000+ configs)** — Existing reconciliation configurations mined from OneRec's database. The AI uses these to find similar patterns when generating new configs. "This looks like a nostro recon against Deutsche Bank — here are 15 similar configs."
- **Incident Knowledge Base** — Historical ServiceNow incidents and Jira tickets, enabling the PS Agent to recognize and resolve recurring failure patterns.
- **Playbook Repository** — Break investigation playbooks and operational procedures, enabling the Break Agent to automate investigation steps.
- **Interaction History** — Captured passively as teams use the platform. Every investigation, every build decision, every resolution becomes a learning data point. This is the most powerful long-term asset — institutional knowledge captured simply by people doing their work through the AI interface.
- **Vector Database** — Semantic search across all knowledge sources, enabling the AI to find relevant context even when the query doesn't match exact keywords.

**Two-phase knowledge strategy:**

- **Phase 1 (Passive Capture):** As people use the new interface, every interaction becomes training data. No extra work required.
- **Phase 2 (Active Ingestion):** Mine existing ServiceNow incidents, Jira tickets, OneRec configs, and any documented runbooks. Build the foundation before people start using the system.

(Note: In practice, active ingestion happens first during Phase 0 to bootstrap the knowledge layer.)

#### Layer 6: Governance and Security (The Guardrails)

- **R2D2 Gateway** — All LLM traffic (inference requests, responses) routes through Citi's R2D2 gateway. Sensitive data is filtered and never leaves Citi's perimeter. R2D2 supports multiple foundation models with higher preference for Gemini and Claude.
- **Human-in-the-Loop Approval Workflows** — Configurable approval gates for different action types. Recon deployment requires explicit approval. Break resolution recommendations require analyst confirmation. Known-pattern PS remediations can be automated with logging.
- **Role-Based Access Control (RBAC)** — Users see and can act on only what their role permits. An ops analyst can't deploy recon configs. A build team member can't approve their own config.
- **Full Audit Trail** — Every AI action, every recommendation, every human decision is logged. Complete traceability for regulatory and audit purposes.
- **Region-Aware Routing** — Ensures data operations target the correct regional data center, maintaining data residency compliance.

### 5.2 Protocol Design: MCP and A2A

**MCP (Model Context Protocol)** is used for tool-level interactions. It provides a standardized way for AI agents to:

- Read data from tools (fetch a recon config, read Health Monitor status, get break details)
- Write/execute actions in tools (deploy a config, restart a job, create a ServiceNow ticket)
- Discover tool capabilities (what operations are available, what parameters are required)

**A2A (Agent-to-Agent)** is used when multiple specialized agents need to collaborate. For example:

- The Build Agent needs source file schema information → it requests this from the Data Agent via A2A
- The PS Agent identifies a data quality issue → it notifies the Break Agent via A2A so break classifications account for the upstream problem
- The Compliance Agent identifies a recon that hasn't run → it queries the PS Agent via A2A to check for known production issues

This separation ensures that tool interactions are standardized (MCP) while agent collaboration is flexible and intelligent (A2A).

---

## 6. Transformation: Before and After

### 6.1 Build Team Transformation

**BEFORE (Today):**
Business need → BA meetings (days) → BRD written (days) → Build Team receives → Analyze source files (manual) → Map columns (manual) → Configure matching rules → Configure enrichments → ETL team request (wait) → Testing and iteration → BA sign-off → CI/CD deploy.

**Timeline: 2-12 weeks. Headcount: ~250 people.**

**AFTER (AI-Powered):**
BA or business user describes the requirement conversationally in the Generative UI → Build Agent automatically pulls source file schemas (from Vanguard or direct source, via Data Agent) → references the library of 4,000+ existing configs to find similar patterns → generates complete JSON config + SQL commands → presents it in the UI as a visual diff showing proposed matching rules, mappings, and tolerances → human reviews, tweaks if needed → approved config goes through existing CI/CD pipeline.

**Timeline: Hours to days. The Build Team transforms from manual configurators to AI supervisors and quality gates.**

The Build Agent's key advantage: it's not generating from scratch. It leverages 4,000 existing configs to find patterns. "This looks like the 15 existing nostro recons — here's the best config based on those patterns, adapted to your specific sources."

### 6.2 ETL Team Transformation

**BEFORE:** Build Team identifies heavy transformation needed → raises Jira to ETL team → ETL team builds Talend job → tests → deploys. Adds days or weeks.

**AFTER:** Data Agent analyzes source data and determines transformations needed → for simple/medium transformations, generates ETL Layer Builder config directly (no ETL involvement) → for genuinely complex transformations, generates a draft Talend job specification for an ETL specialist to review. The ETL team shrinks to a small group of senior specialists handling only edge cases.

### 6.3 Production Support Transformation

**BEFORE (Today):**
Job fails → alert fires → PS analyst picks up → logs into Health Monitor, checks logs, runs DB queries, checks ServiceNow → diagnoses root cause → follows runbook if available → fixes or escalates → creates incident. **40-100+ people, 40-70% repetitive patterns.**

**AFTER (AI-Powered):**
Job fails → PS Agent is triggered instantly → simultaneously checks Health Monitor, reads logs, queries DB, pulls source file status, checks upstream system alerts, searches ServiceNow for similar incidents → within seconds has a diagnosis →

- **Known patterns (40-70%):** Auto-remediates (restarts job, triggers re-fetch, clears stuck queue) and logs the incident automatically.
- **Novel issues:** Presents full diagnosis to a human PS engineer with context: "Here's what failed, here's what I checked, here are 3 similar past incidents and how they were resolved, here's my recommended action."

**PS team becomes a small expert group handling only truly novel failures.**

### 6.4 Ops / Break Management Transformation

**BEFORE (Today):**
Recon runs → breaks generated → ops analyst picks up → opens multiple tools → traces lifecycle in RecTrace → cross-references source data → follows playbooks step by step → determines root cause → takes action or escalates. **150+ people, multiple tools, manual investigation.**

**AFTER (AI-Powered):**
Recon runs → breaks generated → Break Agent immediately kicks in → for each break, auto-runs the relevant playbook: traces through RecTrace, cross-references source data, checks historical patterns → breaks are pre-classified and presented in the Generative UI:

- **"These 200 breaks are timing — they'll auto-resolve by EOD tomorrow"** (with confidence score)
- **"These 15 breaks need action — here's each one with full context, root cause, and recommended resolution"**
- **"These 3 breaks are high-value anomalies that need senior investigation"**

The ops analyst goes from investigating every break to reviewing AI-prepared summaries and approving recommended actions. One screen instead of five tools.

### 6.5 BA Transformation

**BEFORE:** Business request → BA conducts multiple meetings → manually writes BRD in Word/Confluence → iterates through review cycles → hands off to Build Team. Weeks of meetings, writing, iteration.

**AFTER:** Business stakeholder describes their need in the Generative UI → the AI acts as an intelligent BA — asks clarifying questions, understands source systems, references similar existing recons → generates a structured BRD automatically → business stakeholder reviews and confirms → BRD feeds directly into the Build Agent. The BA role transforms from "document writer" to "quality gate" — a smaller team of senior BAs who validate that AI-generated BRDs and configs accurately capture business intent.

### 6.6 Reporting and Analytics Transformation

**BEFORE:** Management needs a report → request goes to Reporting team → dashboard built/modified in Tableau/QlikView → takes days. Ad-hoc questions require new reports.

**AFTER:** Anyone asks a question in natural language → Analytics Agent queries across all recon data, break data, SLA metrics, historical trends → generates dynamic visualizations on the fly through RecViz. "Show me all aged breaks over $1M in APAC cash recons for the last 30 days" — answered instantly. Pre-built dashboards still exist for daily operations, but ad-hoc analytics become unlimited and instant.

### 6.7 Regulatory and Compliance Transformation

**BEFORE:** Audit announced → team scrambles to gather evidence across multiple systems → manually compiles control attestations → manual monitoring of recon completeness.

**AFTER:** Compliance Agent continuously monitors recon completeness, break resolution SLAs, control effectiveness → maintains a living audit trail → when an audit is announced, generates a complete evidence package on demand → proactively flags control gaps before auditors find them. Moves from reactive evidence gathering to proactive continuous compliance.

### 6.8 RCM Team Evolution

The RCM team's role becomes even more critical. They transition from "tool maintainer" to "AI platform enabler":

- Building and maintaining the MCP adapter layer for OneRec modules
- Exposing APIs that AI agents can interact with (building new APIs where existing ones are insufficient)
- Ensuring AI-generated configs conform to OneRec's validation rules
- Evolving OneRec to support AI-native workflows

---

## 7. The Generative UI: One Interface for All

### 7.1 Concept

Rather than building separate UIs for each team, the platform provides a single conversational interface with Generative UI capabilities. The interface dynamically renders the right experience based on who is using it and what they're doing.

### 7.2 Persona-Specific Experiences

**Ops Analyst asks about a break:**
→ Generative UI renders a visual lifecycle trace (from RecTrace), with the break highlighted, source data comparison side-by-side, historical pattern analysis, and suggested resolution actions as clickable buttons.

**Build Team member describes a new recon:**
→ UI renders a mapping canvas showing source fields on one side and target fields on the other, with AI-suggested mappings they can approve or adjust. Matching rules displayed as editable cards. One-click approval to deploy.

**PS Engineer asks about a failure:**
→ UI renders a dependency graph showing exactly where the processing chain broke, with log excerpts, similar past incidents, and recommended remediation steps.

**Manager asks about performance:**
→ UI renders an interactive dashboard: break aging trends, build pipeline status, SLA compliance, team capacity utilization — all generated on demand from natural language.

**BA describing a requirement:**
→ UI renders a structured BRD template that fills in as the conversation progresses, with the AI asking clarifying questions and showing similar existing recons for reference.

### 7.3 Why Generative UI Matters

Traditional UIs are pre-built — every screen, every workflow, every view is designed and coded in advance. Generative UI is contextual — the interface is created on the fly based on the user's intent and the data available. This means:

- No more "which tool do I open for this?"
- No more switching between 5 systems to investigate a break
- New use cases don't require UI development — the AI generates the right view automatically
- The interface gets smarter as the AI learns

---

## 8. Security and Governance: R2D2 and Beyond

### 8.1 R2D2 Gateway

All AI inference traffic routes through Citi's R2D2 gateway, ensuring:

- **Data Protection** — Sensitive reconciliation data is filtered and never transmitted to external LLM providers.
- **Model Flexibility** — R2D2 supports all major foundation models, with higher preference for Gemini and Claude. Different agents can use different models based on task requirements (reasoning-heavy tasks use more capable models; high-volume triage uses faster, cheaper models).
- **Centralized Governance** — Model access, usage policies, and audit logging are managed centrally through R2D2.

### 8.2 Human-in-the-Loop

| Action Type | AI Authority | Human Gate |
|------------|-------------|------------|
| Recon config generation | AI drafts complete config | Human reviews and approves before CI/CD deploy |
| Break classification | AI pre-classifies all breaks | Human reviews and confirms actions |
| PS known-pattern remediation | AI auto-remediates | Logged, human-reviewable after the fact |
| PS novel issue diagnosis | AI provides full diagnosis | Human decides and executes |
| Report generation | Fully autonomous | No gate needed |
| Compliance monitoring | Fully autonomous alerts | Human reviews flagged gaps |

### 8.3 Audit Trail

Every AI action is logged: what the AI was asked, what it analyzed, what it recommended, what the human decided. This creates a complete, tamper-proof audit trail that satisfies regulatory requirements and enables continuous improvement analysis.

---

## 9. Implementation Roadmap

### Phase 0: Foundation (Months 1-3)

**Objective:** Build the infrastructure that everything else depends on.

- Design and implement the core AI orchestration framework on R2D2
- Define and standardize the MCP adapter specification (so all future adapters follow a consistent pattern)
- Build the Generative UI shell (the single chat interface framework)
- Begin knowledge ingestion: ingest 4,000+ existing recon configs from OneRec DB, mine ServiceNow incident history, mine Jira ticket history
- Engage RCM team to scope and build/expose OneRec APIs for configuration read/write (build new APIs where existing ones are insufficient)
- Set up development, testing, and staging environments

**Deliverable:** Working AI framework with knowledge layer bootstrapped. MCP adapter specification documented.

### Phase 1: Build Agent Pilot (Months 3-6)

**Objective:** Prove the highest-value use case — AI-generated recon configurations.

- Deploy the Build Agent — AI generates recon configs from natural language requirements
- Deploy the Data Agent alongside — source file schema understanding and column mapping
- Start with one recon type or one region as a controlled pilot
- Build MCP adapters for OneRec Recon Builder, ETL Layer Builder, and Source Maintenance
- Measure: time-to-build, config accuracy, human override rate

**Win: First AI-generated recon goes live in production.**

### Phase 2: Expand Build + Deploy PS Agent (Months 6-9)

**Objective:** Scale the Build Agent and tackle Production Support.

- Roll out Build Agent across all recon types and regions
- Deploy PS/Reliability Agent — auto-diagnosis and remediation of known incident patterns
- Build MCP adapters for Health Monitor, ServiceNow, application log systems
- Begin capturing passive knowledge from Build Agent interactions
- Measure: MTTR improvement, auto-remediation rate

**Win: Measurable reduction in mean time to resolve production incidents.**

### Phase 3: Break Agent + Analytics (Months 9-12)

**Objective:** Transform break investigation and unlock self-service analytics.

- Deploy Break/Ops Agent — pre-classification of breaks, automatic playbook execution
- Build MCP adapters for RecTrace
- Deploy Analytics Agent — natural language querying across recon data
- Integrate with RecViz for AI-powered visualization
- Measure: break resolution time, analyst productivity, self-service report adoption

**Win: Ops analysts go from investigating every break to reviewing AI-prepared summaries.**

### Phase 4: Full Ecosystem (Months 12-15)

**Objective:** Complete the vision — full end-to-end AI-powered recon lifecycle.

- Deploy Compliance Agent — continuous monitoring, audit evidence generation
- BA workflow fully AI-driven (requirement to BRD to config in one flow)
- A2A orchestration fully mature — agents collaborating autonomously across domains
- Vanguard integration (if the platform is ready)
- SmartStream TLM adapter (for remaining legacy recons)
- Measure: end-to-end recon lifecycle time, compliance readiness score

**Win: Full AI-powered reconciliation lifecycle operational.**

### Phase 5: Self-Optimizing (15+ months, ongoing)

**Objective:** The platform continuously improves itself.

- AI learns from every interaction and continuously improves accuracy
- Predictive capabilities emerge — "This recon is likely to produce excess breaks tomorrow because of the holiday settlement cycle"
- Auto-scaling: AI suggests new recons that should exist based on data patterns
- Cross-agent learning: insights from Break Agent improve Build Agent's rule generation
- The system gets smarter every day without additional human investment

---

## 10. Expected Impact

### 10.1 Efficiency Metrics

| Metric | Current State | AI-Powered Target | Improvement |
|--------|--------------|-------------------|-------------|
| Time to build a new recon | 2-12 weeks | Hours to days | 10x+ faster |
| Break investigation time | 30-60 min per break | Minutes (AI pre-classified) | 70%+ reduction |
| Mean time to resolve PS incidents | Variable (hours) | Minutes (auto-remediation) | 50%+ reduction |
| Time to generate ad-hoc report | Days (requires development) | Seconds (natural language) | Instant |
| Audit evidence preparation | Weeks of manual gathering | On-demand generation | Days → Hours |

### 10.2 Strategic Impact

- **Scale without scaling headcount** — Handle growing reconciliation volumes without proportional headcount increases. Redeploy talent to higher-value work.
- **Institutional knowledge preservation** — The knowledge layer captures and retains operational expertise that would otherwise be lost through attrition.
- **Regulatory confidence** — Continuous compliance monitoring and on-demand audit evidence generation significantly de-risk the regulatory posture.
- **Innovation leadership** — Positions Citi as the first major bank to deploy a comprehensive Agentic AI platform for reconciliation operations. A competitive differentiator in operational excellence.

### 10.3 The People Story

This is not about replacing people. It's about:

- **Redeploying talent to higher-value work** — Build team members become AI supervisors and domain experts who handle the truly complex reconciliations. Ops analysts focus on genuine exceptions that require human judgment. PS engineers become reliability architects.
- **Scaling capacity without scaling headcount** — As reconciliation volumes grow (and they will), the AI platform absorbs the incremental load. No need for proportional hiring.
- **Making work more interesting** — Nobody goes into financial operations to manually copy column mappings or restart the same failed job for the 50th time. AI handles the tedious work; humans handle the interesting problems.

---

## 11. Technical Considerations

### 11.1 Build vs. Buy

The recommendation is to **build in-house on top of foundation models** accessed through R2D2, rather than adopting an enterprise AI platform. Reasons:

- GRU's domain is highly specialized — off-the-shelf AI platforms won't understand recon operations without significant customization.
- MCP and A2A protocols are open standards — no vendor lock-in.
- Building in-house allows tight integration with OneRec and other internal tools.
- Citi's R2D2 infrastructure already provides the model access layer.

### 11.2 Model Strategy

R2D2 supports all major foundation models with preference for Gemini and Claude. The recommended approach is to use different models for different agents based on task requirements:

- **Reasoning-heavy agents** (Build Agent, Compliance Agent) — use the most capable available models for accuracy.
- **High-throughput agents** (PS Agent triage, Break Agent classification) — use faster, cost-effective models for speed.
- **Analytics Agent** — use models optimized for code generation and data analysis.

This multi-model strategy optimizes for both accuracy and cost.

### 11.3 API Requirements for OneRec

The AI platform requires programmatic access to OneRec's modules. Current API coverage may be insufficient. The following APIs need to be assessed and, where necessary, built:

- **Config Read API** — Read existing recon configurations (JSON) from the database.
- **Config Write/Validate API** — Submit AI-generated configurations for validation and deployment.
- **Source Schema API** — Retrieve source file format specifications.
- **Health Monitor API** — Real-time status and alerting.
- **Report API** — Trigger and retrieve reconciliation reports.

(Note: Where existing APIs can be reused, they should be. New APIs should only be built where existing capabilities are insufficient.)

### 11.4 Vanguard Dependency

The architecture is designed to work with or without Vanguard:

- **Vanguard available:** Build one deep MCP adapter to Vanguard → AI gets a unified view of all source data.
- **Vanguard not available:** Individual MCP adapters for SFTP, Kafka, API endpoints → AI works with fragmented but functional source access.

This decoupling ensures GRU's AI transformation is not gated on Vanguard's delivery timeline.

---

## 12. Architecture Diagrams

The following diagrams are provided as part of this proposal:

1. **High-Level Architecture Overview** — The 6-layer architecture showing all components and their relationships.
2. **Agent Interaction Diagram** — How specialized agents collaborate via A2A on a complex task (example: building a new recon end-to-end).
3. **MCP Integration Map** — All tools and their MCP adapters, showing the standardized protocol layer.
4. **Data Flow Diagram** — How data moves through the system from source ingestion to AI processing to user output.
5. **Before/After: Build Team** — Current manual workflow vs. AI-powered workflow.
6. **Before/After: Break Management** — Current manual investigation vs. AI pre-classification.
7. **Phased Implementation Roadmap** — Visual timeline showing deliverables and wins per quarter.

---

## 13. Next Steps

1. **Approve Phase 0 funding and team formation** — Dedicated team to build the foundational AI orchestration framework and MCP adapter specification.
2. **Engage RCM team to scope OneRec API requirements** — Identify which APIs exist, which need enhancement, and which need to be built from scratch.
3. **Set up Build Agent pilot program** — Select one recon type or region as the controlled pilot. Define success metrics.
4. **Establish governance framework** — Define human-in-the-loop policies, approval workflows, and audit trail requirements.
5. **Begin knowledge layer ingestion** — Start mining existing OneRec configs, ServiceNow incidents, and Jira tickets.

**The future of reconciliation starts now.**

---

*This proposal was prepared for Citi's Global Reconciliation Utility leadership team, February 2026.*
