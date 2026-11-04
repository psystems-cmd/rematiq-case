# Pre-Assessment prototype

A clickable prototype of **Pre-Assessment**: the triage step between a new regulation arriving and REMATIQ's existing Detailed SOP Compliance Assessment. For each product it decides whether a requirement applies, how ready we are, and who takes it next.

Built for the REMATIQ × Philips case (AI Deployment Strategist interview, 5 Nov 2026). It is a prototype, not a product: the AI output is simulated and the internal data is illustrative.

## What it shows

The demo follows Anke Weber (Q&R Manager, fictional, shown top right as the logged-in user) through three screens:

| Screen | Hash | One sentence |
| --- | --- | --- |
| Regulatory alert | `#alert` | What came in (EU Battery Regulation), what it asks (8 obligations with dates) and which 12 products were checked, each with a link to its source. |
| Assess and route | `#assess/R4` | Requirements on the left, grouped by topic; pick one to see the AI call, the open decisions grouped by outcome, and every product. |
| Case review | `#assess/R4/P1` | One product × one requirement: facts with source links, AI reasoning, evidence cards; Confirm stays locked until every card is ticked. |
| Handover | `#handover` | Locked until every case is routed and every "not applicable" is signed; then the pre-filled Detailed Assessment overview, follow-up per team, and the audit log. |

- **AI vs human:** blue blocks and `✦ AI` chips are simulated AI output; dark blocks and `✓ Human` chips are decisions by a named person. A legend sits under the top bar on every screen.
- **Routing to teams:** each open decision suggests a team with the reason. Team cards show function, lead, members, SOPs owned, open cases and turnaround; "Compare all teams" shows them side by side. A case goes to a team queue or a named person.
- **Sign-off:** only Regulatory Affairs can sign "not applicable". Switch to Jonas Richter in the account menu (top right) to sign.
- **Comments:** on every requirement and every case; they also go into the audit log.

Colours: red = applies, no SOP · orange = SOP exists, not assessed · purple = unclear, needs expert · green outline = not applicable, needs sign-off · green = done.

## How to open

Open `index.html` in a browser. No build step, no server, no libraries. "Reset demo" in the top bar restores the start state.

## Deploy to GitHub Pages

1. Push this repository to a public GitHub repository.
2. Settings → Pages → Source: "Deploy from a branch", branch `main`, folder `/ (root)`.
3. The page is live at `https://<user>.github.io/<repo>/` after a minute.

## Where the code is

Everything is in `index.html`, in this order: styles, data, rules, state and helpers, screens, router. Comments for Pascal start with `PAS:` (`SECTION`, `WHY`, `SIMULATED`, `SOURCE`, `TODO`, `DEMO`). All data sits in `const DATA`, so a product or SOP can change without touching the rules.

## Data sources

| Data | Tag | Source |
| --- | --- | --- |
| Product names and SKUs | P (Public) | philips.de catalogue scrape, 4 Nov 2026 (1,270 products, 14 categories) |
| X3 / MX100 battery (battery pack, 5 h capacity) | P | philips.co.uk product pages [HC867030](https://www.philips.co.uk/healthcare/product/HC867030), [HC867033](https://www.philips.co.uk/healthcare/product/HC867033) |
| Efficia lithium battery | P | [philips.de HC863304](https://www.philips.de/healthcare/product/HC863304) (German, translated) |
| Efficia user-changeable batteries | P | Efficia patient monitoring brochure (link still to add) |
| Battery facts for MX750, MX850, MX40, Avalon CL, EarlyVue VS30, MR400, MR Portal 5000 | A (Assumed) | Product family; no public source matched yet |
| Art. 13(1), 13(4), 14(1) excerpts | R (Regulation) | Reg. (EU) 2023/1542, as quoted in REMATIQ's demo |
| Art. 13(6) excerpt | R | Reg. (EU) 2023/1542, matches several secondary sources; verify |
| Art. 3, 11, 48, 77, producer registration | R | Placeholders; exact text still to be pasted from [EUR-Lex](https://eur-lex.europa.eu/eli/reg/2023/1542/oj) |
| Requirement dates | R | Regulation timeline |
| SOP library (7 SOPs) and SOP search results | I (Illustrative) | Invented for the demo, not Philips data |
| People (Anke, Jonas, Mei, Sara, Lukas, Tobias) | I | Fictional |
| Teams, members, turnaround times | I | Invented org structure |
| AI reasoning, confidence, SOP search, routing suggestions, SOP outlines | ✦ AI (simulated) | Fixed rules and text in the page; no model call |

## Open PAS: TODO items

From `index.html` (search for `PAS: TODO`):

- [ ] Paste the exact Art. 3 portable battery definition from EUR-Lex.
- [ ] Paste the exact Art. 11(1) and 11(3) text from EUR-Lex.
- [ ] Paste the exact Art. 48 text (as amended by Reg. 2025/1561) from EUR-Lex.
- [ ] Paste the exact Art. 77 text from EUR-Lex.
- [ ] Confirm the article for producer registration and take-back (shown as "Art. 55 ff. (verify)") and paste its text.
- [ ] Verify the Art. 13(6) QR code wording against EUR-Lex.
- [ ] Check whether the X3/MX100 battery pack counts as user-replaceable under Art. 11 (it would turn R5 green for both).
- [ ] Confirm that EarlyVue VS30 is a spot-check device (it makes VS30 the one R&D product-change case).
- [ ] Link the Efficia brochure PDF directly instead of the catalogue page.
- [ ] Confirm that Philips calls the function "Q&R" and how the teams are really cut.
- [ ] Generic: placeholder evidence cards show until the EUR-Lex text is pasted into `DATA.evidence`.

Also from the PRD: match SKUs for MX750, MX850, Avalon CL and EarlyVue VS30, or keep them marked "not matched".
