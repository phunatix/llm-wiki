# Quartz publishing for the LLM Wiki

This folder is a [Quartz v4](https://quartz.jzhao.xyz) site that publishes `wiki/`
(in the repo root) as a static website with backlinks, graph view, and search.

## Local preview

```bash
cd quartz
npm install
npm run serve     # http://localhost:8080, hot reload on changes in ../wiki
```

## Build only

```bash
npm run build     # output goes to quartz/public/
```

Both scripts pass `-d ../wiki` so Quartz reads content from the repo's `wiki/`
folder instead of the default `quartz/content/`. Only `wiki/` is published —
`raw/`, `Clippings/`, `templates/`, `copilot/`, and `.claude*/` are outside
the content root and never seen by the build.

## Configuration

- `quartz.config.ts` — site title, `baseUrl`, `ignorePatterns`, theme
- `quartz.layout.ts` — page layout (sidebar, footer, components)

**Before the first deploy**, set `baseUrl` in `quartz.config.ts` to your final
URL (e.g. `olaf-ngo.github.io/llm-wiki` or a custom domain).

`log.md` is excluded via `ignorePatterns` since it's an internal change log,
not user-facing content. Adjust the list to taste.

## Deploy (GitHub Pages)

The repo's primary remote is Gitea. To publish to GitHub Pages:

1. Create a GitHub repo (e.g. `olaf-ngo/llm-wiki`) and add it as a second remote:
   ```bash
   git remote add github git@github.com:<user>/llm-wiki.git
   git push github main
   ```
2. In the GitHub repo: **Settings → Pages → Source: GitHub Actions**.
3. Push to `main` — `.github/workflows/deploy.yml` builds Quartz and deploys.

The workflow runs `npm ci && npx quartz build -d ../wiki` from `quartz/` and
uploads `quartz/public/` as the Pages artifact.

## Compatibility notes for this vault

- **Wikilinks** (`[[concepts/golden-paths]]`) — handled natively by Quartz's
  `ObsidianFlavoredMarkdown` transformer. Resolution mode is `shortest`,
  so `[[golden-paths]]` works too.
- **Frontmatter `related_pages`** — Quartz reads frontmatter but does not
  render arbitrary wikilink lists. The page body's wikilinks drive the graph
  view and backlinks. If you want `related_pages` to render visibly, surface
  them in the page body or write a small layout component.
- **Mixed-case filenames** (`entities/Apple.md`) — Quartz slugifies, so URLs
  end up lowercase regardless. Internal wikilinks resolve case-insensitively.
- **Drafts** — set `draft: true` in frontmatter to exclude a page from build.

## Updating Quartz

This is a vendored copy (no upstream `.git`). To pull in upstream changes:

```bash
cd /tmp && git clone --depth 1 https://github.com/jackyzha0/quartz.git
# diff /tmp/quartz against this folder; copy over what you want,
# preserving quartz.config.ts and package.json script changes.
```
