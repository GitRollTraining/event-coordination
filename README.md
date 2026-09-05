# Project C: Event Planning & Coordination Brief

Build and run an Agent Skill that helps an Event and Operations Manager combine changing event goals, attendee signals, budget and vendor records, official venue evidence, an official floor plan or image, and calendar constraints into a traceable planning package for human review.

## Start

1. Fork this repository and work on your fork's `main` branch.
2. Open the [Project C stakeholder interview](https://work-sim-alpha.catalyte.ai/s/project-c-event-coordination) to understand the manager's workflow, sources, constraints, uncertainty, and approval boundaries.
3. Implement one documented command that fetches the disclosed current sources, writes each required workflow snapshot when that stage completes, compares options, produces every final artifact, and validates the package.
4. Run the command, review the results, and push the complete repository to `main` without changing or deleting `entire/checkpoints/v1`.

Do not create a separate Session Log. The supported environment records the work automatically.

**Interview rule.** You conduct the stakeholder interview yourself, and the questions are yours. Do not connect a coding agent or any other AI to the interview to run, script, or automate it. The interview transcript is assessed together with the code; a project whose interview was run by an agent is not scored.

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
├── snapshots/
│   ├── 01-scope-and-approval-gates.json
│   ├── 02-source-capture.json
│   ├── 03-constraint-model.json
│   ├── 04-planning-baseline.json
│   ├── 05-option-generation.json
│   ├── 06-feasibility-testing.json
│   ├── 07-decision-and-approval.json
│   ├── 08-draft-propagation.json
│   ├── 09-publication-validation.json
│   └── evidence/
│       └── <retrieved floor plan or image evidence>
├── vendor-comparison.csv
├── event-plan.md
├── event-calendar.ics
└── draft-communications.md
```

## Required snapshot chain

Every stage file must conform to [`snapshot.schema.json`](snapshot.schema.json). All nine use one `run_id`. From stage 2 onward, `predecessor` identifies and hashes the immediately preceding file. Each stage names the upstream record IDs it consumed and records it produced.

| Stage | Required state |
|---|---|
| 01 | objective, deadline, owners, approval gates |
| 02 | every structured, web, image, video, and calendar source attempt |
| 03 | hard constraints, preferences, assumptions, unknowns, conflicts |
| 04 | dated headcount, schedule, budget, accessibility baseline |
| 05 | materially different options and early rejection reasons |
| 06 | option-level feasibility and unresolved conditions |
| 07 | trade-offs, recommendation or deferral, learner decisions, approvals |
| 08 | propagated draft artifacts, affected dependencies, unresolved items |
| 09 | final artifact paths and hashes, validation and publication status |

Run status is `complete`, `partial`, `blocked`, or `failed`. Retrieval status is `retrieved`, `unavailable`, `invalid`, `unverified`, or `stale`. Option feasibility is `feasible`, `infeasible`, `conditional`, or `unverified`. Missing or conflicting records must remain traceable until evidence or a human decision resolves them.

On successful image retrieval, `snapshots/evidence/` preserves the official floor-plan or image bytes as part of the assessed run snapshot. Stage 02 records the file and page, region, timestamp, or equivalent locator; dependent stages consume its evidence ID.

## Decision behavior

The nine files are an ordered audit trail, but the planning workflow must represent decisions and re-planning:

- unavailable required floor-plan evidence suppresses dependent spatial or accessibility claims; one unavailable vendor record only narrows the supported comparison;
- an option that fails a hard constraint is rejected, while insufficient evidence remains unresolved rather than favorable;
- if no option is feasible, explicitly defer and identify what evidence or constraint must change;
- when feasible options do not dominate one another, choose and justify a practical trade-off policy or defer to the human owners;
- a material change returns to the earliest affected constraint, baseline, option, feasibility, decision, or draft stage and regenerates affected downstream work;
- calendars and communications remain drafts until Operations and budget owners decide.

## Final artifacts

- `vendor-comparison.csv` compares materially different options, including availability or verification state, cost and currency where known, feasibility, material constraints, evidence references, trade-offs, and unresolved conditions.
- `event-plan.md` states the objective, planning basis, options, recommendation or deferral, feasibility, schedule, budget, accessibility and safety considerations, risks, unknowns, change impacts, and approval requests.
- `event-calendar.ics` is a valid draft calendar consistent with the selected or proposed plan. `draft-communications.md` contains clearly unsent drafts that preserve uncertainty and approval dependencies.

Follow the [Agent Skills specification](https://agentskills.io/specification). The `SKILL.md` frontmatter must include `name: event-planning-coordination-brief` and a useful `description`. Document prerequisites, runtime inputs, the exact command, output paths, validation, and material failure behavior. Validate the package with:

```bash
skills-ref validate ./event-planning-coordination-brief
```

## Runtime evidence

Each invocation must read the current disclosed structured records, official venue sources, required official floor-plan or image evidence, and calendar data. Video evidence is optional. Do not use bundled answers or a silent cached copy as the primary source.

The nine snapshots are part of the submitted result. Write them during the workflow, not retrospectively after the final drafts. Preserve predecessor hashes and stable record IDs so another reviewer can follow source evidence through constraints, options, feasibility, decisions, and propagated artifacts.

You do not need to reconstruct an earlier external-site version. If one vendor quote or record is missing or cannot be verified, continue supported comparison work and mark that vendor record unavailable or unverified. If required image evidence is unavailable, do not make dependent spatial or accessibility claims.

## Planning and safety boundary

Compare multiple materially different options, explain feasibility and trade-offs, and keep every affected artifact consistent when a material input changes. The calendar and communications are drafts. The skill must not expose credentials, book, pay, invite, commit to a vendor, alter a source, write to a production calendar, or bypass Operations or budget approval.

Before pushing, run the documented command from a clean checkout and confirm that every snapshot passes the schema, the lineage is intact, and the comparison, plan, calendar, and communication drafts agree with stages 07–09.
