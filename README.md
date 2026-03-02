# highlight-author

A [Quarto](https://quarto.org) extension that highlights a specific author's name in bibliography entries.

## Use cases

Any document with a `bibliography` where you want one name to stand out:

- **Academic homepages** — highlight yourself in your publication list
- **CVs and resumes** — make your name visually distinct in references
- **Grant proposals** — NSF, NASA, and other agencies require or expect the PI's name to be highlighted in the bibliography
- **Tenure and promotion packets** — same convention as grants
- **Lab group pages** — highlight all group members' contributions
- **Theses and dissertations** — some institutions require the candidate's name to be marked

Works with any Quarto output format: HTML, PDF, Word, and more.

## Installation

```bash
quarto add michaelaye/highlight-author
```

## Usage

Add to your document's YAML front matter:

```yaml
bibliography: references.bib
citeproc: false
filters:
  - highlight-author

highlight-author: "Aye"
```

**Important:** `citeproc: false` is required because this filter runs citeproc internally to process the bibliography before highlighting names.

### Configuration options

**Shorthand** (defaults to bold):

```yaml
highlight-author: "Aye"
```

**Full form** with style selection:

```yaml
highlight-author:
  name: "Aye"
  style: bold
```

### Supported styles

| Style | Effect | Output element |
|-------|--------|----------------|
| `bold` (default) | **Aye, K.-M.** | `<strong>` |
| `italic` | *Aye, K.-M.* | `<em>` |
| `underline` | <u>Aye, K.-M.</u> | `<u>` |
| Any other value | CSS class | `<span class="value">` |

Custom CSS class example:

```yaml
highlight-author:
  name: "Aye"
  style: "highlight-name"
```

Then in your CSS:

```css
.highlight-name {
  font-weight: bold;
  color: #2563eb;
}
```

### What gets highlighted

The filter matches the surname in all common citation formats:

- Surname-first: **Aye, K.-M.**, **Aye, Klaus Michael**
- Given-name-first: **K.-M. Aye**, **Klaus-Michael Aye**
- Initials only: **K. M. Aye**

Both the surname and all associated given name parts are highlighted together.

## Combining with other bibliography filters

If you use this extension alongside other bibliography filters (e.g., for year grouping), make sure `highlight-author` appears first in the filter list since it invokes citeproc:

```yaml
citeproc: false
filters:
  - highlight-author
  - other-bibliography-filter.lua
```

## License

MIT
