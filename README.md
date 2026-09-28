# notebook

Source for [gabrieldinu.co.uk](https://gabrieldinu.co.uk): lab notes, the lab page, uses and now.
The CV lives separately at [cv.gabrieldinu.co.uk](https://cv.gabrieldinu.co.uk).

## Local development

```sh
npm install
npm run dev        # http://localhost:4321, drafts visible
npm run build      # type-check + production build into dist/ (drafts excluded)
```

## Writing a note

Add a Markdown file to `src/content/notes/`. The file name becomes the URL
(`my-note.md` → `/notes/my-note/`).

```md
---
title: Short, specific title
description: One sentence shown in lists, RSS and search results.
date: 2026-10-05
tags: [kubernetes, traefik]
draft: true        # remove or set false to publish
---
```

Pages outside the notes (`lab`, `uses`, `now`) are in `src/pages/`; their content is at the top
of each file.

## How it deploys

1. Push to `main`.
2. `.github/workflows/build-deploy.yml` builds the image and pushes
   `ghcr.io/gabridinu/notebook:sha-<commit>` and `:latest`.
3. The `deploy` job sets that tag in `gabridinu/homelab` →
   `apps/notebook/manifests/kustomization.yaml` and commits it.
4. Argo CD syncs the `notebook` Application.

Pull requests run the build only; nothing is pushed or deployed.

**Rollback:** in the homelab repo, set `newTag` back to an earlier `sha-xxxxxxx` and commit.

## One-time setup

- Repository secret `HOMELAB_TOKEN`: a fine-grained personal access token with
  **Contents: read and write** on `gabridinu/homelab` only.
- After the first image is pushed, either make the GHCR package `notebook` public, or give the
  deployment an `imagePullSecrets` entry.
