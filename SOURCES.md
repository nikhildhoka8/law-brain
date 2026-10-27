# Where your materials live

Your agent always builds the graph from the `raw/` folder. If your materials are
already on your computer, you're done: drag them into `raw/` and skip this page.

If they live somewhere else, your agent can usually fetch them for you, **if** it has a
connector for that service turned on. A connector (sometimes called an MCP server) is a
small add-on that lets your agent read your Google Drive, Notion, and so on. The agent
will always:

1. look for the files and show you the list,
2. wait for you to say yes,
3. copy them into the right `raw/` subfolder,
4. and only then build the graph from `raw/`.

It never builds notes straight from the online copy, so your vault always matches what's
saved in `raw/`. If the agent says it doesn't have a connector, use the "do it by hand"
line in each section.

---

## On your computer (the default)

Nothing to set up. Drag files into `raw/syllabus/`, `raw/cases/`, `raw/class-notes/`,
`raw/outlines/`, or `raw/exams/`.

> Tell your agent: "Run the ingest prompt."

## Google Drive

- **Claude Code:** turn on the Google Drive connector in your Claude settings
  (Settings, then Connectors), or ask Claude Code "help me add a Google Drive MCP server."
- **Codex:** add a Google Drive MCP server to Codex (ask Codex "help me add a Google
  Drive MCP server").
- **Do it by hand:** in Drive, right-click the folder, choose **Download**, unzip it,
  and drag the files into `raw/`. Google Docs download as Word files, which work fine.

> "Pull everything in my Contracts folder on Google Drive into raw/, then run the
> ingest prompt."

## OneDrive or SharePoint

- **Claude Code:** turn on the Microsoft 365 connector in your Claude settings.
- **Codex:** add a Microsoft 365 or OneDrive MCP server.
- **Do it by hand:** if OneDrive is synced to your computer, the files are already in
  your OneDrive folder in Finder or File Explorer: copy them into `raw/`. Otherwise
  select the files on the OneDrive website and choose **Download**.

> "Copy the files in my OneDrive folder 'Torts Fall 2026' into raw/class-notes/."

## Notion

- **Claude Code:** turn on the Notion connector in your Claude settings.
- **Codex:** add the Notion MCP server (Notion publishes an official one).
- **Do it by hand:** open the page, click the **...** menu, choose **Export**, pick
  **Markdown & CSV**, include subpages, unzip, and drag the `.md` files into `raw/`.

> "Save every page under my Notion page 'Civ Pro Notes' into raw/class-notes/ as
> Markdown."

## Dropbox

- **Claude Code / Codex:** add a Dropbox MCP server if your agent offers one.
- **Do it by hand:** if the Dropbox app is installed, your files are already in the
  Dropbox folder on your computer: copy them into `raw/`. Otherwise download the
  folder from dropbox.com.

> "Copy my Dropbox folder 'Property' into raw/, sorted into the right subfolders."

## Email (Gmail or Outlook)

Professors often send exam memos, hypos, and slides by email.

- **Claude Code:** turn on the Gmail or Microsoft 365 (Outlook) connector.
- **Codex:** add a Gmail or Outlook MCP server.
- **Do it by hand:** download the attachments into `raw/`. For an email with useful
  text in it, copy the text into a new `.txt` file in `raw/`.

> "Find every email from Professor Doe with 'Torts' in the subject this semester. Save
> the attachments into raw/ and save each email's text as a .md file."

## Canvas, TWEN, LexisNexis Classroom, and other course portals

These live in your web browser behind your school login, and most agents have no
connector for them.

- **If your agent can control a browser** (some setups of Claude Code and Codex can),
  you can ask it to log in with you and download files. You type your own password;
  never paste it into the chat.
- **Do it by hand (most reliable):** open the course page, download the syllabus,
  handouts, and practice exams, and drag them into `raw/`. In Canvas, the **Files**
  page lets you select several files and download them as a zip.

> "I downloaded my Canvas files into my Downloads folder. Move the Torts ones into the
> right raw/ subfolders."

---

## What not to bring in

Your own notes, your own briefs and outlines, and handouts your professor gave the
class are great. Scans of your casebook, commercial outlines, and other students' work
are not: they're copyrighted, and the agent will skip them. Each `raw/` subfolder has a
README with details.
