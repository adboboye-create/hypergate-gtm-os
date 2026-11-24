# Clay: tables, Audiences or Workflows for this play

Status: draft, 2026-11-24. Applies to the new-joiner play ([workflow spec](../../output/campaigns/new-joiner-infra-mobility-180-days/workflow-spec.md)). Source for what each surface does: Clay's own guidance in the Clay agent plugin (skills `workflows-vs-tables`, `audiences`, `workflows`, v2.40.0, read 2026-11-24).

## What each one is

| Surface | What it is | Best at | Limits that matter here |
|---|---|---|---|
| **Table** | A spreadsheet of rows and columns. Each column is a formula or an action (enrichment, AI, lookup). | Building and proving a play: you see every cell, run one row first, and fix a column before scaling. One-off or occasional pulls. | Someone has to run it. About 50,000 rows per table. Tables can't be built from the Clay CLI, only in the app (or with `tools/rex`). |
| **Audience** | Clay's store of the workspace's own people and companies. A **segment** is a saved filter over them, not a copy. | Keeping one record per person or company over time. A dynamic segment updates itself as records change, so it works as a live work queue. | Holds records, doesn't enrich them. Search results don't land there by themselves; something has to write them in. |
| **Workflow** | An automation: a trigger, then steps (enrichment, AI, code), branches, and write-back. | Repeatable work that runs on its own: on a schedule, when a record enters a segment, on a signal or webhook. Run history for debugging. Built and edited from Claude Code with the Clay CLI. | Can't use a Clay search as its source yet. Clay's advice is to send the search to Audiences and trigger the workflow from there. Each paid step costs the same as in a table. |

## Which one for which job in this play

| Job | Surface | Why |
|---|---|---|
| Find new joiners (Find People search, last 6 months) | **Table** | Workflows can't use a search as a source yet. The table shows the raw search rows, which we checked by hand (false positives like "MDM & RDM Analyst"). |
| Free checks, company gates, AI role check, routing, Ready to Contact | **Table** | This is where the logic was designed and proved, one row at a time, with each cost read off the cells. 87 people is far from the row limit. |
| One record per contact, kept over time | **Audience** | The person record outlives one monthly pull: next month's search adds rows to the table, but the person stays one record with their status. |
| "Who still needs an email?" | **Dynamic Audience segment** | The filter (Ready to Contact, email market, no email, not yet tried) keeps itself current. A record leaves the segment as soon as the workflow writes an email or "not found". |
| Find emails for that segment, every time someone enters it | **Workflow** | Runs without anyone pressing a button, branches on the result (found or not found), writes the result back, and keeps a run log. |

## Why the play was built in a table first

- The spec had to be proved: each gate, the AI column and the email waterfall were checked on one row, then a few, then all ([build guide](../../output/campaigns/new-joiner-infra-mobility-180-days/clay-build/new-joiner-infra-mobility-180-days-clay-build-guide.md)). A table makes that cheap and visible.
- The source is a Clay search, which a workflow can't start from.
- The volume is small (87 people, 79 companies) and the pull is monthly, so running it by hand isn't a burden yet.

## When to move more of it to Workflows

- The monthly pull should run unattended (schedule, or a signal such as a job change).
- Volume nears the table row limit.
- Routing gets more branches, such as handing replies to a rep or pushing to a sequencer and CRM.

At that point the table's logic is rebuilt as workflow steps. There is no automatic migration; the table's data stays where it is.

## What exists now

See [the clay-build README](../../output/campaigns/new-joiner-infra-mobility-180-days/clay-build/README.md) for links: the table workbook, the Audiences load, the segment and the workflow.
