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

**https://sarawak-growth-check.netlify.app**

Deep links per language:
[BM](https://sarawak-growth-check.netlify.app/?lang=bm) ·
[EN](https://sarawak-growth-check.netlify.app/?lang=en) ·
[中文](https://sarawak-growth-check.netlify.app/?lang=zh) ·
[Iban](https://sarawak-growth-check.netlify.app/?lang=ib)

---

## Deploying

Hosted on Netlify (team `zaiwin`, project `sarawak-growth-check`), publishing the
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
| `中`  | 中文 (Chinese) |
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
| 5 | Your biggest challenge | **One** — kept single so the primary pain point stays clean data |
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

Sarawak green `#0B6E4F` with gold accents, plus a pua kumbu red `#A63A2A` used
sparingly. Sarawak elements are woven in rather than pasted on:

- the **kenyalang** (rhinoceros hornbill) as the brand mark and as faint watermarks
- **pua kumbu** woven banding across card tops, the header, and section kickers
- an **ukiran**-inspired rosette on the introduction step, and a soft woven field
  behind the page

Everything is mobile-first, keyboard-navigable, and respects
`prefers-reduced-motion`. Progress survives an accidental refresh via localStorage.
