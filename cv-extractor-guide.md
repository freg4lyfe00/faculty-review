# CV Extractor — User Guide

## What this tool does

Drop a CV file, set the year range, click Extract. The tool reads the file entirely in your browser — nothing is uploaded or sent anywhere — and uses pattern matching to pull out publications, presentations, grants, and mentees. Review and edit the extracted data by academic year, then download one JSON file per year to import into the Faculty Review tool.

## Quick start

1. Open `cv-extractor.html` in a web browser (double-click), or visit the hosted link
2. Drop your CV onto the upload zone, or click to browse
3. Set the year range (From / To)
4. Click **Extract**
5. Switch to the **Review & Download** tab
6. Edit any mistakes, then click **Download JSON for AY YYYY-YYYY**
7. In your Faculty Review file, click **Import data** and select the downloaded JSON
8. Repeat steps 6–7 for each academic year

## Supported file types

- **PDF** — must be text-based (not a scanned image). If you can click to select and copy text in the PDF, it will work. Scanned PDFs will produce a warning.
- **DOCX** — Microsoft Word documents. Simple paragraph-based CVs extract well. Complex table layouts may not.
- **TXT** — plain text. If PDF and DOCX extraction produce poor results, open your CV in Word, do File → Save As → Plain Text (.txt), and use that.

## Year range

Academic years run **July 1 through June 30**. An item dated October 2023 belongs to academic year 2023-2024. An item dated March 2024 also belongs to 2023-2024.

Selecting From `2020` To `2025` generates six academic years:
`2020-2021`, `2021-2022`, `2022-2023`, `2023-2024`, `2024-2025`, `2025-2026`

Items outside the selected range are discarded. Items with no detectable date appear under the **Unknown date** pill.

## What gets extracted

### Publications
- **Citation** — the full citation text as it appears in your CV
- **Status** — published / submitted / in-revision / in-preparation (guessed from keywords like "In press," "Submitted," "In revision," "In preparation")
- **Type** — original-article / editorial / review / guidelines / book-chapter (guessed from keywords)

### Presentations
- **Date** — month and year (e.g., "Oct 2023")
- **Event** — conference or event name
- **Type** — invited-talk / oral-abstract / poster / workshop (guessed from keywords like "Invited," "Poster," "Workshop")
- **Title** — presentation title

### Grants
- **Date** — month and year the grant was active or awarded
- **Source** — funding agency (NIH, NSF, AHRQ, VA, AHA, etc.)
- **Type** — grant mechanism (R01, K23, R21, Pilot, etc.)
- **Title** — full grant title
- **Status** — awarded / under-review / not-funded

### Mentees
- **Name** — mentee's full name
- **Level** — undergraduate / medical-student / graduate-student / resident / fellow / faculty
- **Comments** — project description or role

Mentors (people who mentor you) and self-evaluation are **not** extracted. Fill those in directly in the Faculty Review tool.

## How pattern matching works

The extractor looks for section headers in your CV — lines like "Publications," "Presentations," "Grants," "Mentees / Trainees." It then splits each section into individual entries and guesses field values from keywords and patterns.

**It is not perfect.** Common issues:

- Publications that are reviews or editorials may be classified as original articles
- Presentation titles and event names may be swapped
- Grants without standard mechanism names (R01, K23) may have empty type fields
- Mentee names may pick up extra words

The **Review tab is your cleanup step** — expect to spend a few minutes correcting entries.

## Tips for better extraction

- Make sure your CV has clearly labeled section headers (not just bold text — actual standalone lines)
- Use numbered or bulleted lists within each section; these split into entries more reliably than dense paragraphs
- Keep one publication per line or paragraph
- If a section uses a non-standard name ("Peer-Reviewed Papers" instead of "Publications"), the tool will still detect it — but very unusual names may be missed

## Valid field values

When editing entries, dropdowns enforce these exact values:

| Section | Field | Valid values |
|---|---|---|
| Publications | status | published, submitted, in-revision, in-preparation |
| Publications | type | original-article, editorial, review, guidelines, book-chapter |
| Presentations | type | invited-talk, oral-abstract, poster, workshop |
| Grants | status | awarded, under-review, not-funded |
| Mentees | level | undergraduate, medical-student, graduate-student, resident, fellow, faculty |

## Reviewing and editing

- Use the **year pills** to switch between academic years
- **Unknown date** pill — items where no date could be detected. Edit the date field or delete and re-add to the right year.
- Hover any row to reveal the **pencil** (edit) and **x** (delete) icons
- Click **+ Add** to add a new row from scratch
- Press **Enter** to save a row, **Escape** to cancel

## Downloading and importing

1. In the Review tab, click **Download JSON for AY YYYY-YYYY** for the currently visible year
2. Or click **Download all years separately** to trigger downloads for every year in your range
3. In your Faculty Review file, click **Import data** (top right of the header, next to the year pills)
4. Select the downloaded JSON file
5. Confirm the replacement if prompted
6. Repeat for each year

The downloaded JSON files are named `cv-extracted-YYYY-YYYY.json` and match the exact format the Faculty Review import button expects.

## Privacy

All processing runs in your browser. Your CV text is never sent to any server or third-party service. Closing the browser tab clears everything.

## Troubleshooting

**"No section headers detected"**
The tool placed everything as publications. It couldn't find labeled sections. Either your CV doesn't have standard section names, or the text extraction produced garbled output. Try the TXT fallback, or add items manually in the Review tab.

**Items assigned to the wrong year**
Edit the date field in the row. The year is recalculated when you download — the download always uses the state of the Review tab, not the original extraction.

**Scanned PDF warning**
The text extraction found very few characters. Use a text-selectable PDF, or copy-paste your CV text into a .txt file.

**Safari downloads only one file**
Use the individual year download buttons instead of "Download all years separately."

**DOCX tables not extracting**
The mammoth.js library reads paragraph text but loses table structure. Copy the table contents into regular paragraphs, or use a TXT export.

**Publications showing wrong type or status**
Edit them in the Review tab. The extraction guesses based on keywords; it often needs correction.
