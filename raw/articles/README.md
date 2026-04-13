# Raw Articles & Sources

This directory stores immutable raw sources that feed the wiki.

## Current Sources

- **karpathy-llmwiki-pattern.md** — Andrej Karpathy's LLM Wiki pattern document describing the philosophy and architecture of personal knowledge bases maintained with LLM assistance.

## Adding Sources

1. Add new files to this directory (or subdirectories like `papers/`, `videos/`, etc.)
2. Preserve original formatting and citations
3. If downloading from web, use Obsidian Web Clipper for articles or manual downloads for PDFs
4. Add metadata comment at top:
   ```
   <!-- 
   Source: [URL or citation]
   Type: article|paper|book|video|note
   Date: [publication date]
   Author: [Author name]
   -->
   ```
5. Notify Claude Code to ingest when ready

## File Organization

- `articles/` — Blog posts, web articles
- `papers/` — Academic papers, preprints
- `books/` — Book chapters, excerpts
- `videos/` — Video transcripts, notes
- `notes/` — Other curated notes
- `assets/` — Images, data files, supporting materials

## Rules

✓ Read-only for the LLM (the LLM creates summaries and edits in `wiki/`, not here)
✓ Preserve original formatting and citations
✓ Include source URL or DOI
✓ Keep file names descriptive

✗ Never modify these files during wiki maintenance
✗ Don't delete sources (archive if needed)
✗ Don't add unvetted or low-quality sources
