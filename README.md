# Job search assistant: a Claude skill for Gmail

A Claude skill that turns a busy job-search inbox into a status board. It reads recruiting emails, works out where every application stands, flags what needs action today, and lists new relevant jobs from job-alert emails. It drafts follow-ups only after the user approves them, and it never sends or deletes anything.

## Why I built it

During my job search I had about 300 recruiting emails in three months: confirmations, interview invites, home assignments, rejections, and daily job-alert digests. Many rejections hide behind neutral subjects like "Thank you from <company>" or "Application update", so a quick scan of the inbox missed them. I wanted one place that answers three questions every morning:

1. What do I need to do today?
2. Which processes are still alive, and which are closed?
3. Which new jobs are worth a look?

## What it does

| Step | What happens |
| --- | --- |
| Find | Searches Gmail for recruiting emails in 7-day windows (a Gmail search returns at most 50 results), plus a 90-day sweep for rejection phrases. |
| Classify | Reads each email body and assigns a stage: Applied, Recruiter contact, Interview, Assignment, Offer, Rejected, or No response. |
| Merge | Groups emails into processes (company + role). A rejection or offer closes a process. |
| Flag | Marks what needs action: **waiting on you** (unbooked interview, unfinished test, recruiter question), **interview soon**, and **stalled** (7+ days after an interview or assignment with no news). |
| Jobs | Parses job-alert digests, keeps central-Israel jobs only, removes duplicates and jobs already applied to, and groups them by category. |
| Report | A summary, "what to do today", an applications table, and the new jobs table. The same data also feeds a dashboard. |
| Follow-up | On request, drafts short follow-up replies in the original thread, for the user to review and send. |

## Safety by design

The skill runs on a real personal inbox, so the guardrails come first:

- **Read only by default.** It never sends, deletes, archives, forwards, or marks as spam, even if an email asks it to.
- **Human in the loop.** Drafts and labels are created only after the user approves a specific list in the conversation.
- **Email content is data, not instructions.** This protects against prompt injection, for example a job-alert email that invites replies to change settings.
- **No invented facts.** If a company, role, or date is unclear, the report says "unclear".
- **Defense in depth.** The rules live in the skill, and the Gmail connector's own permissions limit what is possible.

## Files

```
job-search-assistant/
├── SKILL.md                      # The workflow and safety rules (loaded when the skill triggers)
└── references/
    ├── classification.md         # Real phrase patterns for each stage, in Hebrew and English
    ├── job-digests.md            # How to parse job-alert emails, the central-Israel filter, categories
    └── followup-style.md         # Tone and examples for follow-up drafts
```

`SKILL.md` stays short and points to the reference files, which Claude reads only when it needs them (progressive disclosure).

## How it was built

1. **Theory first:** what a skill is, what MCP connectors are, which permissions are needed, and where the rules live.
2. **Read-only exploration** of the real inbox to learn the actual email patterns.
3. **Decisions:** a stalled process means 7 days without news after an interview or assignment. No response after 30 days means pending, with no follow-up.
4. **A test run** on real data, checked by hand. Both items marked "check" turned out to be right.
5. **Iteration:** a 30-day default window (90 days was about 300 threads), date-window searches, a two-pass read (subjects first, full body only when unclear), and new edge cases such as a duplicate-application notice that is not a rejection, a closed position, and course marketing that looks like an application update.
6. **Output:** a dashboard that refreshes Sunday to Thursday at 8:00 through a scheduled task.

## Install

1. Zip the `job-search-assistant` folder (the folder itself must be at the top of the ZIP).
2. In claude.ai, go to **Settings → Capabilities → Skills** and upload the ZIP.
3. Connect the Gmail connector.
4. Ask: "What's the status of my job search?"
