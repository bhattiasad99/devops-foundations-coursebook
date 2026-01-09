# Module 1 --- Linux & Git Foundations

## Learning Objectives

By the end of this module, the student should be able to:

-   Navigate the Linux filesystem confidently using fundamental commands such as cd, ls, pwd, mv, cp, and rm

-   Understand how Linux organizes system components via a hierarchical filesystem with well-defined directories

-   Manage permissions, users, groups, and file execution privileges using chmod, chown, and chgrp

-   Inspect, monitor, and manipulate processes using commands like ps, kill, top, and related tools

-   Read logs and structured text using cat, less, tail, head, and filter pipelines such as grep, sort, uniq, and wc

-   Develop conceptual literacy in Bash scripting including variables, conditionals, and loops

-   Explain why automation matters in infrastructure and DevOps workflows

-   Initialize, add, commit, push, pull, and manage repositories using Git in a local-to-remote workflow

-   Understand branching, merging, and basic conflict scenarios

-   Apply Linux + Git foundational concepts to debugging, collaboration, and real-world setup scenarios

## 1.1 Introduction to Linux in DevOps

Linux is the operating system that underpins most of the machinery modern DevOps professionals interact with on a daily basis. Servers, cloud VMs, CI/CD runners, containers, orchestrators, logging services, networking appliances, reverse proxies, and databases all rely heavily on Linux conventions. This makes Linux literacy an irreplaceable prerequisite for understanding automation, debugging, and platform engineering.

Linux's design philosophy draws from Unix's historical pursuit of simplicity: discrete tools that do one job well, and that compose gracefully through text pipelines. This modularity allows users to craft workflows without relying on heavy GUIs or monolithic software suites. In DevOps, the command line is often the fastest way to configure, inspect, and reason about systems.

### 1.1.1 History & Philosophy of Linux

Linux inherits a lineage from Unix, developed in the late 1960s and early 1970s. Unix introduced concepts fundamental to DevOps culture:

-   **Everything is a file**: Devices, processes, sockets, configuration, and data expose themselves uniformly

-   **Small composable tools**: Commands are atomic, predictable, and chainable

-   **Text as control surface**: Logs, configuration, and output are plain text rather than opaque formats

Linux emerged as an open-source re-implementation of Unix, eventually dominating servers and cloud computing due to performance, reliability, and licensing freedoms. This ecosystem fosters experimentation, automation, and deep system introspection---all core pursuits in DevOps engineering.

### 1.1.2 Linux in Modern Infrastructure

Today, Linux powers:

-   Public clouds (AWS, GCP, Azure)

-   Docker containers

-   Kubernetes nodes and pods

-   Infrastructure as Code tooling

-   Web servers (Nginx, Apache)

-   Databases (PostgreSQL, MySQL, Redis)

-   CI/CD agents and runners

-   Networking layers and proxies

When engineers execute a deployment pipeline, connect to a remote server, inspect logs, adjust permissions, or restart processes, they are almost always doing so on a Linux-based environment. For this reason, Linux command-line fluency is functionally equivalent to being able to manipulate the operational universe of modern software.

## 1.2 Working with the Linux Filesystem

The Linux filesystem is hierarchical, starting from a single root directory /. Beneath this root branch numerous directories that categorize binaries, logs, devices, configurations, and user-related data. Understanding these conventions enables engineers to predict where files should live and where services expose their operational traces.

### 1.2.1 Filesystem Hierarchy

A simplified representation:

/

├── bin

├── boot

├── dev

├── etc

├── home

├── lib

├── usr

├── var

└── tmp

**Brief description of key directories:**

-   /bin: Essential binaries (e.g., ls, cp, cat)

-   /boot: Kernel and boot loader metadata

-   /dev: Devices represented as files

-   /etc: System-wide configuration

-   /home: User home directories

-   /var: Variable data (logs, caches, queues)

-   /usr: User-level apps, libraries, and documentation

-   /tmp: Temporary writable storage (ephemeral)

### 1.2.2 Navigating the Filesystem

Navigating is done through a handful of commands:

  -----------------------------------------------------------------------
  **Command**              **Meaning**
  ------------------------ ----------------------------------------------
  pwd                      Print working directory

  cd                       Change directory

  ls                       List directory contents
  -----------------------------------------------------------------------

