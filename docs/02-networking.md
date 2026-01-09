# Module 2 --- Networking Fundamentals

## Learning Objectives

By the end of this module, the student should be able to:

-   Describe end-to-end browser → server request flow using DNS, TCP, and HTTP

-   Understand how domain names map to IP addresses using DNS resolution

-   Explain the purpose of IPs, domain names, ports, and protocols

-   Differentiate between TCP and UDP and describe real-world usage scenarios

-   Describe DNS record types: A, AAAA, CNAME, MX, TXT, NS, SOA

-   Conceptually configure DNS for a custom domain and SSL certificate

-   Explain private vs public IP addressing and NAT

-   Understand subnetting, CIDR, and masking for IP range allocation

-   Explain firewalls, routers, proxies, and load balancers at a conceptual level

-   Troubleshoot common networking failures (DNS resolves but app still fails)

-   Use debugging tools such as ping, traceroute, and curl for connectivity tests

-   Reason about cloud networking primitives such as subnets, gateways, and VPCs

## 2.1 Introduction to Networking in DevOps

Networking forms the connective tissue of modern systems. Every deployment pipeline, every API call, and every microservice request traverses a network boundary. Even serverless workloads and containerized platforms like Kubernetes rely deeply on transparent networking fundamentals.

Software developers often focus on code logic or product features, but DevOps engineers must understand how data physically moves from one component to another. Networking is where many "invisible" failures occur: latency, packet drops, DNS misconfiguration, TLS issues, NAT problems, routing anomalies, firewall blocks, or proxy termination layers. This module is intended to surface the machinery beneath everyday interactions.

### 2.1.1 Networking as the Hidden Layer of Software

The modern application stack hides complexity behind abstractions:

-   A user types a domain in a browser

-   The browser resolves the network location

-   A transport session begins

-   Data traverses routers, switches, proxies, and firewalls

-   The server constructs a response and returns it

Developers rarely consider how many hops and protocols are involved. DevOps excellence requires peeling back these layers to understand how availability, performance, and reliability emerge.

### 2.1.2 Concept of the Request Path

Networking introduces the idea of a **request path**, meaning the multi-step chain between client → server → service → database → and possibly another server. For distributed microservices, the request path stretches across multiple internal networks and DNS lookups.

A single user action may result in dozens of network calls, all of which must succeed in the correct order and time budget.

## 2.2 Browser to Server Request Flow

To root the discussion, consider a user typing:

https://example.com

Hit enter. A complex choreography begins involving DNS, TCP, TLS, and HTTP.

### 2.2.1 DNS Resolution Phase

DNS resolution transforms human-readable domains into machine-ready IP addresses. Without DNS, users would need to memorize addresses such as 142.250.72.238 (Google) or 151.101.1.69 (StackOverflow).

DNS queries may hit:

-   local browser cache

-   OS resolver cache

-   recursive resolver

-   authoritative name servers

Resolution latency contributes to perceived page load performance and can degrade UX when DNS misbehaves.

### 2.2.2 TCP Handshake Phase

Once the IP is known, a connection is formed using TCP's three-way handshake:

SYN → SYN-ACK → ACK

TCP ensures reliable, ordered packet delivery before application-level communication begins. This reliability enables HTTP to focus on semantic structure rather than network reliability mechanics.

### 2.2.3 HTTP Request/Response Exchange

With TCP open, the browser sends an HTTP request:

GET / HTTP/1.1

Host: example.com

The server processes the request, computes a response, and returns HTML, CSS, JS, or API data.

### 2.2.4 TLS & Encryption Layer

Modern traffic is encrypted via TLS. Before HTTP requests begin, client and server negotiate ciphers, validate certificates, and establish shared keys for encrypted communication.

End-to-end request flow (Mermaid):
```mermaid
sequenceDiagram

Browser-\>\>DNS: Resolve example.com

DNS\--\>\>Browser: IP address

Browser-\>\>Server: TCP SYN

Server\--\>\>Browser: SYN-ACK

Browser-\>\>Server: ACK

Browser-\>\>Server: TLS handshake

Server\--\>\>Browser: TLS established

Browser-\>\>Server: HTTP GET

Server\--\>\>Browser: HTTP Response
```
ASCII equivalent:
```
\[DNS\] -\> \[TCP\] -\> \[TLS\] -\> \[HTTP\]
```
## 2.3 Internet Identifiers: Domains, IPs, Ports & Protocols

