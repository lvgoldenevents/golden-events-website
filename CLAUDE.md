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

## Site structure (index.html — single self-contained file)
Nav → Hero (animated balloon field + cursor gold-dust trail) → curtain-style
entrance intro animation on load → marquee of service areas → Services (4
cards) → Service Area grid (8 neighborhoods) → Design Studio (interactive
color picker) → Process (4 steps, scroll-animated) → Pricing (3 tiers) →
Gallery (CSS-illustrated tiles, no real photos yet) → Reviews (placeholder
widget slot + fallback testimonial cards) → Instagram (placeholder widget
slot) → FAQ (accordion, matches FAQPage schema) → Booking (Calendly
placeholder) → Footer contact form + Stripe deposit button.

Includes: LocalBusiness + FAQPage JSON-LD schema, hidden AEO answer-first
summary paragraph, semantic structure for AI answer engines.

## Integration status — placeholders that still need real IDs/links
- Formspree form ID (contact form `action` attribute)
- Stripe Payment Link (footer "Pay a Deposit" button)
- Calendly link (`#calendlyEmbed` data-url, plus commented-out widget script)
- Google Reviews embed (EmbedSocial/Taggbox — `#reviews` widget-slot div)
- Instagram feed embed (SnapWidget/Taggbox — Instagram section widget-slot div)
- Real phone/domain in the JSON-LD LocalBusiness schema (currently placeholder)

Swap these in as they're set up — search for `YOUR_FORM_ID`, `your-payment-link`,
`your-handle`, and the widget-slot comments in index.html.

## Deployment
GitHub repo → Netlify (auto-deploy on push) → Cloudflare DNS → Namecheap
domain. Netlify site currently private at
https://golden-events-entertainment.netlify.app — needs to be made public
once ready to go live.

## Accounts already created
- GitHub: lvgoldenevents (repo: golden-events-website)
- Netlify: connected to the GitHub repo
- Google Business Profile: created, category "Balloon artist" / "Event
  planner," service-area business (no public address), verification method
  offered was "Submit a Business Video" — pending as of last check

## Growth plan (for reference — not code work, but informs priorities)
1. **Phase 0**: infra + Google Business Profile + Formspree/Stripe/Calendly/
   review-widget accounts
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
- Single-file HTML site (no build step) — keep it that way unless asked to
  restructure
- Don't add real testimonials/reviews as fact — current ones are clearly
  placeholder copy for the owner to replace with real reviews
- Don't invent pricing beyond what's already set — current tiers are
  placeholders too ($250 / $650 / $1,500 starting) pending the owner's real
  rates
- Respect `prefers-reduced-motion` in any new animation work — the existing
  code already gates all animation behind it
