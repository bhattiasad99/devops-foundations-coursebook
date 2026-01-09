# Module 3 --- Cloud Foundations (AWS-Focused + Cost Awareness)

## Learning Objectives

By the end of this module, the student should be able to:

-   Understand AWS global infrastructure primitives (regions, AZs, edge locations)

-   Compare compute models (EC2 vs ECS vs Lambda) and when to choose each

-   Explain IAM as the root security model of AWS and describe users, policies, and roles

-   Differentiate S3, EBS, and EFS and map use cases to storage classes

-   Describe VPC networking, subnets, gateways, security groups, and basic routing

-   Explain CloudFront and CDN concepts in the context of latency and performance

-   Recommend AWS service strategies for common architectural goals and workflows

-   Articulate tradeoffs and cost implications of different AWS services

-   Identify financial risks such as EC2 autoscaling surges, RDS overprovisioning, or CloudWatch logging verbosity

-   Speak fluently about AWS architectures even before hands-on implementation

## 3.1 Introduction to Cloud Fundamentals

Cloud computing abstracts physical infrastructure, enabling workloads to run on ephemeral and elastic machines controlled through APIs rather than cables and racks. Instead of purchasing hardware upfront, systems can scale up and down on demand while billing tracks consumption.

From a DevOps standpoint, cloud is not merely procurement convenience; it is an operational paradigm. Deployment pipelines, monitoring, compliance, networking, and cost strategy become software-defined activities rather than physical interventions. The cloud converts infrastructure into code.

### 3.1.1 Cloud as Elastic Infrastructure

Elasticity is central. Workloads may experience sudden spikes (e.g., e-commerce sale events, viral traffic). Cloud allows provisioning additional compute automatically via autoscaling, then releasing resources once demand drops.

Elasticity prevents both **under-provisioning** (downtime due to insufficient capacity) and **over-provisioning** (idle cost due to excess hardware).

### 3.1.2 Why AWS Dominates Cloud Workloads

AWS pioneered the public cloud and remains dominant for several reasons:

-   breadth of services (compute, networking, storage, data, ML, security, governance)

-   operational maturity and reliability

-   ubiquitous adoption in industry

-   partner ecosystem (vendors, consultants, trainers, hiring pipelines)

-   rich documentation and API-first design

Architectural literacy in AWS translates well to Azure and GCP, even though services differ.

## 3.2 AWS Global Architecture

AWS organizes its physical infrastructure to support fault tolerance, regulatory compliance, and latency optimization. Understanding this layout is mandatory for designing resilient applications.

### 3.2.1 Regions

A **region** is a geographical cluster of datacenters. Examples:

-   us-east-1 (N. Virginia)

-   eu-west-1 (Ireland)

-   ap-south-1 (Mumbai)

Regions matter for:

-   latency to end users

-   regulatory compliance (e.g., data sovereignty)

-   availability of specific AWS services (not uniform across all regions)

### 3.2.2 Availability Zones (AZs)

Within each region, AWS has multiple **Availability Zones**. Each AZ is a physically separate datacenter with redundant power, cooling, and connectivity. Deploying across AZs protects against failures such as power outages or localized disasters.

Resilient architectures deploy multi-AZ for:

-   RDS databases

-   ECS workloads

-   Load balanced EC2 fleets

### 3.2.3 Edge Locations

Edge locations serve CloudFront (CDN) and sometimes Lambda@Edge workloads. Their purpose is to bring content closer to users, minimizing network round trips.

Edge improves performance for static assets, media, and caching.

## 3.3 Core Compute Models

AWS offers multiple execution models. Engineers must understand the operational, economic, and architectural tradeoffs of each.

### 3.3.1 EC2 (Virtual Machines)

EC2 provides VM instances that behave like regular servers. Engineers manage:

-   OS selection

-   patches & updates

-   security hardening

-   scaling policies

-   networking configuration

Advantages:

-   maximum control

-   durable and predictable runtime

-   stateful services possible

Disadvantages:

-   requires more operational burden

-   poor fit for event-driven or bursty workloads

-   can be misconfigured leading to idle cost burn

### 3.3.2 ECS (Containers)

