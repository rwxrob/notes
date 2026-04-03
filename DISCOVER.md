# Discover

Prompts to discover new public knowledge repos worth following.
## By Topic Tags

Search GitHub for repos tagged with common PKM/zettelkasten topics:

- Search repos with topic `zettelkasten`
- Search repos with topic `digital-garden`
- Search repos with topic `pkm`
- Search repos with topic `second-brain`
- Search repos with topic `notes`
- Search repos with topic `public-notes`
- Search repos with topic `thoughts`
- Search repos with topic `knowledge`
- Search repos with topic `knowledge-base`
- Search repos with topic `ideas`
- Search repos with topic `keg`
- Search repos with topic `zet`
- Search repos with topic `kb`
## By Repo Name Prefix

Search GitHub for repos using the agreed naming conventions:

- Search repos with `zet-` in name
- Search repos with `keg-` in name
- Search repos with `kb-` in name
- Search repos with `notes` anywhere in name
- Search repos with `dg-` in name
## By Plain Repo Name

Search GitHub for repos with these exact or common names:

- `notes`, `thoughts`, `keg`, `zet`, `kb`, `knowledge`, `ideas`, `braindump`, `roam`, `org`, `gtd`, `denote`, `second-brain`, `memex`
## By Network

Discover repos from people already in the community:

- Search repos owned by users who follow rwxrob
- Search repos owned by users that rwxrob follows
- Search repos starring or forking repos already in `FOLLOWING/REPOS`.
## Filters

When reviewing results, prefer repos that:

- Have recent commits (active)
- Use markdown files as primary content
- Have a clear topic focus
- Include a `DISCOVER.md` or `FOLLOWING.md` (signals intentional PKM system)
- Include an `AGENTS.md` (AI-native)

## At Scale with BigQuery

The GitHub Search API caps at 1000 results per query. To discover across all active repos, use [GH Archive](https://www.gharchive.org/) via Google BigQuery (free up to 1TB/month). Run `FOLLOWING/scan-gharchive` to query last month's push events and write results to `FOLLOWING/gharchive.tsv`.
