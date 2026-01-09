# Module 4 --- Containers & Docker

## Learning Objectives

By the end of this module, the student should be able to:

-   Explain clearly and confidently how containers differ from virtual machines technically and operationally

-   Understand Docker's execution model including images, layers, containers, and registries

-   Run Docker containers, expose ports, inject environment variables, and mount volumes

-   Understand how images are tagged, versioned, pushed, and pulled from registries (DockerHub, ECR, private registries)

-   Diagram container request flow from inbound ports to internal application listeners

-   Explain why containers became foundational to modern DevOps, CI/CD, and cloud-native architectures

-   Speak fluently about container advantages in reproducibility, portability, density, and deployment simplicity

## 4.1 Introduction to Containers in DevOps

Containerization represents one of the most influential shifts in software operations over the past decade. Before containers, development and production environments frequently diverged due to differing OS packages, dependency versions, library expectations, or system configurations. These mismatches produced notorious deployment failures summarized by the phrase:

> "But it works on my machine."

Containers eliminate this mismatch by bundling the application code, dependencies, runtime libraries, and environment expectations into a consistent artifact.

Reduced friction between development, staging, CI environments, and production accelerates release cycles and unlocks automation.

### 4.1.1 Why Containers Exist

Containers exist to solve environment inconsistency. When code ships embedded with its runtime (Python/Node/Java) and dependencies (npm, pip, OS libs), deployment becomes deterministic instead of accidental.

This determinism enables:

-   reproducible builds

-   predictable runtime behavior

-   reduced debugging overhead

-   smaller blast radius for errors

### 4.1.2 Containers as Packaging Units

Containers serve as packaging for execution. One can think of containers as compact portable boxes where the application lives with all it needs. Different containers can co-exist on the same host without conflicting dependencies (e.g., Python 3.11 and Node 20 on the same machine).

This is particularly important for microservices, where each service may have its own runtime ecosystem.

## 4.2 Containers vs Virtual Machines

A common misconception is that containers are just lightweight VMs. This is not accurate and merits a structured comparison.

### 4.2.1 VM Architecture

Virtual machines rely on hypervisors to virtualize hardware. Each VM contains:

-   Guest OS

-   User space

-   Applications and dependencies

This requires significant resource allocation and long boot times, but provides strong isolation and compatibility with legacy architectures.

### 4.2.2 Container Architecture

Containers share the host kernel but isolate userspace using:

-   namespaces (PID, network, mounts, IPC)

-   cgroups (resource constraints)

-   union filesystems (image layers)

This results in extremely fast startup (milliseconds), low overhead, and higher density.

### 4.2.3 Performance & Efficiency Differences

Containers outperform VMs in:

-   startup time

-   CPU utilization

-   memory footprint

-   deployment agility

VMs outperform containers in:

-   legacy compatibility

-   strong hardware-level isolation

-   regulated compliance scenarios

### 4.2.4 When to Use VMs vs Containers

Use VMs when:

-   workloads are monolithic

-   legacy OS/driver support required

-   stateful services with custom kernels

-   compliance demands strict isolation

Use containers when:

-   workloads are microservices

-   rapid deployments are desirable

-   resource density matters

-   CI/CD pipelines must be automated

## 4.3 Docker Fundamentals

Docker popularized containerization by providing tooling, ecosystem support, and developer ergonomics.

### 4.3.1 Docker Engine

Docker Engine orchestrates image management, container runtime, storage drivers, and networking. It allows developers to:

-   build images

-   start/stop containers

-   map ports

-   mount volumes

-   pass environment variables

-   manage container networks

### 4.3.2 Docker Run

```
docker run is the core execution command. Example:
```

```
docker run ubuntu:latest echo \"Hello\"
```

This runs a container using the ubuntu image and executes echo.

Flags control runtime behavior:

-   -p for port mapping

-   -e for environment variables

-   -v for volumes

-   \--name to label containers

-   \--rm for cleanup

### 4.3.3 Exposing Ports

Containers isolate network namespaces. To allow inbound traffic:

```
docker run -p 8080:3000 app
```

This maps host port 8080 to container port 3000.

### 4.3.4 Environment Variables

Runtime configuration via -e:

```
docker run -e NODE_ENV=production app
```

This enables twelve-factor configuration patterns.

### 4.3.5 Volumes & Bind Mounts

Volumes persist data. Example:

```
docker run -v data:/mnt/data app
```

Bind mounts share host directories:

```
docker run -v \$(pwd):/app app
```

Volumes enable stateful workloads like databases or logs within otherwise ephemeral containers.

