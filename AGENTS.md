# Agent Instructions

## General

- Automatically update this AGENTS.md file when new preferences, conventions, or context are established for this repo
- Committing directly to main is okay in this repo

## Commits

- Always use conventional commits (e.g. `feat:`, `fix:`, `docs:`, `chore:`)
- Never add `Co-authored-by: Copilot` or any Copilot trailer to commits
- Never add any AI co-authorship trailers to commit messages

## Purpose

This repo is a public knowledge base / zettelkasten. It is part of a broader system for personal knowledge management using Git + Copilot + Obsidian.

## Structure Conventions

- Atomic notes in the zettelkasten/keg style
- File names must be the slug version of the first level 1 markdown header (e.g. `# My Great Note` → `my-great-note.md`)
- Multiple knowledge repos are intentional — different repos for different content types (e.g. `zet`, `keg`, `recipes`, `bookmarks`)
- `FOLLOWING.md` — list of actual git submodule subscriptions (other people's public knowledge repos)
- `scan.md` — discovery prompts/search terms to find new repos to potentially subscribe to

## Discovery & Subscriptions

- Use GitHub topic tags for discoverability: `zettelkasten`, `pkm`, `keg`, `public-notes`, `second-brain`, `digital-garden`, `knowledge-base`
- Repo name conventions to search: `zet`, `keg`, `notes`, `knowledge`, `thoughts`
- `scan.md` contains prompts for Copilot to run discovery searches
- `FOLLOWING.md` contains committed subscriptions with notes on why each is followed

## Tooling

- Obsidian points at this repo locally for graph view, backlinks, canvas
- Copilot used for search, synthesis, linking, and writing assistance across notes
- Git provides version control and sync
