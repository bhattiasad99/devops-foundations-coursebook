[[Module 1 --- Linux & Git Foundations]{.underline}](#module-1-linux-git-foundations)

> [[Learning Objectives]{.underline}](#learning-objectives)

[[1.1 Introduction to Linux in DevOps]{.underline}](#introduction-to-linux-in-devops)

> [[1.1.1 History & Philosophy of Linux]{.underline}](#history-philosophy-of-linux)
>
> [[1.1.2 Linux in Modern Infrastructure]{.underline}](#linux-in-modern-infrastructure)

[[1.2 Working with the Linux Filesystem]{.underline}](#working-with-the-linux-filesystem)

> [[1.2.1 Filesystem Hierarchy]{.underline}](#filesystem-hierarchy)
>
> [[1.2.2 Navigating the Filesystem]{.underline}](#navigating-the-filesystem)
>
> [[1.2.3 Creating, Moving & Deleting Files]{.underline}](#creating-moving-deleting-files)
>
> [[1.2.4 Understanding File Types]{.underline}](#understanding-file-types)

[[1.3 File Viewing & Text Utilities]{.underline}](#file-viewing-text-utilities)

> [[1.3.1 Reading & Paging Files]{.underline}](#reading-paging-files)
>
> [[1.3.2 Searching Within Files]{.underline}](#searching-within-files)
>
> [[1.3.3 Sorting & Filtering]{.underline}](#sorting-filtering)

[[1.4 Permissions, Ownership & Users]{.underline}](#permissions-ownership-users)

> [[1.4.1 Understanding Permissions]{.underline}](#understanding-permissions)
>
> [[1.4.2 Changing Permissions & Ownership]{.underline}](#changing-permissions-ownership)
>
> [[1.4.3 Users, Groups & Identity]{.underline}](#users-groups-identity)

[[1.5 Processes & System Monitoring]{.underline}](#processes-system-monitoring)

> [[1.5.1 Listing & Inspecting Processes]{.underline}](#listing-inspecting-processes)
>
> [[1.5.2 Killing Processes & Signals]{.underline}](#killing-processes-signals)
>
> [[1.5.3 System Logs & Services]{.underline}](#system-logs-services)

[[1.6 Bash Scripting Foundations]{.underline}](#bash-scripting-foundations)

> [[1.6.1 Why Automation Matters]{.underline}](#why-automation-matters)
>
> [[1.6.2 Variables, Loops & Conditionals]{.underline}](#variables-loops-conditionals)
>
> [[1.6.3 Writing & Executing Scripts]{.underline}](#writing-executing-scripts)

[[1.7 Git Foundations for DevOps]{.underline}](#git-foundations-for-devops)

> [[1.7.1 What Problem Git Solves]{.underline}](#what-problem-git-solves)
>
> [[1.7.2 Repositories (init, clone)]{.underline}](#repositories-init-clone)
>
> [[1.7.3 Local Workflow (add, commit)]{.underline}](#local-workflow-add-commit)

[[1.8 Working With Remote Repositories]{.underline}](#working-with-remote-repositories)

> [[1.8.1 Understanding Remotes (origin, upstream)]{.underline}](#understanding-remotes-origin-upstream)
>
> [[1.8.2 Pulling & Pushing Changes]{.underline}](#pulling-pushing-changes)
>
> [[1.8.3 Basic Branching & Merging]{.underline}](#basic-branching-merging)
>
> [[1.9 Practical Logs & Pipelines]{.underline}](#practical-logs-pipelines)
>
> [[1.9.1 Inspecting Application Logs]{.underline}](#inspecting-application-logs)
>
> [[1.9.2 Command Pipelines (\|)]{.underline}](#command-pipelines)
>
> [[1.9.3 Real-World Debugging Scenarios]{.underline}](#real-world-debugging-scenarios)
>
> [[1.10 Capstone Mini-Labs]{.underline}](#capstone-mini-labs)
>
> [[1.10.1 Linux Navigation & Permissions Lab]{.underline}](#linux-navigation-permissions-lab)
>
> [[1.10.2 Git Local-to-Remote Workflow Lab]{.underline}](#git-local-to-remote-workflow-lab)
>
> [[1.10.3 Reading Logs & Debugging Lab]{.underline}](#reading-logs-debugging-lab)

[[Supplements]{.underline}](#supplements)

[[2. Analogies for Conceptual Understanding]{.underline}](#analogies-for-conceptual-understanding)

> [[Filesystem as a City]{.underline}](#filesystem-as-a-city)
>
> [[Permissions as Building Access]{.underline}](#permissions-as-building-access)
>
> [[Processes as Workers in a Factory]{.underline}](#processes-as-workers-in-a-factory)
>
> [[Git as a Time Machine for Code]{.underline}](#git-as-a-time-machine-for-code)

[[3. Diagrams (Mermaid + ASCII)]{.underline}](#diagrams-mermaid-ascii)

> [[3.1 Git Workflow Diagram (Mermaid)]{.underline}](#git-workflow-diagram-mermaid)
>
> [[3.2 Git Branching (ASCII)]{.underline}](#git-branching-ascii)
>
> [[3.3 Linux Pipeline Diagram (Mermaid)]{.underline}](#linux-pipeline-diagram-mermaid)
>
> [[3.4 Permissions Encoding (ASCII)]{.underline}](#permissions-encoding-ascii)

[[4. Exercises (Ungraded Practice)]{.underline}](#exercises-ungraded-practice)

> [[Exercise 1 --- Filesystem Navigation]{.underline}](#exercise-1-filesystem-navigation)
>
> [[Exercise 2 --- Permissions]{.underline}](#exercise-2-permissions)
>
> [[Exercise 3 --- Log Filtering]{.underline}](#exercise-3-log-filtering)
>
> [[Exercise 4 --- Git Workflow]{.underline}](#exercise-4-git-workflow)
>
> [[Exercise 5 --- Simple Debug Pipeline]{.underline}](#exercise-5-simple-debug-pipeline)

[[5. Solved Exercises]{.underline}](#solved-exercises)

> [[Solution to Exercise 1]{.underline}](#solution-to-exercise-1)
>
> [[Solution to Exercise 2]{.underline}](#solution-to-exercise-2)
>
> [[Solution to Exercise 3]{.underline}](#solution-to-exercise-3)
>
> [[Solution to Exercise 4]{.underline}](#solution-to-exercise-4)
>
> [[Solution to Exercise 5]{.underline}](#solution-to-exercise-5)

[[6. Mini-Scenarios (Applied Thinking)]{.underline}](#mini-scenarios-applied-thinking)

> [[Scenario 1 --- Deployment Failure]{.underline}](#scenario-1-deployment-failure)
>
> [[Scenario 2 --- Permission Denied]{.underline}](#scenario-2-permission-denied)
>
> [[Scenario 3 --- Git Conflict]{.underline}](#scenario-3-git-conflict)
>
> [[Scenario 4 --- Service Not Restarting]{.underline}](#scenario-4-service-not-restarting)

[[7. Quiz Questions (with answers at end)]{.underline}](#quiz-questions-with-answers-at-end)

> [[Quiz Answers]{.underline}](#quiz-answers)

[[8. Teaching Notes (Instructor Guidance)]{.underline}](#teaching-notes-instructor-guidance)

[[Module 2 --- Networking Fundamentals]{.underline}](#module-2-networking-fundamentals)

> [[Learning Objectives]{.underline}](#learning-objectives-1)

[[2.1 Introduction to Networking in DevOps]{.underline}](#introduction-to-networking-in-devops)

> [[2.1.1 Networking as the Hidden Layer of Software]{.underline}](#networking-as-the-hidden-layer-of-software)
>
> [[2.1.2 Concept of the Request Path]{.underline}](#concept-of-the-request-path)

[[2.2 Browser to Server Request Flow]{.underline}](#browser-to-server-request-flow)

> [[2.2.1 DNS Resolution Phase]{.underline}](#dns-resolution-phase)
>
> [[2.2.2 TCP Handshake Phase]{.underline}](#tcp-handshake-phase)
>
> [[2.2.3 HTTP Request/Response Exchange]{.underline}](#http-requestresponse-exchange)
>
> [[2.2.4 TLS & Encryption Layer]{.underline}](#tls-encryption-layer)

[[2.3 Internet Identifiers: Domains, IPs, Ports & Protocols]{.underline}](#internet-identifiers-domains-ips-ports-protocols)

> [[2.3.1 Domain Names vs IP Addresses]{.underline}](#domain-names-vs-ip-addresses)
>
> [[2.3.2 Ports as Service Endpoints]{.underline}](#ports-as-service-endpoints)
>
> [[2.3.3 Application vs Transport vs Network Protocols]{.underline}](#application-vs-transport-vs-network-protocols)

[[2.4 DNS Name Resolution]{.underline}](#dns-name-resolution)

> [[2.4.1 DNS as a Hierarchical System]{.underline}](#dns-as-a-hierarchical-system)
>
> [[2.4.2 DNS Records & Their Purpose]{.underline}](#dns-records-their-purpose)
>
> [[2.4.3 DNS Time to Live (TTL) & Caching]{.underline}](#dns-time-to-live-ttl-caching)

[[2.5 DNS Records Deep Dive]{.underline}](#dns-records-deep-dive)

> [[2.5.1 A & AAAA Records]{.underline}](#a-aaaa-records)
>
> [[2.5.2 CNAME Records]{.underline}](#cname-records)
>
> [[2.5.3 MX Records]{.underline}](#mx-records)
>
> [[2.5.4 TXT Records]{.underline}](#txt-records)
>
> [[2.5.5 NS Records]{.underline}](#ns-records)
>
> [[2.5.6 SOA Record]{.underline}](#soa-record)

[[2.6 Configuring DNS for a Custom Domain]{.underline}](#configuring-dns-for-a-custom-domain)

> [[2.6.1 Domain Registrar vs DNS Provider vs Hosting]{.underline}](#domain-registrar-vs-dns-provider-vs-hosting)
>
> [[2.6.2 Pointing a Domain to a Web Server]{.underline}](#pointing-a-domain-to-a-web-server)
>
> [[2.6.3 SSL Certificates & Domain Validation]{.underline}](#ssl-certificates-domain-validation)

[[2.7 Transport Protocols: TCP vs UDP]{.underline}](#transport-protocols-tcp-vs-udp)

> [[2.7.1 TCP Handshake & Reliability Guarantees]{.underline}](#tcp-handshake-reliability-guarantees)
>
> [[2.7.2 UDP Speed & Stateless Delivery]{.underline}](#udp-speed-stateless-delivery)
>
> [[2.7.3 Choosing TCP vs UDP in Real Systems]{.underline}](#choosing-tcp-vs-udp-in-real-systems)

[[2.8 IP Addressing, NAT & Private Networking]{.underline}](#ip-addressing-nat-private-networking)

> [[2.8.1 IPv4 vs IPv6]{.underline}](#ipv4-vs-ipv6)
>
> [[2.8.2 Public vs Private IP Addresses]{.underline}](#public-vs-private-ip-addresses)
>
> [[2.8.3 NAT (Network Address Translation)]{.underline}](#nat-network-address-translation)
>
> [[2.8.4 Port Forwarding]{.underline}](#port-forwarding)

[[2.9 Subnetting, CIDR & Masking]{.underline}](#subnetting-cidr-masking)

> [[2.9.1 What is a Subnet & Why It Matters]{.underline}](#what-is-a-subnet-why-it-matters)
>
> [[2.9.2 CIDR Notation (/24, /16, /32)]{.underline}](#cidr-notation-24-16-32)
>
> [[2.9.3 Calculating Ranges From CIDR]{.underline}](#calculating-ranges-from-cidr)

[[2.10 Routing, Firewalls & Proxies]{.underline}](#routing-firewalls-proxies)

> [[2.10.1 Routers & Routing Tables]{.underline}](#routers-routing-tables)
>
> [[2.10.2 Firewalls & Access Control]{.underline}](#firewalls-access-control)
>
> [[2.10.3 Proxies & Reverse Proxies]{.underline}](#proxies-reverse-proxies)

[[2.11 Common Cloud Network Architectures]{.underline}](#common-cloud-network-architectures)

> [[2.11.1 Subnets, Gateways & Load Balancers]{.underline}](#subnets-gateways-load-balancers)
>
> [[2.11.2 Private Subnets vs Public Subnets]{.underline}](#private-subnets-vs-public-subnets)
>
> [[2.11.3 Service Discovery & Internal DNS]{.underline}](#service-discovery-internal-dns)

[[2.12 Debugging & Troubleshooting Networking]{.underline}](#debugging-troubleshooting-networking)

> [[2.12.1 DNS Works But App Fails]{.underline}](#dns-works-but-app-fails)
>
> [[2.12.2 Ping, Traceroute & Curl as Debug Tools]{.underline}](#ping-traceroute-curl-as-debug-tools)
>
> [[2.12.3 Debugging Ports & Services]{.underline}](#debugging-ports-services)
>
> [[2.12.4 Common Operational Failure Modes]{.underline}](#common-operational-failure-modes)

[[3. Analogies for Conceptual Understanding]{.underline}](#analogies-for-conceptual-understanding-1)

> [[3.1 DNS as a Phonebook]{.underline}](#dns-as-a-phonebook)
>
> [[3.2 TCP as Registered Mail]{.underline}](#tcp-as-registered-mail)
>
> [[3.3 UDP as a Broadcast Radio]{.underline}](#udp-as-a-broadcast-radio)
>
> [[3.4 Subnets as Neighborhood Blocks]{.underline}](#subnets-as-neighborhood-blocks)
>
> [[3.5 Firewalls as Security Guards]{.underline}](#firewalls-as-security-guards)
>
> [[3.6 Load Balancers as Reception Desks]{.underline}](#load-balancers-as-reception-desks)

[[4. Diagrams (Mermaid + ASCII)]{.underline}](#diagrams-mermaid-ascii-1)

> [[4.1 Browser Request Flow (Mermaid)]{.underline}](#browser-request-flow-mermaid)
>
> [[4.2 Network Layers (ASCII)]{.underline}](#network-layers-ascii)
>
> [[4.3 Cloud Private/Public Subnets (Mermaid)]{.underline}](#cloud-privatepublic-subnets-mermaid)
>
> [[4.4 CIDR Allocation (ASCII)]{.underline}](#cidr-allocation-ascii)

[[5. Exercises (Ungraded Practice)]{.underline}](#exercises-ungraded-practice-1)

> [[Exercise 1 --- DNS Lookup]{.underline}](#exercise-1-dns-lookup)
>
> [[Exercise 2 --- TCP vs UDP]{.underline}](#exercise-2-tcp-vs-udp)
>
> [[Exercise 3 --- CIDR Reasoning]{.underline}](#exercise-3-cidr-reasoning)
>
> [[Exercise 4 --- Debugging Scenario]{.underline}](#exercise-4-debugging-scenario)
>
> [[Exercise 5 --- Port Logic]{.underline}](#exercise-5-port-logic)

[[6. Solved Exercises]{.underline}](#solved-exercises-1)

> [[Solution 1]{.underline}](#solution-1)
>
> [[Solution 2]{.underline}](#solution-2)
>
> [[Solution 3]{.underline}](#solution-3)
>
> [[Solution 4]{.underline}](#solution-4)
>
> [[Solution 5]{.underline}](#solution-5)

[[7. Mini-Scenarios (Applied Thinking)]{.underline}](#mini-scenarios-applied-thinking-1)

> [[Scenario A --- DNS is Correct; App Still Down]{.underline}](#scenario-a-dns-is-correct-app-still-down)
>
> [[Scenario B --- Private DB Cannot Be Reached]{.underline}](#scenario-b-private-db-cannot-be-reached)
>
> [[Scenario C --- Multi-Region Deployment Failing]{.underline}](#scenario-c-multi-region-deployment-failing)

[[8. Quiz Questions (answers at end)]{.underline}](#quiz-questions-answers-at-end)

> [[Quiz Answers]{.underline}](#quiz-answers-1)

[[9. Teaching Notes (Instructor Guidance)]{.underline}](#teaching-notes-instructor-guidance-1)

[[Module 3 --- Cloud Foundations (AWS-Focused + Cost Awareness)]{.underline}](#module-3-cloud-foundations-aws-focused-cost-awareness)

> [[Learning Objectives]{.underline}](#learning-objectives-2)

[[3.1 Introduction to Cloud Fundamentals]{.underline}](#introduction-to-cloud-fundamentals)

> [[3.1.1 Cloud as Elastic Infrastructure]{.underline}](#cloud-as-elastic-infrastructure)
>
> [[3.1.2 Why AWS Dominates Cloud Workloads]{.underline}](#why-aws-dominates-cloud-workloads)

[[3.2 AWS Global Architecture]{.underline}](#aws-global-architecture)

> [[3.2.1 Regions]{.underline}](#regions)
>
> [[3.2.2 Availability Zones (AZs)]{.underline}](#availability-zones-azs)
>
> [[3.2.3 Edge Locations]{.underline}](#edge-locations)

[[3.3 Core Compute Models]{.underline}](#core-compute-models)

> [[3.3.1 EC2 (Virtual Machines)]{.underline}](#ec2-virtual-machines)
>
> [[3.3.2 ECS (Containers)]{.underline}](#ecs-containers)
>
> [[3.3.3 Lambda (Serverless Functions)]{.underline}](#lambda-serverless-functions)
>
> [[3.3.4 Choosing VM vs Container vs Serverless]{.underline}](#choosing-vm-vs-container-vs-serverless)

[[3.4 Identity & Access Management (IAM)]{.underline}](#identity-access-management-iam)

> [[3.4.1 IAM Users, Roles & Policies]{.underline}](#iam-users-roles-policies)
>
> [[3.4.2 Trust Relationships]{.underline}](#trust-relationships)
>
> [[3.4.3 Governance & Principle of Least Privilege]{.underline}](#governance-principle-of-least-privilege)

[[3.5 Storage Services Comparison]{.underline}](#storage-services-comparison)

> [[3.5.1 S3 (Object Storage)]{.underline}](#s3-object-storage)
>
> [[3.5.2 EBS (Block Storage)]{.underline}](#ebs-block-storage)
>
> [[3.5.3 EFS (Network File System)]{.underline}](#efs-network-file-system)
>
> [[3.5.4 Choosing S3 vs EBS vs EFS]{.underline}](#choosing-s3-vs-ebs-vs-efs)

[[3.6 Networking in AWS (VPC Concepts)]{.underline}](#networking-in-aws-vpc-concepts)

> [[3.6.1 VPCs]{.underline}](#vpcs)
>
> [[3.6.2 Subnets (Public vs Private)]{.underline}](#subnets-public-vs-private)
>
> [[3.6.3 Security Groups & NACLs]{.underline}](#security-groups-nacls)
>
> [[3.6.4 NAT Gateways & Internet Gateways]{.underline}](#nat-gateways-internet-gateways)
>
> [[3.6.5 Route Tables]{.underline}](#route-tables)

[[3.7 CDN Basics]{.underline}](#cdn-basics)

> [[3.7.1 CloudFront Overview]{.underline}](#cloudfront-overview)
>
> [[3.7.2 CDN Performance & Security Benefits]{.underline}](#cdn-performance-security-benefits)

[[3.8 Architectural Decision-Making in AWS]{.underline}](#architectural-decision-making-in-aws)

> [[3.8.1 Common Goals in Cloud Architectures]{.underline}](#common-goals-in-cloud-architectures)
>
> [[3.8.2 Infrastructure Options Spectrum]{.underline}](#infrastructure-options-spectrum)

[[3.9 AWS Service Strategies for Common Goals]{.underline}](#aws-service-strategies-for-common-goals)

> [[3.9.1 Hosting a Web Backend]{.underline}](#hosting-a-web-backend)
>
> [[3.9.2 CI/CD Pipeline]{.underline}](#cicd-pipeline)
>
> [[3.9.3 Staging + Production Environments]{.underline}](#staging-production-environments)
>
> [[3.9.4 Static Frontend Hosting]{.underline}](#static-frontend-hosting)
>
> [[3.9.5 Data Persistence]{.underline}](#data-persistence)

[[3.10 Tradeoffs & Architectural Reasoning]{.underline}](#tradeoffs-architectural-reasoning)

> [[3.10.1 Operational Complexity]{.underline}](#operational-complexity)
>
> [[3.10.2 Performance & Latency]{.underline}](#performance-latency)
>
> [[3.10.3 Security & Privilege Boundaries]{.underline}](#security-privilege-boundaries)

[[3.11 Cost Awareness & Financial Risk Management]{.underline}](#cost-awareness-financial-risk-management)

> [[3.11.1 EC2 Under Load]{.underline}](#ec2-under-load)
>
> [[3.11.2 RDS Costs for Small Apps]{.underline}](#rds-costs-for-small-apps)
>
> [[3.11.3 CloudWatch Logging Costs]{.underline}](#cloudwatch-logging-costs)
>
> [[3.11.4 Serverless Cost Pitfalls]{.underline}](#serverless-cost-pitfalls)
>
> [[3.11.5 Egress Bandwidth Charges]{.underline}](#egress-bandwidth-charges)

[[3.12 Service Recommendations by Scenario]{.underline}](#service-recommendations-by-scenario)

> [[3.12.1 Low-Traffic MVP]{.underline}](#low-traffic-mvp)
>
> [[3.12.2 High-Throughput API]{.underline}](#high-throughput-api)
>
> [[3.12.3 Enterprise Controlled Environments]{.underline}](#enterprise-controlled-environments)

[[3.13 Speaking Fluently About AWS Without Hands-On]{.underline}](#speaking-fluently-about-aws-without-hands-on)

> [[3.13.1 Vocabulary & Semantic Fluency]{.underline}](#vocabulary-semantic-fluency)
>
> [[3.13.2 Mental Models for Cloud Architecture]{.underline}](#mental-models-for-cloud-architecture)
>
> [[3.13.3 Architecture Diagrams]{.underline}](#architecture-diagrams)

[[3.14 Module Review & Terminology]{.underline}](#module-review-terminology)

[[Analogies]{.underline}](#analogies)

> [[Cloud Regions as Countries]{.underline}](#cloud-regions-as-countries)
>
> [[VPCs as Private Neighborhoods]{.underline}](#vpcs-as-private-neighborhoods)
>
> [[EC2 as Renting a House]{.underline}](#ec2-as-renting-a-house)
>
> [[Lambda as Ride-Hailing]{.underline}](#lambda-as-ride-hailing)
>
> [[IAM as Immigration Control]{.underline}](#iam-as-immigration-control)
>
> [[CDN as Local Libraries]{.underline}](#cdn-as-local-libraries)

[[Diagrams (Mermaid + ASCII)]{.underline}](#diagrams-mermaid-ascii-2)

> [[Mermaid: Backend Architecture Flow]{.underline}](#mermaid-backend-architecture-flow)
```mermaid
>
```
> [[ASCII: VPC Subnetting]{.underline}](#ascii-vpc-subnetting)
```
>
```
> [[Mermaid: IAM Role Assumption]{.underline}](#mermaid-iam-role-assumption)
```mermaid
[[Exercises (Ungraded)]{.underline}](#exercises-ungraded)

[[Solved Exercises]{.underline}](#solved-exercises-2)

[[Mini-Scenarios]{.underline}](#mini-scenarios)

> [[Scenario A: EC2 Autoscaling Shock]{.underline}](#scenario-a-ec2-autoscaling-shock)
>
> [[Scenario B: Logging Burn]{.underline}](#scenario-b-logging-burn)
>
> [[Scenario C: Incorrect Subnet Placement]{.underline}](#scenario-c-incorrect-subnet-placement)
>
> [[Scenario D: Developer Misuses RDS]{.underline}](#scenario-d-developer-misuses-rds)

[[Quiz Questions (answers at end)]{.underline}](#quiz-questions-answers-at-end-1)

> [[Quiz Answers]{.underline}](#quiz-answers-2)

[[Teaching Notes (Instructor Guidance)]{.underline}](#teaching-notes-instructor-guidance-2)

[[Module 4 --- Containers & Docker]{.underline}](#module-4-containers-docker)

> [[Learning Objectives]{.underline}](#learning-objectives-3)

[[4.1 Introduction to Containers in DevOps]{.underline}](#introduction-to-containers-in-devops)

> [[4.1.1 Why Containers Exist]{.underline}](#why-containers-exist)
>
> [[4.1.2 Containers as Packaging Units]{.underline}](#containers-as-packaging-units)

[[4.2 Containers vs Virtual Machines]{.underline}](#containers-vs-virtual-machines)

> [[4.2.1 VM Architecture]{.underline}](#vm-architecture)
>
> [[4.2.2 Container Architecture]{.underline}](#container-architecture)
>
> [[4.2.3 Performance & Efficiency Differences]{.underline}](#performance-efficiency-differences)
>
> [[4.2.4 When to Use VMs vs Containers]{.underline}](#when-to-use-vms-vs-containers)

[[4.3 Docker Fundamentals]{.underline}](#docker-fundamentals)

> [[4.3.1 Docker Engine]{.underline}](#docker-engine)
>
> [[4.3.2 Docker Run]{.underline}](#docker-run)
>
> [[4.3.3 Exposing Ports]{.underline}](#exposing-ports)
>
> [[4.3.4 Environment Variables]{.underline}](#environment-variables)
>
> [[4.3.5 Volumes & Bind Mounts]{.underline}](#volumes-bind-mounts)

[[4.4 Docker Images]{.underline}](#docker-images)

> [[4.4.1 Layers & Caching]{.underline}](#layers-caching)
>
> [[4.4.2 Tags & Versioning]{.underline}](#tags-versioning)
>
> [[4.4.3 Minimal Base Images]{.underline}](#minimal-base-images)

[[4.5 Dockerfile & Image Building]{.underline}](#dockerfile-image-building)

> [[4.5.1 Dockerfile Instructions]{.underline}](#dockerfile-instructions)
>
> [[4.5.2 Build-time vs Run-time]{.underline}](#build-time-vs-run-time)
>
> [[4.5.3 Multi-stage Builds]{.underline}](#multi-stage-builds)

[[4.6 Registries & Image Distribution]{.underline}](#registries-image-distribution)

> [[4.6.1 DockerHub]{.underline}](#dockerhub)
>
> [[4.6.2 ECR (Elastic Container Registry)]{.underline}](#ecr-elastic-container-registry)
>
> [[4.6.3 Private Registries]{.underline}](#private-registries)

[[4.7 Container-Based Request Flow]{.underline}](#container-based-request-flow)

> [[4.7.1 Network Namespaces]{.underline}](#network-namespaces)
>
> [[4.7.2 Port Forwarding]{.underline}](#port-forwarding-1)
>
> [[4.7.3 Internal Service Communication]{.underline}](#internal-service-communication)
>
```
> [[Diagram: Request Flow (Mermaid)]{.underline}](#diagram-request-flow-mermaid)
```mermaid
>
```
> [[Diagram: Request Flow (ASCII)]{.underline}](#diagram-request-flow-ascii)
```
[[4.8 Containers in Modern DevOps]{.underline}](#containers-in-modern-devops)

> [[4.8.1 Immutable Artifacts]{.underline}](#immutable-artifacts)
>
> [[4.8.2 Microservices Architecture]{.underline}](#microservices-architecture)
>
> [[4.8.3 Cloud-Native Tooling]{.underline}](#cloud-native-tooling)

[[4.9 Operational Benefits of Containers]{.underline}](#operational-benefits-of-containers)

> [[4.9.1 Efficiency & Density]{.underline}](#efficiency-density)
>
> [[4.9.2 Portability & Reproducibility]{.underline}](#portability-reproducibility)
>
> [[4.9.3 Rapid Scaling & Deployment]{.underline}](#rapid-scaling-deployment)

[[Analogies for Conceptual Understanding]{.underline}](#analogies-for-conceptual-understanding-2)

> [[Containers as Shipping Containers]{.underline}](#containers-as-shipping-containers)
>
> [[VMs as Houses vs Containers as Apartments]{.underline}](#vms-as-houses-vs-containers-as-apartments)
>
> [[Registry as Library]{.underline}](#registry-as-library)
>
> [[Dockerfile as Recipe]{.underline}](#dockerfile-as-recipe)

[[Exercises (Ungraded Practice)]{.underline}](#exercises-ungraded-practice-2)

[[Solved Exercises]{.underline}](#solved-exercises-3)

[[Mini-Scenarios (Applied Thinking)]{.underline}](#mini-scenarios-applied-thinking-2)

> [[Scenario A: Port Collision]{.underline}](#scenario-a-port-collision)
>
> [[Scenario B: Debugging DB Connection]{.underline}](#scenario-b-debugging-db-connection)
>
> [[Scenario C: Deployment Rollback]{.underline}](#scenario-c-deployment-rollback)
>
> [[Scenario D: Multi-language Microservices]{.underline}](#scenario-d-multi-language-microservices)

[[Quiz Questions (answers at end)]{.underline}](#quiz-questions-answers-at-end-2)

> [[Quiz Answers]{.underline}](#quiz-answers-3)

[[Teaching Notes (Instructor Guidance)]{.underline}](#teaching-notes-instructor-guidance-3)

[[Module 5 --- Systems & Ops Thinking]{.underline}](#module-5-systems-ops-thinking)

> [[Learning Objectives]{.underline}](#learning-objectives-4)

[[5.1 Introduction to Systems Thinking in DevOps]{.underline}](#introduction-to-systems-thinking-in-devops)

> [[5.1.1 Holistic View of Software Systems]{.underline}](#holistic-view-of-software-systems)
>
> [[5.1.2 Operational Responsibilities]{.underline}](#operational-responsibilities)

[[5.2 Build → Artifact → Deploy → Run Lifecycle]{.underline}](#build-artifact-deploy-run-lifecycle)

> [[5.2.1 Build Phase]{.underline}](#build-phase)
>
> [[5.2.2 Artifact Creation]{.underline}](#artifact-creation)
>
> [[5.2.3 Deployment Phase]{.underline}](#deployment-phase)
>
> [[5.2.4 Runtime Phase]{.underline}](#runtime-phase)

[[5.3 Environments & Promotion]{.underline}](#environments-promotion)

> [[5.3.1 Dev Environment]{.underline}](#dev-environment)
>
> [[5.3.2 Staging Environment]{.underline}](#staging-environment)
>
> [[5.3.3 Production Environment]{.underline}](#production-environment)
>
> [[5.3.4 Promotion Flows]{.underline}](#promotion-flows)

[[5.4 CI/CD Concepts]{.underline}](#cicd-concepts)

> [[5.4.1 Continuous Integration]{.underline}](#continuous-integration)
>
> [[5.4.2 Continuous Delivery vs Deployment]{.underline}](#continuous-delivery-vs-deployment)
>
> [[5.4.3 Pipelines as Policy]{.underline}](#pipelines-as-policy)

[[5.5 Data & Schema Operations]{.underline}](#data-schema-operations)

> [[5.5.1 Migrations]{.underline}](#migrations)
>
> [[5.5.2 Rollbacks]{.underline}](#rollbacks)
>
> [[5.5.3 Backups]{.underline}](#backups)
>
> [[5.5.4 Replication]{.underline}](#replication)

[[5.6 Availability, Durability & Consistency]{.underline}](#availability-durability-consistency)

> [[5.6.1 Availability]{.underline}](#availability)
>
> [[5.6.2 Durability]{.underline}](#durability)
>
> [[5.6.3 Consistency Models]{.underline}](#consistency-models)

[[5.7 Observability in Production]{.underline}](#observability-in-production)

> [[5.7.1 Metrics]{.underline}](#metrics)
>
> [[5.7.2 Logs]{.underline}](#logs)
>
> [[5.7.3 Traces]{.underline}](#traces)
>
> [[5.7.4 KPIs & SLOs]{.underline}](#kpis-slos)

[[5.8 RPO & RTO Concepts]{.underline}](#rpo-rto-concepts)

> [[5.8.1 Recovery Point Objective (RPO)]{.underline}](#recovery-point-objective-rpo)
>
> [[5.8.2 Recovery Time Objective (RTO)]{.underline}](#recovery-time-objective-rto)
>
> [[5.8.3 Mapping RPO/RTO to Architecture]{.underline}](#mapping-rporto-to-architecture)

[[5.9 Failure Modes & Risk Mitigation]{.underline}](#failure-modes-risk-mitigation)

> [[5.9.1 Common Failure Modes]{.underline}](#common-failure-modes)
>
> [[5.9.2 Fault Domains]{.underline}](#fault-domains)
>
> [[5.9.3 Risk Mitigation Techniques]{.underline}](#risk-mitigation-techniques)

[[5.10 Decision-Making & Tradeoffs]{.underline}](#decision-making-tradeoffs)

> [[5.10.1 Constraints-Based Reasoning]{.underline}](#constraints-based-reasoning)
>
> [[5.10.2 Architectural Tradeoffs]{.underline}](#architectural-tradeoffs)
>
> [[5.10.3 Documenting Decisions]{.underline}](#documenting-decisions)

[[5.11 Module Review & Terminology]{.underline}](#module-review-terminology-1)

[[Analogies for Conceptual Understanding]{.underline}](#analogies-for-conceptual-understanding-3)

> [[Deployment as Shipping Logistics]{.underline}](#deployment-as-shipping-logistics)
>
> [[Database as a Ledger]{.underline}](#database-as-a-ledger)
>
> [[RPO as Insurance Deductible]{.underline}](#rpo-as-insurance-deductible)
>
> [[RTO as Hospital Recovery Time]{.underline}](#rto-as-hospital-recovery-time)
>
> [[Metrics as Vital Signs]{.underline}](#metrics-as-vital-signs)
>
> [[Logs as Security Footage]{.underline}](#logs-as-security-footage)
>
> [[Traces as GPS Navigation History]{.underline}](#traces-as-gps-navigation-history)

[[Diagrams (Mermaid + ASCII)]{.underline}](#diagrams-mermaid-ascii-3)
```
> [[Mermaid: Build → Artifact → Deploy → Run]{.underline}](#mermaid-build-artifact-deploy-run)
```mermaid
>
```
> [[ASCII: Environments]{.underline}](#ascii-environments)
```
>
```
> [[Mermaid: Observability Pillars]{.underline}](#mermaid-observability-pillars)
```mermaid
>
```
> [[ASCII: RPO/RTO]{.underline}](#ascii-rporto)
```
[[Exercises (Ungraded Practice)]{.underline}](#exercises-ungraded-practice-3)

[[Solved Exercises]{.underline}](#solved-exercises-4)

[[Mini-Scenarios (Applied Thinking)]{.underline}](#mini-scenarios-applied-thinking-3)

> [[Scenario A: DB Partition]{.underline}](#scenario-a-db-partition)
>
> [[Scenario B: Rollback Decision]{.underline}](#scenario-b-rollback-decision)
>
> [[Scenario C: RPO Constraint]{.underline}](#scenario-c-rpo-constraint)
>
> [[Scenario D: Autoscaling Trap]{.underline}](#scenario-d-autoscaling-trap)

[[Quiz Questions (answers at end)]{.underline}](#quiz-questions-answers-at-end-3)

> [[Quiz Answers]{.underline}](#quiz-answers-4)

[[Teaching Notes (Instructor Guidance)]{.underline}](#teaching-notes-instructor-guidance-4)

[[1. Table of Contents (Global)]{.underline}](#table-of-contents-global)

[[2. Curriculum Map (Modules + Outcomes)]{.underline}](#curriculum-map-modules-outcomes)

[[3. Scenario Bank (15+ Scenarios)]{.underline}](#scenario-bank-15-scenarios)

[[4. Viva-Style Question Bank (30 Questions)]{.underline}](#viva-style-question-bank-30-questions)

[[5. Capstone Evaluation Rubric]{.underline}](#capstone-evaluation-rubric)

> [[Core Criteria]{.underline}](#core-criteria)
>
> [[Performance Levels]{.underline}](#performance-levels)
>
> [[Sample Scoring Grid]{.underline}](#sample-scoring-grid)

[[6. Slide Outline (High-Level)]{.underline}](#slide-outline-high-level)

[[7. Student Workbook Outline]{.underline}](#student-workbook-outline)

> [[Sections]{.underline}](#sections)
>
> [[Question Types]{.underline}](#question-types)
>
> [[Reflection Prompts]{.underline}](#reflection-prompts)
>
> [[Checklists]{.underline}](#checklists)

[[8. Teaching Guide for Different Formats]{.underline}](#teaching-guide-for-different-formats)

> [[Async Self-Paced]{.underline}](#async-self-paced)
>
> [[1-Day Crash Workshop]{.underline}](#day-crash-workshop)
>
> [[2-Day Intensive]{.underline}](#day-intensive)
>
> [[4-Week Bootcamp]{.underline}](#week-bootcamp)

[[Final Capstone Projects]{.underline}](#final-capstone-projects)

> [[Capstone 1 --- "Design & Deploy a Production-Ready SaaS MVP (Budget-Constrained)"]{.underline}](#capstone-1-design-deploy-a-production-ready-saas-mvp-budget-constrained)
>
> [[Scenario]{.underline}](#scenario)
>
> [[Deliverables]{.underline}](#deliverables)
>
> [[Evaluation Focus]{.underline}](#evaluation-focus)
>
> [[Capstone 2 --- "Migrate a Legacy Monolith to Containers & CI/CD Pipeline"]{.underline}](#capstone-2-migrate-a-legacy-monolith-to-containers-cicd-pipeline)
>
> [[Scenario]{.underline}](#scenario-1)
>
> [[Deliverables]{.underline}](#deliverables-1)
>
> [[Evaluation Focus]{.underline}](#evaluation-focus-1)
>
> [[Capstone 3 --- "Design for Reliability Under Failure Modes (Systems Thinking Exercise)"]{.underline}](#capstone-3-design-for-reliability-under-failure-modes-systems-thinking-exercise)
>
> [[Scenario]{.underline}](#scenario-2)
>
> [[Deliverables]{.underline}](#deliverables-2)
>
> [[Evaluation Focus]{.underline}](#evaluation-focus-2)

[[Capstone 4 --- "Introduce CI/CD to Enterprise Without Breaking Compliance"]{.underline}](#capstone-4-introduce-cicd-to-enterprise-without-breaking-compliance)

> [[Scenario]{.underline}](#scenario-3)
>
> [[Deliverables]{.underline}](#deliverables-3)
>
> [[Evaluation Focus]{.underline}](#evaluation-focus-3)

[[Capstone 5 --- "Design Observability for a Microservices-Based Product"]{.underline}](#capstone-5-design-observability-for-a-microservices-based-product)

> [[Scenario]{.underline}](#scenario-4)
>
> [[Deliverables]{.underline}](#deliverables-4)
>
> [[Evaluation Focus]{.underline}](#evaluation-focus-4)

[[Capstone 6 --- "Containerize Legacy Multi-Process App With Shared State"]{.underline}](#capstone-6-containerize-legacy-multi-process-app-with-shared-state)

> [[Scenario]{.underline}](#scenario-5)
>
> [[Deliverables]{.underline}](#deliverables-5)
>
> [[Evaluation Focus]{.underline}](#evaluation-focus-5)

[[Capstone 7 --- "Cost Optimization Audit for a Cloud-Native Startup"]{.underline}](#capstone-7-cost-optimization-audit-for-a-cloud-native-startup)

> [[Scenario]{.underline}](#scenario-6)
>
> [[Deliverables]{.underline}](#deliverables-6)
>
> [[Evaluation Focus]{.underline}](#evaluation-focus-6)

[[Capstone 8 --- "Multi-Region Deployment for Global Latency Reduction"]{.underline}](#capstone-8-multi-region-deployment-for-global-latency-reduction)

> [[Scenario]{.underline}](#scenario-7)
>
> [[Deliverables]{.underline}](#deliverables-7)
>
> [[Evaluation Focus]{.underline}](#evaluation-focus-7)

[[Capstone 9 --- "Build Secure Dev Environments for Contractor Teams"]{.underline}](#capstone-9-build-secure-dev-environments-for-contractor-teams)

> [[Scenario]{.underline}](#scenario-8)
>
> [[Deliverables]{.underline}](#deliverables-8)
>
> [[Evaluation Focus]{.underline}](#evaluation-focus-8)

[[Capstone 10 --- "Scale a Queued Processing System Under Burst Load"]{.underline}](#capstone-10-scale-a-queued-processing-system-under-burst-load)

> [[Scenario]{.underline}](#scenario-9)
>
> [[Deliverables]{.underline}](#deliverables-9)
>
> [[Evaluation Focus]{.underline}](#evaluation-focus-9)

[[Capstone 11 --- "Implement Blue/Green + Canary Deployment Strategy"]{.underline}](#capstone-11-implement-bluegreen-canary-deployment-strategy)

> [[Scenario]{.underline}](#scenario-10)
>
> [[Deliverables]{.underline}](#deliverables-10)
>
> [[Evaluation Focus]{.underline}](#evaluation-focus-10)

[[Capstone 12 --- "Disaster Recovery Plan for Regulated Business Data"]{.underline}](#capstone-12-disaster-recovery-plan-for-regulated-business-data)

> [[Scenario]{.underline}](#scenario-11)
>
> [[Deliverables]{.underline}](#deliverables-11)
>
> [[Evaluation Focus]{.underline}](#evaluation-focus-11)

[[Capstone 13 --- "Evaluate Serverless vs Containers vs VMs for API Platform"]{.underline}](#capstone-13-evaluate-serverless-vs-containers-vs-vms-for-api-platform)

> [[Scenario]{.underline}](#scenario-12)
>
> [[Deliverables]{.underline}](#deliverables-12)
>
> [[Evaluation Focus]{.underline}](#evaluation-focus-12)

[[Capstone 14 --- "Rebuild Data Pipeline with Strong RPO/RTO Requirements"]{.underline}](#capstone-14-rebuild-data-pipeline-with-strong-rporto-requirements)

> [[Scenario]{.underline}](#scenario-13)
>
> [[Deliverables]{.underline}](#deliverables-13)
>
> [[Evaluation Focus]{.underline}](#evaluation-focus-13)

[[Capstone 15 --- "Implement Zero-Downtime Migrations for Production Database"]{.underline}](#capstone-15-implement-zero-downtime-migrations-for-production-database)

> [[Scenario]{.underline}](#scenario-14)
>
> [[Deliverables]{.underline}](#deliverables-14)
>
> [[Evaluation Focus]{.underline}](#evaluation-focus-14)

[[Capstone 16 --- "Cloud Exit Strategy (Avoid Vendor Lock-In)"]{.underline}](#capstone-16-cloud-exit-strategy-avoid-vendor-lock-in)

> [[Scenario]{.underline}](#scenario-15)
>
> [[Deliverables]{.underline}](#deliverables-15)
>
> [[Evaluation Focus]{.underline}](#evaluation-focus-15)
```
[Go Home](../README.md) | [Go Next](01-linux-git.md)
