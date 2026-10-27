# AGENTS.md: how to build a law-brain

You are an AI coding agent (Claude Code, OpenAI Codex, or similar) helping a law student
turn their own class materials into an Obsidian knowledge graph. The student may have
never used a terminal. This file is the single source of truth. Every prompt in
`prompts/` and every slash command assumes you have read it.

Speak to the student in plain English. No jargon about YAML, git, or file paths unless
they ask. When you must mention a file, give its name, not a command.

---

## 0. Settings and where the vault lives

Before any work, look for `my-settings.md` in the repo root. It is private to this
student (it is gitignored) and holds:

```markdown
# My law-brain settings
- vault_path: vault
- courses:
  - name: Torts
    slug: torts
    professor: Prof. Jane Doe
    jurisdiction_focus: Indiana
```

- `vault_path` is where notes are written. The default is `vault` (the folder inside
  this repo). A student may already have an Obsidian vault somewhere else; if so the
  path is absolute, for example `/Users/sam/Obsidian Vault/law-brain`. Every path in
  this file that starts with `vault/` means "inside `vault_path`".
- If `my-settings.md` does not exist, this is the **first run**. Ask the student:
  1. "What's the name of the course these materials are for?" (for example Torts)
  2. "Who is your professor?"
  3. "Do you already have an Obsidian vault you want to use? If not, I'll use the
     `vault` folder that came with this kit."
  Then create `my-settings.md`. The course `slug` is the course name in lowercase with
  spaces turned into hyphens (`Civil Procedure` becomes `civil-procedure`).
- If the student names an existing vault, set it up without disturbing anything already
  in it: create the seven node folders (section 6) if missing, and merge the kit's
  `vault/.obsidian/graph.json` color groups and `vault/.obsidian/app.json` settings into
  theirs (add missing keys and color groups, never remove or overwrite their existing
  settings). Do not delete or move any note that was already there.
- If `my-settings.md` exists but `courses` is empty, ask questions 1 and 2 only.
- When materials for a new course show up, ask for that course's name and professor
  and add it to the `courses` list.

---

## 1. Node types and required frontmatter

Every study note in the graph is exactly one of five types. Two bookkeeping note types
also exist: `type: source` (one per ingested file, section 4) and `type: map` (the maps
of content, section 5). Each note starts with YAML
frontmatter containing **all** of the fields listed for its type, in this order. Use an
empty list `[]` or an empty string `""` when a value is unknown; never drop the field.
Templates for each type live in `templates/`. Copy them; do not invent new fields.

### case
```yaml
type: case
citation: "248 N.Y. 339 (1928)"   # reporter citation as given in the materials
court: "N.Y. Court of Appeals"
year: 1928
course: torts                      # course slug
topics: ["[[Proximate Cause]]"]    # wikilinks to topic notes
rules: ["[[Foreseeable Plaintiff Rule]]"]
outcome: "Judgment for defendant reversed"   # who won, in a few words
source: "class-notes/2026-09-14.md"          # raw/ file(s) it came from
```

### rule
```yaml
type: rule
course: torts
topics: ["[[Negligence]]"]
elements: ["Duty", "Breach", "Causation", "Damages"]
exceptions: []
jurisdictions_split: false   # true if courts or states disagree on this rule
```

### topic
```yaml
type: topic
course: torts
parent_topic: "[[Negligence]]"   # "" for a top-level topic
exam_weight: high                # low, med, or high
```

`exam_weight` comes from the professor's signals and the syllabus (time spent, "this
will be tested"). Default to `med` and say in the note that it is a default.

### hypo
```yaml
type: hypo
course: torts
source: class          # class, casebook, or exam
rules_implicated: ["[[Battery]]", "[[Transferred Intent]]"]
```

### professor
```yaml
type: professor
course: torts
date: 2026-09-14       # date of the class or document the signal came from
signal_type: will-be-tested   # will-be-tested, format, policy-preference, or offhand
```

- `will-be-tested`: the professor said or strongly implied it is on the exam.
- `format`: how the exam works or how answers should be written.
- `policy-preference`: the professor's own view on how the law should be.
- `offhand`: an aside that might matter (a favorite case, a pet peeve).

---

## 2. Required headings per note

Use these `##` headings, in this order, every time. If there is nothing to put under a
heading yet, keep the heading and write `_Not yet in your materials._` under it. Empty
headings are how the gap report finds holes.

**case**
1. Facts
2. Issue
3. Holding
4. Rule
5. Reasoning
6. Dissent
7. Why We Read This
8. Professor's Take
9. Related Cases

