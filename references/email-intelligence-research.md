---
type: Reference
title: Email Intelligence Research
description: The Yahoo and Google research and patent lineage behind inbox extraction, classification, action prediction, and summarisation, with citations to the primary papers.
tags: [research, extraction, classification, patents, summarisation, k-anonymity]
generated:
  by: human:jacquescorbytuech
  at: 2026-05-21T00:00:00Z
stale_after: 2027-08-20
sources:
  - id: whittaker-2019-crusher
    resource: https://research.google/pubs/pub48356/
    title: "Whittaker et al., Online Template Induction for Machine-Generated Emails (Crusher), VLDB 2019"
  - id: sheng-2018-juicer
    resource: https://dl.acm.org/doi/10.1145/3219819.3219901
    title: "Sheng et al., Anatomy of a Privacy-Safe Large-Scale Information Extraction System over Email (Juicer), KDD 2018"
  - id: early-2023-spice
    resource: https://doi.org/10.1145/3583780.3615462
    title: "Early, O'Hare and LuVogt, Content-Based Email Classification at Scale (SPICE), CIKM 2023"
---

## The extraction pipeline

Because consumer mail is overwhelmingly templated, providers treat the inbox as data extraction. Messages are clustered into templates by hashing the HTML structure. A k anonymity threshold then determines whether a template is processed at all, which can leave low volume mail invisible to the pipeline. Once a template clears the threshold, field extractors pull structured data for search, assistants, and cards. Google's Crusher system discovers around 1.5 million new templates a week, constantly expanding the corpus of recognised senders.

| System | What it does |
| --- | --- |
| Crusher (Google, VLDB 2019) | Online template induction over machine generated mail; discovers ~1.5M templates weekly. |
| Juicer (Google, KDD 2018) | Privacy safe large scale information extraction over email. |
| RiSER (Google, WWW 2019) | Learns representations for richly structured email, using HTML structure as a feature. |
| SPICE (Yahoo, CIKM 2023) | Labels ~96% of English messages into a 119 class topic, type, and objective taxonomy at delivery time, using only sender and subject. |

The shift from rules to machine learning was explicit: the Gmail team deleted around 45,000 lines of rule code in 2020 moving the pipeline to a learned design.

## Action prediction and ranking

Providers model the action a recipient will take from the envelope alone. With roughly 85% of messages never read and around 89.5% of deletes happening without the message being opened, sender and subject do disproportionate work. Email search has flipped from time ordering to relevance ordering, where user actions like read, reply, and foldering contribute more to rank than sender importance. Apple Mail Priority Messages (Oct 2024) and Gmail AI Inbox (Jan 2026) are this action prediction literature shipped as priority views.

## Layout, summarisation, and profiling

A Google layout aware document encoder patent treats font size, bold, italic, colour, and position as block level features. Bigger, bolder, and higher on the page therefore carries more weight in the representation, which means a model's summary draws disproportionately from headline and CTA blocks. The same research team that built the parser later moved onto LLM summarisation work. A separate Yahoo patent describes classifying the user into a behavioural persona (organizer, minimalist, priority focused, ignorer, unsubscriber, and so on) from inbox characteristics, a profile the brand cannot detect or validate.

## Practical consequences

* Image only emails lose structure, not just text. OCR recovers words but not the DOM, leaving headline, promo code, body, and footer to parse as one flat block.
* Schema markup gives creative freedom back. Consistent structured annotations let a brand vary its visual template without losing parse coverage. Adoption is low, which leaves a less crowded surface.
* Well structured mail becomes a queryable customer record an assistant can cite years later.

## Related

* [Deliverability](/foundations/deliverability.md)
* [Platform interventions](/references/platform-interventions.md)
* [Copywriting](/foundations/copywriting.md)
* [Message design and rendering](/foundations/message-design-and-rendering.md)
