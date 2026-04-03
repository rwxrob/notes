# Following

This directory contains public knowledge repos followed as git submodules (which are not automatically cloned by default.)
## Structure

REPOS contains one repo URL per line.  Submodule paths mirror the full URL of the repo, relative to this directory. For example, `https://github.com/rwxrob/notes-health` is cloned into `github.com/rwxrob/notes-health`.

This convention supports repos from any git host (GitHub, GitLab, Gitea, etc.).
## Submodule Commands

To fetch all submodules after cloning this repo:

```sh
git submodule update --init --recursive
```

To update all submodules to their latest commits:

```sh
git submodule update --remote --merge
```
