# Pre-Assessment prototype

A clickable prototype of **Pre-Assessment**: the triage step between a new regulation arriving and REMATIQ's existing Detailed SOP Compliance Assessment. For each product it decides whether a requirement applies, how ready we are, and who takes it next.

Built for the REMATIQ × Philips case (AI Deployment Strategist interview, 5 Nov 2026). It is a prototype, not a product: the AI output is simulated and the internal data is illustrative.

## What it shows

The demo follows Anke Weber (Q&R Manager, fictional, shown top right as the logged-in user) from the Overview through three steps:

| Screen | Hash | One sentence |
| --- | --- | --- |
| Overview | `#home` | Regulations that need my attention and the product portfolio; click the EU Battery Regulation to start. |
| Product page | `#product/P1` | One product's facts, evidence and status against every obligation. |
| Regulatory alert | `#alert` | What came in (EU Battery Regulation), what it asks (8 obligations with dates) and which 12 products were checked, each with a link to its source. |
| Assess and route | `#assess/R4` | Requirements on the left, grouped by topic; pick one to see every product once, grouped by outcome, with a decision button in each row. |
| Case review | `#assess/R4/P1` | One product × one requirement: facts with source links, AI reasoning, evidence cards, overrides with a written reason, comments. |
| Handover | `#handover` | Locked until every case is routed and every "not applicable" is signed; then the pre-filled Detailed Assessment overview, follow-up per team, and the audit log. |

- **AI vs human:** blue blocks and `✦ AI` chips are simulated AI output; dark blocks and `✓ Human` chips are decisions by a named person. A legend sits under the top bar on every screen.
- **Routing to teams:** each open decision suggests a team with the reason. Team cards show function, lead, members, SOPs owned, open cases and turnaround; "Compare all teams" shows them side by side. A case goes to a team queue or a named person.
- **Deciding:** every row has its own buttons (Confirm, To expert, Sign off, Applies / Not applicable). Tick rows, or a whole section, to act on several at once; this works on the requirement view and on the product page.
- **Roles:** Anke (Q&R) confirms and routes. Unclear and "not applicable" cases go straight to Regulatory Affairs. Log in as Jonas Richter (top right) to sign off or decide them; he never gets "To expert", because he is the expert.
- **"Only what needs me":** filters the requirement list, the sections and the rows. For Anke: open cases not yet routed. For Jonas: unclear and "not applicable" cases in his queue.
- **Evidence:** ticking evidence cards is optional; every decision records how many cards were checked, and the audit log shows it.
- **Highlighted sources:** source links carry a browser text fragment, so Chrome jumps to the quoted words and highlights them.
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
| Art. 3, 11(1), 11(3), 13(1), 13(4), 13(6), 14(1), 48(1), 55(2), 77(1) excerpts | R (Regulation) | Copied verbatim from the [EUR-Lex full text](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32023R1542), 4 Nov 2026 |
| Other regulations on the Overview (AI Act, MDR, CRA, RoHS, ESPR) | I | Names and links are real; their status is illustrative. The CRA exclusion of MDR products (Art. 2(2)(a)) is real |
| Requirement dates | R | Regulation timeline |
| SOP library (7 SOPs) and SOP search results | I (Illustrative) | Invented for the demo, not Philips data |
| People (Anke, Jonas, Mei, Sara, Lukas, Tobias) | I | Fictional |
| Teams, members, turnaround times | I | Invented org structure |
| AI reasoning, confidence, SOP search, routing suggestions, SOP outlines | ✦ AI (simulated) | Fixed rules and text in the page; no model call |

## Open PAS: TODO items

From `index.html` (search for `PAS: TODO`):

- [ ] Check the amended Art. 48 text from Reg. (EU) 2025/1561 (the card quotes the original 2023 text and notes the moved date).
- [ ] Check whether the X3/MX100 battery pack counts as user-replaceable under Art. 11 (it would turn R5 green for both).
- [ ] Confirm that EarlyVue VS30 is a spot-check device (it makes VS30 the one R&D product-change case).
- [ ] Link the Efficia brochure PDF directly instead of the catalogue page.
- [ ] Confirm that Philips calls the function "Q&R" and how the teams are really cut.

Also from the PRD: match SKUs for MX750, MX850, Avalon CL and EarlyVue VS30, or keep them marked "not matched".
