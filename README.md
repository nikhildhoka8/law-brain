# law-brain

Turn your own class materials into a study map you can actually see.

law-brain is a starter kit. You give it your syllabus, class notes, case briefs, and
practice exams. An AI helper (Claude Code or OpenAI Codex) reads them and builds a
connected set of notes in **Obsidian**, a free note-taking app. No coding. Nothing to
install besides those two apps. The kit comes empty on purpose: everything in your
graph comes from your own materials.

## What's a knowledge graph, and why bother?

A normal outline is a long list: Negligence, then Duty, then Breach, and so on. Real
exam questions don't arrive in outline order. One fact pattern can raise battery,
consent, and proximate cause all at once. A **knowledge graph** stores each case, rule,
and topic as its own note and draws a line wherever two of them connect. Open a rule
and you see every case that applies it, every hypo it showed up in, and every time your
professor said "this will be on the exam." Open the graph view and the topics with the
most connections jump out, and so do the lonely rules you never tied to a case. That's
how you spot what to study next, instead of rereading 60 pages of outline.

## Quickstart

You'll do this once. It takes about 15 minutes.

**1. Install Obsidian.** Download it free from [obsidian.md](https://obsidian.md) and
install it like any other app.

**2. Install your AI helper.** Pick one:
- **Claude Code:** follow the install steps at
  [claude.com/claude-code](https://claude.com/claude-code). It also comes inside the
  Claude desktop app.
- **OpenAI Codex:** follow the install steps at
  [developers.openai.com/codex](https://developers.openai.com/codex).

**3. Get this kit onto your computer.** Easiest way: on this page on GitHub, click the
green **Code** button, then **Download ZIP**, and unzip it somewhere you'll find it
(like Documents). If you're comfortable with a terminal, `git clone` works too.

**4. Add your materials.** Drag your own files into the `raw/` folder, into whichever
subfolder fits: `syllabus/`, `cases/`, `class-notes/`, `outlines/`, or `exams/`. PDF,
Word, PowerPoint, Markdown, plain text, saved emails, and even phone photos or scans
of handouts all work. If your stuff is on Google Drive, OneDrive,
Notion, Canvas, or email, see [SOURCES.md](SOURCES.md): your agent can often fetch it.

**5. Tell your agent to build the graph.** Open your AI helper in the `law-brain`
folder (see the sections below) and type:

> Run the ingest prompt.

The first time, it will ask you the course name, your professor's name, and whether you
already have an Obsidian vault. Then it reads everything and tells you what it made.

**6. Open the vault in Obsidian.** In Obsidian, choose **Open folder as vault** and
pick the `vault` folder inside `law-brain` (or your own vault, if you told the agent to
use it). Open `_maps` and click your course's map. Then click the graph icon on the
left to see everything connected: cases are blue, rules green, topics orange, hypos
purple, and professor signals red.

Add new notes after every class and run the ingest prompt again. It adds to what's
there; it never erases your work.

## What else you can ask for

| Say this | What you get |
|---|---|
| "Run the ingest prompt" | Reads new files in `raw/` and updates your graph |
| "Run the attack outline prompt for Negligence" | An exam checklist for one topic |
| "Run the quiz prompt" | A practice hypo, then a grade on your answer |
| "Run the gaps prompt" | What's missing before the exam |

The prompts live in the `prompts/` folder if you're curious.

## Using Claude Code

1. Open the Terminal app (Mac) or PowerShell (Windows).
2. Type `cd ` (with a space), drag the `law-brain` folder into the window, and press
   Enter.
3. Type `claude` and press Enter.
4. Type `/ingest` (or "run the ingest prompt"). Other shortcuts: `/attack-outline`,
   `/quiz`, `/gaps`.

In the Claude desktop app, you can instead open the `law-brain` folder as your project
and type the same thing.

## Using Codex

1. Open the Terminal app (Mac) or PowerShell (Windows).
2. Type `cd ` (with a space), drag the `law-brain` folder into the window, and press
   Enter.
3. Type `codex` and press Enter.
4. Type "run the ingest prompt." Codex reads the rules in `AGENTS.md` automatically.

In the Codex desktop or editor app, open the `law-brain` folder and type the same
thing.

## Using a different agent

Any AI coding agent that can read and write files works. Paste the contents of a file in
`prompts/` into the chat, and it will take it from there.

## Your stuff stays yours

Your materials (`raw/`), your notes (`vault/`), and your settings (`my-settings.md`) are
listed in `.gitignore`, so they are never uploaded if you put your copy on GitHub. Only
bring in materials you have the right to use: your own notes and briefs, and handouts
from your professor. Not casebook scans, commercial outlines, or other students' work.

## What's in the box

| File or folder | What it is |
|---|---|
| `AGENTS.md` | The rulebook your agent follows. You don't need to read it. |
| `SOURCES.md` | How to bring in files from Drive, OneDrive, Notion, Canvas, and more |
| `raw/` | Where you drop your materials |
| `vault/` | Your Obsidian vault, empty until you run the ingest prompt |
| `templates/` | The blank note shapes the agent fills in |
| `prompts/` | The four prompts: ingest, attack outline, quiz, gaps |

MIT licensed. See [LICENSE](LICENSE).
