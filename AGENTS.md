# Agent Instructions

## General

- Automatically update this AGENTS.md file when new preferences, conventions, or context are established for this repo
- Committing directly to main is okay in this repo

## Commits

- Always use conventional commits (e.g. `feat:`, `fix:`, `docs:`, `chore:`)
- Never add `Co-authored-by: Copilot` or any Copilot trailer to commits
- Never add any AI co-authorship trailers to commit messages

## Purpose

This repo is a public knowledge base / zettelkasten. It is part of a broader system for personal knowledge management using Git + Obsidian + agentic AI.

## Structure Conventions

- Always use single long-line paragraphs in markdown (no hard line wraps)
- File names must be the slug version of the first level 1 markdown header (e.g. `# My Great Note` → `my-great-note.md`)
- Multiple knowledge repos are intentional — different repos for different content types (e.g. `zet`, `keg`, `recipes`, `bookmarks`)
- `FOLLOWING/` — git submodules of followed public knowledge repos (see `FOLLOWING/REPOS`)
- `DISCOVER.md` — discovery prompts/search terms to find new repos to potentially subscribe to

## Repo Naming Conventions

Repo name prefix signals the format/style of the knowledge base:

- `zet-*` — strict atomic zettelkasten (one idea per file)
- `keg-*` — keg format (structured, KEG spec)
- `kb-*` — knowledge base (reference/topic pages, multi-idea files)
- `notes-*` — freeform general notes
- `dg-*` — digital garden (public, evolving)

The prefix encodes **format**, GitHub topic tags encode **domain** (e.g. `health`, `tech`, `cooking`).



- Use GitHub topic tags for discoverability: `zettelkasten`, `pkm`, `keg`, `public-notes`, `second-brain`, `digital-garden`, `knowledge-base`
- Repo name conventions to search: `zet`, `keg`, `notes`, `knowledge`, `thoughts`
- `DISCOVER.md` contains prompts for agentic AI to run discovery searches
- `FOLLOWING/REPOS` contains committed subscriptions with notes on why each is followed

## Tooling

- Obsidian points at this repo locally for graph view, backlinks, canvas
- Agentic AI used for search, synthesis, linking, and writing assistance across notes
- Git provides version control and sync
