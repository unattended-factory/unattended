<p align="center">
  <img src="assets/banner.png" alt="unattended: runs with the lights off. Tells you when it needs you." width="100%">
</p>

<h3 align="center">Ship while you sleep. Get woken up only when it matters.</h3>

<p align="center">
  <b>unattended</b> is a dark software factory.<br>
  Your Linear backlog goes in. Verified, gated pull requests come out.
</p>

<p align="center">
  <a href="https://unattended.unmerged.tech"><b>Website</b></a> ·
  <a href="#whats-coming">What's coming</a> ·
  <a href="https://github.com/mikegorelikoff">Author</a>
</p>

<p align="center">
  <img alt="status: work in progress" src="https://img.shields.io/badge/status-work%20in%20progress-f5b83d?style=flat-square&labelColor=black">
  <img alt="tracker: Linear" src="https://img.shields.io/badge/tracker-Linear-lightgrey?style=flat-square&labelColor=black">
  <img alt="merge: GitHub" src="https://img.shields.io/badge/merge-GitHub-lightgrey?style=flat-square&labelColor=black">
</p>

---

## Work in progress. Lights are about to go off.

Most of a backlog is work you already know how to do. It still costs a context switch, a review and an afternoon, every time.

unattended takes that work off your plate and keeps the standard where it was. It does not ask you to trust an agent. It asks an independent verifier, a set of deterministic gates and GitHub's own branch protection, and it stops loudly when any of them says no.

The result is a factory that looks like nothing is happening, until the one moment something needs you.

```mermaid
flowchart LR
    A[Linear issue] --> B[Build]
    B --> C[Verify]
    C --> D[Gates]
    D --> E[GitHub merges]
    D -. only when stuck .-> F((A person))
    style F fill:#f5b83d,stroke:#f5b83d,color:#0d1013
```

## What's coming

- **A factory that reads your backlog.** Label an issue, and it is picked up. No new tool to learn.
- **A second opinion on every change.** The author never grades its own work.
- **Merges you can accept without reading.** GitHub has the last word, always.
- **A console that stays quiet.** One glance, a few times a day. One amber light when it needs you.
- **Trust that is earned.** Every kind of work starts supervised and moves up on evidence.
- **One install.** A single command, configs you can read and review.

The first release is being built in the open, stage by stage.

## Follow along

Star the repository to see it land, and watch the [website](https://unattended.unmerged.tech) for the first night shift.

<p>
  <a href="https://github.com/unattended-factory/unattended"><img alt="Star unattended" src="https://img.shields.io/badge/%E2%98%85%20Star%20to%20follow-f5b83d?style=for-the-badge&labelColor=black"></a>
</p>

---

<sub>unattended · built by <a href="https://github.com/mikegorelikoff">Mihail Gorelikov</a> · Copyright 2026 Mihail Gorelikov</sub>
