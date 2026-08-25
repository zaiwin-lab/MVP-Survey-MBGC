# Sarawak Business Growth Check 2026

A front-door acquisition microsite for **GERAK** and **USTEV** — the MINTRED Sarawak
entrepreneurship grants of up to RM20,000.

Its job is to attract and qualify more of the right applicants (graduates, SPM leavers,
TVET holders, micro and small businesses) and lead them naturally to the official
programme page.

**Live file:** `index.html` — one self-contained file. No build step, no framework,
no npm install. Open it in a browser, or drop it on any static host.

---

## Live

**https://bizgrowthsurvey.netlify.app**

Deep links per language:
[BM](https://bizgrowthsurvey.netlify.app/?lang=bm) ·
[EN](https://bizgrowthsurvey.netlify.app/?lang=en) ·
[中文](https://bizgrowthsurvey.netlify.app/?lang=zh) ·
[Iban](https://bizgrowthsurvey.netlify.app/?lang=ib)

---

## Deploying

Hosted on Netlify (team `zaiwin`, project `bizgrowthsurvey`), publishing the
repo root. `netlify.toml` sets the security headers and keeps the page itself
always revalidating so updates go live immediately.

To host it anywhere else, upload `index.html` — Netlify, Cloudflare Pages, GitHub Pages, or
a plain folder on the ministry's web server. There is nothing to compile.

The page renders completely from the file itself. The two external requests it makes
(Google Fonts and the confetti animation) are progressive enhancement only: if they
are slow or blocked, the site still looks and works correctly with system fonts.
This matters for users on weak rural connections.

---

## Languages

Four language panels, switchable from the header at any point without losing answers:

| Button | Language |
|--------|----------|
| `BM` | Bahasa Malaysia |
| `EN` | English |
| `中` | 中文 (Chinese) |
| `IB` | Jaku Iban |

The starting language is chosen in this order: a `?lang=` parameter → the visitor's
previous choice → their browser language → Bahasa Malaysia.

You can link straight to one language for a campaign:
`…/index.html?lang=ib`, `?lang=zh`, `?lang=en`, `?lang=bm`.

> **Before public launch:** the Iban copy should be reviewed by a native speaker.
> It follows common Sarawak usage and borrows Malay terms where spoken Iban does,
> but it has not been verified by a native speaker.

---

## How many answers each question takes

Not every question is single-answer. Every question carries a badge stating which
kind it is, in the active language, and multi-select questions also show a live
"N selected" counter.

| Q | Question | Answers |
|---|----------|---------|
| 1 | Which best describes you | **One** |
| 2 | Your business currently is | **Several** — a business is often home-based *and* online |
| 3 | Industry | **Several** — many operators straddle two, e.g. Food + Retail |
| 4 | Which best describes your business today | **One** |
| 5 | Your biggest challenges | **Up to 3** — problems rarely come one at a time |
| 6 | By 2030, what would you like your business to become | **Up to 3** — ambitions stack |
| 7 | Annual sales goal by 2030 | **One** |
| 8 | People employed by 2030 | **One** |
| 9 | Which support would help most today | **Several** |
| 10 | Received government assistance before | **One** |

Single-answer questions show a grey badge and a round tick; multi-answer questions
show a gold badge and a square tick, so the difference is visible at a glance even
before reading the label.

To change any of these, edit the `QUESTIONS` array at the top of the script:
`type:'single'` or `type:'multi'`, with an optional `max:` cap.

---

## Collecting responses

Responses currently go to the browser console only. To store them for real, open
`index.html`, search for **`BACKEND HOOK`**, set `ENDPOINT`, and uncomment the
`fetch()`. That is the only change needed.

Suitable targets: Formspree, a Google Apps Script Web App deployed with access
"Anyone", or a MINTRED API endpoint.

The payload looks like this — note that multi-answer questions arrive as arrays:

```json
{
  "submittedAt": "2026-08-06T09:14:22.104Z",
  "language": "bm",
  "answers": {
    "q1": "started-12m",
    "q2": ["home-based", "online"],
    "q3": ["food", "retail"],
    "q4": "ready-grow",
    "q5": "equipment",
    "q6": ["brand", "malaysia"],
    "q7": "300k-1m",
    "q8": "3-5",
    "q9": ["grant", "equipment"],
    "q10": "no"
  }
}
```

---

## Recommendation logic

The results page always surfaces GERAK and USTEV when the profile fits, and names
**USTEV first** when the respondent works in a technical / TVET field, since that is
who the programme exists for.

The message is assembled from the respondent's stage (planning / just started /
operating), then extended when they need capital or equipment, when they are in a
technical field, and when their 2030 ambitions point to real growth. See
`generateResults()`.

---

## Design notes

Rebuilt as an institutional portal rather than a folk-themed microsite. The
kenyalang hornbill and pua kumbu banding are retired; the Sarawak thread is
carried by the enterprise green instead.

**Palette** — three roles, kept strictly separate so the page reads as a system:

| Role | Colour | Used for |
|------|--------|----------|
| Ministry authority | navy `#0A1F44` → `#06142E` | header, hero, footer, primary buttons |
| Enterprise growth | emerald `#00875A` / `#00A36C` | selections, confirmations, the advisor bubble |
| Intelligence | cyan `#22D3EE` → violet `#7C5CFF` | **AI surfaces only** |

The cyan→violet gradient never appears on a non-AI element. That is what makes
the AI layer legible as a distinct capability instead of decoration.

**AI treatments** — an `AI-Powered` chip with a sweeping specular highlight, a
3px intelligence rule under the header, drifting aurora fields behind every
dark AI panel, a shimmering progress bar, an analysis interstitial that shows
the matching work step by step before results, an `AI Match` chip and an
animated match-strength meter on the recommendation.

## Layout across devices

Desktop is a first-class layout, not a stretched phone column.

| Width | Layout |
|-------|--------|
| < 640px | single column; bubble sub-labels collapse below 420px |
| 640–1023px | wider column, option grids go three across |
| ≥ 1024px | split hero, sticky section rail beside the questions, results with the snapshot alongside |
| ≥ 1280px | wider shell and larger display type |

## The three standard items

1. **4-pane language panel** — `BM · EN · 中 · IB` in the header, switchable at
   any point without losing answers.
2. **Corner bubbles** — bottom-left `AI Help · Available 24/7` opens the
   assistant panel; bottom-right `Talk to Us` links to the official MINTRED
   programme page. Both translated. A black spacer below the credit bar keeps
   them clear of the signature line on phones.
3. **KOBIS Berhad signature bar** — per `MASTER_WEBSITE_PROMPT.md`: 0.75in tall,
   `.72rem`, weight 300, on `#07090b`. Hovering **KOBIS Berhad** sweeps a
   specular highlight across the text and reveals an animated gradient.
   Translated in all four languages, link to `www.kobisberhad.com`.

> **On the AI assistant:** the panel's answers are pre-written and translated,
> not generated live, and its footer says so — it is framed as prepared guidance,
> not an eligibility decision. To make it a live assistant, replace `renderFaq()`
> with a call to a model endpoint; the panel markup needs no changes.

Everything is keyboard-navigable, respects `prefers-reduced-motion` (the
analysis interstitial is skipped entirely), and progress survives a refresh
via localStorage.
