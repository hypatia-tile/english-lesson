# Using the skills from claude.ai

Ask and read on claude.ai — from a phone, say — and the notes still land in
the `notes` branch. There are two ways; use the first.

## Claude Code on the web (recommended)

Start a session on [claude.ai/code](https://claude.ai/code) with this
repository and ask as you would locally. The session is a real checkout, so
the skills run unchanged: the session-start hook sets up `notes/` from
origin's `notes` branch, and each note is committed and pushed straight to
it. Nothing to set up, nothing to copy.

Notes are now pushed from more than one place. That is safe: every note is a
file of its own, a rejected push is retried after `pull --rebase`, and
`scripts/flush` rebases `notes` onto origin at every session start.

## claude.ai Project, via issues (fallback)

For a plain claude.ai chat, which cannot write to this repository, each note
travels as a GitHub issue:

```
claude.ai Project ──answer + save block──▶ you tap the link, paste, submit
                                                 │
                                    issue labelled `note`
                                                 │
next Claude Code session here ──scripts/import──▶ notes branch (pushed), issue closed
```

### Setup (once)

1. **Create a Project** on claude.ai, e.g. "English lesson".
2. **Add the skills to its knowledge** from GitHub (the project's knowledge
   panel lets you add files from a repository): choose
   `hypatia-tile/english-lesson` and select
   - `.claude/skills/ask/SKILL.md`
   - `.claude/skills/ask/references/templates.md`
   - `.claude/skills/read/SKILL.md`
3. **Paste the instructions** from
   [`claude-web/project-instructions.md`](../claude-web/project-instructions.md)
   into the project's custom instructions.

When the skills change on `main`, sync the project's GitHub knowledge so
claude.ai follows the new version. The instructions only change when the save
block itself does.

### Daily use

1. In the project, ask as you would in Claude Code: a word, a sentence to
   check, or an article URL / PDF to read together.
2. Each saved answer ends with a **save block**: a link and the note in a code
   block.
3. Copy the code block, tap the link, paste into **Note**, and submit. The
   title is already filled in (`<type>_<slug>`); leave it as it is.

   If Claude could run code, the link may already carry the note too — then
   just submit.

That is all on the phone. The next time a Claude Code session starts in this
repository, the hook runs `scripts/flush` and then `scripts/import`, which

- turns each open `note` issue you opened into
  `notes/<issue creation time, JST>_<type>_<slug>.md`,
- commits it as `note: <file name> (#<issue>)` and pushes `notes`,
- closes the issue with a comment naming the file.

Closed issues stay on GitHub as a history of what was asked; the skills never
read them. You can also run `scripts/import` by hand at any time.

### When an issue stays open

`scripts/import` prints why and leaves the issue for the next run. Edit the
issue, then start a new session or run `scripts/import`.

| message | fix |
|---|---|
| `title must be <type>_<slug>` | set the title to e.g. `word_valve` — lowercase, `a-z0-9-` in the slug |
| `body was not written with the note template` | the issue was opened without the Note form; open it from the save-block link |
| `the note must start with its --- frontmatter` | paste the whole code block, starting at `---` |

Only issues opened by the account `gh` is logged in as are imported. The
repository is public, so anyone can open an issue with the form; theirs are
ignored.
