# Fitness Ledger

[简体中文](README.md) · **English**

A bilingual Codex skill for keeping running, strength, climbing, nutrition and body measurements in one Notion project. It organizes events by the final wake-up from main sleep. If you finish a run and eat at 1 a.m. before going to bed, both belong to the sleep day you were already awake for. An afternoon nap stays in that same day's record.

The skill covers [training plans and event records](skills/fitness-ledger/references/event-records.en.md), [sleep days and daily summaries](skills/fitness-ledger/references/sleep-day.en.md), and [weekly maintenance](skills/fitness-ledger/references/weekly-review.en.md). Each proposed plan, accepted change and completed workout has a distinct place in the ledger. A late report in one chat can be traced back to the original event in another.

## Installation

Download `fitness-ledger.zip` from [Releases](https://github.com/kuoyang1999/fitness-ledger-skill/releases), extract it, and place the `fitness-ledger` folder in your Codex skills directory (by default, `~/.codex/skills/`). Alternatively, ask a Codex chat with GitHub access:

> Install the skill at skills/fitness-ledger from the GitHub repository kuoyang1999/fitness-ledger-skill.

To install from the command line, run the following. If a local copy already exists, the command leaves it in place so you can review it before updating.

```sh
git clone https://github.com/kuoyang1999/fitness-ledger-skill.git
skills_dir="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$skills_dir"
test ! -e "$skills_dir/fitness-ledger" && cp -R fitness-ledger-skill/skills/fitness-ledger "$skills_dir/"
```

In a new chat, invoke `$fitness-ledger` and describe your task. On first use, provide your Notion project home, default IANA time zone and the activities you track. For sleep imports, use an environment connected to your own Apple Health data with read access. You can also report your final wake-up time directly. Daily summaries and weekly reviews can run on request. Recurring schedules are configured separately.

## Connect your Notion project

Enable the Notion connection in the chat where you use the skill and sign in to your own account. Give the account and connection access to the project you want to use. Share the project home or index link in your private chat. For a read-only check, try:

> Use $fitness-ledger to open [my project home] through Notion. Tell me the page title you actually read and where its training records and daily summaries are. Just check the connection this time.

Opening the home page verifies read access to that page. Saving entries requires edit access to the target database and authorization for the task. The skill uses the current chat's Notion tools to look up records, make edits and read them back. The download contains no account credentials, tokens or personal project links. Apple Health is a separate data source.

## Three ways to use it

**A new training, food or measurement chat**

> Use $fitness-ledger to take over my [activity] records. My Notion project is [private link], and my default time zone is [IANA time zone]. Read the index, current confirmed plan, latest source record and open questions. Save actual events in the existing database and apply late reports to the original entries. Start by telling me the current plan and what needs checking next.

**Daily summaries**

> Use $fitness-ledger to maintain my daily summaries. Check my reports and Apple Health for main sleep. Start each sleep day at my final wake-up. If device records are missing, assess whether recent verified sleep in a comparable routine supports an estimate and record the basis. Save a midday snapshot and finalize the sleep day once the next main wake-up is established. If late data move a boundary, recheck the affected source events.

**Weekly maintenance**

> Use $fitness-ledger to review last week's sleep-day labels and records added or corrected since the last check. Review training, food, measurements, plan progress and page placement. Make local corrections supported by source records, read them back, then record the scope and open issues in the existing maintenance log. Notify me when you find something new, a status changes or I need to make a decision.

Keep project links, device exports, actual records and personal goals in your own private project. This repository publishes the workflow. Examples are fictional.
