# 1. Table of Contents (Global)

Module 1 --- Linux & Git Foundations

1.1 Linux Basics & Filesystem

1.2 Permissions & Processes

1.3 Logs & Terminal Tools

1.4 Bash Scripting Concepts

1.5 Git Basics & Workflow

1.6 Local vs Remote Repos

1.7 Branching & Merging

Module 2 --- Networking Fundamentals

2.1 Browser → Server Flow

2.2 DNS, Domains & IPs

2.3 TCP vs UDP

2.4 DNS Records (A, CNAME, MX, TXT, NS)

2.5 Public/Private IPs & NAT

2.6 Subnetting & CIDR

2.7 Firewalls, Proxies & Routing

2.8 Troubleshooting Networking

Module 3 --- Cloud Foundations (AWS + Cost Awareness)

3.1 Regions & AZs

3.2 Compute Models (EC2/ECS/Lambda)

3.3 IAM Basics

3.4 Storage (S3/EBS/EFS)

3.5 VPC Networking (Subnets, SGs, NAT)

3.6 CDN & CloudFront Basics

3.7 Service Strategy & Tradeoffs

3.8 Cost Awareness & Risks

3.9 Scenario Decision-Making

Module 4 --- Containers & Docker

4.1 Containers vs VMs

4.2 Docker Engine & CLI

4.3 Images, Tags & Layers

4.4 Dockerfile & Builds

4.5 Registries (DockerHub/ECR)

4.6 Container Networking & Ports

4.7 Container-based Request Flow

4.8 Containers in DevOps Pipelines

Module 5 --- Systems & Ops Thinking

5.1 Build → Artifact → Deploy → Run

5.2 Environments (Dev/Staging/Prod)

5.3 CI/CD Concepts

5.4 Migrations, Rollbacks & Replication

5.5 Availability vs Durability vs Consistency

5.6 Observability (Metrics/Logs/Traces/KPIs)

5.7 RPO/RTO

5.8 Failure Modes & Fault Domains

5.9 System Tradeoffs & Decisions

# 2. Curriculum Map (Modules + Outcomes)

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Module**            **Core Outcomes**
  --------------------- -----------------------------------------------------------------------------------------------------------------------------------------
  Linux & Git           Navigate Linux, manage permissions/processes, interpret logs, understand bash concepts, use Git with remote workflows

  Networking            Explain DNS & browser flows, differentiate protocols, reason about IP/ports/NAT/subnets, troubleshoot connectivity, understand CIDR

  Cloud Foundations     Explain AWS primitives, compare compute/storage models, understand IAM/VPC/CloudFront, reason about tradeoffs + cost risks

  Containers & Docker   Contrast containers vs VMs, build/run containerized apps, use images/registries, diagram container networking, justify containerization

  Systems & Ops         Explain CI/CD pipelines, environments, rollback/migration/backup, observability, RPO/RTO, think in failure modes & constraints
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------

# 3. Scenario Bank (15+ Scenarios)

Short, realistic, DevOps/system-thinking scenarios:

1.  Deploy low-traffic SaaS with a \$100/mo budget

2.  Add staging environment to startup pipeline

3.  Migrate monolith to container-based deployment

4.  Handle sudden traffic spike (10× load)

5.  Debug "DNS resolves but app fails"

6.  Reduce CloudWatch logging bill by 80%

7.  Deploy API using Lambda vs ECS vs EC2 (tradeoff debate)

8.  Design backup + restore strategy for small DB

9.  Handle partial outage when DB read-replicas degrade

10. Introduce CI/CD without breaking production stability

11. Decide between S3 vs EFS vs EBS for ML artifacts

12. Debug cross-container communication issue (ports/DNS)

13. Perform rollback after bad migration deploy

14. Launch multi-AZ app with minimum cost overhead

15. Tune RPO/RTO policy for compliance-sensitive data

16. Optimize container image size for faster deployment

17. Add CDN to reduce global latency for static SPA

