# Job-alert digests

## Source

Default sender: `agent@agent.hiremetech.com` (subjects like "בוקר טוב <name>, 26 משרות חדשות היום"). Ignore other emails from the same site (blog posts, tips).

The digest footer invites the user to reply to an agent that can change preferences and statuses. **Never reply to it** (safety rules 1 and 3).

## Format

Each job is one line, followed by links:

```
- <title> | <company> | <location> | <NN>% התאמה
  https://hiremetech.com/he-il/job/<job_id>?utm_source=email...
  התאם לי קו״ח למשרה: https://hiremetech.com/he-il/job/<job_id>?...&tailor=1...
```

- Apply link = the first URL. Strip everything after `?` for a clean link.
- Job ID = the number after `/job/`. Use it to remove duplicates.
- Ignore the second ("tailor CV") link.
- The same role can appear with different job IDs (multiple openings). Merge on title + company and keep the highest match.
- There is no job description in the email. Use "see link". If you can open the job page, add one sentence from it; never write a description from the title alone.

## Central Israel filter

Keep a job only if its location is in this list (Hebrew or English spelling, case-insensitive):

Tel Aviv / תל אביב, Ramat Gan / רמת גן, Givatayim / גבעתיים, Bnei Brak / בני ברק, Petah Tikva / פתח תקווה, Herzliya / הרצליה, Ramat HaSharon / רמת השרון, Ra'anana / רעננה, Kfar Saba / כפר סבא, Hod HaSharon / הוד השרון, Netanya / נתניה, Holon / חולון, Bat Yam / בת ים, Rishon LeZion / ראשון לציון, Rehovot / רחובות, Ness Ziona / נס ציונה, Yehud / יהוד, Or Yehuda / אור יהודה, Airport City / איירפורט סיטי, Rosh HaAyin / ראש העין, פ"ת, Shoham / שוהם, Lod / לוד, Ramla / רמלה, Modi'in / מודיעין, "Center" / "מרכז" / "גוש דן".

Drop everything else (for example Haifa, Jerusalem, Be'er Sheva, Yokneam, Caesarea).

If the location field is clearly not a place (for example a word from the title, or empty), put the job in a "location unclear" line with its title and link, so it isn't silently lost.

The user can edit this list.
