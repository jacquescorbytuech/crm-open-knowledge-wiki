# Contributing

This is a practitioner knowledge base for email, lifecycle and CRM marketing, written as an [Open Knowledge Format](https://cloud.google.com/blog/products/data-analytics/how-the-open-knowledge-format-can-improve-data-sharing) (OKF) bundle: a directory of plain Markdown files, each one a self-contained concept, linked into a graph. Contributions are welcome: fixing an error, sharpening an explanation, adding a missing concept, or grounding a claim in a better source.

Before you start, read [`README.md`](README.md) and [`references/about-this-bundle.md`](references/about-this-bundle.md) so your change fits the format. The bundle is also published online at [crmknowledgebase.com](https://crmknowledgebase.com).

## How to contribute

1. **Open an issue first for anything substantial**, a new concept, a structural change, or a claim you want to challenge. Small fixes (typos, broken links, a better citation) can go straight to a pull request.
2. **Fork, branch, and open a pull request.** Describe what changed and why, with the disclosure called for under [Contribution rules](#contribution-rules) below.
3. **Keep each PR focused.** One concept or one coherent change per PR is easier to review than a sweep across the bundle.

## What a good contribution looks like

Because every file is a concept and its path is its identity, changes follow the bundle's conventions:

- **Frontmatter.** Each concept declares a `type` (Principle, Playbook, Framework, Channel, Method, Reference, …) plus `title`, `description`, and `tags`, and records provenance in the OKF v0.2 fields: `generated` (who produced the content and when; agents as `producer/version`, humans as `human:<id>`) and `sources` (each entry an `id`, a `resource` URL, and a title). Match the shape of the files already in the directory you're editing. Update `generated` when you change a page's content.
- **Links are the structure.** Cross-link related concepts with ordinary Markdown links, bundle-relative and beginning with a slash (`/foundations/lifecycle-mapping.md`). A link to a concept that doesn't exist yet is fine: it marks knowledge not yet written.
- **Ground every claim.** Add or extend the concept's frontmatter `sources` list; where you attribute an individual claim in the body, use a Markdown footnote whose label matches the source's `id`. Sources should be primary or authoritative (standards and RFCs, platform documentation, regulators such as the FTC, ICO, FCC, or recognised industry and research references), not marketing pages.
- **No fabricated facts.** Do not invent statistics, benchmarks, or citations. Numbers should be genuine conventions (RFC limits, character counts, statutory quiet hours) or be explicitly framed as defaults.
- **House style.** Plain Markdown, prose over bullet-soup where a paragraph reads better, and no em-dashes in concept files (use commas or restructure).
- **Update the reserved files.** If you add or rename a concept, register it in the relevant `index.md` and add a short entry to [`log.md`](log.md) describing the change and its sourcing.

## Callouts

The bundle is plain Markdown and stays readable as plain Markdown. It is also published through [Quartz](https://quartz.jzhao.xyz/), which renders Obsidian-style callouts: the coloured, icon'd boxes used for warnings, notes, worked examples, and the like. Being pure Markdown, they need no configuration and degrade to ordinary blockquotes anywhere callouts are not supported. GitHub renders a subset (`[!NOTE]`, `[!TIP]`, `[!WARNING]`, `[!IMPORTANT]`, `[!CAUTION]`) natively.

A callout is a blockquote whose first line is `[!type]`, optionally followed by a custom title. Every line of the box, including blank separators, must begin with `>`:

```markdown
> [!warning] Pushing more volume never fixes spam placement
> It deepens it. The engaged core is what you rebuild on, not a bigger send.
```

Omit the title text to use the type's default ("Warning", "Note", and so on). Add a trailing `-` (`[!type]-`) to collapse the box by default, or `+` to make it expandable but open. You can nest callouts with extra `>` and put any Markdown inside.

Use them sparingly. In a dense reference like this one, a callout should lift one sharp, self-contained point out of the prose rather than box a whole paragraph or restate a heading. Most pages need none. Pick the type by meaning:

- **`warning`** (orange) for a genuine gotcha or a "don't do this" the reader is likely to get wrong. This is the most common type here.
- **`danger`** (red) for a hard limit with real consequences: a legal or compliance breach, getting blocked, an irreversible action. Reserve it, because an orange warning is usually enough.
- **`note`** or **`info`** (blue, cyan) for a caveat or piece of context worth pulling out of the flow.
- **`tip`** (green) for an actionable best-practice nudge or a call to action. Because green should mean "do this", do not green-box ordinary statements.
- **`example`** (purple) for a concrete worked example or calculation, wrapping numbers that are already in the page.
- **`bug`** (red), **`question`** (yellow), **`abstract`** (light blue) and the rest are available; see the [Quartz callout list](https://quartz.jzhao.xyz/features/callouts).

Keep titles short and in sentence case. Inside the box, follow the bundle's house style: no em-dashes, no invented facts, and no boxing of tables, the **Related** list, or footnote definitions. A callout should wrap text that already reads as prose elsewhere on the page, not introduce new claims.

> [!tip] Before adding one
> If you are unsure whether a callout helps, leave it as prose. The bundle should read cleanly without any of them.

## Contribution rules

### Vendor neutrality and disclosure

This bundle is **vendor-neutral**. It cites tools and platforms where they illustrate how something works, never to sell them. The single most important rule here:

- **Disclose any interest.** If you have a financial, employment, or other material relationship with a product, vendor, platform, blog, or service that your contribution mentions, cites, or recommends, **say so in the pull request**. Disclosure is not disqualifying; an undisclosed relationship is.
- **No undisclosed self-promotion.** Do not add your own (or your employer's or client's) product, company, blog post, or affiliate link as a citation, recommendation, or example without disclosing the relationship. Submissions that exist mainly to drive traffic or rank a particular vendor will be declined.
- **No link-building.** A contribution made primarily to earn a backlink will be declined, disclosed or not. This is a public, well-linked resource. PRs asking us to "add our URL as a source/reference/further reading" without making the content materially better are the most common abuse we reject. To remove the incentive: outbound links to commercial or vendor sites are marked `rel="nofollow"` and pass no SEO value. Where a link reads as placement rather than evidence, we may convert it to a plain text citation or drop it entirely.
- **Cite to support a claim, not to advertise.** A link should be the best available source for the specific statement it supports. Links whose main purpose is promotion (SEO backlinks, affiliate URLs, "recommended tool" call-outs) will be removed, disclosed or not.
- **No sponsored rankings or "best tool" lists** that favour a particular vendor. Where the bundle compares options (for example, ESP selection), it describes how to evaluate, not which brand to buy.

When in doubt, over-disclose. A one-line note in the PR, such as "I work for X; this citation is to their docs because it's the primary source for Y", is exactly right. An authoritative first-party source cited honestly is welcome.

### Accuracy and scope

- Keep contributions within the bundle's subject: the customer data a programme is built on, the channels it sends through, the operations that run it, and the measurement that proves it worked.
- Correct errors with a source. "This is wrong" is a useful issue; "this is wrong, here's the RFC" is a useful PR.
- Respect the existing structure. If your idea doesn't fit an existing concept, it's probably a new concept of its own.

### Conduct

Be civil and assume good faith. Critique the content, not the contributor. Maintainers may edit, decline, or revert contributions that don't meet these rules.

## License

By contributing, you agree that your contributions are licensed under the same terms as the rest of the bundle. See [`LICENSE`](LICENSE).
