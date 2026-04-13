# Getting Started with Your LLM Wiki

You now have a complete LLM Wiki setup following Andrej Karpathy's pattern. Here's what's been created:

---

## 📁 Directory Structure

```
.
├── raw/                    # Raw sources (immutable)
│   ├── articles/           # Articles & blog posts
│   ├── papers/             # Academic papers
│   ├── books/              # Books & chapters
│   ├── videos/             # Transcripts & notes
│   ├── notes/              # Misc notes
│   ├── assets/             # Images & data
│   └── karpathy-llmwiki-pattern.md  # Your first source!
│
├── wiki/                   # LLM-generated knowledge base
│   ├── entities/           # People, orgs, systems
│   ├── concepts/           # Ideas, methods, theories
│   ├── topics/             # Higher-level areas
│   ├── summaries/          # One-source summaries
│   ├── analyses/           # Multi-source syntheses
│   ├── sources/            # Source metadata
│   ├── index.md            # Content catalog (updated on ingest)
│   └── log.md              # Activity log (append-only)
│
├── templates/              # Page templates
│   ├── entity-template.md
│   ├── concept-template.md
│   ├── topic-template.md
│   ├── summary-template.md
│   ├── analysis-template.md
│   ├── source-template.md
│   └── README.md
│
├── llmwiki.md              # Original pattern document
├── CLAUDE.md               # Schema & operations guide
├── GETTING_STARTED.md      # This file
└── README.md               # Your original vault README
```

---

## 🚀 Quick Start: Ingest Your First Source

Your first source is already in place: `raw/articles/karpathy-llmwiki-pattern.md`

To begin ingesting it, say to Claude Code:

> "Please ingest the first source: `raw/articles/karpathy-llmwiki-pattern.md`. Follow the ingest workflow from CLAUDE.md § 6.1."

I will then:

1. **Read & discuss** — Share key takeaways with you
2. **Create entity pages** — E.g., Andrej Karpathy, Obsidian, RAG systems
3. **Create concept pages** — E.g., semantic-search, wiki-cross-referencing, knowledge-compilation
4. **Create summary page** — Concise overview of the source
5. **Create analysis page** (optional) — Synthesis or comparison
6. **Update index.md** — Add all new pages with metadata
7. **Append to log.md** — Record the ingest event
8. **Show you the diffs** — Review what changed

---

## 📖 Key Files to Read

1. **CLAUDE.md** — The schema that governs how I maintain your wiki
   - Read fully before we start ingesting sources
   - This is the "constitution" of your wiki
   - Feel free to update it as you learn what works for you

2. **wiki/index.md** — The content catalog
   - This is your map of the wiki
   - Updated after every ingest
   - Use it to find pages when answering questions

3. **wiki/log.md** — The activity log
   - Append-only record of everything that happens
   - Helps me understand recent activity
   - Parseable with `grep` for CLI-savvy users

4. **templates/README.md** — How to use the templates
   - Templates are guides, not rigid rules
   - Customize as needed for your domain

---

## 🎯 Three Core Operations

### 1. **Ingest** — Add new sources
```
You: "Ingest raw/articles/[filename]. Let's discuss it."
Claude: Reads source → discusses takeaways → creates/updates 5-15 wiki pages → updates index/log
```

### 2. **Query** — Ask questions
```
You: "What's the relationship between X and Y?"
Claude: Searches wiki → synthesizes answer with citations → optionally files new analysis page
```

### 3. **Lint** — Maintain wiki health
```
You: "Lint the wiki."
Claude: Finds orphans, contradictions, staleness → generates report with suggestions
```

---

## 💡 Philosophy

- **You curate sources.** The LLM maintains the wiki.
- **The wiki is the artifact.** Chat history is ephemeral.
- **Knowledge compounds over time.** Each source updates 5-15 pages; each query can file new analysis.
- **Cross-references are valuable.** The LLM maintains them; you benefit from the connections.

---

## 🔗 Obsidian Integration

- **Graph View** (Cmd+Shift+G): See how your wiki connects
- **Backlinks** (Ctrl+Alt+L): Find all pages linking to current page
- **Quick Open** (Cmd+P): Jump to any page by name
- **Search** (Ctrl+Shift+F): Find pages by content
- **Wikilinks** (`[[page]]`): Click to navigate

---

## 🎨 Optional Enhancements

- **Dataview Plugin**: Query pages by frontmatter (e.g., "show all pages with 5+ sources")
- **Marp Plugin**: Convert wiki pages to slide decks
- **Local Search** ([qmd](https://github.com/tobi/qmd)): Full-text search with vector re-ranking
- **Git**: Your wiki is a git repo; you get version history free

---

## ✅ Next Steps

1. **Read CLAUDE.md fully** — Understand the schema and operations
2. **Review the templates** — See the page types you'll be creating
3. **Tell me to ingest the first source** — Start building the wiki
4. **Browse the wiki as pages are created** — See the connections form in graph view
5. **After 3-5 ingests, ask for a lint pass** — Keep the wiki healthy

---

## ❓ Questions?

- **"What should the schema be for my domain?"** → Let's evolve CLAUDE.md together based on what you need
- **"Can I add more source types?"** → Yes, add them to `raw/` and describe them; I'll handle the wiki updates
- **"How often should I lint?"** → Monthly is good; more frequently if the wiki is growing fast
- **"Should I manually edit wiki pages?"** → You can, but I prefer to do the editing; tell me what you'd like changed and I'll update it

---

## 🎓 Further Reading

- **Original concept**: Andrej Karpathy's gist (which you now have in `raw/articles/`)
- **Related**: Vannevar Bush's Memex (1945) — Bush's vision of associative trails between documents
- **Related**: Personal knowledge management systems (Obsidian, Roam, Logseq)

---

You're ready to build. Let's start ingesting.
