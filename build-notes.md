# Build notes: SOL Bathhouse Membership landing page

Built 7 Nov 2026 by Travis with Claude, from the full-landing-page-builder skill (standalone mode) and the direct response copywriting skill. Brief from Travis: a detailed, on brand landing page that sells the Bathhouse Membership at $59.95 a week and shows the complete SOL experience (helicopter, suites, treatments, testimonials, visuals).

## Intake, as settled
- Client: SOL Elements, https://www.solelements.com.au/ (Webflow site; bookings on solelements.try.be).
- Offer: the SOL Bathhouse Membership, $59.95 a week. Only the name and price were given; every other term is an assumption (below).
- Audience and traffic (assumed, not given): product aware. Meta and Instagram ads plus email to past guests, within an hour of Tamborine Mountain, mostly women 30 to 60 and couples (brand folder target customer).
- Mode: standalone. Enrichment: none exists; `enrichment_mode: skipped_prospect` (the client-enrichment skill was not run; the brand-onboarding folder at `../../brand/` stood in as the fact base).
- Form handler: the site's own forms are Webflow managed (platform form, not extractable). The form currently submits to `thanks.html` by GET so the page works end to end offline. Before traffic: swap `action` for a Formspree endpoint, a Webflow form embed, a Zapier or n8n webhook, or point the CTA at a Trybe membership checkout once the product exists on solelements.try.be. Needs a decision.

## Assumptions that must be confirmed before a dollar of traffic (marked ASSUMED in copy.md)
1. The weekly session is valid any day, including weekends and public holidays, at $59.95 with no surcharge.
2. Billing is weekly, and members can pause or cancel with two weeks' notice (no lock in).
3. Sessions do not roll over if missed.
4. 15 percent off full priced treatments and retail (mirrors the current SOL Signature tier at $299 a month).
5. One Bring a Friend pass a month for a new guest (mirrors SOL Signature).
6. Member invitations to ceremonies and events, and early access to new experiences (mirrors SOL Signature and Society).
7. The SOL team contacts the lead within one business day to set up billing and book the first session.
8. Membership is personal and non transferable (matches the current membership wording on the site).
If any of these differ, the price card, the value table, the four use case cards, the FAQ and the form benefits all need the same edit; search the HTML for the phrase.

## Claims
Every factual line traces to `../../brand/products/elemental-bathhouse/claims.md` (numbers in copy.md) or to the site's own pages read on 7 Nov 2026. No therapeutic claims were used. "Australia's first floating bathhouse" was deliberately left out (qualify verdict). Casual prices are the November 2026 booking calendar ($80 Wed and Thu, $95 Mon, Tue and Fri, $115 Sat and Sun).

## Imagery
- Site images (AVIF) converted to JPEG at max 2000px, quality 82, in `images/`. The folder holds more images than the page uses (the full set from the site), 17 MB in all; prune before deploy or keep for variants.
- Six `tmg-june-*.jpg` files and `tmg-hero-145A6320.jpg` are the June 2026 campaign shots served on the Tamborine Mountain Glades SOL page. They look like SOL's own photography; confirm usage rights with the client before paid traffic.
- Press credit for the Urban List set is Timothy Birch; none of those press images are used.
- Hero: `bathhouse-exterior.jpg`. A short vertical video of the fire pit at dusk would convert harder; ask the client for footage.
- Image slots with no file: none. Every section has a real photograph.

## Fonts
Ogg Roman and Gotham Book, Medium and Light are self hosted in `fonts/` (woff2 converted from the TTFs the site serves). They are licensed faces; the client holds the licence. Confirm before deploying on a third party domain.

## Gates
- `check_page.py`: PASS, 0 warnings (assets, self contained, fonts, alt, form, UTM, thanks, meta, placeholders, dashes).
- `copy_sweep.py --locale en-AU`: CLEAN.
- Visual review at 1440 and 375 px via headless Chrome (one tall capture per viewport, cropped). Fixes applied from the review: stronger left to right hero overlay and the building shifted right so the headline reads; larger nav logo; the Best Value badge hidden on phones; one value line removed because it was wrong (a fortnightly visitor paying weekly would pay more than casual), replaced with the 40 week line, which is true.
- Headless capture gotcha: `min-height: 100svh` sections stretch to the full capture height in a tall headless window. Inject `.hero{min-height:880px!important}` for the review only; real browsers are fine.

## What the review changed
- Headline kept (4 U's: urgent 3, unique 3, ultra specific 4, useful 3).
- Scanner test on the H2s: a reader of headings alone gets product, price, proof, offer and action.
- Honest admission under the price card; the "not for you" list carries the pregnancy and adults only compliance.

## Live
https://travistelfer-hub.github.io/sol-bathhouse-membership/ (7 Nov 2026). Repo TravisTelfer-hub/sol-bathhouse-membership, public, Pages serves `main` at root; this folder is the git working tree. Unused images are gitignored (see `.gitignore`); `.nojekyll` present. Redeploy: commit and push on `main`, then run the pages-publish verify gate. The page carries `noindex`. Not password protected; add StatiCrypt via the encryption-setup skill if the client wants it private.

## Next steps
1. Travis or the client confirms the eight assumptions and the form handler.
2. Prune `images/` to the files the page uses (or keep for A/B variants), then publish (pages-publish skill) or hand to Webflow.
3. Collect two real member quotes in month one and swap them into review slots 1 and 5.
4. Test "Reserve My Membership" against "Hold My Week" on the button.
5. If the client supplies dusk footage, add a muted looping hero video with the still as poster.
