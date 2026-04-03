# Following

This directory contains public knowledge repos followed as git submodules.

## Structure

Submodule paths mirror the full URL of the repo, relative to this directory.
For example, `https://github.com/rwxrob/notes-health` is cloned into
`FOLLOWING/github.com/rwxrob/notes-health`.

This convention supports repos from any git host (GitHub, GitLab, Gitea, etc.).

## REPOS

`FOLLOWING/REPOS` contains one repo URL per line. The local path is derived
from the URL. Use this file to bulk-clone or update followed repos.

## Submodule Commands

To fetch all submodules after cloning this repo:

```sh
git submodule update --init --recursive
```

To update all submodules to their latest commits:

```sh
git submodule update --remote --merge
```
