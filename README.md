# Awesome-Microservice-Orchestration

## Top Microservice Orchestration Tools Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Durable Execution, Polyglot Workers & Deterministic Workflow Replay*  
**Last updated: March 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Microservice Orchestration**. These tools coordinate multi-step business processes across distributed services — handling retries, timeouts, compensation, and state persistence — so a failed payment step doesn't leave an order in limbo and a crashed worker doesn't lose the workflow's progress.

**Examples** include Temporal, Conductor, Camunda 8, Apache Airflow, AWS Step Functions, and the managed orchestration platforms (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, polyglot worker execution, and transparent state management — ideal for platform engineers who need reliable long-running workflows without locking into a single cloud's proprietary state machine syntax.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **AWS Step Functions** — **The serverless state machine service.** Defines workflows in Amazon States Language (JSON) with visual workflow studio. Deep integration with 200+ AWS services. **Best for AWS-native teams** wanting managed orchestration without operating infrastructure. **The catch**: state machine definitions are JSON-based and AWS-specific — portability to other clouds requires rewriting.

- **Google Cloud Workflows** — GCP's managed orchestration service with YAML-based workflow definitions and integration with Google Cloud services. **Best for GCP-native teams** wanting serverless workflow execution.

- **Azure Logic Apps** — Microsoft's managed workflow platform with visual designer and 400+ connectors. **Best for Microsoft-centric organizations** needing low-code workflow automation with enterprise integration.

- **Temporal Cloud** — **The managed version of Temporal's durable execution engine.** Provides the same deterministic replay, event history, and polyglot worker model without operating the Temporal Service yourself. **Best for teams wanting Temporal's code-first model** with managed infrastructure and support.

- **Orkes Conductor** — **The enterprise-ready version of Conductor OSS**, available fully managed or self-hosted. Adds hosted operations, visual debugging, RBAC, secrets, schedules, webhooks, observability, integrations, and support on top of the open-source engine . **100% API and workflow compatible with Conductor OSS** . **Best for enterprises** wanting Conductor's task-and-worker model with production support and governance.

## Open-Source GitHub Projects

- **Temporal** — **The code-first durable execution platform.** MIT licensed. **Workflows are written in your application code** — ordinary control flow with loops, conditionals, and function calls — and Temporal handles retries, state persistence, and crash recovery . **Deterministic replay is the core mechanism**: the Event History is a complete ordered record, and after a crash a new Worker fetches that history, replays the Workflow code to rebuild local state, and resumes exactly where it stopped, with local variables intact . **Workflows must be deterministic** — anything talking to the outside world belongs in **Activities**, which are plain functions with zero framework constraints . **Polyglot SDKs** for Java, Go, TypeScript, Python, .NET, PHP, Ruby, and more . **The operational reality**: **non-determinism errors are the recurring pain** — reordering or adding an `await` on an Activity or Timer can trigger them for every already-running instance unless versioned first . **Worker Versioning** pins Workflow revisions to specific Worker deployments, and **Continue-As-New** bounds event history growth . **The trade-off**: highest operational complexity — determinism and versioning discipline are required — but the central Event History is also your audit trail . **Best for developer-controlled service orchestration** where the workflow outlives a single process and code-first authoring matters more than visual BPMN modeling .

- **Conductor (Conductor OSS)** — **The event-driven agentic orchestration platform.** Apache 2.0 licensed, **built at Netflix and battle-tested at internet scale** — scales horizontally to handle **billions of workflow executions** . **Central service stores durable state**, with **polyglot Workers** polling for tasks — write Workers in any language, use any library, call any API, with zero determinism constraints because the orchestration layer is deterministic by construction . **Full execution history preserved indefinitely** — restart from the beginning, rerun from a specific task, or retry just the failed step via API or UI . **Native AI/LLM integration**: **14+ LLM providers** (Anthropic, OpenAI, Gemini, Bedrock, and more), **MCP tool calling**, function calling, human-in-the-loop approval via WAIT tasks, and vector database integration for RAG . **Conductor OSS requires JDK 21+** for the current mainline . **The trade-off**: **not BPMN-centric** — if your requirement is会签, 退回, and task portals, Conductor requires significant upper-layer construction . **Best for order fulfillment, media processing, cross-service Saga, and AI agent execution chains** where Worker-driven orchestration matches the work .

- **Camunda 8** — **The Zeebe-powered distributed orchestration platform.** Apache 2.0 licensed core, but **Self-Managed production use requires a valid license since 8.6** . **Zeebe uses a partitioned log with Raft replication**, and business code runs as **external Job Workers** accessed via REST/gRPC through the Gateway . **Designed for cross-language services, horizontal scaling, reliable retries, timeouts, backpressure, and fault recovery** . **Enterprise add-ons** include Modeler, Operate, Tasklist, and Identity . **The critical caveat**: **Camunda 8 is not a Maven upgrade from Camunda 7** — process models, Java Delegates, transactions, history queries, operations, and data migration all need redesign . **Best for enterprises** needing BPMN modeling with distributed execution, accepting the license and operational overhead .

- **Apache Airflow** — **The general-purpose workflow orchestrator with the largest ecosystem.** Apache 2.0 licensed, **3,000+ contributors** and **20M+ downloads/month** . **Provider packages include first-class integrations with major compute backends** — SageMaker, Vertex AI, Databricks, MLflow, Weights & Biases, Hugging Face, and Kubernetes execution backends . **DAG-based authoring in Python** with deferrable operators that free worker slots while waiting for long-running jobs . **The trade-off**: **general-purpose, not microservice-specific** — it's a job scheduler and orchestrator, not a durable execution engine with deterministic replay . **Best for batch workflows and data pipelines** where the work is scheduled jobs rather than long-running interactive service coordination .

### Additional Strong Open-Source Options

- **Zeebe** — The workflow engine underlying Camunda 8, available as a standalone Apache 2.0 component . Best for teams wanting Camunda's distributed log architecture without the full platform license.
- **Inngest** — Event-driven workflow engine with durable functions, step functions, and fan-out patterns. Apache 2.0 licensed . Best for event-driven microservice coordination with a simpler model than Temporal.
- **Trigger.dev** — Background jobs and workflow platform with TypeScript-first approach, durable execution, and no timeout limitations. Apache 2.0 licensed . Best for TypeScript teams wanting durable background jobs.

**Frameworks for building custom systems**: Combine **Temporal** for code-first durable execution with deterministic replay and polyglot Workers, **Conductor** for Worker-driven orchestration with native LLM task types and indefinite execution history, **Camunda 8** if BPMN modeling and distributed Zeebe execution justify the license cost, and **Apache Airflow** for scheduled batch pipelines rather than long-running interactive workflows — to build an orchestration stack tailored to your authoring preference (code vs BPMN vs JSON), determinism tolerance, and AI-agent requirements.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- Microservice orchestration tools differ significantly in authoring model, determinism constraints, and operational complexity. **Temporal requires determinism discipline** — reordering or adding awaits on Activities/Timers can trigger non-determinism errors for running instances unless versioned first, and unbounded event history growth requires Continue-As-New . **Conductor eliminates determinism constraints by construction** — Workers are plain code with zero framework restrictions — but is not BPMN-centric and requires building upper-layer approval workflows yourself . **Camunda 8 is not an upgrade from Camunda 7** — it's a distributed platform with license requirements and redesign work . **Apache Airflow is a job scheduler**, not a durable execution engine — don't expect deterministic replay or long-running interactive workflow support. **The choice often comes down to who authors workflows**: developers writing code favor Temporal or Conductor; business analysts modeling BPMN favor Camunda 8.
- Self-hosted open-source solutions require proper database backend configuration, Worker deployment management, and monitoring of workflow state and retry behavior.

---

**Made for platform engineers and architects coordinating reliable workflows across distributed services.**
Let's make microservice orchestration more open, durable, and workload-appropriate.
