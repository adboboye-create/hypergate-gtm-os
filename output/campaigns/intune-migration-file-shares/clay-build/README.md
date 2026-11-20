# Clay build: Intune migration leaves file shares behind

Workflow slug: `intune-migration-file-shares`. Spec: [../workflow-spec.md](../workflow-spec.md).

## Clay

| What | Link |
|---|---|
| Workspace folder | https://app.clay.com/workspaces/1206365/home/f_0too2hlcYvMge63yz2T |
| Workbook "Hypergate-Intune Users (180 days)" | https://app.clay.com/workspaces/1206365/workbooks/wb_0too2hqE6A9WA6UQCp8 |
| Table: Exclusion & Block list | https://app.clay.com/workspaces/1206365/workbooks/wb_0too2hqE6A9WA6UQCp8/tables/t_0topxuyxz6fadCao9d7 |
| Table: Enterprise Architects, DACH, Regulated Industries (people) | https://app.clay.com/workspaces/1206365/workbooks/wb_0too2hqE6A9WA6UQCp8/tables/t_0torupffE645kbSrVwk |
| Table: Companies | https://app.clay.com/workspaces/1206365/workbooks/wb_0too2hqE6A9WA6UQCp8/tables/t_0tose66FtiXahD5gC9D |

Workbook and table links are built from the IDs Clay returned (read with `tools/rex` on 2026-11-20). If one doesn't open, use the folder link and click through.

The links need a login to the Clay workspace. They don't expose data to anyone without access.

## Files in this folder

- [intune-migration-file-shares-clay-build-guide.md](intune-migration-file-shares-clay-build-guide.md): step-by-step build guide (5 tables, 14 parts).
- [intune-migration-file-shares-clay-flow.png](intune-migration-file-shares-clay-flow.png): swimlane diagram of the build. The source is in `.json`, and the `.html` opens in a browser.
- `exclusions.csv`: the never-contact list (37 rows). Not in Git (`*.csv` is ignored); the working copy is in `~/Downloads/exclusions.csv`.

## Status

- First Clay test run 2026-11-19: 77 people imported, 70 passed ICP, 57 work emails found, 222 net credits. Full funnel and spend: `work-log/2026-W47.md` (2026-11-20 20:10 entry).
- **The Clay build differs from the workflow spec:** a 180-day new-joiner people search (architects, DPOs, systems engineers) in DE, CH, AT, UK and CA, with no Intune job-post trigger and no routing cells. Decide whether it's a separate play or gets rebuilt to the spec.
- Don't email the German contacts (opt-in market) or the Canadian ones (spec: LinkedIn-only).
- Nothing sends until legal signs off the compliance brief, Hypergate sales answers the partner-region memo and Hypergate approves `facts.md`.