Example usage:

```
\$ pwd
```

/home/student

```
\$ cd /etc
```

```
\$ ls
```

hosts

passwd

ssh/

systemd/

Navigation forms the foundation for nearly every operation: reading logs, editing configs, inspecting processes, managing projects, or bootstrapping deployments.

### 1.2.3 Creating, Moving & Deleting Files

Linux provides direct manipulation primitives:

-   touch file.txt: Create empty file or update timestamp

-   mv file1 file2: Move or rename

-   cp file1 file2: Copy file

-   rm file: Remove file

Directories are created with:

-   mkdir dir

-   mkdir -p nested/dir/structure

These operations reinforce the Linux philosophy that the filesystem is an interface for control and organization, not merely storage.

### 1.2.4 Understanding File Types

Linux treats everything as a file, but not all files are ordinary. Common types include:

  -----------------------------------------------------------------------
  **Type**           **Description**
  ------------------ ----------------------------------------------------
  Regular            Normal data file

  Directory          Container of files

  Symlink            Pointer to another file

  Device             Hardware or pseudo-hardware

  Socket             IPC communication

  FIFO               Named pipes
  -----------------------------------------------------------------------

Symbolic links are particularly common in deployments where version switching or indirection is needed.

ASCII representation of symlink resolution:
```
app -\> app_v3.1.4/

├── bin/

├── config/

└── logs/
```
## 1.3 File Viewing & Text Utilities

Linux emphasizes text as a universal data surface. Logs, configs, manifests, scripts, deployment histories, and system diagnostics are text-first. Mastery of file inspection tools accelerates debugging, troubleshooting, and automation.

### 1.3.1 Reading & Paging Files

Common tools:

-   cat: Print full file

-   less: Scroll interactively

-   head: Show beginning

-   tail: Show end

Example for log monitoring:

```
tail -f /var/log/syslog
```

The -f flag follows updates as they occur, useful during deployments or incident handling.

### 1.3.2 Searching Within Files

```
grep provides pattern matching via regular expressions:
```

```
grep \"ERROR\" application.log
```

Combining with pipes:

```
tail -f app.log \| grep \"timeout\"
```

This composition enables real-time filtering---an essential debugging tactic.

### 1.3.3 Sorting & Filtering

Text processing tools allow structured analytics:

  -----------------------------------------------------------------------
  **Command**             **Purpose**
  ----------------------- -----------------------------------------------
  sort                    Orders lines

  uniq                    Deduplicates

  wc                      Counts lines/words

  cut                     Extracts columns

  awk                     Pattern-based processing
  -----------------------------------------------------------------------

Pipeline example:

```
cat access.log \| cut -d \' \' -f 1 \| sort \| uniq -c \| sort -nr
```

This yields a frequency distribution of IPs hitting a web server.

## 1.4 Permissions, Ownership & Users

Linux enforces multi-user access control. Permissions determine who may read, write, or execute content.

### 1.4.1 Understanding Permissions

A typical ls -l output:

-rwxr-x\-\--

Breakdown:

\[ owner \]\[ group \]\[ others \]

rwx r-x \-\--

Permissions encode:

-   r: read

-   w: write

-   x: execute

Numeric representation:

  -----------------------------------------------------------------------
  **rwx**                    **Decimal**
  -------------------------- --------------------------------------------
  rwx                        7

  rw-                        6

  r-x                        5

  r\--                       4
  -----------------------------------------------------------------------

Useful for scripting deployment pipelines.

### 1.4.2 Changing Permissions & Ownership

Common operations:

```
chmod 755 script.sh
```

chown user:group file.txt

These apply in many operational contexts including service accounts, container runtimes, and SSH setups.

### 1.4.3 Users, Groups & Identity

Users belong to groups to simplify role-based access:

usermod -aG docker student

Group-based permissions scale better for multi-tenant servers, CI runners, or developer sandboxes.

## 1.5 Processes & System Monitoring

A process is a running instance of a program. Monitoring processes allows engineers to trace performance issues, resource exhaustion, and crashed workloads.

### 1.5.1 Listing & Inspecting Processes

```
ps aux dumps process table; top shows dynamic metrics like CPU and memory.
```

