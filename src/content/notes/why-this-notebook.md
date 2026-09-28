---
title: Why this notebook exists
description: My CV lists what I can do. This site is where I show the working.
date: 2026-09-28
tags: [meta, gitops]
---

For twelve years my job has been fixing things in retail estates: POS terminals, self-checkouts,
the servers behind them, and the rollouts that change all of them at once. Most of what I've
learned doing that lives in tickets, runbooks and my own head. None of it is visible to anyone
reading a CV.

So this is where I write it down. Each note is a real problem from work or from my homelab,
with what I tried, what actually fixed it, and what I'd do differently. Work notes keep the
technique and leave out customer details.

## How this site is built

The site is plain [Astro](https://astro.build), written in Markdown and kept in a GitHub
repository. When I push:

1. GitHub Actions builds a container image and pushes it to GHCR, tagged with the commit SHA.
2. The same workflow commits the new tag to my homelab repository.
3. Argo CD notices the change and rolls it out to my k3s cluster.

No step involves me logging into a server. The [lab page](/lab/) covers the rest of the stack.

## What's coming

- Tracing a broken public HTTPS path from CGNAT checks down to a Traefik Helm override.
- Moving a k3s node from bare metal to a VM without losing the GitOps state.
- Why Argo CD won't redeploy a `:latest` image, and how SHA tags fix it.