## 4.4 Docker Images

Images are templates from which containers are instantiated.

### 4.4.1 Layers & Caching

Docker images use layered filesystems. Each instruction in Dockerfile creates a layer. Layers are immutable and cached, improving build efficiency and distribution.

Example conceptual stack:

base image (alpine)

\+ runtime (node)

\+ dependencies (npm install)

\+ application code

### 4.4.2 Tags & Versioning

Images are versioned using tags:

node:18

node:18-alpine

myapp:1.0.3

myapp:latest

Semantic tagging supports safe rollbacks.

### 4.4.3 Minimal Base Images

Using alpine or distroless images reduces:

-   attack surface

-   build size

-   CVE exposure

-   deployment time

## 4.5 Dockerfile & Image Building

Containers are built using Dockerfiles, declarative scripts that define instructions.

### 4.5.1 Dockerfile Instructions

Key rules (conceptual only here):

-   FROM: base image

-   COPY: files from host to image

-   RUN: build commands

-   EXPOSE: port metadata

-   ENTRYPOINT / CMD: runtime commands

Example snippet (conceptual, not executed):

FROM node:18-alpine

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

CMD \[\"node\", \"server.js\"\]

### 4.5.2 Build-time vs Run-time

Build-time:

-   RUN npm install

-   compiling code

Run-time:

-   reading env vars

-   connecting to network services

Distinguishing these reduces errors in CI/CD.

### 4.5.3 Multi-stage Builds

Multi-stage builds reduce image size:

Stage 1: build code\
Stage 2: ship minimal binary/runtime

Critical for Go, Node, Java, and Python microservices.

## 4.6 Registries & Image Distribution

Registries store images for consumption by CI/CD and production workloads.

### 4.6.1 DockerHub

Public registry, dominant for open source and standard base images.

### 4.6.2 ECR (Elastic Container Registry)

Private registry integrated with AWS:

-   IAM authentication

-   lifecycle policies

-   secure artifact distribution

### 4.6.3 Private Registries

Used in enterprise:

-   governance

-   compliance

-   internal artifacts

-   offline/air-gapped deployments

## 4.7 Container-Based Request Flow

A container running a web service must receive requests from outside the container boundary, process them, and respond. This creates a structured flow involving:

1.  network namespace isolation

2.  port binding and forwarding

3.  container-internal listeners

4.  service-level routing (if multiple containers)

5.  external clients

Docker abstracts these mechanisms but understanding them is crucial for debugging.

### 4.7.1 Network Namespaces

Containers run with isolated network namespaces, meaning:

-   isolated loopback

-   isolated interfaces

-   isolated routing table

-   isolated port space

Two containers can run the same app binding to the same internal port (:3000) without conflict, as long as host mappings differ.

### 4.7.2 Port Forwarding

Port forwarding bridges the container namespace to the host:

```
docker run -p 8080:3000 app
```

Meaning:

-   container listens on 3000

-   host receives traffic on 8080

-   Docker forwards packets to internal listener

This mechanism allows users to hit containerized services via browser or curl.

### 4.7.3 Internal Service Communication

Containers often communicate with each other within custom networks:

-   Docker automatically provides DNS-based service discovery within a network

-   containers can reference each other by name (e.g., db:5432)

This lays the foundation for microservice architectures and service meshes.

## Diagram: Request Flow (Mermaid)
```mermaid
flowchart LR

Client \--\> HostPort\[Host Port 8080\]

HostPort \--\> DockerForwarding

DockerForwarding \--\> ContainerPort\[Container Port 3000\]

ContainerPort \--\> App\[Web App Listener\]

App \--\> Response

Response \--\> Client
```
## Diagram: Request Flow (ASCII)
```
client \--\> host:8080 \--\> container:3000 \--\> app \--\> client
```
## 4.8 Containers in Modern DevOps

Containers have become deeply entangled with DevOps due to their repeatability, portability, and compatibility with CI/CD pipelines.

### 4.8.1 Immutable Artifacts

Traditional deployments deploy code, libraries, config, and dependencies directly onto servers, introducing drift. Containers instead create immutable artifacts which remain unchanged between:

-   local dev

-   staging

-   production

-   CI pipelines

This eliminates drift and simplifies rollbacks.

### 4.8.2 Microservices Architecture

Microservices require dozens or hundreds of services running in isolation. Containers provide:

-   independent versioning

-   independent build pipelines

-   independent scaling

-   independent failure domains

This decomposition is infeasible with traditional VM workflows.

### 4.8.3 Cloud-Native Tooling

Cloud platforms and Kubernetes derivatives rely on containers. Examples:

-   ECS (AWS)

-   EKS (AWS Kubernetes)

-   Fargate (serverless container execution)

-   GKE (Google)

-   AKS (Azure)

-   Nomad (HashiCorp)

The cloud-native ecosystem presumes containerized workloads as first-class.

## 4.9 Operational Benefits of Containers

### 4.9.1 Efficiency & Density

Containers pack more workloads into a single host due to low overhead and shared kernel model. This increases compute density and reduces cost.

### 4.9.2 Portability & Reproducibility

Containers run consistently on:

-   laptops

-   CI runners

-   staging clusters

-   production clusters

-   cloud providers

This portability eradicates platform fragmentation.

### 4.9.3 Rapid Scaling & Deployment

Containers support:

-   fast boot (milliseconds)

-   blue/green deployments

-   rolling deployments

-   canary deployments

-   shadow deployments

These strategies reduce downtime risk.

# Analogies for Conceptual Understanding

### Containers as Shipping Containers

Containerization mirrors global logistics: standardized boxes enable predictable transport, stacking, inventory, and customs control. In software, standardization reduces environmental mismatch and friction.

### VMs as Houses vs Containers as Apartments

VMs contain their own infrastructure (guest OS) like standalone houses. Containers share the building's infrastructure (host OS) like apartments.

### Registry as Library

Registries store images like libraries store books. Pulling an image is analogous to borrowing a standardized artifact.

### Dockerfile as Recipe

Instructions in a Dockerfile mimic a cooking recipe that yields consistent outputs when executed.

# Exercises (Ungraded Practice)

1.  Explain in your own words the difference between a VM and a container.

2.  Run a conceptual Docker command that:

    -   uses an image

    -   exposes a port

    -   passes an environment variable

3.  Select appropriate storage strategy for a containerized DB (volume vs bind mount vs ephemeral).

4.  Explain why microservices are difficult without containerization.

5.  Describe the meaning of docker run -p 8080:3000 app.

# Solved Exercises

1.  VMs virtualize hardware + guest OS; containers share host kernel and isolate user space.

2.  Example conceptual command:

```
docker run -p 8080:3000 -e NODE_ENV=production myapp:latest
```

3.  Persistent DB → use Docker volume; ephemeral storage would lose data on restart.

4.  Microservices require isolated dependencies, independent runtimes, and autonomous scaling.

5.  Maps host port 8080 to container port 3000 enabling inbound network access.

# Mini-Scenarios (Applied Thinking)

### Scenario A: Port Collision

Two containers run Node apps both listening on 3000, but cannot both bind to host 3000. Student must reason about namespace isolation and host mappings.

### Scenario B: Debugging DB Connection

Service containers communicate via Docker network. DNS resolution fails→ container cannot resolve db hostname. Student checks networking config.

### Scenario C: Deployment Rollback

New image fails health checks. Immutable containers allow instant rollback by redeploying previous tag.

### Scenario D: Multi-language Microservices

Python, Node, Go services coexist without system dependency conflicts due to container isolation.

# Quiz Questions (answers at end)

1.  What problem do containers solve in DevOps?

2.  Name a key difference between VMs and containers.

3.  What does Docker Hub provide?

4.  Why are Docker images layered?

5.  What does -p 8080:3000 mean?

6.  Why are containers preferred in CI/CD pipelines?

7.  What is an immutable artifact?

8.  Why are registries important?

### Quiz Answers

1.  Eliminates environment drift & increases reproducibility.

2.  VMs include a guest OS; containers share the host kernel.

3.  A public registry for pulling/pushing container images.

4.  To enable caching, efficient builds, and distribution.

5.  Maps host port 8080 to container port 3000 for inbound traffic.

6.  Fast, portable, reproducible builds; reduced friction.

7.  A deployable unit that remains unchanged across environments.

8.  They store and distribute container images.

# Teaching Notes (Instructor Guidance)

-   Use diagrams frequently; container networking is visual.

-   Demonstrate live examples if possible for intuitive uptake.

-   Reinforce container vs VM differences until students articulate fluently.

-   Encourage creating personal Dockerfiles to demystify builds.

-   Tie container concepts to CI/CD pipelines and cloud deployments for motivation.

-   Stress image immutability and tags for real-world rollback workflows.

-   Prepare students for Kubernetes later; containers are the foundation.
[Go Back](03-cloud-foundations.md) | [Go Home](../README.md) | [Go Next](05-systems-ops.md)

