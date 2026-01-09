# Module 5 --- Systems & Ops Thinking

## Learning Objectives

By the end of this module, the student should be able to:

-   Describe the lifecycle from build → artifact → deploy → run across environments

-   Understand dev vs staging vs production and how artifacts promote through them

-   Explain CI/CD pipeline concepts and why automation matters for reliability

-   Describe migrations, rollbacks, backups, and replication as data/infrastructure operations

-   Understand the operational dimensions of availability, durability, and consistency

-   Explain observability (metrics, logs, traces, KPIs, SLOs) and why it matters for production

-   Define and apply RPO and RTO for business continuity planning

-   Reason through failure modes, fault domains, and mitigation strategies

-   Justify architectural decisions under constraints (latency, cost, compliance, throughput, SLAs)

## 5.1 Introduction to Systems Thinking in DevOps

Traditional software development often focuses primarily on feature delivery and correctness in isolation. However, operational systems exist in dynamic, unpredictable environments with failure, traffic spikes, resource contention, time-based load cycles, cost constraints, and user expectations. Systems thinking shifts perspective from code to operational outcomes.

Systems thinking emphasizes:

-   inputs (user traffic, workloads)

-   transformations (services, pipelines)

-   constraints (compute, network, latency)

-   dependencies (databases, queues, caches)

-   feedback loops (metrics, alerts, logs)

-   externalities (cost, security, compliance)

-   failure modes (network partitions, DB crashes, cascading failures)

This mindset is what distinguishes a DevOps or SRE engineer from a pure application developer.

### 5.1.1 Holistic View of Software Systems

Applications do not run in isolation; they operate in ecosystems composed of:

-   runtime environments

-   infrastructure

-   users

-   data stores

-   networks

-   deployment tooling

-   monitoring toolchains

Thinking holistically improves reliability and reduces operational surprises.

### 5.1.2 Operational Responsibilities

Running software in production introduces new responsibilities:

-   uptime: system must be available

-   resilience: withstand failure

-   security: defend against threats

-   performance: meet latency/throughput targets

-   cost efficiency: operate economically

-   compliance: adhere to policies & regulations

Software value is only realized when it runs reliably under real conditions.

## 5.2 Build → Artifact → Deploy → Run Lifecycle

The delivery lifecycle reflects the journey from code to operational system.

### 5.2.1 Build Phase

Code is transformed from source into executable form:

-   compiled binaries

-   bundled JS/CSS

-   packaged deb/rpm

-   container images

Builds frequently include tests, linting, and static analysis.

### 5.2.2 Artifact Creation

Artifacts are immutable representations of a build. They detach build from deployment. Examples:

-   Docker images

-   JAR/WAR files

-   binary distributions

-   release bundles

Artifact immutability enables repeatability, rollback, and deterministic releases.

### 5.2.3 Deployment Phase

Deployment moves artifacts into environments. Deployment can be:

-   manual

-   semi-automated

-   fully automated (continuous deployment)

Modern deployments rely on:

-   health checks

-   staging rollout

-   versioning

-   canary strategies

-   blue/green deployments

### 5.2.4 Runtime Phase

The runtime represents execution under real workloads. Runtime characteristics include:

-   traffic patterns

-   state management

-   scaling behavior

-   failover and recovery

-   resource utilization

Runtime is where the majority of operational complexity emerges.

## 5.3 Environments & Promotion

Environments serve as controlled domains for testing, validation, and release readiness.

### 5.3.1 Dev Environment

Dev is flexible and volatile. Developers test features, break stuff frequently, and optimize debugging workflows.

Artifacts in dev may not be optimized for performance or security.

### 5.3.2 Staging Environment

Staging (or pre-production) mirrors production as closely as possible:

-   similar resource sizing

-   similar data (synthetic or sanitized)

-   similar configuration

-   similar security boundaries

-   similar observability

The purpose of staging is validation and risk reduction.

### 5.3.3 Production Environment

Production is the environment that serves real users. It operates under constraints:

-   minimal downtime

-   tight SLOs

-   cost awareness