Mermaid diagram (process-state lifecycle):
```mermaid
flowchart LR

A\[New\] \--\> B\[Ready\]

B \--\> C\[Running\]

C \--\>\|Interrupt\| B

C \--\> D\[Waiting\]

D \--\> B

C \--\> E\[Terminated\]
```
ASCII equivalent:
```
New -\> Ready -\> Running -\> Terminated

\^ \|

\|\-\-\-\-\-\-\-\--\|
```
### 1.5.2 Killing Processes & Signals

Signals control process termination:

-   SIGTERM: Graceful stop

-   SIGKILL: Forced kill

Example:

```
kill -15 \<pid\>
```

```
kill -9 \<pid\>
```

### 1.5.3 System Logs & Services

Systemd-based systems manage services:

```
systemctl status nginx
```

```
systemctl restart nginx
```

Operational debugging frequently uses service logs + status introspection.

## 1.6 Bash Scripting Foundations

Automation is the multiplier for DevOps productivity. Bash scripting converts manual tasks into reproducible pipelines.

### 1.6.1 Why Automation Matters

In DevOps, the scale of tasks inflates rapidly:

-   Managing environments

-   Deploying services

-   Rotating logs

-   Synchronizing configs

-   Running migrations

Manual steps become liabilities; scripting becomes governance.

### 1.6.2 Variables, Loops & Conditionals

Conceptual building blocks:

Variables:

```
NAME=\"student\"
```

Conditionals:

```
if \[ \$VALUE -gt 10 \]; then
```

```
echo \"greater\"
```

```
fi
```

Loops:

```
for file in \*.log; do
```

```
echo \$file
```

```
done
```

### 1.6.3 Writing & Executing Scripts

Shebang:

# !/bin/bash

Execution:

```
chmod +x script.sh
```

```
./script.sh
```

Scripting literacy enhances CI/CD design, infra-as-code, and orchestration.

## 1.7 Git Foundations for DevOps

Git is a distributed version control system enabling reproducible builds, collaborative workflows, rollbacks, and CI pipelines.

### 1.7.1 What Problem Git Solves

Git addresses coordination problems among developers:

-   Version history

-   Branch divergence

-   Code review

-   Reproducibility

-   Rollbacks

### 1.7.2 Repositories (init, clone)

Initializing:

```
git init
```

Cloning:

```
git clone git@host:repo.git
```

Local repos allow experimentation without affecting others.

### 1.7.3 Local Workflow (add, commit)

Workflow:

```
git add file.txt
```

```
git commit -m \"message\"
```

Commits capture snapshots of state.

## 1.8 Working With Remote Repositories

Remotes allow synchronization across contributors, CI/CD pipelines, and deployment infrastructure.

### 1.8.1 Understanding Remotes (origin, upstream)

A common setup:

origin -\> developer repo

upstream -\> canonical source of truth

### 1.8.2 Pulling & Pushing Changes

Synchronizing:

```
git pull
```

```
git push
```

### 1.8.3 Basic Branching & Merging

Branches isolate change:

```
git branch feature/login
```

```
git checkout feature/login
```

Merge conflicts arise when divergent changes touch the same lines.

## 1.9 Practical Logs & Pipelines

The real power of Linux is unlocked when commands are chained together to form dynamic workflows. Logs, text streams, and diagnostic data become inputs to analytical pipelines. This is a cornerstone of operational debugging, where the goal is to identify the root cause of failures, performance issues, deployment anomalies, or unexpected system behavior.

### 1.9.1 Inspecting Application Logs

Most applications emit logs to files under /var/log or to custom log directories inside /opt, /srv, or application-specific folders. Logs contain timestamps, severity markers, error messages, and contextual metadata like IPs or request paths.

Example scenario: tailing a web server log for HTTP 500 errors.

```
tail -f access.log \| grep \" 500 \"
```

The continuous streaming nature of tail -f allows real-time incident investigation during deployments, releases, or load spikes.

### 1.9.2 Command Pipelines (\|)

Pipelines chain command output into subsequent commands:

command1 \| command2 \| command3

Example:

```
ps aux \| grep nginx \| wc -l
```

This answers: *How many nginx processes are currently running?*

Example pipeline for log analysis:

```
cat app.log \| grep \"ERROR\" \| cut -d \' \' -f 4 \| sort \| uniq -c \| sort -nr
```

This might reveal the frequency of distinct error codes or subtypes.

