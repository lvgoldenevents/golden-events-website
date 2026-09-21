# Golden Events & Entertainment — Project Context

## The business
Golden Events & Entertainment is a Las Vegas-based luxury balloon and event
decor company — garlands, arches, hotel/suite styling, corporate and grand
opening decor, and custom sculptural installations. No physical storefront;
travels to clients across the entire Las Vegas Valley. Tagline: "Turning
Moments Into Golden Memories."

- Phone: 818-261-2520
- Email: lvgoldenevents@gmail.com
- Instagram: https://www.instagram.com/lasvegasgoldenevents/ (~3,401 followers)
- TikTok: @lvgoldenevents
- Domain: lasvegasgoldenevents.com (DNS on Cloudflare, registered via Namecheap)
- Service area: Las Vegas, Henderson, Summerlin, North Las Vegas, Paradise,
  Spring Valley, Enterprise, Downtown Las Vegas — "the entire Las Vegas Valley"

## Brand / design direction
Black-and-gold luxury aesthetic matching their real balloon work. Fonts:
Fraunces (display/headings) + Sora (body). Signature interactive element:
a "Design Studio" section where clicking color swatches live-recolors an
SVG balloon arch. Premium, animated, "fun Vegas glam" — not corporate.

## Site structure — 10-page static site, no build step
- `index.html` — homepage is **intentionally just the hero + marquee,
  full stop**: Nav → Hero (animated balloon field + cursor gold-dust
  trail) → curtain entrance animation on load → the service-area marquee
  ticker. `body` is a flex column locked to `100dvh` with
  `overflow:hidden`; `.hero` is `flex:1` and `.marquee-wrap` is
  `flex:0 0 auto`, so the marquee always sits at the bottom of that one
  screen and the homepage never scrolls, by design. There's no footer or
  any other section here — reaching anything else means using the nav.
- Nine standalone pages hold everything else, each reached via a clean
  URL (Netlify serves `/slug` from `slug.html` by default, no redirects
  file needed):
  - `services.html`, `areas.html`, `pricing.html`, `reviews.html`,
    `faq.html` — the original content, unchanged, one per page.
  - `gallery.html` — the tile grid **plus** the Instagram/TikTok "Follow
    Along" embeds merged in below it (moved here from the homepage —
    thematically both are "see our real work").
  - `design-studio.html` — the interactive color-picker widget.
  - `how-it-works.html` — the 4-step process.
  - `book.html` — the Calendly placeholder + "DM on Instagram Instead",
    now the destination for every "Get a Quote" button sitewide.
- **Nav bar (top, every page including the homepage) lists 7 pages**:
  Services / Areas / Pricing / Gallery / Reviews / FAQ / How It Works,
  switching to the mobile hamburger menu at the standard
  `max-width:980px`. Design Studio and Book a Consult are deliberately
  NOT in the top nav — a 9-item nav was tried and felt too cluttered —
  they live in the footer-links row instead (present on every non-home
  page) alongside Services/Pricing/Gallery/FAQ/Instagram/TikTok, and in
  the homepage's mobile menu. Every "Get a Quote" button sitewide points
  to `/book`.
- No shared partials/includes (matches the "no build step" constraint) —
  each page duplicates its own nav, footer (incl. the Netlify contact
  form), and CSS/JS. Only `index.html` skips the footer entirely, since
  it has no scrollable area for one to live in.
- `#contact` resolves to that page's own footer contact form. The
  homepage has no `#contact` (no footer) — don't link to
  `index.html#contact` from anywhere.
- LocalBusiness JSON-LD is duplicated in every page's `<head>`. FAQPage
  JSON-LD lives only on `faq.html`, next to the matching visible FAQ text
  (each `faq-item` has a stable `id`, e.g. `faq-cost`, so other pages can
  deep-link to a specific question with `/faq#faq-cost`).
