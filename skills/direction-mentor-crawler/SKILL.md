---
name: direction-mentor-crawler
description: Use when collecting mentor/advisor information from a specific university department, research direction, lab, or faculty-list page. The workflow crawls one confirmed direction-level list page, extracts only teacher detail links from that page, exports mentor records, and produces a missing-check file so coverage can be audited.
---

# Direction Mentor Crawler

Use this skill for direction-level mentor collection, not whole-school crawling. The reliable unit is:

```text
school -> college -> direction/department -> one faculty list page -> teacher detail pages
```

For graduate admission projects, the reliable unit may also be:

```text
school -> official admission catalog/project page -> mentor table -> coverage table
```

When an official admission catalog conflicts with a project-introduction page, prefer the admission catalog for current-year mentor coverage.

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

1. Identify the exact authoritative page and record why it is authoritative.
   - Good: `.../szdw/zzjs/sjzdhyjsxtx1/index.htm` for one department/direction.
   - Good: official graduate admission catalog or official project mentor table.
   - Avoid: a college homepage or generic news/research page.
   - If there are multiple official pages, use this priority: current-year admission catalog > current-year project admission notice > project mentor table > general project introduction page.
2. Open or fetch the URL first. If it cannot be accessed, do not use it as the main source.
3. Run `scripts/direction_mentor_crawler.py` from the user workspace.
   - Use default `--source-type auto` for normal cases.
   - Use `--source-type table` when the official page lists mentors in a table and does not link to teacher detail pages.
   - Use `--section-keyword "<专业/项目名>"` for large admission catalogs that contain multiple majors in one table.
3. Inspect the coverage check CSV:
   - every teacher link found on the list page should have `抓取状态=ok`;
   - if using official table mode, every table row should have `抓取状态=ok` and `错误=official_table_source`;
   - if not, repair selectors or record unresolved links explicitly.
4. Deliver the records CSV and the check CSV.
5. For Chinese data intended for Excel, always use `utf-8-sig` CSV. If the user reports Excel乱码 or the file is important, also provide `.xlsx` from a spreadsheet library or bundled workspace dependency.

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
- `--source-type auto|detail-links|table`: choose detail-page crawling or official table extraction.
- `--section-keyword "0812J3 数据科学和信息技术"`: when a large admission catalog contains many programs, extract only the section after this keyword and stop before the next major heading.

## Output Files

- `mentors.csv`: one row per successfully parsed mentor.
- `mentors.xlsx`: generated when `openpyxl` is available; prefer this for Excel review.
- `mentors.jsonl`: same records in JSONL.
- `coverage_check.csv`: one row per teacher link found on the list page, including parse status.
- `source_notes.md`: present when the script uses an official table instead of teacher detail pages.

## Quality Bar

- Do not claim completeness from a college homepage crawl.
- Completeness means: complete relative to the confirmed list page, verified by `coverage_check.csv`.
- For admissions projects, do not use an older project-introduction page as the final mentor authority when a current-year admission catalog exists.
- For large admission catalogs, never run table mode without a project-level `--section-keyword`; otherwise the output may mix unrelated majors.
- Do not include an official URL in final source tables unless it was opened or fetched successfully during the run.
- Never write Chinese CSV content through PowerShell here-strings or shell-built string scripts. Use Python source files, `apply_patch`, or structured writers with UTF-8/UTF-8-BOM.
- If the list page is paginated or split by tabs/directions, collect every relevant list URL and run the script once per list URL or merge outputs afterward.
- Preserve official URLs in the output; do not infer missing emails or research directions.
