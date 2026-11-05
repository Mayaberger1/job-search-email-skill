# Classification rules

Classify by the email **body**. The subject is a hint at most. These patterns come from a real job-search inbox (Israel, Hebrew and English, 2026).

## Applied

Typical senders: applicant tracking systems (`*.comeet-notifications.com`, `greenhouse-mail.io`, `ashbyhq.com`, `hire.lever.co`, `recruitee-mailbox.com`, `careers.<company>`).

Phrases:
- "Thank you for applying for the <role> position at <company>"
- "We got your application for the <role> role"
- "Thanks for your recent interest in joining us at <company>"
- "תודה על הגשת מועמדותך למשרת <role>"

Company and role usually appear in the subject. One application often produces two confirmations; merge them.

## Recruiter contact

A person (not a no-reply address) writes to the user: asks for a call, asks a question, replies to the user's outreach.
- "I tried calling you, but I wasn't able to reach you. Could you let me know when would be a convenient time?"
- A reply from `careers@` or a named recruiter to the user's cold email.

If the last message in the thread is from them and asks something, mark **Waiting on you**.

## Interview

- "Scheduling your Phone interview with <company>"
- "Your phone interview with <company> for <role> position"
- "Screening Interview for <role>", "Manager Interview - <name> for <role>"
- Calendar invitations: "Invitation: Interview <role> - <name> @ <date>"
- Hebrew: "הצוות שלנו מצפה לפגוש אותך", "נא לאשר את מועד הריאיון"

Interview invitations that ask the user to pick a slot ("We're happy to invite you to a Phone interview ... please choose a time") are not a booked interview. If no confirmation with a date follows, mark **Waiting on you: book the interview**.

Reschedules and cancellations: "Updated: Your in-person interview", "Interview cancellation", "Cancelled event". If a new date follows, the stage stays Interview and the newest date counts. A cancellation with no new date: keep Interview and note "cancelled, no new date".

Take-home tests delivered through platforms (e.g. "Thanks for taking the SQL Interview" from a testing platform) count as Assignment.

## Assignment

- "<role> - home assignment", "Take-Home Assignment", "<role> - Challenge"
- Follow-ups like "HTML Guidelines & Environment Setup" in the same process
- The user's own sent email submitting the assignment

The assignment date is the later of received / submitted.

## Rejected

Neutral subjects are common: "Update on Your Application", "Thank you from <company>", "Application Update", "<role> opportunity at <company>". Look for:
- "we've decided to move forward with other candidates"
- "we won't be continuing the recruitment process with you"
- "we have decided not to move forward with your application"
- "you haven't met the requirements for this position"
- "After evaluating them against our needs ... we decided to move forward with other candidates"
- Hebrew: "החלטנו להתקדם עם מועמדים אחרים", "לא נוכל להתקדם"

A rejection after an interview ("It was a pleasure meeting with you recently ... move forward with other candidates") closes the process.

## Closed without a rejection

These close the process too. Show them under closed, with the reason:
- **Position closed:** "this position is now closed and we are no longer accepting applications".
- **No opening for cold outreach:** a recruiter answers the user's speculative email with "we don't have a relevant open position at the moment, but I'll keep your CV on file".

## Looks like an update, but isn't

- **Duplicate application notice:** "We recently received another application from you for this position". Not a rejection. Merge into the existing process.
- **Training-program marketing:** "We received your CV ... a training program for the high-tech industry". Not a job process. Exclude.
- **Third-party online tests** (for example from `adam-milo.com`, `hackerrankforwork.com`): count as Assignment for the company named in the email.

## Offer

"We are happy to offer you", "offer letter", "הצעת עבודה". Closes the process. Flag it at the top of the report.

## Not recruiting (exclude)

- Job-alert digests (handled separately, see `job-digests.md`)
- Content marketing from job sites ("here's what they ask at <company> interviews")
- "You have been referred to <company>" with no application yet: show as a note, not a process
- Receipts, invoices, promotions that happen to contain words like "decided" or "unfortunately"
- Emails the user sent to their own work address
