# Japan-Readiness Index

**How ready are foreign developer tools for the Japanese market?**

A live audit of 40 popular foreign dev-tools — API, database, auth, observability, CMS, CI/workflow, BaaS, feature-flag, and infra companies — measured against the surface a Japanese buyer actually hits *before* they can adopt or pay.

*Scanned 2026-06-25 by [greymoth](https://greymoth-jp.github.io/proof-dashboard). Every signal is verifiable against each company's own live site.*

---

## The headline

> **40 tools scanned. None has a 特商法 (Specified Commercial Transactions Act) page. None prices in JPY. Only 3 have a real Japanese-language site.**

The average Japan-Readiness score is **5.6 / 100**, and the highest score any single tool reaches is **60**. Not one foreign dev-tool in this index is fully ready for the Japanese market — and the gaps are almost entirely at the procurement and finance gate, not the engineering one.

| Result | Count |
|---|---|
| Tools scanned | **40** |
| With a 特商法 page | **0** |
| Pricing in JPY (or a JPY toggle) | **0** |
| With a real localized Japanese site | **3** (Auth0, Twilio Segment, HashiCorp) |
| With `hreflang="ja"` for JP search | **2** |
| Scoring exactly 0 | **31** |

This isn't a story about bad products. Every tool here is excellent. It's a story about a **front door** that's closed to Japan — and almost every gap is a static page or a config change, not product work.

---

## Methodology

Each company is scored 0–100 across five independently verifiable signals. The weights reflect where a Japanese deal actually dies — heaviest on the procurement-gate items (特商法, real localization), lighter on the discoverability and finance items.

| Signal | Weight | Why it matters |
|---|---|---|
| **特商法 page** (Specified Commercial Transactions Act) | 25 | Legally expected for any paid online service sold in Japan. Its absence is a hard stop for many corporate procurement/legal teams — the deal dies before engineering is ever evaluated. |
| **Localized Japanese site / `/ja` route** | 25 | A real Japanese-language entry point. **Scored on rendered Japanese marketing copy, not on a route merely existing** — an English SPA shell served at `/ja` scores zero. |
| **Japanese content / language switcher** | 20 | Any genuine Japanese copy, or a switcher that offers Japanese. Partial credit (10) for a bundled product locale with an otherwise-English site. |
| **`hreflang="ja"` alternate** | 15 | Without it, Japanese-language search traffic never lands on a localized page — invisible in JP Google results. |
| **JPY pricing / currency** | 15 | USD-only forces JP finance to FX-convert and absorb forex fees, and gives them no clean number to approve. A JPY *display* toggle is enough; billing can stay USD. |

**How signals were checked (reproducible):**
- HTTP status, `<html lang>`, and `hreflang` were read with direct requests to each site on 2026-06-25.
- `/ja` routes were followed to their final destination — a `200` that resolves to an English SPA shell or a login page (Vercel, Linear, Sentry) is **not** counted as localization.
- Pricing currency and on-page Japanese copy were read from the rendered marketing/pricing pages.

**Honesty notes.** Where a check couldn't be confirmed (e.g. HashiCorp's homepage `hreflang` was bot-rate-limited at scan time), the signal is marked unverified and scored as a fail rather than guessed up. Six companies (Turso, Infisical, Inngest, ToolJet, Appsmith, Flagsmith) and nine others (Unleash, Novu, SuperTokens, Windmill, Appwrite, Logto, Coolify, Umami, Formbricks) reuse evidence from prior individual teardowns; the rest were scanned fresh for this index. Sites are the property of their respective owners; this report quotes only publicly observable facts.

---

## The ranking

> Tiers: **70–100** JP-ready front door · **30–69** partial / localized but gaps remain · **0–29** front door closed to Japan.
> No tool reached the top tier.

### Partial — localized, but the commercial surface lags (30–69)

| Score | Tool | Category | What's there | What's missing |
|---|---|---|---|---|
| **60** | **Auth0** | Auth / Identity | Full Japanese site at `/jp`, JP-discoverable, JP pricing page | **特商法**, **JPY** (prices still `$35/月`) |
| **60** | **Twilio Segment** | CDP / Analytics | Mature `ja-jp` site, Segment covered in Japanese | **特商法**, **JPY** |
| **45** | **HashiCorp** (Terraform/Vault) | Infra / DevOps | Genuinely localized `lang="ja"` site, JP case studies | **特商法**, **JPY**, `hreflang ja` unconfirmed |

