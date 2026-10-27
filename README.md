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

You'll do this once. It takes about 15 minutes. You don't need a GitHub account or any
coding experience.

**1. Install Obsidian.** Download it free from [obsidian.md](https://obsidian.md) and
install it like any other app.

**2. Install your AI helper.** Pick one:
- **Claude Code:** follow the install steps at
  [claude.com/claude-code](https://claude.com/claude-code). It also comes inside the
  Claude desktop app.
- **OpenAI Codex:** follow the install steps at
  [developers.openai.com/codex](https://developers.openai.com/codex).

**3. Open your AI helper in your Documents folder.** Open the Terminal app (Mac) or
PowerShell (Windows), type `cd Documents`, and press Enter. Then type `claude` (or
`codex`) and press Enter.

**4. Paste this setup prompt.** Copy the whole box below and paste it in:

```text
Set up law-brain for me. I'm a law student and I've never used a terminal, so explain
everything in plain English and don't install anything.

1. Download https://github.com/nikhildhoka8/law-brain/archive/refs/heads/main.zip
   into this folder, unzip it, and rename the folder to law-brain. (No GitHub account
   needed. If a law-brain folder already exists here, ask me first.)
2. Then open law-brain/prompts/setup.md and follow it, starting at step 2.
```

Your helper downloads the kit and asks where your class materials are: a folder on
your computer (like Desktop or Downloads), Google Drive, OneDrive, Notion, Canvas, or
email. It shows you the list of files and waits for your OK. Then it copies them into
the kit's `raw/` folder, sorted into `syllabus/`, `cases/`, `class-notes/`,
`outlines/`, and `exams/`. It asks you the course name, your professor's name, and
whether you already have an Obsidian vault. Then it builds your notes and tells you
what it made.

PDF, Word, PowerPoint, Markdown, plain text, saved emails, and even phone photos or
scans of handouts all work. See [SOURCES.md](SOURCES.md) for how the helper reaches
Drive, OneDrive, Notion, Canvas, and email.

**5. Open the vault in Obsidian.** In Obsidian, choose **Open folder as vault** and
pick the `vault` folder inside `law-brain` (or your own vault, if you told the helper
to use it). Open `_maps` and click your course's map. Then click the graph icon on the
left to see everything connected: cases are blue, rules green, topics orange, hypos
purple, and professor signals red.

**After every class:** drop your new notes into `raw/` (or tell your helper where they
are), open your helper in the `law-brain` folder (see below), and type `/ingest` or
"run the ingest prompt." It adds to what's there; it never erases your work.

> **Rather click than paste?** Download the kit straight from
> [this link](https://github.com/nikhildhoka8/law-brain/archive/refs/heads/main.zip)
> (no account needed), unzip it into Documents, and rename the folder to `law-brain`.
> Open your helper in that folder (see below) and type "run the setup prompt."

## What else you can ask for

| Say this | What you get |
|---|---|
| "Run the setup prompt" | Finds and copies more materials into `raw/`, then builds |
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
4. Type `/ingest` (or "run the ingest prompt"). Other shortcuts: `/setup`,
   `/attack-outline`, `/quiz`, `/gaps`.

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

Everything stays on your computer. Your materials, notes, and settings are never
uploaded anywhere by this kit. (If you ever share your copy of the kit online, the
`.gitignore` file keeps your `raw/` files, notes, and `my-settings.md` out of it.) Only
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
| `prompts/` | The five prompts: setup, ingest, attack outline, quiz, gaps |

MIT licensed. See [LICENSE](LICENSE).
