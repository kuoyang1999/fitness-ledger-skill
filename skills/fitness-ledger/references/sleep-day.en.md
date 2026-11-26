# Sleep Days and the Two Daily Fitness Summaries

[简体中文](sleep-day.md) · **English**

Read this reference when handling early-morning records, importing sleep data, assigning events across time zones, or preparing daily summaries. First read the project's current rules and field definitions. This reference describes the general method; personal routines, actual time zones, and adopted exceptions belong in the user's own project.

## Define cycles by the final wake-up from main sleep

A sleep day cycle is a half-open interval: **the final wake-up from this main sleep ≤ event occurrence time < the final wake-up from the next main sleep**. Identify each cycle by a stable record ID. Its “sleep day” is a display label derived from the local date of the wake-up that starts it. The date alone is not guaranteed to be unique.

- If the person is still awake after midnight, meals and training remain in the current cycle. Midnight does not automatically start a new sleep day.
- Naps, brief awakenings during the night, and waking before resuming the same main sleep do not open a new cycle. Main sleep may be split by awake intervals. Do not count those intervals as sleep.
- Follow the states “awake → possible main sleep, awaiting confirmation → final wake-up opens a new cycle.” Falling asleep can indicate a pause in activity. It does not by itself mean the next cycle has begun.
- Identify main sleep using the person's account, sleep continuity, subsequent activity, and recent routine. Duration or a fixed clock time can help, but cannot alone establish that “a short sleep is a nap” or “passing this time always starts a new sleep day.”
- An explicit statement such as “I haven't slept yet,” “that was only a nap,” or “I've got up and started my day” takes precedence over an estimate based only on routine. If it conflicts with device records, retain both sources and explain which boundary is used.
- A cycle may exceed 24 hours when there is evidence that the person stayed awake all night. Missing sleep data alone does not establish several days of continuous wakefulness, nor should every later event remain attached indefinitely to an old cycle.

**Count the main sleep that opens a sleep day only once.** The main sleep ending in the current cycle's opening wake-up supplies that cycle's opening recovery data, even though the sleep itself occurred before the cycle began. The preceding cycle uses that final wake-up only as its end boundary and does not also add the same main sleep to its totals. Assign daytime naps to the cycle active when they occurred, and list them separately. They neither replace nor duplicate the main sleep that opens the sleep day. Each sleep segment must have one traceable cycle assignment.

## Sleep evidence and Apple Health

Determine “when the person woke up,” “how long they slept,” and “which cycle an event belongs to” separately. One piece of evidence does not answer every question. For boundaries, normally prioritize the person's explicit account of their final wake-up or of not having slept, then reconcile timestamped sleep records with known sources and activity in the same period. Use recent personalized estimates last. Calculate sleep duration from actual sleep segments. A reported getting-up time does not mean the entire gap between the device's last sleep segment and getting up was spent asleep.

When Apple Health is currently readable and the task permits access:

1. Read Apple Health `sleepAnalysis` samples over a window covering both sides of the target boundary. Record the actual query time, UTC range, sources, whether all pages were retrieved, and the coverage returned. Only data successfully read in this run may be described as “queried.”
2. Preserve original times, device or app, sleep categories, and source identifiers actually returned. If there is no native ID, source, original start and end times, and category can support duplicate checks. Do not present that combination as a native ID.
3. Check for overlap across devices, mirrored apps, and sleep stages. Do not add generic “asleep” samples to detailed stages covering the same time. Awake time is not sleep, and “in bed” does not mean asleep. Preserve both the raw values and the method used to deduplicate totals.
4. The end of a device's last sleep segment is only a candidate wake-up boundary. Check whether the person slept again or started activity before confirming the final wake-up from main sleep. Do not fill gaps between segments with assumed sleep.
5. A completed query does not mean all real sleep has synced. When data arrives late, reuse existing cycles and sleep events before correcting boundaries, relations, and affected summaries. Avoid creating duplicate cycles.

No connection, a failed read, or no samples in the window means only that evidence is unavailable or was not returned. Do not record it as “did not sleep.” Respect access restrictions returned by tools. Do not report a denial as a success or retry the same restricted source through another route. Previously obtained records, the person's account, and estimates within the task's scope remain usable.

## Use recent personalized estimates when evidence is missing

Base estimates on recent verified main sleep close to the target period and under comparable living conditions. Start with the most recent 14 days if useful, selecting measured samples from the same routine and environment. Preserve the window, sample count, median or range of wake-up times, applicable time zone, and reasons for exclusions. Do not feed naps or earlier estimates back into the sample as measured sleep. Reduce the weight of older habits after travel, shift work, late nights, or a routine change. With few samples, state the low confidence instead of applying a universal fixed cutoff time.

Use the event's meaning to narrow its assignment first. Statements such as “last night before I slept” or “after I got up today” usually provide more direct evidence than a habitual wake-up time. Entry time, image-save time, and chat-send time do not automatically equal occurrence time.

Within the scope in which the current task already permits estimated filing:

- If the cycle label can reasonably be determined but exact boundaries cannot, create or reuse an **estimated cycle**. Record the basis and estimation window, leave exact start, end, and actual sleep fields empty, and mark the event's cycle assignment as estimated.
- Enter an estimated boundary only when evidence supports a specific time and the field permits estimates. Mark it explicitly as estimated. A median wake-up clock time must not become an exact measured timestamp.
- If an event cannot reliably be assigned between two cycles, preserve the event and its original filing, mark it as awaiting assignment, and list the missing evidence. Do not force it into the currently open cycle. This is especially important for older records without an occurrence time.
- When measured data arrives, correct the original event and existing estimated cycle. Preserve their IDs, the estimation basis, and the correction history. Authorization to estimate one batch does not automatically authorize migration of all history.

