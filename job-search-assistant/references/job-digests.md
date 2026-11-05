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

Parse from the **right**, because company names sometimes contain `|` themselves (for example `NONO GROUP | NONO - GROUP` or `Ness Technologies | נס טכנולוגיות`):

- Match % = the last field.
- Location = the field just before the match %.
- Title = the first field.
- Company = everything between title and location.

Then:

- Apply link = the first URL. Strip everything after `?` for a clean link.
- Job ID = the number after `/job/`. Use it to remove duplicates.
- Ignore the second ("tailor CV") link.
- The same role can appear with different job IDs (multiple openings). Merge on title + company and keep the highest match.
- There is no job description in the email. Use "see link". If you can open the job page, add one sentence from it; never write a description from the title alone.

## Central Israel filter

Keep a job only if its location is in this list (Hebrew or English spelling, case-insensitive):

Tel Aviv / תל אביב, Ramat Gan / רמת גן, Givatayim / גבעתיים, Bnei Brak / בני ברק, Petah Tikva / פתח תקווה / פ"ת, Herzliya / הרצליה, Ramat HaSharon / רמת השרון, Ra'anana / רעננה, Kfar Saba / כפר סבא, Hod HaSharon / הוד השרון, Netanya / נתניה, Holon / חולון, Bat Yam / בת ים, Rishon LeZion / ראשון לציון, Rehovot / רחובות, Ness Ziona / נס ציונה, Yehud / יהוד, Or Yehuda / אור יהודה, Airport City / איירפורט סיטי, Rosh HaAyin / ראש העין, Shoham / שוהם, Lod / לוד, Ramla / רמלה, Modi'in / מודיעין.

Region names that count as central: "Center", "מרכז", "אזור המרכז", "גוש דן".

Drop everything else (for example Haifa, Jerusalem, Be'er Sheva, Sderot, Or HaNer, Yokneam, Misgav, Migdal Tefen, Emek Hefer, Caesarea).

Put these in a short "location unclear" line with title and link, so nothing is silently lost:
- The location field is clearly not a place (a fragment of the title, or empty). This happens often with recruiting agencies such as Matrix.
- Broad regions that may or may not be central, such as "אזור השפלה" or "השרון".

The user can edit this list.

## Categories

Group the jobs table by category, in this order. Pick the category from whole words in the title. The order matters: the first matching category wins, so "Software Verification Engineer" is QA and "Backend & DevOps Engineer" is DevOps. Inside each category, sort by match %, highest first.

| Category | Typical title words |
| --- | --- |
| Analyst & Data | Analyst, Data, BI, Statistician, Data Science, אנליסט, נתונים |
| AI | AI, ML, Machine Learning, GenAI, LLM, Algorithm |
| DevOps & Infrastructure | DevOps, Infrastructure, SRE, Cloud, HPC, FinOps |
| QA & Testing | QA, Tester, Verification, Automation (testing), בודק/ת |
| Design | Designer, UX, UI, Graphic, ביצועיסט/ית, עיצוב |
| Product & Operations | Product, Operations, Project Manager, Implementer, Integration, מנהל/ת פרויקטים |
| Software Development | Developer, Software Engineer, Full Stack, Backend, Frontend, Web, SDE, מפתח/ת |
| Other | Anything else |

Mark student and intern positions with "(student)" after the title, inside their category. Don't filter any category out; the user wants to see all of them.
