# Sweet AI Consulting — Site Project Notes

This repo builds and deploys [sweetaiconsulting.com](https://sweetaiconsulting.com) — a Jekyll site on GitHub Pages for a Bay Area AI advisory.

## Project owner

David Hart, Principal. Contact: hello@sweetaiconsulting.com · david.hart@sweetaiconsulting.com · (415) 355-4362.

The advisory offers both AI consulting and MBA-level business consulting capabilities. Site copy may reference the firm's MBA consultant capacity in the abstract; do not name individuals beyond David Hart in published copy without his explicit approval.

## Positioning — read before writing copy

Sweet AI Consulting is Bay Area consulting practice launched in 2026. The narrative is continuity, not novelty, from all of the years of principal David Hart's experience. Audience: SMBs, non-profits, and corporate executives across the East Bay, San Francisco, and the Peninsula, plus selected remote engagements.

The differentiator is **knowing when *not* to use AI**. This is not a tagline to sprinkle — it is the through-line. Most pages should leave the reader with a clearer sense of where AI does and doesn't belong in their business. Pair this with the rare credential — David's 25+ years in AI, including co-founding the OpenCog Foundation — to filter for higher-quality buyers.

Engagement areas the site needs to surface (terms buyers actually search for):

- AI education for owners and management teams
- Competitive landscape reviews
- Readiness assessments and strategic AI roadmaps
- Cost/benefit analysis and right-sizing
- AI tool selection and vendor evaluation
- Acceptable-use policies and staff training
- Executive and management AI workshops
- Cybersecurity assessments tied to AI deployments
- Data-privacy work and CCPA/GDPR compliance
- AI pilot trials with defined success criteria
- Ethical-practice frameworks for AI deployment

First consultation is complimentary. Surface this where it earns its place; don't lead with it.

## Voice

Advisory and grounded. Not breathless, not credulous, not jargon-laden. Closer to a senior practitioner explaining a tradeoff to a peer than to a vendor pitching a product. Concrete over abstract. Specific over generic. Honest about limits — including AI's. Plain English; if a term needs explaining, explain it once and move on.

Avoid: "leverage cutting-edge," "harness the power of," "transform your business," "AI-powered everything," anything that sounds like it could appear on every other AI consultancy site.

## Design

Defer to the `frontend-design` plugin (installed from `anthropics/claude-plugins-official`) for component patterns, layout, and styling craft. Invoke `/frontend-design` explicitly when starting visual work, or expect it to auto-invoke for component or styling requests.

Project-specific overrides on top of the plugin's defaults:

- **Single source of truth for tokens.** Color, typography, and spacing live in `_sass/_tokens.scss` (or equivalent). Don't hardcode values in components.
- **Type and spacing.** Generous. This is an advisory site, not a SaaS landing page; whitespace is part of the credibility signal.
- **Imagery.** Stock images are acceptable when they are *mild, distinctive, and fit the advisory ethos* — understated photography of objects, materials, light, or environments rather than generic AI tropes. Do not use generic "AI brain," blue-circuit, glowing-network, robot-handshake, or hologram-touching imagery. Original diagrams, typographic compositions, and grounded Bay Area context are still preferred where they fit. Empty is better than wrong.
- **Motion.** Subtle. Respect `prefers-reduced-motion`. No autoplay anything.
- **Accessibility.** WCAG AA minimum. One h1 per page. Color-contrast ratios in `_tokens.scss` must explicitly meet 4.5:1 for body text and 3:1 for large text. Focus rings visible by default. Test with keyboard navigation and a screen reader before declaring a page done.
- **Performance.** Static-first. No client-side JS unless a feature genuinely requires it. Lighthouse Performance ≥ 95 on the homepage; ≥ 90 acceptable on content-heavy pages. Core Web Vitals targets: LCP < 2.5s, CLS < 0.1, INP < 200ms. 

## Privacy posture — walk the talk

The advisory's credibility on CCPA/GDPR work depends on the site itself being a model. These rules are non-negotiable:

- **Self-hosted fonts only — or use the system font stack.** No Google Fonts, no Adobe Typekit, no third-party font CDNs. Loading a Google Font leaks visitor IPs to Google and is a real CCPA/GDPR concern.
- **No third-party trackers.** No Google Analytics, Meta Pixel, Hotjar, or similar. If analytics are useful, prefer Plausible (no cookies, no personal data, self-hosted preferred). Skip analytics entirely if not actively useful.
- **No cookies if avoidable.** A cookies-free site needs no cookie banner, which is itself a credibility signal.
- **Privacy Policy page that says what it actually does.** Name the first-party data the site collects (form submissions, server access logs, anything else), the legal basis, and the retention period. No boilerplate.
- **Asset pipeline keeps things first-party.** All CSS, JS, fonts, and images served from the site's own domain. No external CDN includes for libraries unless absolutely required, and if so, with `crossorigin` and SRI hashes.

The site itself becomes a case study for how the advisory works.

## SEO — progressive playbook

SEO is built progressively. Phase 1 is the cheap wins shipped on day one. Phase 2 is content-led, accumulated over months as articles and Services pages mature. Phase 3 is reactive — only undertaken if Phases 1 and 2 plateau.

**Phase 1 — ship at launch:**

- `jekyll-seo-tag` — adds title/description/og/twitter/canonical tags. On the GitHub Pages allowlist; install via `_config.yml`.
- `jekyll-sitemap` — auto-generates `sitemap.xml`. Same source.
- `robots.txt` — permits all, references the sitemap.
- Schema.org structured data in `_includes/schema.html`: `LocalBusiness` + `ProfessionalService` for the home page, with the East Bay / San Francisco / Peninsula service area, contact, and hours. `Person` for David's About page. Embed via JSON-LD.
- One target keyword phrase per page, named in the page front-matter (`seo_target:`), and reflected naturally in the H1, the first 150 words, and the meta description. No keyword stuffing.
- Alt text on every image. Decorative images get `alt=""` rather than omitting.
- Page titles formatted: `{Page} — Sweet AI Consulting` for sub-pages; bare positioning headline on home.

**Phase 1 target keywords (one per page, refine after a quick keyword check at publish):**

- Home: "AI consulting Bay Area"
- Approach: "when not to use AI"
- Services index: "AI strategy consulting"
- Service — AI readiness: "AI readiness assessment"
- Service — vendor evaluation: "AI vendor selection"
- Service — privacy: "CCPA AI compliance" or "GDPR AI compliance"
- Service — cybersecurity: "AI cybersecurity assessment"
- About: "David Hart AI consultant"

**Phase 2 — accumulate over months:**

- Each new article targets a long-tail buyer query. Title and slug encode it.
- Internal linking discipline: every Services page links to at least one relevant article, and vice versa.
- Update Phase 1 page targets as performance data accumulates.
- Backlinks: acquired by content quality and selective guest contribution; never by paid placement, link exchanges, or AI-generated outreach.

**Phase 3 — only if needed:**

- Local citations (Google Business Profile, etc.).
- Service-area landing pages (e.g., "AI consulting Oakland") only if Phases 1 and 2 leave a clear gap.

## Stack and build

- Jekyll, deployed via GitHub Pages.
- `_config.yml` is authoritative for site metadata and plugin config. Don't duplicate values elsewhere.
- Standard structure: `_layouts/`, `_includes/`, `_sass/`, `_data/`, `_posts/`, `_drafts/`, `assets/`, top-level `.md` for pages. Pick top-level pages over a `_pages/` directory; commit to one approach.
- Local preview: `bundle exec jekyll serve --livereload`.
- Before pushing: `bundle exec jekyll build` must succeed without warnings; check the rendered HTML for the page touched; confirm internal links resolve.

**Plugin scope decision:** GitHub Pages allowlist plugins only, or GitHub Actions building Jekyll and deploying to Pages? Both work; the choice limits what's possible later. This decision is deferred to the Jekyll repo's setup conversation — David will work through it with Claude in that environment.

For Liquid, Sass, or Jekyll plugin syntax that may have shifted — use the `context7` plugin (also in `anthropics/claude-plugins-official`) rather than relying on training-data memory.

## Variables and single sources of truth

Anything that appears in more than one place gets a variable. The most common pitfall is time-relative claims drifting against each other.

- `site.years_in_ai`: integer, used as `{{ site.years_in_ai }}+ years in AI`. Update yearly with a calendar reminder.
- `site.contact.email_general`: `hello@sweetaiconsulting.com`
- `site.contact.email_principal`: `david.hart@sweetaiconsulting.com`
- `site.contact.phone`: `(415) 355-4362`
- `site.service_area`: `East Bay, San Francisco, and the Peninsula`
- `site.first_consultation_offer`: `complimentary first hour-long consultation`

Never hardcode any of the above in page copy. The rate card is the internal source-of-truth for pricing and lives outside the public repo. If a public pricing surface is added later, render from `_data/rates.yml` and treat the markdown rate card as the canonical input — do not paraphrase numbers from memory.

## Information architecture

Build out is progressive over weeks. Plan, but don't pre-build pages without content. Navigation order is intentional: **Approach** comes before **Services** so buyers self-qualify by reading the firm's stance before they consider scope.

- **Home** — positioning, primary CTAs (Approach link, contact).
- **Approach** — the "when not to use AI" stance, advisory philosophy, working style. This is the qualifying funnel.
- **Services** — index page plus a page per engagement area as content matures. Each service page: who it's for, what's in scope, what isn't, what an engagement looks like, indicative timeline.
- **About** — David Hart bio. Mirrors the LinkedIn About in voice and substance.
- **Articles** — stubbed for now. Build the `_posts/` collection, the `jekyll-feed` RSS plumbing, dated permalinks, and the article layout, but ship the section *unlinked from primary navigation*, with `noindex` on the empty index page and excluded from the sitemap, until the first article is published. Drafts live in `_drafts/`. David approves each article before promotion to `_posts/`.
- **Contact** — email, phone, complimentary first-consultation note, service-area statement. Keep as-is for now. **TODO (open question for David):** build a bespoke contact form that sends mail via the resend.com account already configured for `sweetaiconsulting.com`. Open sub-questions: (a) where does the form-handling endpoint live — Cloudflare Worker, Netlify function, GitHub Actions on dispatch? (b) bot-protection approach without third-party CAPTCHA (honeypot field plus time-trap is the lightweight default); (c) does the form accept attachments, and if so what size cap?
- **Privacy Policy** — required by the privacy posture above. Link from the footer.

Do not add pages with placeholder content. An absent page is better than a thin one.

## Content rules

- Every claim that could be checked should be checkable. No fabricated client names, logos, case studies, or testimonials. If we don't have a real one yet, the section doesn't ship.
- Time-relative claims (e.g., "25+ years in AI") render from `_config.yml` variables, not hardcoded strings, so a single edit propagates.
- Bay Area service area is a feature. Name neighborhoods and corridors when natural — it signals real local presence.
- Article drafts go through David before publishing. Don't auto-publish.

## Cross-system mirrors

David's LinkedIn About copy is the working source for the site's About copy; site About and LinkedIn About should mirror in voice and substance. When one changes, propose the matching change for the other in the same review cycle.

## Working norms

- Small commits with descriptive messages. Treat the live site as production.
- Branch for non-trivial changes; preview locally before merge.
- Don't introduce dependencies (gems, JS libraries, build tools) without flagging them and the reason.
- When something is genuinely unclear, ask before guessing. The cost of asking is low; the cost of a wrong direction compounds. When ambiguity is value-laden (positioning, voice, brand), default to asking David rather than choosing on grounds of consistency.

## Out of scope for this repo

- Email marketing platforms, CRM integrations, dashboards.
- Client portals or auth.
- LLM-powered features on the live site itself. The advisory's credibility comes from judgment, not from a chatbot in the corner.
  - **Exception:** a static, branching-logic AI-readiness questionnaire — pure form-based scoring with no LLM and no API call — is *not* the chatbot ruled out here. If proposed, it can ship: it's the firm's diagnostic tool rendered as a web artifact, not an AI feature.
