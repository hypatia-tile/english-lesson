---
name: ask
description: Answer any question about English — a word, phrase, grammar point, a sentence to check, or two expressions to compare — and save the answer as a note. Use whenever the user asks something about English in this repository, in Japanese or English, however casually. Duplicates are fine; never refuse or redirect because a similar question was asked before.
---

# Ask anything about English

The user wants to ask quickly and without friction. Do not ask clarifying
questions unless the question is genuinely unanswerable; pick the most likely
reading and answer it.

## 1. Classify

Pick exactly one `type`:

| type         | when                                                        |
|--------------|-------------------------------------------------------------|
| `word`       | meaning, nuance, usage of a single word                     |
| `phrase`     | idiom, phrasal verb, collocation, set expression            |
| `grammar`    | a grammar or usage rule                                     |
| `correction` | the user wrote English and wants it checked or made natural |
| `compare`    | the difference between two or more expressions              |

If a message holds several independent questions, write one note per question.

## 2. Answer

Follow the body template for the type in
[references/templates.md](references/templates.md).

- Explanations in Japanese. Headwords, example sentences and corrected
  sentences in English.
- Keep it compact: something readable in under a minute.

Show the answer to the user in the conversation as well as saving it.

## 3. Save the note

The `notes/` directory is a worktree of the local-only `notes` branch. If it
does not exist, run `scripts/flush` first; it creates the worktree.

**File name** — `notes/<timestamp>_<type>_<slug>.md`

- `timestamp`: output of `TZ=Asia/Tokyo date +%Y%m%dT%H%M%S`
- `slug`: only `[a-z0-9-]`, at most 50 characters
  - `word` / `phrase`: the headword in kebab-case (`take-for-granted`)
  - `compare`: the items joined by `-vs-` (`affect-vs-effect`)
  - `grammar` / `correction`: a 3–5 word English summary
    (`present-perfect-vs-past`, `email-opening-greeting`)

**Content** — frontmatter holds only the user's original question, verbatim,
as a YAML block scalar; the body follows the template.

```markdown
---
question: |-
  serendipityってどういうニュアンス？
---

(body)
```

**Commit and push** — one commit per note, inside the worktree, then push:

```sh
git -C notes add <file> && git -C notes commit -m "note: <file name>"
git -C notes push origin notes
```

If the push fails, say so in one line and carry on: the note is committed, and
the next push (or the next session's flush) carries it. Never commit notes to
`main`.
