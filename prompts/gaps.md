# Find the gaps in my notes

Read `AGENTS.md` first. This prompt only reads the vault; it does not change notes
unless I ask you to fix something.

Check every course in my vault (or the one I name) and report:

1. **Orphan rules:** rules with no case and no hypo linked to them.
2. **Cases missing "Why We Read This":** cases where that heading still says
   `_Not yet in your materials._`
3. **Thin high-weight topics:** topics with `exam_weight: high` that have fewer than
   three linked cases, rules, or hypos combined.
4. **Stubs:** notes tagged `#stub` that are still waiting for real material.
5. **Empty headings:** any other required heading that is still a placeholder, grouped
   by note.
6. **Broken structure:** notes missing required frontmatter fields, or cases that don't
   link to at least one rule and one topic.

For each item, give the wikilink and one plain-English suggestion of what to bring in
(for example "your notes from the 9/14 class probably cover this" or "ask your
professor in office hours"). End with the three gaps that matter most for the exam,
based on professor signals and exam weight. Do not fill gaps from your own knowledge.