### 2.3.1 Domain Names vs IP Addresses

Domains exist for humans; IPs exist for machines.

Examples:

-   example.com → 93.184.216.34

-   google.com → dynamic pool of anycast addresses

Domains decouple identity from topology, enabling service mobility (CDNs, load balancers, failover setups).

### 2.3.2 Ports as Service Endpoints

Ports multiplex services on a single IP:

  -----------------------------------------------------------------------
  **Service**                             **Default Port**
  --------------------------------------- -------------------------------
  HTTP                                    80

  HTTPS                                   443

  SSH                                     22

  DNS (UDP/TCP)                           53
  -----------------------------------------------------------------------

Example:

192.168.0.10:22 (SSH)

192.168.0.10:443 (HTTPS)

### 2.3.3 Application vs Transport vs Network Protocols

Layers form abstractions:

Application: HTTP, SMTP, DNS

Transport: TCP, UDP

Network: IP

Understanding these layers accelerates debugging---failures at one layer may not manifest at another.

## 2.4 DNS Name Resolution

DNS is a distributed, hierarchical database resolving names into addresses.

### 2.4.1 DNS as a Hierarchical System

Hierarchy:

Root (.)

└── TLD (.com, .org, .dev)

└── Authoritative Name Servers

└── Records

Recursive resolvers perform iterative queries until an authoritative answer returns.

### 2.4.2 DNS Records & Their Purpose

Common record types:

  -----------------------------------------------------------------------
  **Record**               **Purpose**
  ------------------------ ----------------------------------------------
  A                        Domain → IPv4

  AAAA                     Domain → IPv6

  CNAME                    Alias domain

  MX                       Mail exchange

  TXT                      Metadata

  NS                       Delegation

  SOA                      Authority metadata
  -----------------------------------------------------------------------

### 2.4.3 DNS Time to Live (TTL) & Caching

TTL determines record lifespan in caches. Longer TTL reduces resolver load; shorter TTL enables rapid failover or migration.

DNS cache invalidation delays can distort production rollouts.

## 2.5 DNS Records Deep Dive

### 2.5.1 A & AAAA Records

Example:

A example.com 93.184.216.34

AAAA example.com 2606:2800:220:1:248:1893:25c8:1946

IPv6 adoption continues gradually across cloud platforms.

### 2.5.2 CNAME Records

Uses:

-   CDN aliasing

-   Multi-region load balancing

-   Service indirection

Example:

www.example.com CNAME example.com

### 2.5.3 MX Records

Email routing:

example.com MX 10 mail1.example.com

example.com MX 20 backup.example.com

Priority numbers determine failover sequence.

### 2.5.4 TXT Records

Used for:

-   SPF (spam control)

-   DKIM (cryptographic email auth)

-   Domain verification (Google, AWS, Cloudflare)

-   Arbitrary data

### 2.5.5 NS Records

Delegates domain control. Registrars set NS records to authoritative name servers.

### 2.5.6 SOA Record

Metadata including serial number, refresh intervals, admin contact info.

## 2.6 Configuring DNS for a Custom Domain

### 2.6.1 Domain Registrar vs DNS Provider vs Hosting

These are separate roles:

-   Registrar = buys domain

-   DNS provider = hosts DNS records

-   Hosting = serves content

Users often mistakenly assume unity between them.

### 2.6.2 Pointing a Domain to a Web Server

Conceptual workflow:

1.  Purchase domain

2.  Add A or CNAME pointing to server or LB

3.  Wait for DNS propagation

4.  Test via ping/curl

5.  Apply SSL certificate

### 2.6.3 SSL Certificates & Domain Validation

Certificate issuance proves domain control. ACME protocols automate validation, e.g., via DNS TXT challenge or HTTP path challenge.

Browsers enforce TLS for security and user trust.

## 2.7 Transport Protocols: TCP vs UDP

Transport layer determines delivery semantics.

### 2.7.1 TCP Handshake & Reliability Guarantees

TCP guarantees:

-   ordered delivery

-   no duplication

-   congestion control

-   retransmission on loss

Ideal for web, APIs, and data integrity workloads.