18. Investigate cascading failure from overloaded queue

19. Enforce IAM least privilege for dev team vs prod team

20. Re-architect system for multi-region durability

# 4. Viva-Style Question Bank (30 Questions)

Concept-heavy, oral-defense style:

1.  Why do containers solve "works on my machine"?

2.  What is the difference between a process and a container?

3.  Why do we need staging environments?

4.  Define RPO and RTO with real-world examples.

5.  Distinguish availability from durability.

6.  What is DNS resolution and why does it matter?

7.  How do NAT gateways differ from Internet Gateways?

8.  Explain TCP vs UDP in operational terms.

9.  Why do orgs adopt CI/CD pipelines?

10. What are immutable artifacts and why do we want them?

11. What is IAM and why is it central to AWS?

12. Compare S3, EBS, and EFS.

13. Why might Lambda be cheap for small workloads but expensive for large?

14. What are CIDR blocks and why do cloud engineers care?

15. Why do distributed systems need tracing?

16. Define "eventual consistency".

17. Why do systems fail in cascading patterns?

18. What is the responsibility of logs vs metrics vs traces?

19. Why should backups be tested via restores?

20. What is a canary deployment?

21. Why is Docker Hub not always appropriate for enterprise?

22. Why is DNS caching both useful and dangerous?

23. What is a fault domain?

24. Why is rollback easy for code but hard for data?

25. Why does SLO definition change engineering behavior?

26. Why is latency budgeting important?

27. How do artifacts promote across environments?

28. Why is egress cost important in cloud architecture?

29. What is least-privilege IAM and why does it matter?

30. Why do we separate concerns between build and deploy phases?

# 5. Capstone Evaluation Rubric

### Core Criteria

-   Technical correctness

-   Operational reasoning

-   Tradeoff justification

-   Cost awareness

-   Reliability & failure thinking

-   Clarity & communication

### Performance Levels

  --------------------------------------------------------------------------
  **Score**   **Descriptor**
  ----------- --------------------------------------------------------------
  4           Expert: coherent, cost-sensitive, strong tradeoff reasoning

  3           Competent: correct but lacks full tradeoff/ops maturity

  2           Emerging: partial correctness, missing constraints

  1           Weak: surface-level or mismatched reasoning

  0           Incorrect or incoherent
  --------------------------------------------------------------------------

### Sample Scoring Grid

  -----------------------------------------------------------------------------------
  **Criterion**                        **Weight**   **Score (0--4)**   **Weighted**
  ------------------------------------ ------------ ------------------ --------------
  Architecture fit for scenario        25%                             

  Cost & resource reasoning            20%                             

  Reliability & failure modes          20%                             

  Operational & CI/CD reasoning        15%                             

  Data + backup + migration strategy   10%                             

  Communication clarity                10%                             

  **Total**                            **100%**                        
  -----------------------------------------------------------------------------------

# 6. Slide Outline (High-Level)

Slides per module (not full slides):

**Module 1**

-   Linux mental model

-   Processes & permissions

-   Logs & shell

-   Git workflows

-   Branching models

**Module 2**

-   Browser → server flow

-   DNS & domains

-   TCP/UDP & ports

-   Subnets & CIDR

-   Debugging connectivity

**Module 3**

-   AWS global layout

-   Compute tradeoffs

-   Storage types

-   VPC basics

-   Cost traps & case studies

**Module 4**

-   Containers vs VMs

-   Docker basics

-   Images & layers

-   Registries

-   Container networking

**Module 5**

-   Build → deploy → run

-   Environments

-   CI/CD

-   Observability

-   RPO/RTO & failure modes

# 7. Student Workbook Outline

Workbook contents should include:

### Sections

-   Guided notes per module

-   Diagramming exercises

-   Tradeoff reasoning tasks

-   Cost reasoning tasks

-   Failure analysis tasks

### Question Types

-   Short answer (concepts)

-   Fill-in diagrams

-   Compare & contrast tables

-   Debugging exercises

-   Scenario-based decision making

