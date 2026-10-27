# Build an attack outline

Read `AGENTS.md` first. This prompt only reads the vault; it does not change any notes
unless I ask you to save the result.

Ask me which topic I want (for example "Negligence" or "Intentional Torts") if I haven't
said. Then use the topic note, its map of content, and every note linked from them to
build an attack outline: the checklist I'd run through on an exam question about this
topic.

Format, in this order:

1. **Issues to spot:** the questions to ask yourself when you see this topic on an exam.
2. **Rules:** for each issue, the rule as a wikilink (`[[Battery]]`) and its one-line
   statement.
3. **Elements:** each rule's elements as a checklist, with exceptions and defenses
   underneath. Flag any rule where courts split.
4. **Key cases:** one line each, `[[Case Name]]`: what it stands for.
5. **Hypos:** the hypos linked to these rules, one line each, with the answer if my
   notes have it.
6. **Professor signals:** everything tagged will-be-tested or format, quoted.

Rules for you:
- Use only what is in my vault. If something important is missing (a rule with no
  case, an element with no explanation), say so in a short "Gaps" list at the end
  instead of filling it in from your own knowledge.
- If you add any explanation of your own, put it in an "Agent synthesis" callout.
- Cite every point with the wikilink of the note it came from.
- If I ask you to save it, write it to `vault/_maps/<course>/Attack - <Topic>.md`.