These three did the hard part — real localization — and stop one or two static pages short of a JP-ready front door. The 特商法 page and a JPY display are the finish line, not a rebuild.

### Closed — front door shut to Japan (0–29)

The bundled-locale group (score 10) ships a Japanese *product UI* but offers a Japanese buyer **nothing on the marketing site** — so JP search never finds the localized product, and procurement stalls at an English/USD page:

| Score | Tool | What's there | The catch |
|---|---|---|---|
| **10** | **Appwrite** | Bundled `ja.json` UI locale | Locale is ~16% (48 keys) behind English; site fully English/USD |
| **10** | **Logto / Coolify / Umami / Formbricks** | Maintained `ja` product UI | Marketing site has zero Japanese, no 特商法, USD-only |
| **10** | **ToolJet** | Builder UI now Japanese-capable (community PR) | `/ja`, `/jp` all 404; USD-only; no 特商法 |

Everything else — **31 tools at score 0** — has no Japanese surface at all: `<html lang="en">`, `/ja` returning 404 (or an English shell), no `hreflang`, USD-only pricing, no 特商法 page. This includes Turso, Infisical, Inngest, Appsmith, Unleash, Flagsmith, Novu, SuperTokens, Windmill, Clerk, Neon, PlanetScale, Supabase, Vercel, Linear, Sentry, Railway, Render, Fly.io, PostHog, Hasura, Upstash, Algolia, Retool, Contentful, Sanity, n8n, Directus, BrowserStack, Mux, and Doppler.

---

## Three patterns worth naming

**1. "Looks localized, isn't."** Vercel, Linear, and Sentry all return `200` on `/ja` — but the page is an English SPA shell or a login form with a locale param, not a localized site (`<html lang="en">`, zero Japanese characters). A route existing is not localization. This index scores rendered Japanese copy, so these correctly score 0.

**2. Localized everywhere except Japan.** Algolia built the entire i18n machine — it offers English, German, French, Brazilian Portuguese, Spanish, and Italian. Japanese is the one major market it skipped. The hard part (i18n infrastructure) is already done; Japan was simply not prioritized.

**3. The product is ready; the storefront isn't.** Appwrite, Logto, Coolify, Umami, Formbricks, and ToolJet all ship a Japanese product UI — yet a Japanese buyer evaluating them sees an English site, USD pricing, and no 特商法 page, and never learns the product speaks Japanese. The localization investment is stranded behind an English front door.

And the universal one: **特商法 is missing everywhere — 0 of 40.** It is one static page. Its absence quietly disqualifies a vendor from many Japanese corporate purchases, and most teams never hear why the deal went quiet.

---

## What "fixing it" looks like

For almost every tool in the closed tier, the entire JP-readiness gap is footer-and-page-level work, not engineering:

1. **特商法に基づく表記** — one static page (事業者名・所在地・連絡先・販売価格・支払方法・返金/解約).
2. **`/ja` landing + top-10 docs** — a real localized entry point, not an English shell. Native review, not raw machine translation (critical for security tools like Infisical and Doppler, where a mistranslated scope or rotation step is an incident, not a typo).
3. **`hreflang="ja"`** — so JP-language Google serves the localized page.
4. **JPY display** — a reference price or toggle; billing can stay in USD.

For the partial tier (Auth0, Twilio, HashiCorp), it's just steps 1 and 4 — they're one or two pages from the top tier.

---

## About this index

This index is maintained by **greymoth** — Japan-market readiness and localization work for foreign developer tools, with an emphasis on the precision that procurement, legal, and security-literate localization actually require. Each tool above also has (or can have) a one-page teardown with the exact evidence and the exact fix.

If you run one of these tools and want the detailed map for your front door — or you're a Japanese team evaluating one of them and want to know what to ask the vendor — that's the work.

**greymoth** · [greymoth-jp.github.io/proof-dashboard](https://greymoth-jp.github.io/proof-dashboard) · glovrex

*Data: `index_data.json` (this directory). Scan date 2026-06-25. Corrections welcome — every claim links to a live, checkable source.*