- Hidden AEO answer-first summary paragraph stays homepage-only.
- Each page's CSS/JS only includes what that page actually uses —
  page-specific styles (e.g. `.designer`/`.swatches` on `design-studio.html`,
  `.process`/`.step` on `how-it-works.html`, `.social-embed-*`/`.ig-strip`
  on `gallery.html`) live in a `<style>` block in that page's own `<head>`,
  not in the shared boilerplate. Keep that discipline when adding new
  pages: don't copy component CSS "just in case" a page doesn't use it.
- **Local testing**: a plain static file server (e.g. `ruby -run -e httpd`)
  will 404 on the clean URLs since it doesn't know to try `slug.html` —
  that's a local-server limitation, not a site bug. A small custom
  WEBrick script that mimics Netlify's behavior is the right way to test
  clean URLs locally if that comes up again.

## Integration status — placeholders that still need real IDs/links
- Stripe Payment Link (footer "Pay a Deposit" button, every page — search
  `your-payment-link`)
- Calendly link (`#calendlyEmbed` data-url on `book.html`, plus a
  commented-out widget-script note right above it — search `your-handle`)
- Google Reviews embed (EmbedSocial/Taggbox/OpenWidget — the `.widget-slot`
  div on `reviews.html`)
- A 4th embed in `gallery.html`'s "Fresh off the install" social grid —
  3 TikTok embeds are in, the last slot is reserved for an Instagram post
  (Instagram only exposes its "Embed" option to logged-in viewers, so this
  one needs a manual grab while signed in — see the HTML comment right
  above the grid)

Already done, for reference (not still pending): contact form uses native
Netlify Forms sitewide (no Formspree — same `name="contact"` form on every
page feeds one inbox); TikTok is linked throughout; LocalBusiness schema
has the real domain and intentionally omits phone/email (contact is
form/DM only — see the comment above that schema block if that changes).

## Deployment
GitHub repo (`lvgoldenevents/golden-events-website`) → Netlify (auto-deploy
on push to `main`) → Cloudflare DNS (Bot Fight Mode / WAF / SSL hardening
in progress) → Namecheap domain. Live at https://lasvegasgoldenevents.com.

## Accounts already created
- GitHub: lvgoldenevents (repo: golden-events-website)
- Netlify: connected to the GitHub repo
- Google Business Profile: created, category "Balloon artist" / "Event
  planner," service-area business (no public address), verification method
  offered was "Submit a Business Video" — pending as of last check

## Growth plan (for reference — not code work, but informs priorities)
1. **Phase 0**: infra + Google Business Profile + Stripe/Calendly/
   review-widget accounts (contact form itself is already handled by
   Netlify Forms, no separate signup needed)
2. **Phase 1**: local SEO — directory listings (Yelp, Bing Places,
   WeddingWire, The Knot, Thumbtack, Nextdoor, Facebook), NAP consistency,
   review-collection habit
3. **Phase 2**: content/authority — neighborhood landing pages, vendor
   roundup pitches, planner directory listings
4. **Phase 3**: automation — Instagram DM auto-replies, Calendly self-serve
   booking, Stripe deposits
5. **Phase 4 ideas**: hotel concierge referral relationships, bachelorette/
   proposal planner partnerships, photo-tag signage on installs, QR-code
   review cards, seasonal Vegas-event content calendar, TikTok content,
   referral program

## Working conventions
- Multi-page static site, still no build step — every page is a
  self-contained HTML file (own `<style>`/`<script>`, no shared includes).
  Keep it that way unless asked to restructure again.
- Don't add real testimonials/reviews as fact — current ones are clearly
  placeholder copy for the owner to replace with real reviews
- Don't invent pricing beyond what's already set — current tiers are
  Basic Package ($250), Dream Package ($300), and Golden Package ($500),
  all "starting" prices
- Respect `prefers-reduced-motion` in any new animation work — the existing
  code already gates all animation behind it
- The business intentionally doesn't publish a phone/email on the site —
  contact is by form or Instagram DM only. Don't add visible phone/email
  text without checking first.