TCP handshake (ASCII):
```
Client: SYN \-\-\-\--\>

Server: SYN-ACK \-\-\-\--\>

Client: ACK \-\-\-\--\>
```
### 2.7.2 UDP Speed & Stateless Delivery

UDP lacks ordering, reliability, or congestion awareness. Useful for latency-sensitive workloads where dropped packets are tolerable.

Examples:

-   VoIP

-   Games

-   Streaming

-   DNS queries

### 2.7.3 Choosing TCP vs UDP in Real Systems

Compare:

  -----------------------------------------------------------------------
  **Workload**                            **Protocol**
  --------------------------------------- -------------------------------
  Web / API                               TCP

  HTTPS                                   TCP + TLS

  VoIP                                    UDP

  DNS                                     UDP/TCP

  Gaming                                  UDP

  Email (SMTP)                            TCP
  -----------------------------------------------------------------------

## 2.8 IP Addressing, NAT & Private Networking

IP addressing binds identity to a network location.

### 2.8.1 IPv4 vs IPv6

IPv4 exhaustion drove IPv6:

-   IPv4 supports \~4.3B addresses

-   IPv6 supports \~3.4×10\^38 addresses

Cloud hosts support dual-stack deployments.

### 2.8.2 Public vs Private IP Addresses

RFC1918 private ranges:

10.0.0.0/8

172.16.0.0/12

192.168.0.0/16

Private ranges enable local networks that require NAT for internet access.

### 2.8.3 NAT (Network Address Translation)

NAT maps internal private IPs to external public IPs.

Mermaid model:
```mermaid
flowchart LR

A\[Private Host 10.0.0.5\] \--\> B\[NAT Gateway\]

B \--\> C\[Public Internet\]
```
### 2.8.4 Port Forwarding

Port forwarding exposes internal services externally for SSH, web, or game servers.

## 2.9 Subnetting, CIDR & Masking

Subnetting divides networks into manageable segments.

### 2.9.1 What is a Subnet & Why It Matters

Subnets isolate services for:

-   security

-   performance

-   organizational structure

Cloud VPCs rely heavily on them.

### 2.9.2 CIDR Notation (/24, /16, /32)

CIDR compresses masks:

-   /24 ≈ 256 IPs

-   /16 ≈ 65k IPs

-   /32 = single IP

### 2.9.3 Calculating Ranges From CIDR

Example:

192.168.1.0/24 yields:

-   network: 192.168.1.0

-   broadcast: 192.168.1.255

-   hosts: 192.168.1.1 → 192.168.1.254

Useful for firewall/ACL/VPC setups.

## 2.10 Routing, Firewalls & Proxies

Networking infrastructure introduces intermediaries that shape, direct, protect, or optimize traffic. Each intermediary serves a unique operational purpose, and DevOps engineers must understand how packets travel through these devices in order to debug connectivity and performance issues in distributed systems.

### 2.10.1 Routers & Routing Tables

Routers transmit packets between networks. When a host sends a packet, the destination network is compared against local routing tables to determine the next hop.

Routing tables encode rules such as:

destination → gateway → interface

Example (conceptual):

0.0.0.0/0 via 192.168.1.1 dev eth0

10.0.0.0/8 via 10.0.0.1 dev eth1

Cloud platforms abstract routing via VPC constructs. Routing failures are extremely common sources of intra-service outages, especially in microservices that rely on internal DNS and cross-subnet communication.

### 2.10.2 Firewalls & Access Control

Firewalls enforce allowed and disallowed traffic using:

-   IP ranges

-   protocols

-   ports

-   direction (ingress/egress)

Example whitelist rules:

  ------------------------------------------------------------------------
  **Source**             **Destination**        **Port**    **Action**
  ---------------------- ---------------------- ----------- --------------
  0.0.0.0/0              server                 443         allow

  VPC subnet             DB                     5432        allow

  0.0.0.0/0              server                 22          deny
  ------------------------------------------------------------------------

In cloud contexts, security groups and NACLs act as firewalls. A frequent debugging scenario is:

> "App works locally but fails in cloud" → blocked by egress firewall.

### 2.10.3 Proxies & Reverse Proxies

A **proxy** sits between client and server. A **reverse proxy** sits in front of servers, receiving external requests and routing them to internal services.

Reverse proxies enable:

-   TLS termination

