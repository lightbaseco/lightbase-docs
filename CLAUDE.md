# Documentation project instructions

## About this project

- This is a documentation site built on [Mintlify](https://mintlify.com)
- Pages are MDX files with YAML frontmatter
- Configuration lives in `docs.json`
- Custom CSS lives in `style.css`. Mintlify includes any `.css` file in the content
  directory on every page, so scope rules to a class used by the page that needs them
- Never reference a repo asset from `url()` in CSS. Mintlify rewrites image paths it
  finds in MDX to its CDN, and it does not rewrite `url()` inside a stylesheet, so the
  path resolves against the deployed origin and returns 403. This works under
  `mint dev`, which serves the repo from disk, and fails in production. Put the image
  in the MDX as an `<img>` with a class, and style it from `style.css`
- Use the Mintlify MCP server, `https://mcp.mintlify.com`, to edit content and settings via MCP
- Use the Mintlify docs MCP server, `https://www.mintlify.com/docs/mcp`, to query information about using Mintlify via MCP
- For Mintlify product knowledge (components, configuration, writing standards),
  install the Mintlify skill: `npx skills add https://mintlify.com/docs`

## Terminology

One term per concept. Check an existing page before introducing a new one.

- **service** for a deployable unit of the system. Lightbase's own features are named
  after applications (application detection, application groups), so use "application"
  only on the pages that document those surfaces
- **Indexer**, no article, for the component that analyzes code: "Indexer reads",
  "Indexer identifies". Reserve **Lightbase** for what the company does
- **the model**, not map, graph, or representation, for what indexing produces
- **code flow**, not trace or path, for one execution path through the system
- **entrypoint** for the HTTP route, queue consumer, or CLI command that starts a flow
- **counterparty** for an external entity the code interacts with
- **business entity** for a domain concept mapped to the tables and flows that use it
- **blast radius** for the downstream reach of a change

## Style preferences

The register is technical documentation for architects and engineers at large
organizations. Not friendly, not conversational, not selling. Flat declarative sentences
that state what the system does.

### Voice

- The reader is a developer, engineering manager, or architect. Don't name their role.
- Explanation and reference pages describe the system, not the reader. Use the impersonal
  voice: "the connected repositories", not "your repositories". How-to pages take second
  person, because the reader performs the steps: "Click **Settings**".
- Name the actor doing the work. Indexer reads, resolves, records, reconstructs.
  Reserve "Lightbase" for what the company does, such as a curation pass during rollout.
- Active voice, present tense.
- Define a term where it first appears rather than linking away to its definition.
- Don't name internal surfaces like the UI or dashboard unless a page documents them.
- Bold for UI elements: Click **Settings**.
- Code formatting for file names, commands, paths, and code references.

### Sentences and paragraphs

- 25 words is a ceiling, not a target. Uniform length is what makes prose tick like a
  metronome.
- Vary length and shape. Watch for claim-then-gloss repeating down a paragraph: a short
  assertion, its explanation, another short assertion, its explanation.
- Say the specific thing first. Naming something vague and then clarifying it with a colon
  says everything twice: "reanalyze what changed: the files in new commits" is just
  "reanalyze the files in new commits". A colon that defines a term the page needs is fine.
- Cut the sentence that sets up the real sentence. "Nothing in the source states where a
  service ends, so those boundaries are inferred" is throat-clearing before "in some cases
  this heuristic leads to incorrect boundaries".
- Prefer the concrete instance to the abstraction it illustrates. "Ask which operations
  write to `payment_intents`" beats "questions resolve at the level of a business operation".
- One thought per sentence. Split when the reader has to hold two unrelated ideas at once,
  not merely because the sentence contains commas.
- One to four sentences per paragraph. A single-sentence paragraph is a legitimate beat;
  don't pad to reach three.
- Short declaratives are for emphasis. When every sentence is short, none of them is.
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
  Name the mechanism: "Projects start with an incomplete list of the services they
  need to touch."
- Triads for rhythm. "faster, safer, and more predictable."
- Filler and self-praise. "simply", "just", "seamless", "powerful", "robust".
- Editorializing. Document function, not impressiveness.
- Sentences that explain their own logic. "Because each interaction is recorded against
  the flow, questions resolve at the level of an operation" narrates the connection; two
  plain statements let the reader make it. Watch for because, so, since, therefore, which
  means, and that is what.
- Summarizing what was just described. If a paragraph explains the mechanism, it doesn't
  need a closing sentence naming what the mechanism achieves.
- Narrative setup. Don't walk the reader from the problem to the solution: "Within a
  service, a call names a function. Between services there is no symbol to resolve. The
  caller builds a URL…" is a story nobody asked for. State what the system does.
- Essayistic observations. "A topic name alone is rarely enough", "what matters as much
  as the list". Say what is extracted and what is matched.
- Reassurance and permission. Don't tell the reader how much to trust a section, or that
  they don't need to read it. State the scope of the page and move on.

### Content

- Open with the reader's problem in concrete terms, then what Lightbase does about it.
- A positioning sentence names the category and the concrete capabilities together.
- Prefer an example to a characterization. Name real endpoints, tables, and topics.
- State limits. Distinguish what is parsed exactly (routes, cross-service calls, data
  access) from what is inferred (service boundaries, business entities, counterparty
  names). Don't call inferred values "proposed": the model uses them as they are, and
  curation corrects them when they are wrong. Nothing waits for the reader's approval.
- Document just enough for the reader to succeed. Gateway prefixes, query-string
  handling, and tie-breaking rules are implementation detail. An accordion is for detail
  some readers need, not a place to put detail that didn't earn a place on the page.
- Check for a keyword repeating across adjacent sentences. Reach for the specific word:
  edit, rename, migration, rather than "change" four times.
- Don't build a page around a comparison. State what Lightbase does; a page that keeps
  score against another tool invites the reader to judge us on that tool's home ground.
- When a comparison does earn its place, compare against distributed tracing, not against
  static analysis. Lightbase is a static analyzer, so "unlike static analysis tools"
  disowns our own approach. Tracing shows which services called each other in the observed
  window. Lightbase reports the paths present in the code, attached to the business
  operations that trigger them.
- Against code search and navigation tools, the difference is the boundary. Symbol
  resolution stops at the process edge. A Lightbase flow continues across an HTTP call,
  a queue topic, or a function invocation, into the code that handles it.

## Product framing

- Indexing is one process. Per-repository analysis and cross-repository resolution are
  never presented as separate steps the reader schedules or thinks about.
- Indexing runs daily by default; on every commit is available on request. Not a tier,
  not a different mechanism.
- Database analysis and counterparty resolution are documented as current behavior.

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
- Decorative images still go in the MDX as an `<img>` with `alt=""` and a class, for
  the CDN rewriting reason above. Position and mask them from `style.css`. Mintlify's
  prose styles cap images at the column width, so a decorative image that bleeds past
  the column needs `max-width: none`.
- Check images in production, not only under `mint dev`. The two serve assets
  differently.

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

For the `architecture/*` pages, which document internals rather than usage:

- https://docs.cockroachlabs.com/docs/stable/architecture/overview — layered explanation
  with overview and component tiers so the reader picks their depth. Take the structure,
  not the habit of opening a section with motivation
- https://sourcegraph.com/docs/code-search/code-navigation — precise versus search-based
  navigation as the spine of the page, which is our exact versus proposed distinction
- https://docs.github.com/en/code-security/code-scanning/introduction-to-code-scanning/about-code-scanning-with-codeql
  — names the languages it does not support, which is what makes the coverage claim credible
- https://neon.com/docs/introduction/architecture-overview — one diagram per data path and
  a table mapping user-facing concepts to the internals behind them
- https://docs.temporal.io/temporal — short paragraphs, terms defined at first use, the
  same idea restated with growing precision
- https://docs.datadoghq.com/tracing/services/services_map/ — the incumbent view of a
  service map, and candid about its own limits (sampling, 30-day ageing, complete traces)

Think hard to build a good flowing documentation, walking the user through the product
in an intuitive way, with an easy to follow, natural language aimed at a technical
audience.

## Working practice

- Ask for clarification rather than making assumptions.
- You can push back on ideas. Cite sources and explain your reasoning when you do.
- Never use `--no-verify` when committing.