ECS orchestrates containers, often paired with Fargate (serverless compute for containers). Engineers manage containerization and deployment primitives rather than servers.

Advantages:

-   less OS and patching overhead

-   cleaner deployment artifacts (container images)

-   suited for microservices

Disadvantages:

-   still operationally complex

-   requires container literacy

-   networking becomes more diagnostic-heavy

### 3.3.3 Lambda (Serverless Functions)

Lambda executes functions in response to events:

-   API Gateway

-   S3 uploads

-   SNS notifications

-   CRON schedules

-   queue consumption (SQS)

Advantages:

-   zero idle cost

-   automatic scaling

-   minimal operations

Disadvantages:

-   cold start latency

-   vendor lock-in risks

-   architectural shift toward stateless/event-driven design

-   may outprice EC2 for heavy sustained load

### 3.3.4 Choosing VM vs Container vs Serverless

Decision drivers:

  -----------------------------------------------------------------------------------------------
  **Constraint**        **VM (EC2)**      **Container (ECS/Fargate)**   **Serverless (Lambda)**
  --------------------- ----------------- ----------------------------- -------------------------
  Operational control   High              Medium                        Low

  Scaling model         Manual/auto       Auto/managed                  Automatic

  Cost under idle       High              Medium                        Zero

  Architecture style    Stateful/legacy   Microservices                 Event-driven

  Throughput            High              High                          Burst

  Complexity            OS + app          app + container               app only
  -----------------------------------------------------------------------------------------------

A senior DevOps engineer must be able to articulate such tradeoffs clearly during design reviews.

## 3.4 Identity & Access Management (IAM)

IAM is the security backbone of AWS. Every action invoked against AWS APIs must be permitted through IAM policies.

### 3.4.1 IAM Users, Roles & Policies

IAM defines:

-   **Users:** individuals or systems

-   **Roles:** identities assumed temporarily by services

-   **Policies:** JSON-based permission documents

Example policy conceptually:

{

\"Effect\": \"Allow\",

\"Action\": \"s3:\*\",

\"Resource\": \"\*\"

}

Policies can be extremely granular, limiting precise actions on specific resources.

### 3.4.2 Trust Relationships

Services must trust each other to assume roles. For example:

-   ECS task assumes role to read S3

-   Lambda function assumes role to write CloudWatch logs

-   EC2 instance assumes role to pull secrets from SSM

Trust boundaries enforce least privilege.

### 3.4.3 Governance & Principle of Least Privilege

Least privilege reduces blast radius. If credentials are compromised, an attacker should not be able to delete S3 buckets, create users, or issue expensive compute.

IAM misunderstandings are a top cause of security breaches and compliance failures.

## 3.5 Storage Services Comparison

AWS storage is not one thing---it spans multiple paradigms.

### 3.5.1 S3 (Object Storage)

S3 stores immutable objects (files) addressed by key. Ideal for:

-   backups

-   logs

-   static hosting

-   ML datasets

-   archives

Key properties:

-   extremely durable (11 9's)

-   scalable

-   global integrations

-   low cost

-   eventual consistency semantics

### 3.5.2 EBS (Block Storage)

Attached volumes for EC2. Behaves like a disk:

-   formatted with filesystem

-   supports low-latency block I/O

-   used for databases or application servers

Downside: tied to a single AZ and EC2 instance (though snapshots mitigate portability).

### 3.5.3 EFS (Network File System)

POSIX file system shared across multiple EC2 instances. Popular for distributed workloads needing shared artifacts or persistent state.

Downside: pricing scales unexpectedly if storage growth is unbounded.

### 3.5.4 Choosing S3 vs EBS vs EFS

Rational mapping:

  -----------------------------------------------------------------------
  **Need**                                                   **Use**
  ---------------------------------------------------------- ------------
  Durable static data                                        S3

  Low-latency disk for DB                                    EBS

  Shared filesystem across EC2                               EFS
  -----------------------------------------------------------------------

Storage selection impacts performance and cost.

## 3.6 Networking in AWS (VPC Concepts)

Cloud networking abstracts traditional datacenter constructs (routers, switches, firewalls, NAT, and CIDR planning) into programmable APIs. A DevOps engineer must be fluent in VPC mental models because almost every production workload touches VPC boundaries.

### 3.6.1 VPCs

A **Virtual Private Cloud (VPC)** is an isolated network defined within a region. Within a VPC, the engineer provisions:

-   subnets

-   route tables

-   gateways

-   security groups

-   NAT

-   CIDR ranges

Isolation prevents untrusted traffic from reaching private workloads.

### 3.6.2 Subnets (Public vs Private)

Subnets subdivide VPC IP ranges. They are categorized by exposure:

-   **Public subnets** → route to Internet Gateway (IGW) enabling inbound access (e.g., load balancers)

-   **Private subnets** → route only outbound via NAT or not at all (e.g., databases, internal APIs)

Private networking reduces attack surfaces significantly.

### 3.6.3 Security Groups & NACLs

AWS provides layered controls:

-   **Security Groups** (SGs) operate at instance/container level and are stateful

-   **Network ACLs** (NACLs) operate at subnet level and are stateless

Example SG rule:

  --------------------------------------------------------------------------
  **Direction**     **Source**      **Port**   **Protocol**    **Action**
  ----------------- --------------- ---------- --------------- -------------
  Inbound           0.0.0.0/0       443        TCP             Allow

  --------------------------------------------------------------------------

Example NACL rule would require explicit allow rules for both directions.

### 3.6.4 NAT Gateways & Internet Gateways

Network gateways define traffic paths:

-   **Internet Gateway (IGW):** allows internet inbound/outbound for public subnets

-   **NAT Gateway:** enables private subnets to make outbound requests without exposing inbound routes

Example scenario:

A private DB instance needs to pull package updates or reach S3 without becoming internet-exposed.

### 3.6.5 Route Tables

Route tables control traffic flow between subnets and gateways. A typical design might route:

0.0.0.0/0 → nat-gateway → private-subnet

0.0.0.0/0 → internet-gateway → public-subnet

VPC-level routing remains a major debugging domain when services fail to communicate even when DNS and app logic are correct.

## 3.7 CDN Basics

Content Delivery Networks reduce latency by caching static and semi-static assets close to users.

### 3.7.1 CloudFront Overview

CloudFront distributes content through edge locations. Requests hit edge first, then fall back to origin if uncached.

Popular for:

-   SPAs (React, Vue, Angular)

-   images/video

-   API caching

-   SSR workloads (with Lambda@Edge)

### 3.7.2 CDN Performance & Security Benefits

Benefits include:

-   reduced latency

-   lower origin load

-   improved throughput

-   built-in DDoS mitigation

-   TLS certificate management

-   geo-blocking and routing policies

CDNs help with global availability without multi-region deployment complexity.

## 3.8 Architectural Decision-Making in AWS

### 3.8.1 Common Goals in Cloud Architectures

Typical DevOps tasks include:

-   Deploying application backends

-   Hosting frontends

-   Automating CI/CD pipelines

-   Designing test/staging environments

-   Persisting structured or unstructured data

-   Handling scaling and resilience

### 3.8.2 Infrastructure Options Spectrum

Infrastructure selection spans from maximum control to maximum abstraction:

EC2 → ECS → Fargate → Lambda → Managed SaaS services

The more abstract the service, the more AWS manages --- but the less granular control you retain.

## 3.9 AWS Service Strategies for Common Goals

A fluent cloud engineer must be able to recommend multiple solutions for a single need and articulate tradeoffs clearly.

### 3.9.1 Hosting a Web Backend

Possible strategies:

**Option A: EC2 + Load Balancer**

-   Pros: control, flexibility, stateful support

-   Cons: operational overhead, patching, scaling complexity

**Option B: ECS + Fargate**

-   Pros: container workflows, reduced ops, auto-scaling

-   Cons: container orchestration requires literacy

**Option C: Lambda + API Gateway**

-   Pros: zero idle cost, event-driven, fast iteration for small workloads

-   Cons: cold starts, concurrency limitations, cost spikes under steady high throughput

### 3.9.2 CI/CD Pipeline

Strategies vary by governance preference:

**Option A: CodePipeline**

-   tightly integrated AWS-first pipeline

**Option B: GitHub Actions + deployment via AWS**

-   decouples CI logic from infrastructure

-   increasingly dominant in modern teams

**Option C: Terraform + Scripts**

-   multi-cloud portable

-   declarative infra definition

### 3.9.3 Staging + Production Environments

Consistent patterns:

-   separate VPCs

-   separate subnets

-   separate databases

-   tighter IAM for production

Tradeoffs center around blast radius and cost.

### 3.9.4 Static Frontend Hosting

**Option A: S3 + CloudFront**

-   canonical pattern for SPAs, cheapest and most scalable

**Option B: Amplify Hosting**

-   reduces cognitive overhead for fullstack teams

**Option C: EC2 Nginx**

-   suboptimal, but sometimes chosen for legacy patterns

### 3.9.5 Data Persistence

**Option A: RDS**

-   relational, strong consistency, expensive for low-traffic apps

**Option B: DynamoDB**

-   NoSQL, auto-scaling, predictable performance, cost scales with request volume

**Option C: S3**

-   object storage for logs/backups/snapshots/static content

## 3.10 Tradeoffs & Architectural Reasoning

### 3.10.1 Operational Complexity

Higher abstraction → less operational burden but more vendor lock-in.

### 3.10.2 Performance & Latency

Application workload patterns dictate choice:

-   steady long-running processes → EC2/ECS

-   bursty event-driven workloads → Lambda

-   global reads → CloudFront + DynamoDB

### 3.10.3 Security & Privilege Boundaries

IAM + VPC boundaries enforce least privilege while enabling service interconnectivity.

## 3.11 Cost Awareness & Financial Risk Management

Here lies one of the most misunderstood aspects of cloud operations: cloud risk is financial as well as technical. Engineers with strong cost literacy are more valuable in enterprises than engineers who only optimize performance.

### 3.11.1 EC2 Under Load

Auto-scaling clusters can scale out rapidly during surges, and EC2 capacity under sustained load can burn budget quickly.

Risk factors:

-   misconfigured auto-scaling policies

-   traffic spikes

-   DDoS-like events

-   inefficient application code leading to high CPU/Memory needs

### 3.11.2 RDS Costs for Small Apps

RDS provides convenience:

-   backups

-   failover

-   replicas

-   patching

-   monitoring

But small apps often don't need these luxuries and pay significant premiums. Realistic alternatives may include:

-   SQLite on EBS

-   DynamoDB for certain workloads

-   Serverless Postgres/Aurora variants

### 3.11.3 CloudWatch Logging Costs

CloudWatch charges based on:

-   ingestion volume

-   retention

-   queries (in logs insights)

High verbosity logs in dev/staging environments commonly inflate bills silently.

### 3.11.4 Serverless Cost Pitfalls

Lambda has zero idle cost, but can become more expensive than EC2 under sustained high throughput (TP99 latency optimizations matter here).

### 3.11.5 Egress Bandwidth Charges

Data leaving AWS costs money. Serving public video or streaming media from S3 might incur more cost from egress than from storage.

## 3.12 Service Recommendations by Scenario

### 3.12.1 Low-Traffic MVP

Best pattern:

-   Lambda

-   API Gateway

-   DynamoDB

-   S3 + CloudFront

Minimizes ops + cost.

### 3.12.2 High-Throughput API

Best pattern:

-   ECS

-   Fargate

-   ALB

-   RDS

-   ElastiCache

Prioritizes performance + scaling.

### 3.12.3 Enterprise Controlled Environments

Best pattern:

-   VPC peering

-   SSO + IAM federation

-   Private subnets

-   RDS with multi-AZ

-   central logging + audit posture

## 3.13 Speaking Fluently About AWS Without Hands-On

Cloud fluency does not require prior console usage; it requires conceptual frameworks and correct vocabulary.

### 3.13.1 Vocabulary & Semantic Fluency

Examples:

-   AZ ≠ region

-   SG ≠ NACL

-   NAT ≠ IGW

-   EBS ≠ S3 ≠ EFS

-   Lambdas are not containers

-   ECS is not just Docker

-   CloudFront ≠ load balancer

### 3.13.2 Mental Models for Cloud Architecture

Cloud diagrams often collapse to:

client → edge → LB → compute → data

### 3.13.3 Architecture Diagrams

Visual reasoning accelerates onboarding, security reviews, and failure analysis.

## 3.14 Module Review & Terminology

Recaps core cloud vocabulary and primitives for retention.

# Analogies

### Cloud Regions as Countries

Regions act like sovereign states, each with their own datacenters (AZs).

### VPCs as Private Neighborhoods

Subnets become streets; security groups are fences; NAT is the gated exit.

### EC2 as Renting a House

Control everything but pay for idle space.

### Lambda as Ride-Hailing

Only pay when used; zero idle; highly optimized for bursts.

### IAM as Immigration Control

Determines who can enter, what they can do, and how far they can go.

### CDN as Local Libraries

Copies of static content stored near readers for lower latency.

# Diagrams (Mermaid + ASCII)

### Mermaid: Backend Architecture Flow
```mermaid
flowchart LR

Client \--\> Edge\[CloudFront CDN\]

Edge \--\> LB\[ALB\]

LB \--\> ECS\[ECS Service\]

ECS \--\> DB\[(RDS)\]
```
### ASCII: VPC Subnetting
```
\[ VPC 10.0.0.0/16 \]

\|\-- Public Subnet 10.0.1.0/24

\|\-- Private Subnet 10.0.2.0/24
```
### Mermaid: IAM Role Assumption
```mermaid
sequenceDiagram

User-\>\>STS: AssumeRole

STS\--\>\>User: Temp Credentials

User-\>\>S3: Access via Role
```
# Exercises (Ungraded)

1.  Compare EC2 vs ECS vs Lambda for a chat app backend.

2.  Choose storage: S3 vs EBS vs EFS for an ML training dataset.

3.  Identify which subnet (public/private) is appropriate for:

    -   Load balancer

    -   Database

    -   Internal services

4.  Explain three reasons RDS may be expensive for small startups.

5.  Explain why CloudWatch logging can silently inflate billing.

# Solved Exercises

1.  Chat app → ECS or EC2 for long-lived WebSocket sessions; Lambda unsuitable for persistent connections.

2.  ML datasets → S3 (scalable, durable, cheap).

3.  LB → public, DB → private, internal APIs → private.

4.  RDS: managed failover, multi-AZ, backups, provisioned IOPS, fixed instance types.

5.  Logging: ingestion + retention + insights queries all bill independently.

# Mini-Scenarios

### Scenario A: EC2 Autoscaling Shock

Traffic spike causes 40x EC2 scale-out, bill surges overnight.

### Scenario B: Logging Burn

Ingesting 200GB/day debug logs into CloudWatch; finance panics.

### Scenario C: Incorrect Subnet Placement

DB deployed in public subnet exposing it to internet scans.

### Scenario D: Developer Misuses RDS

Tiny startup pays enterprise-grade managed Postgres they barely query.

# Quiz Questions (answers at end)

1.  Define region vs AZ.

2.  Describe S3 vs EBS vs EFS.

3.  Why might Lambda become expensive?

4.  What is a NAT gateway used for?

5.  Why is IAM central to AWS?

6.  Which service handles CDN caching?

7.  Why is egress cost significant?

8.  Which tool hosts static SPAs cheaply?

### Quiz Answers

1.  Region = geographic cluster; AZ = datacenter inside region.

2.  S3=object, EBS=block, EFS=shared filesystem.

3.  At sustained high throughput.

4.  Private subnet outbound internet.

5.  It mediates all permissions and API calls.

6.  CloudFront.

7.  Data leaving AWS is billed.

8.  S3 + CloudFront.

# Teaching Notes (Instructor Guidance)

-   Emphasize cost literacy --- rare but high-value DevOps skill.

-   Use real billing anecdotes to motivate student curiosity.

-   Encourage architectural debates: VM vs container vs serverless.

-   Introduce diagrams early; cloud is spatial and layered.

-   Encourage narrative labs involving NAT/SG/IAM misconfiguration debugging.

-   Reinforce IAM vocabulary --- prevents major misunderstandings.

-   Have students explain designs verbally; fluency matters in interviews and architecture reviews.