-   Reflection prompts

-   Architecture sketching

-   Checklist validation tasks

### Reflection Prompts

-   "What tradeoffs did you prioritize and why?"

-   "Where could failure occur in this design?"

-   "What costs surprised you?"

-   "Which constraints shaped your design?"

### Checklists

-   Deployment readiness checklist

-   Observability checklist

-   Backup & restore checklist

-   Container build checklist

-   CI/CD checklist

# 8. Teaching Guide for Different Formats

### Async Self-Paced

-   Emphasis on reading + workbook + quizzes

-   Capstone optional

-   Instructor feedback asynchronous

-   Works best for junior devs or cross-training

### 1-Day Crash Workshop

-   Focus on conceptual fluency + diagrams

-   Minimal hands-on

-   Lots of viva-style discussions

-   Goal: "Ops literacy fast"

### 2-Day Intensive

-   Day 1 → Modules 1--3

-   Day 2 → Modules 4--5 + scenarios

-   Includes mini-capstone or design challenge

-   Works for dev-teams & tech leads

### 4-Week Bootcamp

-   Week-by-week:

    -   W1: Linux/Git + Networking

    -   W2: Cloud + cost

    -   W3: Containers + CI/CD

    -   W4: Systems Thinking + Capstone

-   Capstone defended viva-style

-   Ideal for upskilling talent pipeline

# Final Capstone Projects

## Capstone 1 --- "Design & Deploy a Production-Ready SaaS MVP (Budget-Constrained)"

### Scenario

You\'re asked to deploy a small multi--tenant SaaS application with:

-   expected low-to-moderate traffic

-   limited operational staff (a single developer or dev+ops hybrid)

-   **strict budget ceiling: \$150/month**

-   requirement for **zero human intervention deployments**

-   feature updates must ship weekly without downtime

-   customer data must not be lost on failure

-   must support minimal global latency for customers (US + EU)

### Deliverables

-   Architecture diagram (cloud + networking + storage + containers)

-   CI/CD pipeline design

-   Backup + RPO/RTO policy

-   Rollback policy

-   Cost breakdown (estimated monthly costs)

-   Tradeoff justification document (why X vs Y)

-   Risk register (what can break and mitigation strategy)

-   Deployment runbook (high-level operational steps)

### Evaluation Focus

-   Cost awareness + frugality

-   Containers vs serverless tradeoff reasoning

-   Storage choice (S3/EBS/EFS)

-   Observability basics

-   Disaster recovery plan scaled to budget

-   Realistic constraints (skills, money, SLA)

## Capstone 2 --- "Migrate a Legacy Monolith to Containers & CI/CD Pipeline"

### Scenario

A legacy monolithic app runs on a VM:

-   Single EC2 instance

-   Manual SSH deploys

-   Outage during deploys

-   No rollbacks

-   No staging environment

-   No backups of DB

-   No CI/CD

-   DB is 120GB Postgres

-   Traffic peaks during weekdays, dips nights/weekends

Goal: modernize deployment pipeline + runtime without fully rewriting the app.

### Deliverables

-   Containerization strategy (Dockerfile + registry plan)

-   Deployment pipeline design (CI + artifact + promotion)

-   Staging + production environment split

-   DB migration + backup/restore strategy

-   Rollback plan (for code + schema)

-   Availability strategy (blue/green / rolling / canary)

-   Operational & failure-mode analysis

-   What you would **not** change yet (and why)

### Evaluation Focus

-   Practical modernization vs over-engineering

-   Minimal risk migration sequencing

-   Failure-aware DB strategy (120GB is serious, not trivial)

-   Rollback realism

-   CI/CD literacy

-   Operational literacy (downtime, reliability, observability)

## Capstone 3 --- "Design for Reliability Under Failure Modes (Systems Thinking Exercise)"

### Scenario

You're architecting a backend API + DB + queue + cache workload for a medium-scale application. Requirements:

-   Traffic: 5k req/s peak

