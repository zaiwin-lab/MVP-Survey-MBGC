# Sarawak Business Growth Check

> **Portfolio maturity:** Working Public Prototype · Multilingual Opportunity-Discovery Microsite

[Open the verified live demonstration](https://bizgrowthsurvey.netlify.app)

Sarawak Business Growth Check is a four-language self-assessment that helps an entrepreneur describe their current position, growth ambition and support needs, then receive a transparent programme-oriented next step.

The repository name retains MVP for development history. **Sarawak Business Growth Check** is the permanent product identity.

## Business problem

Entrepreneurship programmes can be difficult to navigate when eligibility language, application pathways and support options are spread across multiple channels. At the same time, programme teams need a low-friction way to understand the stage, sector, challenges and ambitions of potential applicants.

This prototype provides an accessible front door without pretending to make an official eligibility or funding decision.

## Intended users

- aspiring and early-stage Sarawak entrepreneurs;
- graduates, SPM leavers and TVET participants exploring enterprise support;
- micro and small-business owners;
- outreach teams preparing an authorised entrepreneurship campaign.

## Core capabilities

- ten-question mobile-first business growth check;
- single-answer and controlled multi-answer question types;
- four switchable languages: Bahasa Malaysia, English, Chinese and Iban;
- direct language links for campaign channels;
- progress persistence in localStorage;
- deterministic recommendation logic based on business stage, sector, needs and ambition;
- programme-oriented results and a handoff toward an official information source;
- an assistant panel of prepared, translated answers about the check and the programmes;
- a dedicated desktop layout alongside tablet and phone breakpoints;
- keyboard-friendly interaction and reduced-motion support;
- one self-contained HTML file with no build requirement.

## Strategic value

The product demonstrates how a public programme can convert broad awareness into structured, consent-aware interest.

With an approved backend and official content governance, it could:

- widen access across common Sarawak languages;
- give visitors a clearer route from curiosity to action;
- help an outreach team understand recurring barriers and support needs;
- preserve campaign context through language-specific links;
- provide structured demand signals without building a large platform first.

These are intended uses, not claims of measured applications, approvals, funding or programme impact.

## Recommendation approach

The current recommendation is deterministic, not generative AI. It assembles a result from the respondent's declared stage, technical or TVET context, capital and equipment needs, and growth ambitions.

The result is an orientation aid only. It does not assess official eligibility, guarantee programme acceptance or replace the latest published criteria.

## What is implemented

The repository contains a complete self-contained HTML application with the multilingual interface, question definitions, selection rules, recommendation logic, browser persistence, responsive styles and deployment headers.

### Technology

Semantic HTML · CSS · vanilla JavaScript · localStorage · deterministic rules · Netlify

There is no framework, package installation, database, authentication service or live AI model.

## Interface design

The interface presents as an institutional portal rather than a themed microsite.
The kenyalang hornbill and pua kumbu banding used in earlier drafts are retired;
the Sarawak thread is carried by the enterprise green.

The palette holds three roles and keeps them strictly separate, so the page reads
as one system:

| Role | Colour | Applied to |
|------|--------|------------|
| Institutional authority | navy `#0A1F44` → `#06142E` | header, hero, footer, primary actions |
| Enterprise growth | emerald `#00875A` / `#00A36C` | selections, confirmations, advisor bubble |
| Intelligence layer | cyan `#22D3EE` → violet `#7C5CFF` | assisted-matching surfaces only |

The cyan-to-violet gradient appears on no other element. That separation is what
makes the matching layer legible as a distinct capability rather than ornament.

Its treatments are a capability chip with a sweeping specular highlight, a
gradient rule beneath the header, drifting aurora fields behind dark panels, a
shimmering progress indicator, a step-by-step interstitial shown while the
answers are matched, and an animated match-strength meter on the result.

### What the intelligence layer is, and is not

This presentation is an interface style. It does not change the substance
described under **Recommendation approach**: the matching remains deterministic
rules over declared answers, and there is no live model in the deployed page.

- the match-strength meter is computed from the same declared signals that
  assemble the recommendation text, and is an orientation aid, not a score of
  official eligibility;
- the interstitial makes existing work visible; it does not perform additional
  processing, and it is skipped entirely under reduced-motion settings;
- the assistant panel serves prepared, translated answers. It is not generative,
  and its footer states that its answers are guidance rather than an eligibility
  decision.

Should a public campaign require the interface wording to mirror the deterministic
approach more literally, the capability labels are single translated strings
(`aiTag`, `aiMatch`, `aiHelpLabel`) and can be reworded without touching layout
or logic.

## Layout across devices

The desktop presentation is a distinct layout, not a widened phone column.

| Width | Layout |
|-------|--------|
| below 640px | single column; bubble sub-labels collapse below 420px |
| 640–1023px | wider column, option grids move to three across |
| 1024px and above | split hero, sticky section rail beside the questions, result with the snapshot alongside |
| 1280px and above | wider shell and larger display type |

## Standard delivery components

1. **Four-language panel** — `BM · EN · 中 · IB` in the header, switchable at any
   point without losing answers.
2. **Corner assist bubbles** — bottom-left opens the assistant panel and is
   labelled as available at any time; bottom-right links to the official
   programme information source. Both are translated. A matching spacer beneath
   the credit bar keeps them clear of the signature line on small screens.
3. **KOBIS Berhad signature bar** — built to the house specification in
   `MASTER_WEBSITE_PROMPT.md`: 0.75in tall, `.72rem`, weight 300, on `#07090b`.
   Hovering the **KOBIS Berhad** link sweeps a specular highlight across the text
   and reveals an animated gradient. Translated in all four languages.

## Delivery role

**Ts. Zaiwin Kassim** leads product strategy, stakeholder requirements, solution architecture and supervised AI-assisted delivery with the **KOBIS AI Prodigy Team**. For this product, that role covers the outreach journey, multilingual experience, recommendation structure and responsible handoff to official programme information.

This portfolio attribution does not imply commissioning, endorsement, approval or partnership by MINTRED Sarawak or any programme referenced in the demonstration.

## Responsible-use boundaries

- The result is not an official eligibility, grant, financing or application decision.
- Programme names, funding values, dates, criteria and official links must be checked against current authoritative sources before every public campaign.
- Respondent answers are self-declared and are not independently verified.
- The current public prototype does not transmit responses to a database; submission data remains a demonstration output.
- A production collection endpoint would require an approved privacy notice, consent record, data minimisation, retention policy and restricted access.
- The language experience improves accessibility but does not replace native-speaker and programme-owner review.
- Recommendations must not create false expectations of financial assistance or acceptance.

## Current limitations

- responses are not stored by a production backend;
- there is no applicant account, case tracking or administrative dashboard;
- eligibility logic is informational and has not been validated as an official decision model;
- Chinese and Iban content require authorised native-speaker review before formal public use;
- programme facts can change and are not automatically synchronised;
- external fonts and animation are progressive enhancements, not controlled application assets;
- assistant-panel answers are prepared content and require the same programme-owner
  review as the rest of the copy before public use;
- no automated test suite is documented.

## Live and language links

The connected hosting record identifies **bizgrowthsurvey** as the project and reports its current deployment as ready.

- [Bahasa Malaysia](https://bizgrowthsurvey.netlify.app/?lang=bm)
- [English](https://bizgrowthsurvey.netlify.app/?lang=en)
- [Chinese](https://bizgrowthsurvey.netlify.app/?lang=zh)
- [Iban](https://bizgrowthsurvey.netlify.app/?lang=ib)

## Run or deploy

Open index.html directly in a browser, or serve the repository root using any static web server. Netlify publishes the repository root with security and cache headers defined in netlify.toml.

Before an authorised campaign:

1. verify all programme facts and official destination links;
2. obtain language review and content-owner approval;
3. publish the privacy notice and consent terms;
4. connect an approved secure response endpoint if data collection is required;
5. test the complete journey on common mobile devices and slower connections.

## Portfolio evidence

Sarawak Business Growth Check demonstrates multilingual public-service UX, low-bandwidth static architecture, deterministic recommendation design and responsible separation between opportunity discovery and official programme decisions.
