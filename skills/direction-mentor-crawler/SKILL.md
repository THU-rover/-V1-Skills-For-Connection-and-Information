---
name: direction-mentor-crawler
description: Use when collecting mentor/advisor information from a specific university department, research direction, lab, or faculty-list page. The workflow crawls one confirmed direction-level list page, extracts only teacher detail links from that page, exports mentor records, and produces a missing-check file so coverage can be audited.
---

# Direction Mentor Crawler

Use this skill for direction-level mentor collection, not whole-school crawling. The reliable unit is:

```text
school -> college -> direction/department -> one faculty list page -> teacher detail pages
```

## Unified Output Folder

All outputs should be placed under the user's workspace in:

```text
skill-outputs/01-direction-mentor-crawler/
```

Each run must create one clearly named child folder:

```text
YYYY-MM-DD-school-college-direction-mentors/
```

Examples:

```text
skill-outputs/01-direction-mentor-crawler/2026-05-30-pku-electronics-design-automation-computing-systems-mentors/
skill-outputs/01-direction-mentor-crawler/2026-05-30-fudan-physics-optical-science-mentors/
```

The folder name should identify the collection date, school, college or department, direction or lab cluster, and output type.

Do not create loose outputs directly in `outputs/` unless the user explicitly asks for a quick temporary test.

## Workflow

1. Ask for or identify the exact direction-level list page.
   - Good: `.../szdw/zzjs/sjzdhyjsxtx1/index.htm` for one department/direction.
   - Avoid: a college homepage or generic news/research page.
2. Run `scripts/direction_mentor_crawler.py` from the user workspace.
3. Inspect the coverage check CSV:
   - every teacher link found on the list page should have `抓取状态=ok`;
   - if not, repair selectors or record unresolved links explicitly.
4. Deliver the records CSV and the check CSV.

## Command

```powershell
python C:\Users\Zhang\.codex\skills\direction-mentor-crawler\scripts\direction_mentor_crawler.py `
  --list-url "https://example.edu/path/to/direction/index.htm" `
  --school "学校名" `
  --college "学院名" `
  --direction "方向/系名" `
  --out-dir "skill-outputs/01-direction-mentor-crawler/YYYY-MM-DD-school-college-direction-mentors"
```

Optional flags:

- `--delay 0.2`: polite delay between detail-page requests.
- `--include-external-homepages`: keep external lab/homepage links in the output.
- `--debug-html`: save fetched HTML snippets for selector debugging.

## Output Files

- `mentors.csv`: one row per successfully parsed mentor.
- `mentors.jsonl`: same records in JSONL.
- `coverage_check.csv`: one row per teacher link found on the list page, including parse status.

## Quality Bar

- Do not claim completeness from a college homepage crawl.
- Completeness means: complete relative to the confirmed list page, verified by `coverage_check.csv`.
- If the list page is paginated or split by tabs/directions, collect every relevant list URL and run the script once per list URL or merge outputs afterward.
- Preserve official URLs in the output; do not infer missing emails or research directions.