-   rate limiting

-   load balancing

-   caching

-   auth middleware

-   redirection logic

Common reverse proxies:

-   Nginx

-   HAProxy

-   Envoy

-   Traefik

Microservices architectures rely extensively on these mechanisms for routing and observability.

## 2.11 Common Cloud Network Architectures

Networking manifests differently in cloud environments, where engineers must operate virtualized equivalents of traditional datacenter constructs.

### 2.11.1 Subnets, Gateways & Load Balancers

Cloud networks introduce:

-   **Subnets:** logical IP allocations

-   **Gateways:** internet or NAT egress points

-   **Load balancers:** distribute traffic among instances

Load balancers often operate at layer 4 (TCP) or layer 7 (HTTP), providing request awareness, stickiness, and SSL termination.

### 2.11.2 Private Subnets vs Public Subnets

Public subnets expose workloads to the public internet. Private subnets isolate workloads such as:

-   databases

-   caches

-   internal APIs

Traffic moves through NAT gateways for outbound connectivity while remaining inaccessible from outside.

### 2.11.3 Service Discovery & Internal DNS

Internal DNS is essential for microservices. Applications rely on internal resolvers to locate services by name rather than by IP.

Example internal call:

auth.internal.svc.cluster.local

DNS-driven discovery enables dynamic scaling---services start and stop without manual reconfiguration.

## 2.12 Debugging & Troubleshooting Networking

Networking failures are often subtle. Tools and methodology matter more than memorizing commands. DevOps engineers must reason through failure modes using structured tests.

### 2.12.1 DNS Works But App Fails

Common scenario:

-   Domain resolves correctly

-   Curl times out

-   Browser spins

-   App is unreachable

Possible causes:

-   Port closed

-   Firewall block

-   TLS mismatch

-   Proxy misconfig

-   Routing failure

-   Backend unavailable

### 2.12.2 Ping, Traceroute & Curl as Debug Tools

**ping** tests basic connectivity and latency (ICMP).\
**traceroute** displays route hops through the network.\
**curl** inspects HTTP behavior (headers, TLS, codes).

Example analysis sequence:

ping example.com

traceroute example.com

```
curl -v https://example.com
```

Each layer verifies a different assumption.

### 2.12.3 Debugging Ports & Services

Tools like ss, netstat, or lsof inspect port bindings:

ss -tlnp

If a web server listens on port 8080 locally but inbound firewall only allows 443, external users will fail to reach the service.

### 2.12.4 Common Operational Failure Modes

Examples worth knowing:

-   DNS stale cache

-   MTU mismatch

-   Broken SSL cert

-   Blocked egress traffic

-   Proxy redirect loops

-   NAT exhaustion

-   Over-aggressive rate limiting

-   CORS denial

-   DDoS saturation

A DevOps engineer must learn to treat networking failures as layered problems.

# 3. Analogies for Conceptual Understanding

Analogies help internalize abstract protocols and infrastructure concepts.

## 3.1 DNS as a Phonebook

Domains = names\
IPs = phone numbers\
DNS = directory lookups\
TTL = caching phonebook entries

Changing DNS records resembles updating a contact---old numbers may persist temporarily due to caching.

## 3.2 TCP as Registered Mail

TCP ensures:

-   delivery

-   order

-   retries

-   confirmation

Like registered mail requiring signatures, TCP verifies delivery correctness.

## 3.3 UDP as a Broadcast Radio

UDP sends information without confirmation---useful when losing a bit of audio or video is tolerable for speed.

## 3.4 Subnets as Neighborhood Blocks

A city subdivides into blocks (subnets). Addresses define where houses are located. Routers direct between blocks.

## 3.5 Firewalls as Security Guards

Firewalls grant or deny access based on:

-   identity (IP)

-   purpose (port)

-   behavior (protocol)

## 3.6 Load Balancers as Reception Desks

A reception desk routes incoming visitors to available staff---similar to balancing requests across servers.

# 4. Diagrams (Mermaid + ASCII)