-   Reads \>\> writes

-   Global latency sensitivity

-   Compliance: customer data durability required

-   Zero tolerance for silent data loss

-   Must survive partial failures (AZ outage, DB failover, cache flush, queue backlog)

-   Must support deployment with no downtime

-   Cost can be moderate (not hypersensitive like Capstone 1)

### Deliverables

-   Full distributed systems architecture diagram

-   Availability vs durability vs consistency analysis

-   RPO/RTO definition & rationale

-   Replication & failover strategy

-   Cache strategy (write-through / write-back / write-around)

-   Queue processing strategy (idempotency + backpressure plan)

-   Observability plan (metrics + logs + traces + KPIs + SLO)

-   Runbook for handling:

    -   AZ failure

    -   DB failover

    -   cache cold-start

    -   version rollback

    -   traffic surge (10× burst)

### Evaluation Focus

-   Failure modeling maturity

-   Reliability engineering fundamentals

-   Real-world DR/BCP reasoning

-   SLO/SLA vocabulary fluency

-   Consistency model reasoning (eventual vs strong)

-   Queue + cache + DB interplay understanding

# Capstone 4 --- "Introduce CI/CD to Enterprise Without Breaking Compliance"

### Scenario

A large enterprise deploys apps manually. Compliance mandates approvals, audit logs, and security scans. The goal is to introduce CI/CD without violating compliance or causing accidental prod deploys.

### Deliverables

-   CI/CD architecture

-   Security scanning + approvals + audit logging

-   Separation of duties (dev vs ops vs approver)

-   Rollback flow

-   Compliance alignment (SOC2 / ISO-inspired)

-   Risk register

### Evaluation Focus

-   Governance + controls + security

-   Policy-aware automation

-   Realistic rollout sequencing

# Capstone 5 --- "Design Observability for a Microservices-Based Product"

### Scenario

The product team runs 12 microservices but is blind during incidents. No metrics, logs, or traces tied together.

### Deliverables

-   Full observability plan

-   Metrics + logs + traces + SLOs + dashboards

-   Alerting & escalation policies

-   Incident runbook

-   Cross-service trace design

### Evaluation Focus

-   Observability literacy

-   SLO/SLA thinking

-   Incident & reliability culture

# Capstone 6 --- "Containerize Legacy Multi-Process App With Shared State"

### Scenario

Legacy app uses shared filesystem state + multiple worker processes + cron tasks. Containerization adds complexity around shared state consistency.

### Deliverables

-   Containerization strategy

-   Shared state redesign (volumes / object storage / DB)

-   Cron job handling (sidecar / platform scheduler)

-   Rollout + rollback design

-   Operational risks

### Evaluation Focus

-   State management inside container models

-   Refactoring without rewriting monolith

-   Legacy → modern compromise tradeoffs

# Capstone 7 --- "Cost Optimization Audit for a Cloud-Native Startup"

### Scenario

Startup burns \$12k/month in AWS spend. Product traffic doesn't justify expense. No one knows where costs originate.

### Deliverables

-   Cost audit (compute, storage, bandwidth, logging)

-   CloudWatch logging/metrics spend strategy

-   Resource right-sizing plan

-   Spot/RI/Fargate/Serverless comparison

-   Before/after cost model

### Evaluation Focus

-   FinOps awareness

-   Pragmatic vs purist optimization

-   Cost vs performance vs risk

# Capstone 8 --- "Multi-Region Deployment for Global Latency Reduction"

### Scenario

Users across US, EU, and Asia suffer latency. System must serve reads low-latency; writes must remain consistent enough for UX needs.

### Deliverables

-   Multi-region architecture

-   Data consistency strategy

-   Global DNS + CDN plan

-   RPO/RTO + failover

-   Latency SLA comparison

### Evaluation Focus

-   Geo-distribution reasoning

-   Consistency vs performance tradeoffs

-   DR + failover maturity

# Capstone 9 --- "Build Secure Dev Environments for Contractor Teams"

### Scenario

