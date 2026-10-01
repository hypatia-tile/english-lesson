# english-lesson

Claude Code skills for asking questions about English quickly, without worrying
about duplicates. Answers are saved as Markdown notes and published to public
gists; `main` keeps no learning history. The skills also work from claude.ai,
e.g. on a phone.

## How it works

- `main` holds only the skills and the machinery that runs them.
- Notes are written to `notes/`, a worktree of the orphan branch `notes`,
  which is pushed after every note. Its tip shows the notes of the last few
  days; flushed notes leave the tip but stay in its history.
- On every Claude Code session start, a hook runs `scripts/flush`, which
  uploads notes 3 or more days old (JST calendar days) to a new public gist,
  removes them from `notes` and pushes the branch. On failure the notes stay
  and the next session retries.
- The same hook then runs `scripts/import`, which turns `note` issues filed
  from claude.ai into notes and closes them. Closed issues stay as a history
  of what was asked; the skills never read them.

Requirements: `git` 2.42+, an authenticated `gh`.

## Usage

Open Claude Code in this repository and ask anything about English. The `ask`
skill classifies the question, answers it and saves a note.

To read a technical article or paper, give Claude its URL, a PDF or the text.
The `read` skill discusses it by quoting the exact passages, and saves your
questions about its English as notes.

To use both from a phone, open this repository in Claude Code on the web; a
plain claude.ai Project works too, through issues. See
[docs/claude-web.md](docs/claude-web.md).

## Output contract

This repository does not know how the gists are used. Consumers can rely on:

**Gist description** — `english-lesson <YYYY-MM-DD>` (the flush date, JST).
Find them with `gh gist list --public | grep 'english-lesson '`.

**File name** — `<YYYYMMDDTHHMMSS>_<type>_<slug>.md`

- timestamp: creation time in JST (for notes from claude.ai, the issue's)
- `type`: `word`, `phrase`, `grammar`, `correction`, `compare` or `sentence`
  (more may be added)
- `slug`: `[a-z0-9-]`, at most 50 characters

Splitting on `_` always yields exactly these three fields.

**Content** — YAML frontmatter with a single key, `question`, holding the
original question verbatim. The body is free-form Markdown and may differ by
type.

Duplicates are expected: the same word asked in different ways produces
separate notes.

## License

[MIT](LICENSE)