### 1.9.3 Real-World Debugging Scenarios

Consider a Node.js application emitting timeouts during peak traffic. A debugging pipeline:

```
tail -f app.log \| grep \"timeout\"
```

A performance investigation on memory leaks:

top -o %MEM

Or identifying which user accounts are spamming SSH attempts:

```
grep \"Failed password\" /var/log/auth.log \| cut -d \' \' -f 11 \| sort \| uniq -c \| sort -nr
```

These patterns illustrate that Linux tools are not isolated commands---they compose into powerful investigative workflows.

## 1.10 Capstone Mini-Labs

Capstones translate conceptual understanding into operational habits. These labs confirm that students can navigate, interrogate, and manipulate systems rather than merely reciting commands.

### 1.10.1 Linux Navigation & Permissions Lab

Tasks include:

-   Move around the filesystem

-   Create files and directories

-   Change permissions

-   Inspect ownership

-   Execute commands on real logs

Example tasks:

1.  Create a directory /tmp/devops_lab

2.  Inside it, create script.sh and data.txt

3.  Set script.sh permissions to 755

4.  Set data file permissions to 600

5.  Verify using ls -l

### 1.10.2 Git Local-to-Remote Workflow Lab

Exercise workflow:

1.  Initialize a local repository

2.  Create a new file notes.md

3.  Commit changes

4.  Add remote origin

5.  Push to remote branch

6.  Pull updates from remote

Basic remote mechanics reinforce collaboration fundamentals.

### 1.10.3 Reading Logs & Debugging Lab

Tasks:

1.  Tail syslog while starting/stopping a service

2.  Grep for error or failed strings

3.  Count process occurrences

4.  Investigate results and discuss possible causes

These labs simulate real world runtime introspection.

# Supplements

# 2. Analogies for Conceptual Understanding

Analogies provide cognitive shortcuts --- useful especially when teaching beginners or cross-disciplinary professionals.

### Filesystem as a City

-   / is downtown

-   /etc is city hall (rules & configs)

-   /bin is tool shops (applications)

-   /home is residential neighborhoods (users)

-   /var/log is newspapers and archives (history)

-   /tmp is a public park (temporary, messy, constantly changing)

### Permissions as Building Access

-   owner = private resident

-   group = shared residents (e.g., tenants)

-   others = general public

-   rwx permissions = whether you can read, modify, or enter the building

Numeric permissions equate to keys granting access to different rooms.

### Processes as Workers in a Factory

-   Scheduler = manager allocating time

-   Processes = workers executing tasks

-   Signals = notifications from management

-   Kill signal = firing a worker

-   System load = how many workers vs. how many tasks

### Git as a Time Machine for Code

-   Commits = snapshots

-   Branches = alternate timelines

-   Merging = reconciling parallel universes

-   Conflicts = paradoxes when two timelines modify the same event

-   Remote = shared historical archive for the whole team

These analogies assist memory retention and help students form mental models that will anchor later advanced topics like containers, orchestration, and CI/CD pipelines.

# 3. Diagrams (Mermaid + ASCII)

## 3.1 Git Workflow Diagram (Mermaid)
```mermaid
flowchart LR

A\[Working Directory\] \--\> B\[Stage Changes\]

B \--\> C\[Commit to Local Repo\]

C \--\> D\[Push to Remote Repo\]

D \--\> E\[Collaborators Pull\]

E \--\> A
```
## 3.2 Git Branching (ASCII)
```
main: A \-\-- B \-\-- C \-\-- D

\\

feature/login: E \-\-- F \-\-- G
```
## 3.3 Linux Pipeline Diagram (Mermaid)
```mermaid
flowchart LR

logs\[Log File Stream\]

\--\> grep\[grep ERROR\]

\--\> cut\[cut -d \' \' -f 4\]

\--\> sort\[sort\]

\--\> uniq\[uniq -c\]

\--\> final\[sorted Frequency Output\]
```
## 3.4 Permissions Encoding (ASCII)
```
rwx rw- r\--

7 6 4
```
# 4. Exercises (Ungraded Practice)

### Exercise 1 --- Filesystem Navigation

Perform:

1.  Navigate to /var/log

2.  List files sorted by size

3.  Identify largest file

4.  Return to home directory

### Exercise 2 --- Permissions

Perform:

