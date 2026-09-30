---
name: read
description: Read a technical article or paper together with the user — load it from a URL, PDF or pasted text, then discuss it by quoting the exact passages. Use when the user shares an article, blog post, documentation page or paper to read, or asks about a passage of one already loaded, in Japanese or English. English questions about the text are saved as notes, like ask.
---

# Read a technical text together

The user reads mostly technical English: blog posts, documentation, papers.
The goal is a conversation anchored to the text — every answer points at the
exact words it is about.

## 1. Load

Accept whatever the user gives:

- **URL** — fetch it. For arXiv, prefer the HTML version
  (`arxiv.org/html/<id>`) over the abstract page; fall back to the PDF.
- **PDF** — read it with the Read tool, in page ranges for long papers.
- **Pasted text** — use it as is.

Keep the text in the conversation only. Never write the article itself to
`notes/` or anywhere else: notes become public gists.

## 2. Orient

Reply once, in Japanese, with:

- title, author(s), and source
- the gist in 2–3 lines
- an outline using the text's own structure (section numbers or headings),
  so the user can say "§3" or "Background" and be understood

Then wait for questions. Do not walk through the text unprompted.

## 3. Discuss

**Locators** — refer to places by the text's own structure plus a paragraph
count inside it: `§3.2 ¶2`, `Background ¶1`. With no headings, count
paragraphs from the top: `¶7`. Use the same locator every time for the same
place.

**Quotes** — every answer quotes the passage it is about, verbatim, as a
blockquote with its locator, before explaining:

```markdown
> We amortize the cost of rebalancing across insertions. (§3.2 ¶2)
```

Quote only what is needed — usually one sentence, never more than a short
paragraph. If the user's reference is ambiguous ("the second paragraph"),
pick the most likely place and quote it, so a wrong guess is obvious at once.

Explanations are in Japanese; keep technical terms in English where that is
how the field says them.

## 4. Save English questions as notes

Questions about the **English** of the text — a word, a phrase, a grammar
point, or how to parse a sentence — are saved as notes. Questions about the
technical content alone (what the algorithm does, whether the claim holds) are
answered in the conversation and not saved.

Classify with the `ask` skill's types, plus one more:

| type       | when                                                    |
|------------|---------------------------------------------------------|
| `sentence` | how to parse and read a sentence from the text          |

Write the body with the template for the type — `ask`'s
[references/templates.md](../ask/references/templates.md), or the one below
for `sentence` — and append a source section:

```markdown
## 出典

> <quoted passage>

<title> — <URL or file name>, <locator>
```

Name, write and commit the file exactly as `ask` step 3 describes; the slug
for `sentence` is a 3–5 word English summary of the sentence. The frontmatter
`question` is still the user's own words, verbatim.

### `sentence` template

```markdown
# <the sentence, shortened with … if long>

## 構造
<主語・動詞・修飾の関係を、括弧やインデントで示す>

## 訳
## 読み解きのポイント
<つまずきやすい語順・省略・技術英語特有の言い回し>
```
