# Meta Muse Prompt Recipes

**A growing library of shareable, copy-paste prompt recipes for Meta Muse.**

Give these recipes to your own Muse once, and let them set up durable workflows, automations, and living Spaces on your behalf. **Many more prompt recipes for Muse are on the way** as we continue building and battle-testing new workflows.

---

## Featured Recipe: Weekly Quota Audit

### What this recipe does

Your Muse quota resets to zero every week, which means the final closing usage number disappears unless you capture it right before the reset. At the same time, scheduled jobs, background runs, and frequent polling checks can quietly consume quota without giving you a clear picture of where it went.

**Muse Weekly Quota Audit** solves this with a single, read-only setup prompt that creates a self-maintaining weekly audit system tailored to your exact reset schedule:

1. **Captures your closing usage automatically:** Schedules a tiny, low-cost snapshot job 21 minutes before your weekly reset to log your closing usage percentage, plan, and token pools.
2. **Audits your week after reset:** Schedules a read-only audit job 42 minutes after your reset to inventory every scheduled job and hook, count actual runs, attribute activity honestly, and identify concrete ways to reduce wasted runs.
3. **Publishes a living Space (`Weekly Quota Audit`):** Adds a new dated edition (newest first) each week with headline stat cards, trend charts (once 3+ snapshots exist), per-job run breakdowns, and **one-click copyable "fix-it" prompts** for every recommended saving or better-use idea.
4. **Never touches your settings on its own:** The audit is strictly read-only. It recommends changes and gives you self-contained prompts you can paste into Muse chat if you choose to apply them.

> **Standalone file:** You can also view or download the raw recipe directly at [`recipes/weekly-quota-audit.md`](recipes/weekly-quota-audit.md).

### Copy-paste ready recipe

Copy the entire block below and paste it into your Muse chat (or paste just the **Setup** section if you prefer):

````markdown
# Muse Weekly Quota Audit: a shareable recipe

## Setup (give this to your Muse once)

You are setting up my Weekly Quota Audit. Do these steps in order, then confirm what you created.

1. **Find my reset.** Check my current plan, usage, and weekly limit reset time. Note the plan type (free or paid), the reset day and time, and any additional token pools my status reports. My audit schedule hangs off my own reset time, never a hardcoded day.

2. **Create the snapshot job.** Create a small scheduled job that runs once a week, 21 minutes BEFORE my reset time. Its entire job is: read my current usage, and append exactly one line to a snapshot log file you maintain for this audit (one JSON object per line, with the date, the closing usage percent, the plan, and the reset time, plus any additional-pool figures), then stop. Append only; it never rewrites the log or touches anything else. Keep it as cheap as possible. This snapshot is the only way to know my closing usage for a week, because the counter resets to zero at the reset and the final figure is gone afterward. Without it, the audit must say the closing figure is unknown, and it must never guess one.

3. **Create the audit job.** Create a scheduled job that runs once a week, 42 minutes AFTER my reset time. Its instructions are the Audit Prompt section of this recipe, copied exactly. At the end of every run, the audit re-checks my reset time; if it has moved, it adjusts both jobs to match and notes the change in that week's edition.

4. **Create the Space.** Create one Space titled "Weekly Quota Audit" that the audit will update with a new dated edition each week. Do not create a new Space per week. Editions run newest first, and old editions are never deleted, so I can see the trend. The first edition establishes the visual design described in the Audit Prompt (step 9); later editions reuse that exact design system.

5. **Confirm back to me:** my plan and reset time as you found them, the two run times you set, and the Space link. If any step could not be completed, say which one and why, plainly.


## Audit Prompt (this is what the weekly audit job runs)

You are running my Weekly Quota Audit for the week that just ended. This is a read-only audit. Do not delete, disable, reschedule, or edit any job, hook, or setting. Recommendations only; I make the changes.

### Gather