External contractors need access to development tools, but production data + infra must remain protected.

### Deliverables

-   IAM segmentation

-   VPC/network isolation

-   Access control policy

-   Production data sanitization workflow

-   Audit logging strategy

### Evaluation Focus

-   Security + governance

-   Least privilege enforcement

-   Dev vs staging vs prod isolation

# Capstone 10 --- "Scale a Queued Processing System Under Burst Load"

### Scenario

Batch ingestion spikes 20× during brief time windows. System must handle backpressure without cascading failure.

### Deliverables

-   Queue + worker architecture

-   Idempotency strategy

-   Backpressure plan (drop / delay / throttle / fail)

-   Observability + metrics for queue depth

-   Scaling strategy (horizontal vs vertical)

### Evaluation Focus

-   Distributed systems reasoning

-   Queue semantics

-   Idempotency + retry behavior

# Capstone 11 --- "Implement Blue/Green + Canary Deployment Strategy"

### Scenario

Product introduces high-risk features weekly. CTO demands lower failure blast radius without slowing deployment velocity.

### Deliverables

-   Blue/green rollout

-   Canary traffic splitting logic

-   Health checks + rollback signals

-   Monitoring KPIs

-   Dashboard for release safety

### Evaluation Focus

-   Deployment safety culture

-   Canaries vs feature flags vs toggles

-   Rollback maturity

# Capstone 12 --- "Disaster Recovery Plan for Regulated Business Data"

### Scenario

Client handles financial records. Compliance requires strict durability + auditable backup + verifiable restore.

### Deliverables

-   Backup schedule + retention policy

-   RPO/RTO justification

-   Restore procedures (tested)

-   Data sanitization rules

-   Audit documentation template

### Evaluation Focus

-   Compliance & risk management

-   Practical DR/BCP literacy

-   Backup testing reality

# Capstone 13 --- "Evaluate Serverless vs Containers vs VMs for API Platform"

### Scenario

Technical leadership debates platform direction. All three deployment models are viable.

### Deliverables

-   Side-by-side evaluation table

-   Cost comparison (steady + burst)

-   Operational complexity comparison

-   Latency + throughput constraints

-   Recommendation + anti-recommendations

### Evaluation Focus

-   Tradeoff articulation

-   Constraints mapping to design

-   Nuanced reasoning vs hype

# Capstone 14 --- "Rebuild Data Pipeline with Strong RPO/RTO Requirements"

### Scenario

Pipeline ingests transactional data. Current ETL system fails during outages. Business demands \<5min RPO and \<30min RTO.

### Deliverables

-   Pipeline architecture redesign

-   Replication + checkpointing strategy

-   Failure recovery workflow

-   Observability metrics for lag + quality

-   Runbook for DR scenario

### Evaluation Focus

-   Data durability + reliability engineering

-   RPO/RTO integration

-   Pipeline as mission-critical system

# Capstone 15 --- "Implement Zero-Downtime Migrations for Production Database"

### Scenario

Monolithic DB schema changes frequently. Downtime during migrations is unacceptable.

### Deliverables

-   Migration sequencing strategy

-   Backwards compatibility rules

-   Feature flag integration

-   Fallback + rollback paths

-   Safety criteria for promotion

### Evaluation Focus

-   Hard real-world problem in ops

-   Data-first thinking

-   Rollback economics

# Capstone 16 --- "Cloud Exit Strategy (Avoid Vendor Lock-In)"

### Scenario

Company wants optionality --- retain leverage against cloud pricing + regulatory risk.

### Deliverables

-   Lock-in assessment (compute, data, IAM, networking)

-   Dual deployment strategy

-   Abstraction layers (infra as code / containerization / DB compatibility)

-   Governance + risk policy

-   Cost & latency implications

### Evaluation Focus

-   Multi-cloud realism

-   Vendor economics + geopolitics

-   Pragmatism vs abstraction overhead
[Go Back](05-systems-ops.md) | [Go Home](../README.md)
