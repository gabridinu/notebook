---
title: Debugging a broken HTTPS path, from CGNAT to a Helm override
description: The public site timed out. The cause was four layers down, in a duplicate containerPort.
date: 2026-10-05
tags: [networking, traefik, kubernetes]
draft: true
---

<!--
  DRAFT. Visible with `npm run dev`, excluded from production builds.
  Fill in each section from your own notes, then set draft: false and fix the date.
  Keep commands and output real; redact IPs, tokens and hostnames you don't want public.
-->

## The symptom

What did you see? Browser error, curl output, which hostnames failed and which worked.

## Ruling out the ISP: am I behind CGNAT?

How you checked that your WAN IP was public (router WAN address vs. what the internet sees).

## Router NAT rules

What the port forwards looked like and how you tested them from outside.

## Into the cluster

Traefik service, entrypoints, what `kubectl` showed.

## The actual cause: a duplicate containerPort

The Helm values override, the rendered manifest, and why the duplicate broke it.

```yaml
# paste the offending values snippet here
```

## The fix

```yaml
# paste the corrected values here
```

## What I'd check first next time

Two or three lines. This is the part people search for.