## 4.1 Browser Request Flow (Mermaid)
```mermaid
flowchart LR

User \--\> Browser

Browser \--\> DNS\[DNS Lookup\]

DNS \--\> Connect\[TCP/TLS Connect\]

Connect \--\> HTTP\[HTTP Request\]

HTTP \--\> Server\[Application Server\]

Server \--\> Response\[HTTP Response\]

Response \--\> Browser

Browser \--\> User
```
## 4.2 Network Layers (ASCII)
```
Application: HTTP, SMTP, DNS

Transport: TCP, UDP

Network: IP

Link: Ethernet, WiFi

Physical: Cables, Radio
```
## 4.3 Cloud Private/Public Subnets (Mermaid)
```mermaid
graph TD

LB\[Load Balancer\] \--\> PUB\[Public Subnet\]

PUB \--\> NAT\[NAT Gateway\]

NAT \--\> PRIV\[Private Subnet\]

PRIV \--\> DB\[(Database)\]
```
## 4.4 CIDR Allocation (ASCII)
```
192.168.1.0/24

Hosts: 192.168.1.1 - 192.168.1.254

Net: 192.168.1.0

Bcast: 192.168.1.255
```
# 5. Exercises (Ungraded Practice)

### Exercise 1 --- DNS Lookup

Perform conceptually:

1.  Resolve example.com

2.  Identify IP

3.  Identify whether it's IPv4 or IPv6

### Exercise 2 --- TCP vs UDP

Classify:

-   Web browsing

-   Streaming

-   VoIP calls

-   Email

-   DNS queries

### Exercise 3 --- CIDR Reasoning

Given:

10.0.0.0/16

Calculate:

-   total usable IPs

-   first usable IP

-   last usable IP

### Exercise 4 --- Debugging Scenario

You can ping domain.com but curl domain.com returns connection refused. List three possible root causes.

### Exercise 5 --- Port Logic

Explain why SSH uses 22 and HTTPS uses 443 and why services don't collide.

# 6. Solved Exercises

### Solution 1

DNS lookup → IPv4 for most public sites.

### Solution 2

Classification:

  -----------------------------------------------------------------------
  **Workload**                        **Protocol**
  ----------------------------------- -----------------------------------
  Web                                 TCP

  Streaming                           UDP

  VoIP                                UDP

  Email                               TCP

  DNS                                 UDP/TCP
  -----------------------------------------------------------------------

### Solution 3

/16 yields 65,536 total addresses.

Hosts ≈ 65,534 usable (network + broadcast excluded).

### Solution 4

Possible causes:

-   Firewall block

-   Closed port

-   Reverse proxy misconfig

-   TLS failure

### Solution 5

Ports multiplex services. 22 and 443 are reserved and standardized.

# 7. Mini-Scenarios (Applied Thinking)

### Scenario A --- DNS is Correct; App Still Down

Expected student reasoning:

-   Check ports

-   Check firewall

-   Check app service

-   Check TLS

-   Check load balancer health checks

### Scenario B --- Private DB Cannot Be Reached

Likely networking conditions:

-   DB in private subnet

-   Missing route table

-   Security group denies inbound

### Scenario C --- Multi-Region Deployment Failing

Consider latency, propagation, and CDN routing.

# 8. Quiz Questions (answers at end)

1.  What does DNS do?

2.  What is the difference between TCP and UDP?

3.  What does a CNAME record do?

4.  Why do private networks require NAT?

5.  What does /24 indicate in CIDR?

6.  Why do firewalls matter?

7.  Why can DNS resolve while app still fails?

8.  Name two debugging tools for network issues.

### Quiz Answers

1.  Maps domain names to IP addresses.

2.  TCP is reliable and ordered; UDP is fast and unreliable.

3.  Maps a domain to another domain.

4.  Private IPs cannot route directly to the public internet.

5.  /24 defines an address range (\~256 IPs).

6.  Firewalls restrict traffic for security.

7.  Application layer may fail on ports, TLS, routing, or proxy layers.

8.  ping, traceroute, curl, dig.

# 9. Teaching Notes (Instructor Guidance)

-   Students struggle with multi-layer failure reasoning; encourage structured debugging

-   Use visual diagrams often; networking is spatial and layered

-   Reinforce DNS concepts repeatedly---DNS is the silent culprit in many outages

-   Emphasize cloud networking primitives (VPC, subnets, SGs)

-   Offer hands-on labs: dig, curl, ss, traceroute, internal DNS checks

-   Encourage mapping request paths on whiteboards

-   Connecting networking to DevOps pipelines improves realism

