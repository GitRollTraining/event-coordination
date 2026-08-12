# Project 3: Event Planning and Coordination Brief

Interview the Event and Operations Coordinator, then build and run an Agent Skill that turns the provided attendee, budget, calendar, vendor, and event-brief sources into normalized evidence and a human-reviewable event plan.

## Start

1. Fork this repository and work on your fork's `main` branch.
2. Interview the Gemini stakeholder in English. Explain which source you need and why; links are provided only when relevant.
3. Implement, run, and validate the skill.
4. Push the complete repository to `main` without changing or deleting `entire/checkpoints/v1`.

Do not create a separate Session Log. The supported environment records the work automatically.

## Required submission

```text
event-planning-coordination-brief/
├── SKILL.md
├── scripts/
│   └── <executable implementation>
└── references/
    └── <focused operating references>
deliverables/
├── normalized/
│   ├── attendee_signals.csv
│   ├── budget.csv
│   ├── calendar_constraints.csv
│   └── vendor_quotes.csv
└── report.md
```

Follow the [Agent Skills specification](https://agentskills.io/specification). The `SKILL.md` frontmatter must include `name: event-planning-coordination-brief` and a useful `description`. Document the runtime, inputs, exact command, outputs, validation, and safe-failure behavior. Validate with:

```bash
skills-ref validate ./event-planning-coordination-brief
```

The implementation must recognize source roles from schemas rather than fixed filenames or column order, preserve source versions, separate hard constraints from preferences, compare vendor capacity, accessibility, availability, expiry, and cost, and surface approval needs or unresolved conflicts. It must not send invitations, commit to a vendor, make a payment, alter a production calendar, or invent missing facts.

Keep secrets and hidden assessment material out of the repository. Before pushing, run the documented command from a clean checkout and confirm that `report.md` agrees with all normalized CSV files.