-   strict access controls

-   auditing and logging requirements

### 5.3.4 Promotion Flows

A healthy release pipeline promotes artifacts forward in one direction:

dev → staging → production

Artifacts do not mutate between environments; only configuration does.

## 5.4 CI/CD Concepts

CI/CD is the operational backbone of high-velocity engineering organizations.

### 5.4.1 Continuous Integration

Continuous integration automates building/testing code on merge or push:

-   automated linting

-   automated tests

-   static analysis

-   artifact creation

CI prevents integration hell by validating incremental changes frequently.

### 5.4.2 Continuous Delivery vs Deployment

Important distinction:

-   **Continuous Delivery:** artifacts always ready for deployment; approval required

-   **Continuous Deployment:** deploy automatically without manual intervention

Both reduce release friction; the difference lies in control policy.

### 5.4.3 Pipelines as Policy

Pipelines enforce organizational governance:

-   security scanning

-   code signing

-   compliance checks

-   approvals

-   artifact promotion

-   runtime guardrails

This formalizes release discipline.

## 5.5 Data & Schema Operations

Code deployment is only one half of operational change; data often defines the harder half.

### 5.5.1 Migrations

Migrations alter schemas or transform data. Constraints include:

-   zero downtime requirements

-   backward compatibility

-   transactional safety

For example, adding a column with no default might break code if not sequenced properly.

### 5.5.2 Rollbacks

Rollbacks revert changes. Easier for stateless artifacts, harder for stateful data.

Data rollbacks require:

-   preserving invariants

-   compensating transactions

-   reverse migrations

### 5.5.3 Backups

Backups provide last-resort recovery and support compliance. Proper backups consider:

-   frequency (hourly, daily, weekly)

-   retention period

-   encryption

-   restore tests (backup without restore is meaningless)

### 5.5.4 Replication

Replication improves:

-   latency (geo-distribution)

-   availability (failover)

-   read isolation (read replicas)

Replication may reduce durability if replication lag or split-brain scenarios occur.

## 5.6 Availability, Durability & Consistency

Distributed systems rely on different operational guarantees.

### 5.6.1 Availability

Availability refers to a system responding correctly within operational bounds. Downtime erodes trust and revenue.

Measured as:

uptime %

error rate

latency SLOs

### 5.6.2 Durability

Durability ensures that once data is stored, it persists permanently despite failures. Databases, object stores, and logs prioritize durability.

Example: S3 provides 11 nines durability for stored objects.

### 5.6.3 Consistency Models

Consistency refers to how reads reflect writes.

Models include:

-   strong consistency

-   eventual consistency

-   read-your-own-write

-   causal consistency

Eventual consistency is common in distributed key-value stores like DynamoDB or Cassandra.

## 5.7 Observability in Production

Observability provides insight into what internal system states led to observed outputs.

### 5.7.1 Metrics

Metrics are quantitative time-series values capturing:

-   CPU

-   memory

-   throughput (req/sec)

-   latency (p50, p90, p99)

-   queue depth

-   error rate

-   cache hit ratio

Metrics support alerting and capacity planning.

### 5.7.2 Logs

Logs represent discrete events in structured or unstructured text. Logs assist with:

-   debugging

-   security analytics

-   incident audits

-   user behavior tracing

### 5.7.3 Traces

Traces stitch together execution paths across distributed systems. Tracing reveals bottlenecks, microservice interactions, and request timing.

### 5.7.4 KPIs & SLOs

KPIs represent business outcomes (conversion, uptime, churn).\
SLOs define operational objectives around reliability (latency targets, error budgets).

SLOs establish contracts between engineering and product.

## 5.8 RPO & RTO Concepts

Business continuity requires grappling with the uncomfortable truth that systems will fail, data will be lost, and downtime will occur. The question is not *whether*, but *how much* can be tolerated and for how long. RPO and RTO provide structured vocabulary for quantifying these tolerance thresholds.

### 5.8.1 Recovery Point Objective (RPO)

RPO defines the maximum tolerable period of *data loss* measured in time.

Examples:

-   RPO = 1 hour → acceptable to lose up to 1 hour of writes

-   RPO = zero → no data loss acceptable (requires synchronous writes + replication)

-   RPO = 24 hours → daily backups acceptable for low-stakes systems

RPO shapes backup frequency and replication strategies.

### 5.8.2 Recovery Time Objective (RTO)

RTO defines the maximum tolerable *downtime* before the system must be restored.

Examples:

-   RTO = 1 min → requires failover automation + hot replica

-   RTO = 1 hour → acceptable manual intervention

-   RTO = 24 hours → acceptable to wait for disaster recovery workflows

RTO shapes tooling, staffing, runbooks, and infrastructure cost.

### 5.8.3 Mapping RPO/RTO to Architecture

Lower RPO/RTO requires:

-   more replication

-   more automation

-   higher infra cost

-   more skilled operational stewardship

Higher RPO/RTO tolerances lower cost but sacrifice user experience and revenue.

## 5.9 Failure Modes & Risk Mitigation

Systems fail in diverse and often compounding ways. Modeling failure modes allows engineers to shape resilient architectures.

### 5.9.1 Common Failure Modes

Examples include:

-   DB write pressure → queue backlog → cascading failures

-   network partition → split brain → inconsistent writes

-   traffic spike → autoscaler lag → degraded latency

-   deployment bug → crash loop → incident recovery

-   human error → privilege escalation → misconfiguration

-   disk failure → data loss → restore workflow

Failure modes often combine rather than occur independently.

### 5.9.2 Fault Domains

Fault domains define isolation boundaries that limit blast radius.

Domains include:

-   thread/process

-   pod/container

-   host

-   rack

-   AZ (Availability Zone)

-   region

-   provider

SRE disciplines formalize the idea: never allow a single failure to collapse all coupled systems.

### 5.9.3 Risk Mitigation Techniques

Mitigation strategies include:

-   **retries:** recovering from transient network failures

-   **timeouts:** limiting blocking operations

-   **circuit breakers:** preventing cascading collapse

-   **bulkheads:** isolating resources to prevent shared failure

-   **replication:** adding redundancy

-   **throttling & load shedding:** protecting system integrity

-   **failover:** activating standby resources

Risk mitigation trades performance and cost against reliability.

## 5.10 Decision-Making & Tradeoffs

Systems engineering is largely about balancing tradeoffs. There is no ideal architecture; only architectures optimized for constraints.

### 5.10.1 Constraints-Based Reasoning

Constraints may include:

-   latency targets

-   throughput requirements

-   compliance rules (HIPAA, SOC2)

-   regulatory boundaries (GDPR, data locality)

-   SLAs

-   cost ceilings

-   team skillset

-   operational maturity

Constraints convert vague architectural desires into concrete design decisions.

### 5.10.2 Architectural Tradeoffs

Classic tradeoff vectors include:

-   cost vs performance

-   consistency vs availability

-   security vs convenience

-   automation vs control

-   durability vs write latency

-   abstraction vs transparency

These tradeoffs appear everywhere from database selection to deployment strategy.

### 5.10.3 Documenting Decisions

Teams formalize decisions using:

-   ADRs (Architectural Decision Records)

-   RFCs (Request for Comments)

-   design docs

-   postmortems

Artifacts build institutional memory and reduce repeated mistakes.

## 5.11 Module Review & Terminology

This module reinforces operational vocabulary indispensable in modern engineering:

-   CI/CD

-   RPO/RTO

-   SLO/KPI

-   availability

-   durability

-   consistency

-   replication

-   failover

-   rollback

-   reliability

-   observability

-   fault domains

Understanding this vocabulary enables credible conversations in architecture reviews, incident bridges, and compliance audits.

# Analogies for Conceptual Understanding

### Deployment as Shipping Logistics

Artifacts are packages; staging is customs inspection; production is final delivery. Failed inspection leads to rollback.

### Database as a Ledger

Durability resembles financial auditing---once written, records must not vanish.

### RPO as Insurance Deductible

