# Event Planning & Coordination — starter

Read the [formal assignment](https://private-pecorino-70e.notion.site/Project-C-Event-Planning-Coordination-Brief-Learner-assignment-3da0b700541e813a8a91d0741d6ac96a?source=copy_link), [stakeholder interview](https://work-sim-alpha.catalyte.ai/s/project-c-event-coordination) and the [shared course guide for session capture](https://classroom.google.com/c/ODcyMjA4NTkwNDk2/m/ODc0NzI2NzQzMzQ2/details). The assignment contains the required work, source routes and submission contract.

## Start

Use the supported Agent Skills-capable coding environment and working-copy route assigned by your facilitator. To clone this starter into an isolated working directory:

```bash
git clone https://github.com/GitRollTraining/event-coordination.git
cd event-coordination
```

The only supplied technical file is [snapshot.schema.json](snapshot.schema.json). Keep its contract unchanged.

Optional schema-read smoke from this directory:

```bash
python3 -c "import json,pathlib; s=json.loads(pathlib.Path('snapshot.schema.json').read_text()); assert s['type']=='object'; print('Public schema readable; business workflow not implemented')"
```

## Run and submit

Create the Skill and document its end-to-end command as required by the online assignment. This starter contains no implementation to run. Submit your implementation and the assignment's required outputs at an identified revision through the assigned submission route; preserve the actual interview and coding-session evidence described in the shared guide. Keep credentials out of the repository.

If a required online assignment, guide or business source is unavailable, report the actual access problem; do not replace it silently with repository data. The designer's pre-S3 Agent trial uses its declared isolated test and capture route and does not establish human learner performance.
