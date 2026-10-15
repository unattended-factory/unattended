<p align="center">
  <img src="assets/banner.png" alt="unattended: runs with the lights off. Tells you when it needs you." width="100%">
</p>

<p align="center">
  <b>A dark software factory.</b> Issues go in through Linear. Reviewed, merged pull requests come out of GitHub.<br>
  A person is paged only when something needs one.
</p>

<p align="center">
  <img alt="status: pre-alpha" src="https://img.shields.io/badge/status-pre--alpha-f5b83d?style=flat-square&labelColor=0d1013">
  <img alt="config: TOON" src="https://img.shields.io/badge/config-TOON-4fc3f7?style=flat-square&labelColor=0d1013">
  <img alt="tracker: Linear" src="https://img.shields.io/badge/tracker-Linear-e8edf0?style=flat-square&labelColor=0d1013">
  <img alt="license: MIT" src="https://img.shields.io/badge/license-MIT-e8edf0?style=flat-square&labelColor=0d1013">
</p>

---

> **Status: pre-alpha.** The concept, the loop and the design system are done. The installer is being built. Nothing here is published to npm yet, and the commands below describe the target behaviour.

## What it is

**unattended** pulls issues from Linear, builds each one with headless Claude Code, verifies the result with an independent verifier, runs deterministic gates, and merges through GitHub branch protection. If a change cannot pass, it stops and escalates with the reason. The default state of the factory looks like nothing happened.

It ships as one npm package with a CLI, a web console and an optional nginx deploy. Every config is [TOON](https://github.com/toon-format/toon), so people and models read the same short files.

## The loop

```
Linear issue ─▶ Intake ─▶ Builder ─▶ Verifier ─▶ Gates ─▶ Draft PR ─▶ Merge
   (labelled)    5 checks   worktree    other model   7 checks   GitHub      branch rules
                    │          │            │            │
                    └──────────┴────────────┴────────────┴──▶ Needs a person (with the reason)
```

| Stage | Who acts | What it returns |
| --- | --- | --- |
| Intake | Code | Five checks. "Not taken. Missing: Acceptance criteria, Size." |
| Builder | Agent | A branch with a failing reproduction test, then the fix |
| Verifier | Agent, different model | Strict JSON verdict: PASS or FAIL with risks |
| Gates | Code | CI, acceptance scenarios, diff budget, forbidden paths, dependencies |
| Merge | GitHub | Required checks `factory/verifier` and `factory/gates`, then auto-merge or a queue |

The Builder never grades its own work. Held-out scenarios, which the Builder cannot read, decide acceptance.

## Principles

- **Real systems only.** Real Linear, real GitHub, real money. No mocks in the loop.
- **Every call is metered.** A token ledger and budgets are checked before each call, per issue and per day. Cost per accepted change is the number that matters.
- **Promotion is earned.** Each task type climbs S1 to S6, from shadow mode to project mode, on evidence. One revert drops it a stage.
- **A failure is never silent.** Every Hold or Fail carries its cause with a number or a name, in the console and in the Linear comment.
- **One switch.** Pause stops everything. Calls in flight finish their current step and nothing new starts.

## Quickstart (target)

```bash
npm i -g unattended
unattended init        # writes .unattended/config.toon, checks Linear and GitHub access
unattended doctor      # verifies tokens, branch protection, sandbox
unattended run --once  # shadow mode: drafts PRs, a person merges
unattended ui          # web console on 127.0.0.1:7421
```

A minimal config:

```toon
version: 1
mode: shadow
linear:
  team: ENG
  label: factory
budgets:
  issue_usd: 5.00
  day_usd: 60.00
max_rounds: 3
workers: 1
```

## The console

Seven screens on one shell: Overview, Queue, Issue, Cost, Scenarios, Task types, Project, Config. The Tower in the header shows three lamps. Only the amber one asks for a person.

| State | Mark | Word |
| --- | --- | --- |
| Queued | hollow circle | Queued |
| Running | turning ring | Building, round 2 |
| Pass | disc with check, sky blue | Merged |
| Hold | amber diamond | Needs a person |
| Fail | square with cross | Rejected at intake |
| Paused | two bars | Paused by Mike |

Status is always shape, word and color together, and pass is blue, not green, so nothing depends on a red-green difference.

## Remote access

An optional nginx deploy puts the console on your own domain: sign-in, `viewer` and `operator` roles, CSRF protection, trusted-proxy handling, systemd units and a compose file.

## Design

The look is "monochrome until something needs you". Night is the default theme, Day is the same structure for bright rooms. The design system, with 29 components and nine example pages, lives with the project.

| Token | Night | Day |
| --- | --- | --- |
| `ground` | `#0d1013` | light graphite on white |
| `pass` | `#4fc3f7` | `#0a6492` |
| `hold` | `#f5b83d` | `#855400` |
| `fail` | `#ff7b5c` | `#b2371a` |

Type: Instrument Sans for text, IBM Plex Mono for ids and numbers, Barlow Semi Condensed for the one figure a screen is about.

## Roadmap

- [x] Concept: loop, project layer, limits
- [x] Design system
- [ ] G1 Core: Linear client, intake, token ledger, TOON config
- [ ] G2 Build and verify: worktrees, Builder, Verifier, gates
- [ ] G3 Merge: branch protection, auto-merge, escalation
- [ ] G4 Console: web UI, roles, nginx deploy
- [ ] G5 Promotion: S1 to S6, evidence and demotion
- [ ] G6 Project mode: planner, waves, held-out scenarios
- [ ] Native Linear agent: delegation instead of a label

## Limits

A dark factory does not remove review, it moves it. Without held-out scenarios and a second model, a green pipeline can still be wrong. Start in shadow mode, keep budgets low, and promote a task type only when the evidence says so.

## License

MIT.
