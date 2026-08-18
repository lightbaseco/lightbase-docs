# Lightbase documentation

The source for the Lightbase documentation site, built on [Mintlify](https://mintlify.com)
and deployed to [onboarding.lightbase.co](https://onboarding.lightbase.co).

## Local preview

Install the Mintlify CLI and run it from the repository root, where `docs.json` lives:

```bash
npm i -g mint
mint dev
```

The preview runs at `http://localhost:3000`.

`mint dev` serves the repository straight from disk, so assets resolve differently than
they do in production. Check anything image-related on the deployed site before
considering it done.

## Publishing

Pushing to `main` deploys automatically through the Mintlify GitHub app.

## Layout

| Path | Contents |
| --- | --- |
| `index.mdx` | Introduction page |
| `getting-started/` | Installing Lightbase and indexing repositories |
| `architecture/` | How the analysis works, and what it resolves |
| `mcp/` | The MCP server and its tools |
| `security/` | Analysis processing and code storage |
| `data-curation/` | Refining the model Lightbase builds |
| `docs.json` | Navigation, theme, logo, and navbar configuration |
| `style.css` | Custom CSS, applied on every page |
| `images/` | Screenshots and graphics, with their uncompressed sources |
| `outline.md` | Working outline of the sections still to write |

## Writing

`CLAUDE.md` holds the style guide: voice, sentence and paragraph rules, the
constructions to avoid, which component belongs on which page type, and how to handle
media. `AGENTS.md` points at the same file, so Claude Code, Cursor, and Codex all read
one set of rules. Read it before adding a page.

One rule worth knowing before you touch `style.css`: never reference a repo asset from
`url()` in CSS. Mintlify rewrites image paths it finds in MDX to its CDN and does not
rewrite `url()` inside a stylesheet, so those requests work locally and 403 in
production. Put the image in the MDX as an `<img>` with a class and style it from CSS.
