# Project C: Event Planning & Coordination Brief

Build and run an Agent Skill that helps an Event and Operations Manager combine changing event goals, attendee signals, budget and vendor records, official venue evidence, an official floor plan or image, and calendar constraints into a traceable planning package for human review.

## Start

1. Fork this repository and work on your fork's `main` branch.
2. Open the [Project C stakeholder interview](https://work-sim-alpha.catalyte.ai/s/project-c-event-coordination) to understand the manager's workflow, sources, constraints, uncertainty, and approval boundaries.
3. Implement one documented command that fetches the disclosed current sources, creates a snapshot, compares options, produces every required artifact, and validates the package.
4. Run the command, review the results, and push the complete repository to `main` without changing or deleting `entire/checkpoints/v1`.

Do not create a separate Session Log. The supported environment records the work automatically.

## Required submission

```text
snapshot.schema.json  # provided contract; keep unchanged
event-planning-coordination-brief/
├── SKILL.md
├── scripts/
│   └── <executable implementation>
└── references/
    └── <focused operating references>
deliverables/
├── snapshot.json
├── snapshot-files/
│   └── <retrieved floor plan or image evidence>
├── vendor-comparison.csv
├── event-plan.md
├── event-calendar.ics
└── draft-communications.md
```

Minimum artifact contract:

- `snapshot.json` must conform to [`snapshot.schema.json`](snapshot.schema.json). It records every attempted source, including failed or unused attempts, and marks whether retrieved evidence was used for claims.
- Run status is `complete`, `partial`, `blocked`, or `failed`. Retrieval status is `retrieved`, `unavailable`, `invalid`, `unverified`, or `stale`. Option feasibility is `feasible`, `infeasible`, `conditional`, or `unverified`.
- `complete` means the normal package passed validation; `partial` means supported work remains usable with non-blocking gaps; `blocked` means required evidence prevents dependent claims but a reviewable failure package exists; `failed` means no reviewable package beyond the failure record could be produced. Record the status that actually occurred—do not simulate every state.
- For source attempts, use `retrieved` only after content checks pass; `unavailable` when it cannot be obtained; `invalid` when the response fails format or semantic checks; `unverified` when identity, authority, or freshness cannot be established; and `stale` when retrieved content is too old for a current claim.
- Keep every required `decision_state` collection in the JSON. Use an empty array when that class did not occur; do not invent records merely to demonstrate a status.
- Record the selected option ID in `selected_recommendation`, or `null` when the recommendation is deferred.
- On a successful image retrieval, `snapshot-files/` preserves the official floor-plan or image bytes used for spatial or accessibility claims. Snapshot observations reference that local file and a page, region, or equivalent locator.
- `vendor-comparison.csv` compares materially different options, including availability or verification state, cost and currency where known, feasibility, material constraints, evidence references, trade-offs, and unresolved conditions.
- `event-plan.md` states the objective, planning basis, options, recommendation or deferral, feasibility, schedule, budget, accessibility and safety considerations, risks, unknowns, change impacts, and approval requests.
- `event-calendar.ics` is a valid draft calendar consistent with the selected or proposed plan. `draft-communications.md` contains clearly unsent drafts that preserve uncertainty and approval dependencies.

Follow the [Agent Skills specification](https://agentskills.io/specification). The `SKILL.md` frontmatter must include `name: event-planning-coordination-brief` and a useful `description`. Document prerequisites, runtime inputs, the exact command, output paths, validation, and material failure behavior. Validate the package with:

```bash
skills-ref validate ./event-planning-coordination-brief
```

## Runtime evidence

Each invocation must read the current disclosed structured records, official venue sources, required official floor-plan or image evidence, and calendar data. Video evidence is optional. Do not use bundled answers or a silent cached copy as the primary source.

`deliverables/snapshot.json` is part of the submitted result. Record the run context, every attempted source and retrieval result, evidence actually used, hard constraints, preferences, assumptions, unknowns, conflicts, considered and rejected options, unresolved items, affected dependencies, approvals, and your material design decisions and rationale. Media-derived observations need a page, region, timestamp, or equivalent locator. Validate the snapshot against `snapshot.schema.json` before reporting a successful run.

You do not need to reconstruct an earlier external-site version. If one vendor quote or record is missing or cannot be verified, continue supported comparison work and mark that vendor record unavailable or unverified. If required image evidence is unavailable, do not make dependent spatial or accessibility claims.

## Planning and safety boundary

Compare multiple materially different options, explain feasibility and trade-offs, and keep every affected artifact consistent when a material input changes. The calendar and communications are drafts. The skill must not expose credentials, book, pay, invite, commit to a vendor, alter a source, write to a production calendar, or bypass Operations or budget approval.

Before pushing, run the documented command from a clean checkout and confirm that the snapshot, comparison, plan, calendar, and communication drafts agree.
