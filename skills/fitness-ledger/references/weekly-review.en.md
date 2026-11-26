# Weekly Maintenance

[简体中文](weekly-review.md) · **English**

Start by reading the project home, project index and collaboration rules, record templates, and the log entry for the last successful weekly review. When taking over an existing ledger for the first time, record the objects and configurations you actually read as the starting baseline. If a query returns no results, check permissions, view filters, and pagination. If the user asks you to initialize a ledger, create the source databases needed for the current task under the specified project home, and save their actual returned addresses in the private index.

## Define the Review Scope

- Use the project's time zone to select sleep-day labels for the previous complete week. By default, the week runs from Monday, inclusive, to the following Monday, exclusive. Record the sleep-day IDs you actually retrieve, their UTC start and end times, and any sleep days that remain open. Wakeful activity after midnight on Monday may still belong to a sleep day from the preceding weekend.
- Check separately for source events that occurred during the week, records created or modified since the last review, late entries for earlier periods, and unresolved items from the previous review. List events that have occurred but have no sleep-day association separately, using their known actual dates or legacy labels, and state which you used.
- Read the current field definitions and view configurations before querying. Search within the accessible scope and read through the final page. If a complete change history is unavailable, use accessible views, relevant source pages, and known issues for a targeted review. State the coverage, cutoff, and gaps. Describe the actual scope read from devices and from each specialist chat separately.

## Find Issues That Affect Results

| Area | What to Check |
| --- | --- |
| Sleep days and summaries | Verify boundaries using the final wake-up from main sleep and stable sleep-day IDs. Check whether a source event is linked to multiple sleep days, whether the main sleep that opens a sleep day is counted twice, or whether an interim summary is incorrectly presented as a final daily summary. Recheck events and summaries revised after delayed synchronization. |
| Intake | Verify actual consumption status, serving units, sources, and the version in effect. Recalculate recorded subtotals from eligible source events, stating gaps and estimates. Keep product labels on a per-serving basis, and check the actual number of servings when ingredients may be counted both within a combination and separately. |
| Training and body measurements | Count events through parent records; use child records for sets, splits, or individual readings. Check mirrored device records, units, set counts, averages, and sums. Preserve separate identities for multiple real activities on the same day. |
| Plans | Compare the confirmed version with actual training. Link progress summaries to evidence of completion. If splits are missing, leave split-level verification pending. When only part of a proposal is adopted, update only that part. |
| Data sources and dependencies | Compare the index, templates, and dashboard with the actual fields. If aggregate values cannot be read directly, recalculate them from source records eligible for inclusion and state the method. Keep summaries based on legacy date labels separate. |

## Navigation and Repairs

Read the project home, the direct children of every existing module, and the data sources behind relevant views. Compare their locations and object IDs with the previous review. The seven-module baseline is in the [Skill entry point](../SKILL.md). Place new shortcut views, supporting rules, and set-level details within their appropriate modules. A genuinely independent topic may have a new entry point; document the reason. Use page mentions or linked views for references across modules.

For a misplaced object whose destination is clear and whose sharing scope can be verified, save its original location, ID, view filters, and sorting before moving the original object within the project. After the change, open the original link and verify the new parent chain, configuration, and dependencies. For changes involving permissions, merging real records, or altering the meaning of historical statistics, present the affected objects, impact, and smallest proposed change for the user to decide.

Before a targeted correction, reread the original values and sources. Afterward, read back the affected relationships, fields, and summaries. If attribution or values change, document why a review is needed, then close only the corresponding issue once it has been verified. If the outcome of a creation operation is uncertain, check for an existing record using the source event's characteristics before deciding how to proceed.

## Logs and Notifications

Reuse the entry for the same week in the private maintenance log, along with existing issue records. State the window, coverage, and access gaps. For each issue, give the source page, field, evidence, impact, outcome, and next checkpoint. For moves and structural repairs, save the original and new locations, object IDs, and rollback evidence. Do not include maintenance logs in event counts or ledger totals.

Follow the project's notification preferences: report new issues, status changes, repairs, access failures, or matters requiring a decision. Skip repeat reports when nothing material has changed. For recurring mistakes, provide a prompt the user can paste into the relevant chat, specifying who should check which source record and after what action.
