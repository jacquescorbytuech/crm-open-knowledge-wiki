# Contributing

This is a practitioner knowledge base for email, lifecycle and CRM marketing, written as an [Open Knowledge Format](https://cloud.google.com/blog/products/data-analytics/how-the-open-knowledge-format-can-improve-data-sharing) (OKF) bundle: a directory of plain Markdown files, each one a self-contained concept, linked into a graph. Contributions are welcome — fixing an error, sharpening an explanation, adding a missing concept, or grounding a claim in a better source.

Before you start, read [`README.md`](README.md) and [`references/about-this-bundle.md`](references/about-this-bundle.md) so your change fits the format.

## How to contribute

1. **Open an issue first for anything substantial** — a new concept, a structural change, or a claim you want to challenge. Small fixes (typos, broken links, a better citation) can go straight to a pull request.
2. **Fork, branch, and open a pull request.** Describe what changed and why, and include the disclosure called for under [Contribution rules](#contribution-rules) below.
3. **Keep each PR focused.** One concept or one coherent change per PR is easier to review than a sweep across the bundle.

## What a good contribution looks like

Every file is a concept and its path is its identity, so changes follow the bundle's conventions:

- **Frontmatter.** Each concept declares a `type` (Principle, Playbook, Framework, Channel, Method, Reference, …) plus `title`, `description`, `tags`, and a `timestamp`. Match the shape of the files already in the directory you're editing.
- **Links are the structure.** Cross-link related concepts with ordinary Markdown links, bundle-relative and beginning with a slash (`/foundations/lifecycle-mapping.md`). A link to a concept that doesn't exist yet is fine — it marks knowledge not yet written.
- **Ground every claim.** Add or extend the concept's **Citations** section. Sources should be primary or authoritative — standards and RFCs, platform documentation, regulators (FTC, ICO, FCC), or recognised industry and research references — not marketing pages.
- **No fabricated facts.** Do not invent statistics, benchmarks, or citations. Numbers should be genuine conventions (RFC limits, character counts, statutory quiet hours) or be explicitly framed as defaults.
- **House style.** Plain Markdown, prose over bullet-soup where a paragraph reads better, and no em-dashes in concept files (use commas or restructure).
- **Update the reserved files.** If you add or rename a concept, register it in the relevant `index.md`, and add a short entry to [`log.md`](log.md) describing the change and its sourcing.

## Contribution rules

### Vendor neutrality and disclosure

This bundle is **vendor-neutral**. It cites tools and platforms where they illustrate how something works, never to sell them. The single most important rule here:

- **Disclose any interest.** If you have a financial, employment, or other material relationship with a product, vendor, platform, blog, or service that your contribution mentions, cites, or recommends, **say so in the pull request**. Disclosure is not disqualifying; an undisclosed relationship is.
- **No undisclosed self-promotion.** Do not add your own (or your employer's or client's) product, company, blog post, or affiliate link as a citation, recommendation, or example without disclosing the relationship. Submissions that exist mainly to drive traffic or rank a particular vendor will be declined.
- **No link-building.** A contribution made primarily to earn a backlink will be declined, disclosed or not. This is a public, well-linked resource, and "add our URL as a source/reference/further reading" PRs that don't make the content materially better are the most common abuse we reject. To remove the incentive: outbound links to commercial or vendor sites are marked `rel="nofollow"` and carry no SEO value, and we may convert a link to a plain text citation or drop it entirely if it reads as placement rather than evidence.
- **Citations support claims, they don't advertise.** A link earns its place by being the best available source for a specific statement. Links whose main purpose is promotion — SEO backlinks, affiliate URLs, "recommended tool" call-outs — will be removed, disclosed or not.
- **No sponsored rankings or "best tool" lists** that favour a particular vendor. Where the bundle compares options (for example, ESP selection), it describes how to evaluate, not which brand to buy.

When in doubt, over-disclose. A one-line note in the PR — "I work for X; this citation is to their docs because it's the primary source for Y" — is exactly right, and an authoritative first-party source cited honestly is welcome.

### Accuracy and scope

- Keep contributions within the bundle's subject: the customer data a programme is built on, the channels it sends through, the operations that run it, and the measurement that proves it worked.
- Correct errors with a source. "This is wrong" is a useful issue; "this is wrong, here's the RFC" is a useful PR.
- Respect the existing structure. If your idea doesn't fit an existing concept, it's probably a new concept of its own.

### Conduct

Be civil and assume good faith. Critique the content, not the contributor. Maintainers may edit, decline, or revert contributions that don't meet these rules.

## License

By contributing, you agree that your contributions are licensed under the same terms as the rest of the bundle. See [`LICENSE`](LICENSE).