1. Read the audit state file (last week's job inventory and findings) and the snapshot log (one line per week). If this is the first run, say so in the report and start the series.
2. Read my current plan and usage status. Note the plan, the new week's starting usage, the next reset time, and any additional token pools.
3. Take the prior week's closing usage from the last line of the snapshot log. If no snapshot exists, report the closing usage as unknown. Never estimate it.
4. Inventory my scheduled jobs and hooks: name, schedule, how many times each ran in the last 7 days, and what each one is for. Count runs; do not guess at counts.
5. Reconstruct the week's activity split as far as the records allow: direct chats, scheduled jobs, and background or one-off work. State what portion you could attribute and what you could not. An honest "not measurable from here" beats a tidy invented split.

### Analyze

6. Compare against prior weeks where snapshots exist: closing usage trend, total scheduled runs trend, and whether last week's adopted suggestions actually reduced anything. Judge adopted suggestions by measured change, not by intention.
7. Find the savings. Look for: polling jobs that check for changes on a timer when an event-driven check or a plain script would do; overlapping jobs that could merge into one run; jobs running more often than their value justifies; long-running background work that produced nothing I used; heavyweight approaches to lightweight tasks (for example, voice for quick requests, or a full research run for a lookup). Every saving you propose must name the specific job or pattern, state the countable effect (runs per week eliminated, checks reduced from X to Y), and say what, if anything, is lost by the change. No invented percentage savings.
   For every saving, also write its **fix-it prompt**: a short, self-contained prompt, written in my voice to my Muse, that carries out exactly that remedy. It names the exact jobs or settings involved and the exact change to make, and it ends by asking Muse to confirm what it changed. Pasting that prompt into my chat is how I approve and trigger the fix, so it must work with no other context. Write the fix-it prompt for the better-use suggestions in step 8 too, wherever the suggestion involves a change Muse can make for me.
8. Find the better uses. At most 3 suggestions for getting more from Muse, each tied to something you actually observed in my setup or activity: a capability I have never used, a connector relevant to my work that is not connected, a recurring manual chore in my chats that could be a scheduled job, a goal or routine I maintain by hand that Muse could track. No generic feature tours. If nothing observed supports a suggestion, give fewer than 3, including zero.

### Report

9. Update the "Weekly Quota Audit" Space with a new edition dated today, newest first. This Space is the product; make it genuinely impressive, not a text report pasted into a page. Design requirements:
   - A headline row of large stat cards: prior week's closing usage (or "unknown, no snapshot") with a week-over-week change indicator once a trend exists, scheduled runs this week, and the single biggest saving identified, stated as its countable effect. Every card carries a distinct figure; the same number never appears in two cards. If a fourth slot needs a figure, use total counted weekly load (runs plus wakes).
   - A trend visual of closing usage and scheduled runs across every week on record. Keep it compact, a small placeholder, until three or more snapshots exist; never fake a trend from one or two points. From three points, expand it to a full line chart plus a cumulative banked-savings area showing the total runs and wakes saved by adopted fixes over time.
   - Where the week went: the activity split from step 5 as a visual breakdown, with the attribution limits stated in one line. Any stacked bar uses clearly distinct colors per segment, and its legend lists only buckets that actually appear as segments; anything that is not run-counted is noted in text, never in the legend.
   - A per-job horizontal bar chart, sorted biggest first, of counted runs or wakes per week for every inventoried job. This is the chart that shows where the week actually went; use only counted figures, exact or honestly bounded (for example "up to ~42").
   - Savings for next week: at the top of the section, one aggregate visual: total counted weekly runs and wakes now versus if every proposed fix were applied, stated in runs and wakes only, never converted to a token percentage. Below it, the step 7 list, ranked biggest first, each as its own card showing the named job or pattern, the countable effect, what is lost, a one-line summary, and a **copy button** that copies that item's fix-it prompt to the clipboard, labeled so it is obvious pasting it into Muse chat applies the fix. The full fix-it prompt text stays collapsed behind a "show prompt" disclosure; the prompt is a payload, not reading material.
   - Getting more from Muse: the step 8 list, at most 3 cards, each with the same collapsed-prompt and copy button treatment where a fix-it prompt applies.
   - Follow-through: last week's suggestions, which I adopted (if you know), and the measured result, shown as kept promises, not buried prose.
   - Polish throughout: strong typography, generous spacing, a coherent color system used consistently across editions (usage, savings, and better-use sections each keep their color), and correct rendering in light and dark mode. Every edition looks like the same publication, only the numbers and findings change.
10. Send me a short chat summary: closing usage, the top saving, and the Space link. Nothing more; the detail lives in the Space.
11. Save this week's figures and findings to the state file so next week's audit can measure the trend and grade these suggestions.

### Rules that never bend

- Every number in the report names where it came from (a snapshot, a status check, a run count). If a figure cannot be sourced, it does not appear.
- Results are reported as measured, including misses. If usage went up, the report says so.
- The audit is not complete until the Space edition exists and the state file is updated.
````

---

## Recipe Index

| Recipe | Purpose | File |
| :--- | :--- | :--- |
| **Weekly Quota Audit** | Automated weekly quota snapshot, read-only usage audit, savings finder, and living Space publication | [`recipes/weekly-quota-audit.md`](recipes/weekly-quota-audit.md) |
| *More recipes coming soon* | New Muse prompt recipes for daily workflows, research, and automation are actively in development | Stay tuned |
