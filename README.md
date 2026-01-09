# DevOps Foundations Coursebook

A markdown-first DevOps foundations coursebook covering Linux/Git, networking, cloud fundamentals, containers, and systems/ops thinking. It also includes instructor resources and capstone projects.

## How to read

Start at `docs/00-preface.md`, then continue in order:

- `docs/01-linux-git.md`
- `docs/02-networking.md`
- `docs/03-cloud-foundations.md`
- `docs/04-containers-docker.md`
- `docs/05-systems-ops.md`
- `docs/06-instructor-resources.md`

## Build

This repo is Markdown-first. If you want a single-file build, concatenate the chapter files in order:

```powershell
Get-Content docs/00-preface.md,docs/01-linux-git.md,docs/02-networking.md,docs/03-cloud-foundations.md,docs/04-containers-docker.md,docs/05-systems-ops.md,docs/06-instructor-resources.md | Set-Content book.md
```