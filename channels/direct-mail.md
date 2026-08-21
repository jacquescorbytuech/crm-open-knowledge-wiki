---
type: Channel
title: Direct Mail
description: How to run a physical channel that lands intact: choose a format by segment value, make each piece trackable back to the CRM, validate addresses against decay and measure by holdout and match-back.
tags: [channel, direct-mail, physical, retention, control-group, variable-data, match-back]
generated:
  by: human:jacquescorbytuech
  at: 2026-08-20T00:00:00Z
sources:
  - id: usps-marketing-mail-formats-and-200-piece
    resource: https://pe.usps.com/businessmail101?ViewName=StandardMail
    title: "USPS, Marketing Mail (formats and 200-piece / 50-pound minimum)"
  - id: poplar-direct-mail-attribution-match-back-and
    resource: https://heypoplar.com/articles/a-complete-guide-to-direct-mail-attribution
    title: "Poplar, direct mail attribution (match-back and control-group lift)"
---

## What it is

Direct mail is a physical piece delivered to a postal address: a postcard, a letter, a catalogue, a dimensional package. It has seen renewed interest in direct-to-consumer marketing precisely because the message arrives whole, with no model in the delivery path to summarise, rank or suppress it, on a surface the recipient handles directly.

## Permission and reach

Postal marketing operates under a lighter consent regime than electronic channels in most jurisdictions, though data protection law still governs how the address was obtained and used. Reach depends on holding a deliverable postal address, which is a different and often staler data point than an email or phone number.

## Filtering and editing

None. Nothing ranks, bundles, summarises or filters a physical piece; that absence is the channel's main draw. It lands on a surface the recipient handles directly. The trade is that it is the slowest channel and the most expensive per touch short of a staffed call.

## Technical specifics

The format choice sets the cost, the lead time and how likely the piece is to be noticed.

* **Formats.** Postcards (cheapest, no envelope to open), letters, flats and large envelopes, catalogues and dimensional packages that trade cost for a better chance of being opened and noticed. Cost rises steeply from postcard to letter to dimensional; the lead time runs to weeks, not minutes, because everything is printed, finished and physically transported.
* **Postal class.** Bulk promotional classes carry volume minimums. A single piece falls back to the standard letter rate, which rules out an economical one-off send. In the US, USPS Marketing Mail is bulk-only: 200 pieces or 50 pounds minimum. Royal Mail and other national operators set their own minimums and format rules.
* **Variable-data printing.** Variable-data printing personalises copy, imagery and offers per recipient from the customer record, the print equivalent of merge tags and dynamic content. Drive it from the same fields the rest of the programme uses, name, last product, lapsed segment, tier, so the piece is as relevant as the digital channels rather than a generic mailshot.
* **Bridging to digital.** A QR code, personalised URL (PURL) or unique promo code per recipient connects the physical piece to a trackable digital response. The mechanics matter: mint a unique value per recipient rather than one shared code for the whole drop, then stamp it on the CRM record before the file goes to the printer. A per-recipient QR or PURL resolves to a landing page that records who scanned; a per-recipient promo code redeems against that one customer. Shared codes tell you the drop worked; unique codes tell you which recipient acted, which is what match-back needs.

## Format decision rule

Pick the format from the value of the segment and the job, because the per-piece cost climbs fast and only high-value work justifies a dimensional package.

* **Postcard** for volume reactivation and offer drops to mid-value segments: cheapest, lands face-up with no envelope to open, fits one offer and one code.
* **Letter** for recognition, winback copy that needs length or anything where an envelope and a personalised letter raise the perceived value: more expensive, but it reads as addressed-to-you rather than a flyer.
* **Dimensional package** only for the top tier where the lifetime value of recovering or retaining the account dwarfs the piece cost: high-value winback, top-customer recognition, premium acquisition where the digital channels are already saturated. Reserve the spend for segments where the expected incremental return clears the steep cost.

## Address hygiene

Because the address is the staler data point and decays continuously as people move, a drop runs through a hygiene step before it goes to print.

* **Validate and standardise** every address against a postal reference (in the US, CASS-certified processing) so it is deliverable and in the postal format the class requires.
* **Apply move data** where available to catch recipients who have relocated.
* **Dedup** the file so one household or one customer does not get two pieces.
* **Expect and budget for decay.** A share of any list will be undeliverable however clean the source, which on a physical channel means a postal-returns cost paid after print rather than a free bounce. Treat it as a line in the cost of the drop, not a surprise.

Validate before the file leaves for the printer, because nothing about the piece can change once it is printed and posted.

## Best-fit jobs

High value retention and reactivation moments where the cost is justified: top tier customer recognition, winback of lapsed high value accounts, milestone and loyalty gestures and premium acquisition where a physical piece gets attention that a crowded inbox no longer gives. The channel suits a few high value moments rather than broadcast volume.

## Constraints

Cost per piece is orders of magnitude above email; lead times are measured in days or weeks; creative cannot be changed once printed and posted. Because address data decays, list hygiene here is a postal returns problem rather than a bounce problem.

## Measurement

Measurement runs on holdout and match-back, because there is no open or click to read. Incrementality is built into how the channel has always been run, which makes it one of the more honestly measured.

The how-to, in order:

1. **Hold out a randomised control.** Before the drop, randomly split the eligible audience into a treated group that gets mailed and a control group that does not. Randomise at the individual or household level so the two arms are otherwise identical. Size the control so the expected lift clears the noise. See [holdouts and control groups](/measurement/holdouts-and-control-groups.md).
2. **Mail the treated group** with a unique per-recipient code, QR or PURL stamped on each record, so a response can be traced to the individual who acted.
3. **Match responders back over a defined window.** Pick a window long enough to capture the physical channel's slow response, then attribute conversions to the mailed file by the unique code first, falling back to a name and address match where no code was used. Match-back is how a physical piece with no click gets connected to a downstream order.
4. **Read incrementality, not gross response.** Compare conversion in the treated group against the held-out control: the difference is the incremental effect of the mailing, not the raw number of responders, many of whom would have converted anyway. The arithmetic and the worked read are in [uplift and incrementality](/measurement/uplift-and-incrementality.md).

Match-back alone counts responses; the holdout is what turns that count into a causal lift. See also [attribution](/measurement/attribution.md).

## Production-readiness checklist

Run this before committing a drop, because there is no post-print fix. Frame the timeline in weeks rather than minutes so the lead time is built in.

* **Artwork** final and proofed, with the variable-data fields and the per-recipient code, QR or PURL placed and tested on the layout.
* **Data file** pulled, with the segment defined, variable fields populated and the file deduped to one piece per household or customer.
* **Address validation** run: standardised, move-updated, undeliverables removed, decay budgeted.
* **Control group** split out and recorded, with the unique codes minted and written back to the CRM.
* **Seed and proof.** Send a physical proof and seed a few internal addresses in the live drop to confirm print, finishing and the scan-to-landing-page path actually work end to end.
* **Postal class** chosen and the mailing checked against that class's minimums and format rules (in the US, USPS Marketing Mail sets a 200-piece or 50-pound minimum).

## Lifecycle role

A premium, low frequency complement to the digital channels, reserved for moments that justify the spend. It owns the high value end of retention that the cheap channels handle poorly.

## Related

* [The channel mix](/channels/index.md)
* [Personalisation mechanics](/foundations/personalisation-mechanics.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)
* [Uplift and incrementality](/measurement/uplift-and-incrementality.md)
* [Retention and LTV](/measurement/retention-and-ltv.md)
* [Loyalty and retention programs](/foundations/loyalty-and-retention-programs.md)