RPO defines acceptable loss similar to insurance defining financial risk tolerances.

### RTO as Hospital Recovery Time

How long until a patient (system) must be stabilized post-incident.

### Metrics as Vital Signs

Metrics resemble pulse, heart rate, and blood pressure---indicating health trend.

### Logs as Security Footage

Logs help reconstruct incidents for analysis and prosecution.

### Traces as GPS Navigation History

Traces show journey paths with timing across microservices.

# Diagrams (Mermaid + ASCII)

### Mermaid: Build → Artifact → Deploy → Run
```mermaid
flowchart LR

Source \--\> Build\[Build\]

Build \--\> Artifact\[Immutable Artifact\]

Artifact \--\> Deploy\[Deployment\]

Deploy \--\> Run\[Runtime\]
```
### ASCII: Environments
```
dev \--\> staging \--\> prod

(code) (validation) (real users)
```
### Mermaid: Observability Pillars
```mermaid
flowchart TD

Metrics \--\> Observability

Logs \--\> Observability

Traces \--\> Observability
```
### ASCII: RPO/RTO
```
RPO: acceptable data loss

RTO: acceptable downtime
```
# Exercises (Ungraded Practice)

1.  Describe the difference between availability and durability.

2.  Given an RPO of 5 minutes and RTO of 1 hour, explain backup and recovery implications.

3.  Explain why backups without restore validation are unreliable.

4.  Sketch a CI/CD pipeline conceptually for a backend service.

5.  Describe a failure mode where retries make things worse instead of better.

# Solved Exercises

1.  Availability → uptime/response; Durability → data permanence.

2.  RPO=5 min → frequent replication; RTO=1 hr → slower restore acceptable.

3.  Because restoring is the true test of backup integrity; backups alone provide no assurance.

4.  Example: push → CI tests → build → artifact → staging deploy → approval → prod deploy.

5.  Retries under overload increase downstream pressure, causing cascading failures.

# Mini-Scenarios (Applied Thinking)

### Scenario A: DB Partition

DB becomes unavailable but cache remains operational; read requests succeed but writes fail. Student must assess consistency + partial availability.

### Scenario B: Rollback Decision

Deployment introduces errors. Should rollback artifact or perform schema migration reversal?

### Scenario C: RPO Constraint

Banking system demands zero data loss; synchronous replication required; cost and latency implications surface.

### Scenario D: Autoscaling Trap

Traffic spike triggers autoscaler but RDS cannot scale; app nodes saturate DB; cascading failure triggered.

# Quiz Questions (answers at end)

1.  Define CI vs CD.

2.  Define RPO.

3.  Define RTO.

4.  What are the three pillars of observability?

5.  What is durability?

6.  Why is staging important?

7.  How do fault domains reduce blast radius?

8.  Why do ADRs matter?

### Quiz Answers

1.  CI integrates and tests code; CD deploys artifacts automatically or semi-automatically.

2.  Maximum acceptable data loss measured in time.

3.  Maximum acceptable downtime before restoration.

4.  Metrics, logs, traces.

5.  Guarantee that data, once written, persists despite failure.

6.  It validates artifacts before real users see them.

7.  They isolate failures to localized zones (pod/host/AZ/region).

8.  They document tradeoffs and decisions for institutional memory.

# Teaching Notes (Instructor Guidance)

-   Encourage students to reason about tradeoffs rather than chase "correct answers."

-   Use real-world outages and postmortems to make concepts vivid.

-   Reinforce vocabulary---Ops is language-heavy and precision matters.

-   Stress that restore testing is more important than backup itself.

-   Use whiteboard diagrams for RPO/RTO reasoning.

-   Use chaos engineering scenarios to simulate failure mode discussions.

-   Encourage ADR writing as homework to simulate professional artifacts.

Perfect --- here are all requested global artifacts in clean, structured **Markdown**, drawing from the 5 completed modules and extending them into a coherent course framework. No repetition of module content, only higher-level meta structure as requested.
[Go Back](04-containers-docker.md) | [Go Home](../README.md) | [Go Next](06-instructor-resources.md)