## Time zones, travel, and daylight saving time

Compare chronology and calculate elapsed duration using absolute UTC times. Also preserve the event's original local time, UTC offset, and IANA time zone when known. The computer's time zone, the query's display time zone, or the person's current location must not substitute for where a historical event occurred.

Travel alone does not open a new sleep day cycle. A cycle spanning time zones may have different local zones at its start and end. Keep the label based on the local date of its opening wake-up, and retain its stable ID. Repeated or skipped date labels do not need to be forced into a consecutive sequence. During daylight saving changes, a repeated local hour needs an offset to disambiguate it; a skipped hour must not be invented. If only a local clock time is known and the time zone is uncertain, preserve that uncertainty rather than manufacture a unique UTC timestamp.

Do not shift all older date-only records forward or backward under the new sleep day rules. Calendar dates for appointments, races, plan effective dates, and similar items retain their original meaning.

## Minimum information to represent

Reuse existing fields. These are semantic requirements, not a requirement to create a separate property for every item.

| Object | Minimum information |
| --- | --- |
| Cycle | Stable ID, derived sleep day label, start and end times with time zones (nullable), boundary status and evidence, open or closed status |
| Main sleep that opens the sleep day | Unique source relation, actual sleep segments or deduplicated duration, evidence for the final wake-up. Distinguish measured, mixed, estimated, and unknown data |
| Original event | Original occurrence time and precision, original filing label, one cycle relation or awaiting assignment, assignment basis, source |
| Summary | Cycle, snapshot type, generation time, data cutoff time, actual read coverage, completeness, and whether recalculation is needed |

Cycle closure and record completeness are separate dimensions: a known boundary may still leave meals missing. Apparently complete records may still lack confirmation of the next wake-up. Do not enter 0 for unknown values or label partial data as a full day.

## Responsibilities of the two daily fitness summaries

The two daily summaries maintain shared cycles and sleep boundaries. Specialist chats for food, training, body measurements, and other areas provide original events, sources, and proposed assignments. They reference the same cycle instead of each creating a separate day. The current maintainer coordinates under the project's existing rules and does not independently change other chats' scheduled tasks.

- **Midday snapshot:** Identify the cycle, cutoff time, and records actually read. Summarize only the activity and intake recorded so far, and identify gaps in coverage.
- **Interim snapshot:** If midnight arrives before the cycle ends, continue the current cycle and state that the snapshot is interim. Keep scheduled execution times separate from sleep day boundaries. Changing the day definition does not automatically change a task's time or frequency.
- **Final snapshot:** Generate the cycle's final summary after the next final wake-up from main sleep has been verified and events affecting assignment have been checked. If the end boundary is supported only by a habitual estimate, keep an interim snapshot, explaining the estimate and the next evidence needed for verification.

For every snapshot, distinguish generation time, data cutoff time, and source coverage. If records remain missing after a boundary closes, retain “partial coverage.” Do not interpret unrecorded intake as no intake or use it to calculate a definite full-day deficit. Keep the original time window for metrics available only as calendar-day aggregates, such as steps or active energy. When hourly or individual samples are available, deduplicate and aggregate over the actual cycle interval. State the definitions of exercise energy expenditure and total daily energy expenditure separately.

When late syncs or backfilled records change a boundary, preserve earlier snapshots as history, flag affected summaries for recalculation, and update the current valid version with the reason for correction. Old text saying “awaiting verification” must not continue to represent the current state, and historical records must not be overwritten without explanation.

## Compatibility with historical filing and summaries

Preserve original occurrence times, old dates, old daily relations, raw values, and sources. An old date may represent a calendar day, a food logging day, or another filing convention adopted at the time. Interpret it under its original definition rather than relabeling everything as a calendar day. When adding cycle relations, make the sleep day label a read-only derived value. Assign each original event to only one cycle; child details inherit their parent record's assignment.

Calculate new statistics from deduplicated original events with clear assignments. Do not add original events and old daily summaries into the same total. Present estimated data, unknown data, and complete coverage separately. Also distinguish “the most recent seven cycles” from “a seven-day UTC window ending at a specified time.”

Claim migration only for the scope actually processed. Preserve old and new relations, reasons for changes, and a mapping that supports rollback. Historical events without times may retain their original filing while awaiting verification. Do not invent boundaries to fill a trend chart. Linking part of the history does not mean all history has been migrated.

## Entirely fictional boundary example

The person, dates, and records below are fictional. All times use `Etc/UTC`.

| Record | Decision |
| --- | --- |
| Person A has their final wake-up from main sleep at 08:40 on 2040-06-04 | Open the cycle labeled 06-04 |
| At 00:25 on 06-05, they have a late-night snack and say they have not yet slept | Assign the snack to the 06-04 cycle; do not split at midnight |
| Main sleep begins after 02:10. They briefly wake and eat at 06:00, then sleep again at 06:25. The device's last sleep segment ends at 09:05; they confirm that their final wake-up was not until 09:20 | The 06:00 intake still belongs to the 06-04 cycle. Open the 06-05 cycle at 09:20. Retain both device segments and the person's account; do not automatically count 09:05–09:20 as sleep |
| The deduplicated sleep segments from that main sleep | Count them only as the main sleep opening the 06-05 cycle. The 06-04 cycle ends at 09:20 and does not also count that sleep |
| Sleep from 16:00 to 16:25 on 06-05 is explicitly identified as a nap | Assign it as a nap in the 06-05 cycle; do not open a new cycle |

If device samples are missing on a later day, record only that evidence is missing. If estimation is authorized and the meaning of “lunch after getting up” supports a filing label, link the event to an estimated cycle while leaving exact boundaries empty. This does not justify creating “measured sleep” or claiming that Person A stayed awake all night.