1.  Create deploy.sh

2.  Set to executable for owner only

3.  Verify via ls -l

### Exercise 3 --- Log Filtering

Using /var/log/syslog:

1.  Grep all lines containing error

2.  Extract timestamps

3.  Count frequency by timestamp

### Exercise 4 --- Git Workflow

Perform:

1.  Initialize a repo

2.  Add & commit a file

3.  Create a new branch

4.  Switch to that branch

5.  Merge back into main

### Exercise 5 --- Simple Debug Pipeline

Given logfile:

10.0.0.1 GET /index 200

10.0.0.1 GET /users 404

10.0.0.2 GET /index 200

Task:

-   Count unique IPs

-   Count how many 404 errors occurred

# 5. Solved Exercises

### Solution to Exercise 1

Commands:

```
cd /var/log
```

```
ls -lhS
```

Largest file is first in output. Return home:

```
cd \~
```

### Solution to Exercise 2

```
touch deploy.sh
```

```
chmod 700 deploy.sh
```

```
ls -l deploy.sh
```

### Solution to Exercise 3

```
grep -i \"error\" /var/log/syslog \| cut -d \' \' -f 1-3 \| sort \| uniq -c
```

### Solution to Exercise 4

```
git init
```

```
git add file
```

```
git commit -m \"initial\"
```

```
git branch feature
```

```
git checkout feature
```

```
git checkout main
```

```
git merge feature
```

### Solution to Exercise 5

```
cat logfile \| cut -d \' \' -f 1 \| sort \| uniq -c
```

```
grep \"404\" logfile \| wc -l
```

# 6. Mini-Scenarios (Applied Thinking)

### Scenario 1 --- Deployment Failure

A deployment completes but the service returns 500 errors. Logs show timeouts.

Key questions:

-   Is CPU saturated? (top)

-   Is DB accessible? (ps + logs)

-   Are logs showing retry loops? (grep timeout)

-   Did new config take effect?

Expected investigation tools: tail, grep, pipelines.

### Scenario 2 --- Permission Denied

A script cannot run; error: permission denied.

A likely diagnosis path:

-   Check permissions: ls -l

-   Check ownership: whoami, id

-   Modify via chmod / chown

### Scenario 3 --- Git Conflict

Two developers modify the same lines in config.js.

Git requests manual conflict resolution. Student must decide intended final state using domain knowledge + communication.

### Scenario 4 --- Service Not Restarting

```
systemctl restart app fails silently; logs show missing environment variables. Student must inspect logs and deployment pipeline.
```

# 7. Quiz Questions (with answers at end)

1.  Which directory typically contains system configuration files?

2.  What does chmod 755 file.sh do?

3.  What command tails logs in real-time?

4.  What problem does Git solve?

5.  What is a branch in Git?

6.  What is the difference between git push and git pull?

7.  What do rwx permissions mean?

8.  Why are pipelines useful in Linux?

### Quiz Answers

1.  /etc

2.  Owner rwx, group r-x, others r-x

3.  tail -f

4.  Version control and collaboration on code

5.  An isolated timeline of development changes

6.  Push uploads commits, pull downloads commits

7.  read, write, execute

8.  They compose small tools to inspect, process, and analyze text streams

# 8. Teaching Notes (Instructor Guidance)

-   Students often memorize commands without context; stress workflows and reasons

-   Teach pipelines early; it unlocks debugging superpowers

-   Avoid GUI-based Git tools in foundations; CLI builds transferable discipline

-   Encourage narrative labs (e.g., "deployment broke, investigate!")

-   Reinforce mental models via analogies to reduce cognitive load

-   Allow pair exercises for Git conflicts; social dynamics mirror real teams

-   Return frequently to /var/log, systemd, ps, and grep---these recur in DevOps

-   Use capstone projects with narrative stakes to simulate operations

Perfect. I'll begin writing **Module 2 --- Networking Fundamentals** in full, using:

-   verbose textbook style

-   Markdown structure

-   both Mermaid + ASCII diagrams

-   analogies

-   exercises + solved exercises

-   mini-scenarios

-   quiz + answers

-   teaching notes

Because this will be extremely long (multiple thousand words), I'll generate it in chunks. When the output stops, just say **continue** and I'll resume exactly at the next subsection with no repetition and no summaries.

Starting now...

