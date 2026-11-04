# markdown

Markdown to HTML for [Moth](https://github.com/samyyy2423/moth), as CommonMark and GitHub write it:
headings, paragraphs, emphasis, links and pictures, code, lists (and lists in lists), quotes, tables, task
lists, rules and line breaks. In Moth alone, so it works everywhere Moth does.

```text
moth add markdown
```

```
use the package "markdown" as markdown

say markdown's to_html("# Notes\n\nSome *very* **useful** `code`.")
```

```html
<h1 id="notes">Notes</h1>
<p>Some <em>very</em> <strong>useful</strong> <code>code</code>.</p>
```

## What it has

| | |
|---|---|
| `to_html(words)` | the Markdown as HTML |
| `to_html_trusted(words)` | the same, with any HTML in the Markdown put in the page as it is |
| `inline_html(words)` | one line or paragraph as HTML, with no `<p>` around it |
| `headings(words)` | the headings, in order, as records of their `level`, `text` and `id`: a table of contents |

HTML written in the Markdown is shown as text, not put in the page, so what people type can't add scripts
to it. That makes `to_html` right for a web app that shows what its visitors write, such as Moth's
[guestbook](https://github.com/samyyy2423/moth/tree/main/apps/guestbook):

```
use the package "markdown" as markdown

# each message with its *emphasis* and [links](https://example.com), where book.moth has
# "<p>" + html_of(item "message" of entry) + "</p>"
add "<article>" + markdown's to_html(item "message" of entry) + "</article>" to rows
```

Use `to_html_trusted` only for Markdown you wrote yourself. Either way, a link or picture to a
`javascript:`, `vbscript:`, `file:` or `data:` address (but `data:image/...`) is left out, keeping its words.

Each heading gets an `id`, as GitHub's do, so a page can link to it: "Getting started" is `getting-started`,
and a second heading of that name `getting-started-1`.

```
for each h in markdown's headings(read "notes.md")
    say "{h's level} {h's text} #{h's id}"
end
```

## What it reads

`#` headings (and a line of `===` or `---` under one), paragraphs, `*em*` and `_em_`, `**strong**`,
`~~struck~~`, `` `code` ``, `[links](address "title")`, `[links][name]` with `[name]: address` on a line of its
own, `<https://...>` and bare `https://` addresses, `![pictures](address)`, `>` quotes, `- + *` and `1.` `1)`
lists, `[ ]` and `[x]` task items, ` ``` ` and `~~~` fenced code (with its language), code indented 4 spaces,
`| tables |` with `:--:` alignments, `---` `***` `___` rules, `\` before a mark for the mark itself, two spaces
or a `\` at a line's end for a `<br />`, and `&entities;`.

## Tests

```text
moth test markdown.test.moth
```

## License

Apache License 2.0, as Moth is: see [LICENSE](LICENSE).
