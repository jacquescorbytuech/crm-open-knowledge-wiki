---
type: Channel
title: Direct Mail
description: How to run a physical channel that lands intact: choose a format by segment value, make each piece trackable back to the CRM, validate addresses against decay, and measure by holdout and match-back.
tags: [channel, direct-mail, physical, retention, control-group, variable-data, match-back]
timestamp: 2026-06-14T00:00:00Z
---

## What it is

Direct mail is a physical piece delivered to a postal address: a postcard, a letter, a catalogue, a dimensional package. It has seen renewed interest in direct-to-consumer marketing precisely because the message arrives whole, with no model in the pipe to summarise, rank, or suppress it, on a surface the recipient handles directly.

## Permission and reach

Postal marketing operates under a lighter consent regime than electronic channels in most jurisdictions, though data protection law still governs how the address was obtained and used. Reach depends on holding a deliverable postal address, which is a different and often staler data point than an email or phone number.

## Filtering and editing

None, and this is the point. Nothing ranks, bundles, summarises, or filters a physical piece. It lands on a surface the recipient handles directly. The trade is that it is the slowest channel and the most expensive per touch by a wide margin.

## Technical specifics

The format constrains the cost, the lead time, and the cut-through, and the choices are concrete.

* **Formats.** Postcards (cheapest, no envelope to open), letters, flats and large envelopes, catalogues, and dimensional packages that trade cost for cut-through. The cost ladder runs postcard, then letter, then dimensional, climbing steeply; the lead time runs to weeks, not minutes, because everything is printed, finished, and physically transported.
* **Postal class.** In the US, bulk promotional mail goes as USPS Marketing Mail, which is bulk-only: a mailing must meet a minimum of 200 pieces or 50 pounds, so there is no economical single-piece send.
* **Variable-data printing.** Variable-data printing personalises copy, imagery, and offers per recipient from the customer record, the physical analogue of merge tags and dynamic content. Drive it from the same fields the rest of the programme uses, name, last product, lapsed segment, tier, so the piece carries the relevance the digital channels do rather than a generic mailshot.
* **Bridging to digital.** A QR code, personalised URL (PURL), or unique promo code per recipient connects the physical piece to a trackable digital response. The mechanics matter: mint a unique value per recipient, not one shared code for the whole drop, and stamp it on the CRM record before the file goes to the printer. A per-recipient QR or PURL resolves to a landing page that records who scanned; a per-recipient promo code redeems against that one customer. Shared codes tell you the drop worked; unique codes tell you which recipient acted, which is what match-back needs.

## Format decision rule

Pick the format from the value of the segment and the job, because the per-piece cost climbs fast and only high-value work earns the dimensional end.

* **Postcard** for volume reactivation and offer drops to mid-value segments: cheapest, lands face-up with no envelope to open, carries one offer and one code.
* **Letter** for recognition, winback copy that needs length, or anything where an envelope and a personalised letter raise the perceived value: more expensive, but it reads as addressed-to-you rather than a flyer.
* **Dimensional package** only for the top tier where the lifetime value of recovering or retaining the account dwarfs the piece cost: high-value winback, top-customer recognition, premium acquisition into a saturated inbox. Reserve the spend for segments where the expected incremental return clears the steep cost.

The rule of thumb: match the unit cost of the piece to the value at stake in the segment, and never send the dimensional package to a list the postcard would have served.

## Address hygiene

The address is the staler data point and it decays continuously as people move, so a drop runs through a hygiene step before it goes to print.

* **Validate and standardise** every address against a postal reference (in the US, CASS-certified processing) so it is deliverable and in the postal format the class requires.
* **Apply move data** where available to catch recipients who have relocated.
* **Dedup** the file so one household or one customer does not get two pieces.
* **Expect and budget for decay.** A share of any list will be undeliverable however clean the source, and on a physical channel that is a postal-returns cost paid after print, not a free bounce. Treat it as a line in the cost of the drop, not a surprise.

Validate before the file leaves for the printer, because nothing about the piece can change once it is printed and posted.

## Best-fit jobs

High value retention and reactivation moments where the cost is justified: top tier customer recognition, winback of lapsed high value accounts, milestone and loyalty gestures, and premium acquisition where a physical piece cuts through a saturated inbox. It is a scalpel, not a broadcast tool.

## Constraints

Cost per piece is orders of magnitude above email, lead times are measured in days or weeks, and creative cannot be changed once printed and posted. Address data decays, so list hygiene is a postal returns problem rather than a bounce problem.

## Measurement

There is no open or click, so measurement is by holdout and match-back, and the channel is one of the more honestly measured because incrementality is built into how it has always been run.

The how-to, in order:

1. **Hold out a randomised control.** Before the drop, randomly split the eligible audience into a treated group that gets mailed and a control group that does not. Randomise at the individual or household level so the two arms are otherwise identical. Size the control so the expected lift clears the noise. See [holdouts and control groups](/measurement/holdouts-and-control-groups.md).
2. **Mail the treated group** with a unique per-recipient code, QR, or PURL stamped on each record, so a response can be traced to the individual who acted.
3. **Match responders back over a defined window.** Pick a window long enough to capture the physical channel's slow response, then attribute conversions to the mailed file by the unique code first, and by name and address match where a code was not used. Match-back is how a physical piece with no click gets connected to a downstream order.
4. **Read incrementality, not gross response.** Compare conversion in the treated group against the held-out control: the difference is the incremental effect of the mailing, not the raw number of responders, many of whom would have converted anyway. The arithmetic and the worked read are in [uplift and incrementality](/measurement/uplift-and-incrementality.md).

Match-back alone counts responses; the holdout is what turns that count into a causal lift. Run both. See also [attribution](/measurement/attribution.md).

## Production-readiness checklist

Run this before committing a drop, because there is no post-print fix. Frame the timeline in weeks, not minutes, and build the lead time in.

* **Artwork** final and proofed, with the variable-data fields and the per-recipient code, QR, or PURL placed and tested on the layout.
* **Data file** pulled, with the segment defined, variable fields populated, and the file deduped to one piece per household or customer.
* **Address validation** run: standardised, move-updated, undeliverables removed, decay budgeted.
* **Control group** split out and recorded, with the unique codes minted and written back to the CRM.
* **Seed and proof.** Send a physical proof and seed a few internal addresses in the live drop to confirm print, finishing, and the scan-to-landing-page path actually work end to end.
* **Postal class** chosen and the mailing checked against its rules (for USPS Marketing Mail, the 200-piece or 50-pound minimum).

## Lifecycle role

A premium, low frequency complement to the digital channels, reserved for moments that earn the spend. It owns the high value end of retention that the cheap channels handle poorly.

## Related

* [The channel mix](/channels/index.md)
* [Personalisation mechanics](/foundations/personalisation-mechanics.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)
* [Uplift and incrementality](/measurement/uplift-and-incrementality.md)
* [Retention and LTV](/measurement/retention-and-ltv.md)
* [Loyalty and retention programs](/foundations/loyalty-and-retention-programs.md)

## Citations

[1] [USPS, Marketing Mail (formats and 200-piece / 50-pound minimum)](https://pe.usps.com/businessmail101?ViewName=StandardMail)
[2] [Poplar, direct mail attribution (match-back and control-group lift)](https://heypoplar.com/articles/a-complete-guide-to-direct-mail-attribution)
