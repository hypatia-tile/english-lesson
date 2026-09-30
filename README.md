# english-lesson

Claude Code skills for asking questions about English quickly, without worrying
about duplicates. Answers are saved as Markdown notes and published to public
gists; this repository keeps no learning history.

## How it works

- `main` holds only the skills and the machinery that runs them.
- Notes are written to `notes/`, a worktree of the local-only orphan branch
  `notes`. It is never pushed.
- On every Claude Code session start, a hook runs `scripts/flush`, which
  uploads notes 3 or more days old (JST calendar days) to a new public gist and
  removes them from `notes`. On failure the notes stay and the next session
  retries.

Requirements: `git` 2.42+, an authenticated `gh`.

## Usage

Open Claude Code in this repository and ask anything about English. The `ask`
skill classifies the question, answers it and saves a note.

## Output contract

This repository does not know how the gists are used. Consumers can rely on:

**Gist description** — `english-lesson <YYYY-MM-DD>` (the flush date, JST).
Find them with `gh gist list --public | grep 'english-lesson '`.

**File name** — `<YYYYMMDDTHHMMSS>_<type>_<slug>.md`

- timestamp: creation time in JST
- `type`: `word`, `phrase`, `grammar`, `correction` or `compare`
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
