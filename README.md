# Email, Lifecycle and CRM Marketing Knowledge Base

A practitioner knowledge base covering email, lifecycle and CRM marketing: the customer data a programme is built on, the channels it sends through, the operations that run it day to day, and the measurement that proves it worked.

It is written as an **Open Knowledge Format (OKF)** bundle, a directory of plain Markdown files, each one a self-contained concept, linked to the others so the whole thing reads as a graph from any entry point. There is no app to run and no database: clone it, open any file, and follow the links.

The bundle is also browsable online at [crmknowledgebase.com](https://crmknowledgebase.com).

## What is OKF?

[Open Knowledge Format](https://cloud.google.com/blog/products/data-analytics/how-the-open-knowledge-format-can-improve-data-sharing) (OKF) is an open, vendor-neutral specification for representing knowledge as a portable bundle of Markdown files with YAML frontmatter. The core ideas:

- **Every file is a concept.** Its path is its identity.
- **Frontmatter carries metadata.** Each concept declares a `type` (Principle, Playbook, Framework, Channel, Method, Reference, …) plus `title`, `description`, `tags`, and a `timestamp`.
- **Links are the structure.** Concepts reference each other with ordinary Markdown links, turning the directory into a navigable graph. Broken links are allowed and simply mark knowledge not yet written.
- **Reserved files.** `index.md` gives a directory a human-readable table of contents; `log.md` records the change history.
- **No required tooling.** If you can read Markdown and clone a git repo, you can read and ship this bundle.

See [`references/about-this-bundle.md`](references/about-this-bundle.md) for the conformance details and where the content comes from.

## How it's organised

Start at [`index.md`](index.md), then follow the layer your question sits in:

- **[`principles/`](principles/)**: the stances every recommendation should serve (list quality, metrics discipline, the welcome window, engagement as deliverability, …).
- **[`foundations/`](foundations/)**: the cross-channel operations: customer data and identity, segmentation and its models, consent, list building, lifecycle mapping, copywriting, message design, automation, offers, loyalty, campaign planning, orchestration, ESP selection, and AI decisioning and personalisation.
- **[`channels/`](channels/)**: the media you send through: email, SMS and RCS, push, in-app, and direct mail, each with its permission, reach, filtering, technical specifics, constraints, and measurement.
- **[`measurement/`](measurement/)**: the metric tree, holdouts and control groups, attribution, retention and LTV, experiment sizing and volume thresholds, frequentist versus Bayesian inference, and uplift and incrementality.
- **[`references/`](references/)**: external platform behaviour, the email-intelligence and notification-decisioning research, legislation and compliance, and a glossary.

## Attribution

Each concept carries a **Citations** section grounded in primary and authoritative sources: standards and RFCs, platform documentation, regulators (FTC, ICO, FCC), and recognised industry and research references. Attribution lives in those Citations sections rather than in a single frontmatter field.

## Community

If you work in this field, the [Email Geeks](https://email.geeks.chat/) community is where a lot of the practitioners behind these sources hang out, a vendor-neutral Slack for email, deliverability, and lifecycle marketing. A good place to ask the questions this bundle doesn't yet answer.

## Contributing

Corrections, sharper explanations, and missing concepts are welcome. The bundle is **vendor-neutral**: cite tools to show how something works, never to sell them, and disclose any relationship you have with a product or vendor you add or cite. See [`CONTRIBUTING.md`](CONTRIBUTING.md) for the conventions and the rules on disclosure and self-promotion.

## License

See [`LICENSE`](LICENSE).