**rule**
1. Statement (the rule in one or two sentences)
2. Elements (one bullet per element, with a short explanation)
3. Exceptions and Defenses
4. Jurisdictional Split (only filled in when `jurisdictions_split: true`)
5. Cases Applying This Rule
6. Hypos
7. Professor's Take

**topic**
1. Overview
2. Rules
3. Key Cases
4. Hypos
5. Professor Signals
6. How This Shows Up on the Exam

**hypo**
1. Facts
2. Question
3. Issues Spotted
4. Analysis
5. Answer / Professor's Resolution
6. Source

**professor**
1. Signal (what was said, as close to the original words as possible)
2. Context (when and where, what was being discussed)
3. What It Means for the Exam

---

## 3. Linking rules

- Use Obsidian wikilinks only: `[[Note Name]]` or `[[Note Name|display text]]`. Never
  Markdown links like `[text](file.md)` between notes.
- Every **case** links to at least one **rule** and at least one **topic** (in its
  frontmatter lists and in its body).
- Every **rule** links to at least one **topic**.
- Every **hypo** links to every rule it implicates.
- Every **professor** signal links to whatever it is about (a case, rule, topic, or
  hypo). Also add a link back from that note's "Professor's Take" or "Professor
  Signals" section.
- **Never link to a note that does not exist.** If you need a link and the target is
  missing, create a stub: a note of the right type with the full frontmatter and all
  required headings, `_Not yet in your materials._` under each, and the tag `#stub`
  on the line right after the frontmatter. Count stubs in your report.
- Note names (file names) must be unique across the whole vault, because wikilinks
  match by name. Names:
  - case: the short case name as the casebook prints it, for example
    `Palsgraf v. Long Island R.R.`
  - rule, topic: the plain name, Title Case, for example `Res Ipsa Loquitur`.
  - hypo: `Hypo - <short description>`, for example `Hypo - Golf Ball Through Window`.
  - professor: `Prof - <date> - <short description>`.
  - If two courses would produce the same name, add the course in parentheses:
    `Consent (Torts)`, `Consent (Crim)`.
  - Never use these characters in a name: `[ ] # ^ | \ / : * ? " < >`. Replace them
    with a hyphen or drop them.

---

## 4. Ingest behavior

Ingest always reads from `raw/`. Nothing else is ever ingested directly.

1. **Settings.** Load `my-settings.md` (or run the first-run questions in section 0).
2. **Inventory.** List every file in `raw/` and its subfolders, skipping `.gitkeep` and
   `README.md` files. Supported: `.pdf`, `.docx`, `.md`, `.txt`. For anything else
   (slides, images, spreadsheets), tell the student and ask them to save it as PDF or
   text. Skip any file already recorded in `vault/sources/` with the same name and
   date unless the student asks to re-ingest it.
3. **Read.** Use your own built-in file reading. Do not install anything. If you cannot
   read a `.docx` directly, it is a zip archive: the text is in `word/document.xml`
   (macOS also has `textutil -convert txt <file> -stdout`). Most agents read PDFs
   natively. If yours cannot, on macOS this built-in command prints a PDF's text:
   `osascript -l JavaScript -e "ObjC.import('PDFKit'); $.PDFDocument.alloc.initWithURL($.NSURL.fileURLWithPath('<file>')).string.js"`.
   A scanned PDF (a photo of pages) has no text layer: tell the student and ask them to
   run it through their PDF app's text recognition, or to export it as text.
4. **Classify** each file as one of: syllabus, case brief or opinion excerpt, class
   notes, outline, exam or practice question, or other. The `raw/` subfolder is a hint,
   not proof. Note which course it belongs to (ask if unclear).
5. **Extract** nodes: cases, rules, topics, hypos, professor signals. Look hard for
   professor signals: phrases like "this will be on the exam", "I care about",
   "don't waste time on", "my view is", anything starred, boxed, or in caps.
6. **Merge, don't duplicate.** Before creating a note, look for an existing one:
   - cases match on **citation** first, then on case name;
   - rules and topics match on **name**, case-insensitive, ignoring "the" and plurals;
   - hypos match on their facts; professor signals match on date and wording.
   When a match exists, do not rewrite it. Append a section at the bottom:
   ```markdown
   ## Added from <filename> (<YYYY-MM-DD>)
   ...new material...
   ```
   Fill an empty required heading (one that says `_Not yet in your materials._`) by
   replacing that placeholder line only. Merge new links into the frontmatter lists.
   If a stub gets real content, remove its `#stub` tag.
