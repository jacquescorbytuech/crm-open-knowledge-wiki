---
type: Reference
title: About This Bundle
description: What the Open Knowledge Format is, where this bundle's content comes from, and how to navigate it.
resource: https://github.com/GoogleCloudPlatform/knowledge-catalog/tree/main/okf
tags: [meta, okf, provenance]
generated:
  by: human:jacquescorbytuech
  at: 2026-08-20T00:00:00Z
sources:
  - id: okf-intro-blog
    resource: https://cloud.google.com/blog/products/data-analytics/how-the-open-knowledge-format-can-improve-data-sharing
    title: "Introducing the Open Knowledge Format"
  - id: okf-spec
    resource: https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md
    title: "OKF v0.2 specification"
  - id: okf-v02-announcement
    resource: https://cloud.google.com/blog/products/data-analytics/okf-v0-2-adds-trust-signals
    title: "OKF v0.2 adds trust signals"
---

## What this is

This is a knowledge bundle in Open Knowledge Format (OKF) v0.2, an open, vendor neutral specification published by Google Cloud: v0.1 in June 2026, and v0.2 in July 2026, which added the provenance and trust fields this bundle now uses. OKF represents knowledge as a directory of markdown files with YAML frontmatter. Every file is a concept. The file path is the concept identity. Concepts link to each other with ordinary markdown links, which turns the directory into a graph. There is no required tooling: if you can read a markdown file, you can read this bundle, and if you can clone a git repository, you can ship it.

## Conformance

Every concept file carries a frontmatter block with a required `type` field, and usually `title`, `description`, and `tags`. Provenance and freshness use the v0.2 trust fields. `generated` records who produced the content and when, with the spec's actor convention: agents as `producer/version`, humans as `human:<id>`. `sources` lists the external material a concept draws on, each entry carrying an `id`, a `resource` URL, and a title; where a page attributes individual claims, it uses markdown footnotes whose labels match those `sources` ids. The fast-moving reference concepts also carry a `stale_after` date marking when their external facts are due a re-check. No concept yet carries a `verified` record, so under the spec's derived trust tiers the bundle reads as unverified; a human review would be recorded as `verified: { by: human:<id>, at: <date> }`. The reserved filenames `index.md` (a directory listing for progressive disclosure) and `log.md` (a chronological change history) appear at the bundle root and in some subdirectories. Cross links are bundle relative, beginning with a slash.

> [!note] Broken links are intentional
> Broken links are permitted by the spec and simply mark knowledge not yet written.

## Where the content comes from

This is a general practitioner reference for email, lifecycle and CRM marketing, synthesised from authoritative sources rather than copied from any single one:

* Standards and regulators for the mechanics and the law: the IETF RFCs, Apple and Google platform documentation, and the FTC, ICO, and FCC.
* Recognised industry and research sources for the practice: deliverability, design, benchmark, and measurement references such as Litmus, Campaign Monitor, Klaviyo, HubSpot, Baymard, Word to the Wise, and the academic literature on extraction, bandits, and uplift.
* The platform behaviours, research, and regulations these draw on are mirrored into [references](/references/) as first-class concepts, with the specific sources cited in each concept.

## How to navigate

The bundle is organised around the work: the [principles](/principles/) that set the stances, the [foundations](/foundations/) that hold the cross-channel operations (data, segmentation, lifecycle, content, automation, tooling), the [channels](/channels/) you send through, and the [measurement](/measurement/) layer that proves incrementality and sizes experiments. The [references](/references/) hold the external platform behaviour, research, legislation, and a glossary. The [root index](/index.md) maps the lot; start with the layer your question sits in and follow the cross links.
