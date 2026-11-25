# ai-report-co-writing

English | [中文](README.md)

An Agent Skill for co-writing long Word documents with AI, suited to bid technical proposals, feasibility studies, solution documents, and project reports. It gives the AI a fixed way of working from tender documents to the final version: break down the requirements and produce an outline first, then, once you confirm it, draft chapter by chapter, review, merge, and add figures, and after that revise over many rounds under the same rules. Three things hold throughout: every statement has a source, the whole document stays consistent, and your own edits are never overwritten.

## What it is

A single `SKILL.md` for AI agents that support Skills. It is not a writing template. It is a working method.

It comes from a real bid: a technical proposal of 300+ pages that started with requirements analysis and went through 18 versions. This Skill turns the practices used and the problems met along the way into rules the AI follows at every step.

## Problems it addresses

| Common problem | What the Skill does |
|---|---|
| The tender runs to dozens of pages, and requirements or mandatory clauses get missed | Breaks the tender down into four tables (functional requirements, non-functional requirements, mandatory clauses, information gaps); the outline includes a coverage check so every requirement has a place |
| The AI starts writing body text at once, and a wrong structure means starting over | Produces an outline with writing guidance first, and drafts chapters only after you confirm it |
| After the first draft, it is unclear what you must supply and what the AI can fix | Reviews the first draft and produces a fix list split into "for people to supply" and "for the AI to fix", with priorities and dependencies |
| Edits you made in Word/WPS are overwritten by the AI's next version | Checks the file's md5 and modification time before each round, takes your latest file as the base, and builds on your edits |
| A changed duration, headcount, or version number is updated in one place and missed in a dozen tables and figures | Maintains a terminology-and-facts sheet; when a fact changes, scans body text, tables, and figures, then scans again to confirm nothing is left |
| Qualifications, references, or certificates are invented | Facts come only from the tender documents and your materials; anything without a source is written as a 【待补充：…】 ("to be supplied") placeholder in red |
| Padding with boilerplate sections to reach a page count | Expands only by deepening existing functional points, with no templated filler sections |
| Page count and page breaks change after saving in another program | Edits the document XML directly and keeps the original formatting; never saves your file with LibreOffice |
| Headings, tables, and figures all look different | Uses one set of default layout, table, and figure conventions, applied through styles |
| After a large revision nobody can say what changed | Delivers a revision log, a highlighted comparison copy, and a list of items for you to confirm with every version |

## What's inside

`SKILL.md` has ten parts:

1. **Drafting principles**: sourced facts, conclusion first, no new commitments, the terminology-and-facts sheet, structure following the tender clauses.
2. **Drafting process**: the four requirements tables, outline with writing guidance, chapter-by-chapter drafting, first-draft review and the split fix list, merging and figures, scoring checklist and tender changes.
3. **Revision process**: propose before changing, latest file as base, versioning, verified write-back, full-document scans, short delivery notes.
4. **Layout conventions**: defaults for page, body text, heading levels, captions, and table of contents.
5. **Table conventions**: style, column widths and alignment, content and placement, how to build tables.
6. **Figure conventions**: palette, font sizes, how to draw layered architecture diagrams, schedule charts, Gantt charts, and flowcharts, plus checking and filing.
7. **Safe editing of Word documents**: how to edit without breaking formatting or pagination.
8. **Clause-by-clause response and deviation table**: how to write and verify the response to each tender clause.
9. **Expansion and page count**: how to add length and how to adjust pages.
10. **Deliverables**: revision log, comparison copy, confirmation list.

## Scope

Suited to Word documents of tens to hundreds of pages that are drafted from scratch and go through multiple revision rounds, such as bid technical proposals, feasibility studies, solution documents, and project reports.

Less suited to one- or two-page pieces, documents written once and never revised, or non-Word formats.

## Quick start

**1. Install**

**One-line install**: send this in your agent's chat box:

```text
Install the Skill from https://github.com/ReyYoung/ai-report-co-writing and name it ai-report-co-writing. When it is installed, confirm that SKILL.md can be read and tell me the install path.
```

**Manual install**: put the `ai-report-co-writing` folder (containing `SKILL.md`) into the skills directory of your agent, or import it the way your agent expects.

```bash
git clone https://github.com/ReyYoung/ai-report-co-writing.git
# Example for Claude Code, whose personal skills directory is ~/.claude/skills/
cp -r ai-report-co-writing ~/.claude/skills/
```

For other agents, follow their official documentation.

**2. Prepare your materials**

- Tender or requirements documents (a de-identified copy is recommended)
- Your existing solution and product materials
- A document template, if the buyer or your company requires one

**3. Start**

```text
Use ai-report-co-writing to draft the technical proposal from this tender document.
Analyze the requirements first, then give me an outline with writing guidance; draft the chapters after I confirm.
```

When revising:

```text
The project duration changes from 8 months to 6. List what needs to change and to what first; edit after I confirm.
```

## Requirements

- An AI agent that can read and write local files and run Python.
- Python libraries: `python-docx`, `lxml`.
- Playwright (Chromium), to render SVG figures to PNG.
- LibreOffice (optional), used only for PDF preview and checking page counts, never to save the document. The Skill works without it: page counts are then estimated from the layout settings, and what you see in Word or WPS is what counts.

It has been tested and works in Claude, WorkBuddy, and 千问办公. Other agents that support Skills should be able to use it, but they have not been tested one by one.

## Language and defaults

`SKILL.md` is written in Chinese, and its defaults follow common conventions for formal Chinese documents (SimSun 12 pt body text, SimHei headings, 1.5 line spacing, a single blue palette for figures). Details about WPS and style IDs come from experience in a Chinese office environment.

If the tender, your company template, or you require something else, those take precedence. You can also edit the defaults in `SKILL.md` directly, or adapt it to another language.

## Usage notes

**Division of work**: people decide, AI executes. How the outline and the approach are set, how each fact is fixed, whether the product can really do something, and whether each commitment holds are human decisions. Breaking down the requirements and producing the outline, drafting chapters, rewriting and formatting, drawing figures, consistency checks, revision logs, and comparison copies go to the AI.

**Confirmation points**: the AI stops and waits for you after the outline, after the chapter drafts and the two fix lists, after the sample figures, and before each revision round. To skip one, say so explicitly, for example "no need to confirm the outline, write directly".

**Data security**: give the AI a de-identified copy of the tender documents. Keep sensitive content such as qualifications, references, certificates, and personnel details away from the AI, and fill them into the placeholders yourself.

**Three things to read with each version**: the revision log (what changed), the comparison copy (where it changed), and the confirmation list (what you need to decide).

**Update the table of contents first**: page numbers in the table of contents are left blank. Open the document in Word or WPS, right-click the table of contents, choose "Update Field", then "Update entire table", and the page numbers appear.

## What it cannot do

- It cannot win the bid for you.
- It cannot judge whether your product has a given capability; everything written as a feature needs your confirmation.
- The placeholders have to be filled in by a person.

## Repository layout

```text
ai-report-co-writing/
├── SKILL.md        # The Skill itself (in Chinese)
├── README.md       # Chinese README
├── README_EN.md    # English README
└── LICENSE         # MIT License
```

## Feedback

Issues with problems and field experience are welcome, as are pull requests that add conventions for other kinds of documents.

## License

Released under the [MIT License](LICENSE). You are free to use, modify, and distribute it, provided the copyright notice is kept.