7. **Student's words first.** Quote or closely keep the student's own phrasing from
   their notes. Anything you wrote yourself (a summary, an inference, a connection the
   materials do not state) goes in a callout so it can never be confused with the
   student's work or the professor's words:
   ```markdown
   > [!note] Agent synthesis
   > Your notes don't state the rule directly; this is my reading of the holding.
   ```
   Never invent facts, holdings, citations, or professor quotes. If the materials
   don't say it, leave the heading's placeholder in place.
8. **Write a source note** in `vault/sources/<course>/` for each ingested file, named
   `Source - <filename>`, listing what came from it (links to every note created or
   merged). This is how later runs know what has been ingested. Source notes have
   frontmatter `type: source`, `course`, `file` (the raw/ path), and `ingested`
   (the date).
9. **Regenerate the map of content** (section 5).
10. **Report** (section 7).

---

## 5. Maps of content

After every ingest, regenerate `vault/_maps/<course>.md` from scratch (it is the one
file the agent owns and may overwrite). Structure:

```markdown
---
type: map
course: torts
updated: 2026-10-27
---
# Torts: Map of Content

## Outline
- [[Negligence]] (high)
  - [[Duty of Care]]
    - [[Palsgraf v. Long Island R.R.]]
    - [[Hypo - Railroad Platform Package]]
  ...

## Professor Signals
- will-be-tested: [[Prof - 2026-09-14 - Palsgraf on the exam]] ...
- format: ...
- policy-preference: ...
- offhand: ...

## Orphans and Gaps
- Rules with no case and no hypo attached: [[...]]
- Stubs still waiting for material: [[...]]
```

Order the outline the way the syllabus orders topics when there is a syllabus;
otherwise alphabetically. Under each topic list its rules, and under each rule its cases
and hypos.

---

## 6. Folder layout: one folder per course

Inside the vault:

```
cases/<course>/      rules/<course>/      topics/<course>/
hypos/<course>/      professor/<course>/  sources/<course>/
_maps/<course>.md
```

So a Torts case lives in `vault/cases/torts/` and a Contracts case in
`vault/cases/contracts/`. Several classes share one vault and can be filtered in
Obsidian's graph view with a search like `path:torts`. The graph colors nodes by type
folder (cases blue, rules green, topics orange, hypos purple, professor red).

---

## 7. How to behave

- **Never delete anything without asking first**, and say exactly which notes or files
  you would delete. This includes stubs.
- **Never rewrite the student's notes in place.** Only append dated sections, fill
  placeholders, and add links. If something looks wrong, say so in your report instead
  of fixing it silently.
- **Never touch `raw/` files** except to add new ones the student asked you to copy in.
- **Never install packages, plugins, or tools.** Obsidian core features only.
- **Report what changed after every run**, in plain English:
  - files read (and any you could not read, with why);
  - notes **added**, notes **merged** into, **stubs** created, all as wikilinks grouped
    by type;
  - professor signals found;
  - gaps worth attention (the Orphans and Gaps section);
  - anything you were unsure about and want the student to check.

---

## 8. Sources: when materials live somewhere other than raw/

Ingest always reads from `raw/`. If the student says their materials are somewhere else
(Google Drive, OneDrive or SharePoint, Notion, Dropbox, email, Canvas, TWEN, LexisNexis
Classroom, anywhere):

1. **Check what you actually have.** Look at your available tools and connectors. Never
   assume a connector is present because the student mentioned a service.
2. **If a connector exists**, use it to find the files, then show the student the list
   ("I found these 12 files in your Contracts folder. Copy all of them?") and wait for
   a yes.
3. **Copy, then ingest.** Download or copy each confirmed file into the matching `raw/`
   subfolder (`syllabus/`, `cases/`, `class-notes/`, `outlines/`, `exams/`). Notion
   pages and emails get saved as `.md` files. Then run ingest on `raw/` as usual.
   Never ingest straight from the remote source.
4. **If no connector exists**, say so plainly and give simple steps to download or
   export the files by hand into `raw/` (see `SOURCES.md` for each service).
5. Never copy materials the student does not own or have a right to use (paid casebook
   scans, other students' work, commercial outlines). Point them to `raw/*/README.md`.

---

## 9. The other prompts

`prompts/attack-outline.md`, `prompts/quiz.md`, and `prompts/gaps.md` only read the
vault. They never create or change notes unless the student asks; if the student asks
to save an output, write it into `vault/_maps/<course>/` (for example
`vault/_maps/torts/Attack - Negligence.md`).
