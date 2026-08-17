# Documentation project instructions

## About this project

- This is a documentation site built on [Mintlify](https://mintlify.com)
- Pages are MDX files with YAML frontmatter
- Configuration lives in `docs.json`
- Custom CSS lives in `style.css`. Mintlify includes any `.css` file in the content
  directory on every page, so scope rules to a class used by the page that needs them
- Use the Mintlify MCP server, `https://mcp.mintlify.com`, to edit content and settings via MCP
- Use the Mintlify docs MCP server, `https://www.mintlify.com/docs/mcp`, to query information about using Mintlify via MCP
- For Mintlify product knowledge (components, configuration, writing standards),
  install the Mintlify skill: `npx skills add https://mintlify.com/docs`

## Terminology

One term per concept. Check an existing page before introducing a new one.

- **application**, not service. Applications are what Lightbase detects and groups
- **model**, not map, graph, or representation, for what Lightbase builds
- **code flow**, not trace or path, for one execution path through the system
- **entrypoint** for the HTTP route, queue consumer, or CLI command that starts a flow
- **counterparty** for an external entity the code interacts with
- **business entity** for a domain concept mapped to the tables and flows that use it
- **blast radius** for the downstream reach of a change

## Style preferences

### Voice

- Second person. The reader is a developer, engineering manager, or architect.
  Don't name their role: "You explore that model", not "Engineers explore that model".
- Active voice, present tense.
- Define a term where it first appears rather than linking away to its definition.
- Don't name internal surfaces like the UI or dashboard unless a page documents them.
- Bold for UI elements: Click **Settings**.
- Code formatting for file names, commands, paths, and code references.

### Sentences and paragraphs

- Under 25 words per sentence. One idea per sentence.
- If a sentence needs several commas or semicolons to hold together, split it.
- Two to four sentences per paragraph.
- Numbered sequences for steps, never run-on prose.
- Sentence case headings that answer a question rather than label a topic.
- Never skip heading levels. No H1 in the body; the title comes from frontmatter.

### Constructions to avoid

These read as machine-written. Rewrite as a plain statement.

- Antithesis. "The hard part is not writing it. It is knowing what it touches."
  Also "not just X, but Y" and "X rather than Y" used for emphasis.
- Em-dash appositives that exist for cadence. "The services three hops downstream —
  the one reading a column you are about to rename, the one consuming an event whose
  shape you are about to change — are where incidents come from."
- Aphoristic closers. "A model of your architecture is only useful if you agree with it."
- Commentary on your own writing. "worth stating plainly", "which matters more than it
  sounds", "it's worth noting that".
- Vague personification. "work nobody flagged", "changes the team didn't catch".
  Name the mechanism: "Projects start with an incomplete list of the applications they
  need to touch."
- Triads for rhythm. "faster, safer, and more predictable."
- Filler and self-praise. "simply", "just", "seamless", "powerful", "robust".
- Editorializing. Document function, not impressiveness.

### Content

- Open with the reader's problem in concrete terms, then what Lightbase does about it.
- A positioning sentence names the category and the concrete capabilities together.
- Prefer an example to a characterization. Name real endpoints, tables, and topics.
- State limits. Distinguish what is parsed exactly (routes, cross-application calls,
  data access) from what is proposed heuristically (application boundaries, business
  entities).
- Document just enough for the reader to succeed.
- Check for a keyword repeating across adjacent sentences. Reach for the specific word:
  edit, rename, migration, rather than "change" four times.
- Compare against distributed tracing, not against static analysis. Lightbase is a
  static analyzer, so "unlike static analysis tools" disowns our own approach. Tracing
  shows which applications called each other in the observed window. Lightbase reports
  the paths present in the code, attached to the business operations that trigger them.

## Page types

Every page is one of four types. Mixing them on one page makes it hard to use and hard
to maintain.

| Type | Purpose | Our pages |
| --- | --- | --- |
| How-to | Reader has a task | `getting-started/*`, `data-curation/*` |
| Explanation | Reader wants to understand | `index`, `architecture/*`, `security/*` |
| Reference | Reader is looking something up | `architecture/languages`, `mcp/*` |
| Tutorial | Reader is learning by doing | none yet |

### How-to pages

Prerequisites, then action-oriented headings with numbered steps, then verification.

- `<Steps>` for the sequence. One action per step, with a title that names the action.
- `<Tabs>` for mutually exclusive paths. `getting-started/source-control` should have a
  tab per provider (GitHub, GitLab, Bitbucket) rather than three sequential sections.
- `<Tip>` for the mistake readers commonly make at that step.
- `<Warning>` before anything slow, costly, or hard to undo, such as a full reindex.
- `<Accordion>` for troubleshooting, so failure cases don't interrupt the happy path.
- Close with `<Columns>` of `<Card>` links to the next task.

### Explanation pages

Open with a definition, then how it works, then the tradeoffs, then when it applies.

- One diagram near the top. Prefer a Mermaid diagram over a screenshot for anything
  structural: it stays accurate when the product changes and needs no re-export.
- `<Frame>` with a caption for screenshots. One short line naming what the reader is
  looking at. Don't narrate the contents of the image or repeat the labels visible in
  it, and don't restate specifics the image already shows. Detail belongs in the alt
  text, where it serves screen readers.
- `<Accordion>` for per-language or per-framework detail that only some readers need.
- `<Note>` for the boundary of what we resolve exactly versus heuristically. Every
  `architecture/*` page needs one.
- `<Tooltip>` to gloss a term inline the first time it appears.

### Reference pages

Scannable. Tables, consistent field order, short descriptions, no narrative.

- Tables for support matrices. `architecture/languages` should be a language-by-feature
  table, not prose.
- `<ParamField>` and `<ResponseField>` for MCP tool inputs and outputs.
- `<CodeGroup>` for the same configuration across clients (Claude Code, Cursor, VS Code).
- `<Prompt>` for copyable questions readers can paste into their agent. This is the
  right component for the "what can I ask it" content on `mcp/*`.
- Document defaults, limits, and edge cases. Completeness matters more than flow here.

## Media

- Screenshots for UI-heavy workflows where the reader needs visual orientation. Not for
  simple actions, and not for decoration.
- Crop tightly to the relevant element. Tightly cropped screenshots stay accurate
  longer than full-window captures, and media is the most expensive thing in the docs
  to maintain.
- Native resolution or scale down. Never scale up; it introduces blurriness. On a 2x
  display an image needs twice its rendered width in pixels to look sharp.
- PNG for screenshots and diagrams. Compress before committing.
- Descriptive kebab-case filenames.
- Every image needs alt text describing what it shows. Use `alt=""` only for purely
  decorative graphics.
- Avoid screenshots of pages that change often. Prefer a diagram or prose.

## Callouts

- One callout per section at most. A page of callouts flattens the emphasis and the
  reader skips all of them.
- `<Note>` for context, `<Tip>` for advice, `<Warning>` for risk, `<Info>` for a
  neutral aside. Don't use a callout for something that belongs in the paragraph.

## Content boundaries

- Don't document detailed internal working of the indexing process

## High level content outline

- A first high level version of the outline of the sections in the documentation is
  available in the `outline.md` file

## References

The documentation we are writing is aimed at developers to help them understand the
capabilities, high level internal architecture concepts and security considerations they
could be interested in as users of Lightbase. Some references of high quality
documentation from other SaaS products we can use as inspiration are:

- https://www.tinybird.co/docs/forward/quickstarts
- https://www.sketch.com/docs/getting-started/
- https://docs.carto.com/carto-for-agents/carto-for-agents

Think hard to build a good flowing documentation, walking the user through the product
in an intuitive way, with an easy to follow, natural language aimed at a technical
audience.

## Working practice

- Ask for clarification rather than making assumptions.
- You can push back on ideas. Cite sources and explain your reasoning when you do.
- Never use `--no-verify` when committing.
