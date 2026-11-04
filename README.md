# Pre-Assessment prototype

A clickable prototype of **Pre-Assessment**: the triage step between a new regulation arriving and REMATIQ's existing Detailed SOP Compliance Assessment. For each product it decides whether a requirement applies, how ready we are, and who takes it next.

Built for the REMATIQ × Philips case (AI Deployment Strategist interview, 5 Nov 2026). It is a prototype, not a product: the AI output is simulated and the internal data is illustrative.

## What it shows

The demo follows Anke Weber (Q&R Manager, fictional) through five screens:

| Screen | Hash | One sentence |
| --- | --- | --- |
| Intake | `#intake` | A regulatory alert for the EU Battery Regulation, 9 of 12 products affected, plus the product sync from philips.de. |
| Triage board | `#triage` | Every product against requirements R1 to R8, coloured by readiness, with deadline chips and a "Needs my decision" filter. |
| Case review | `#case/P1-R4` | One product × one requirement: facts, AI reasoning, SOP search, evidence cards; Confirm stays locked until every card is ticked. |
| Routing | `#routing` | Open cases grouped by reason, each with a suggested owner; red groups open the new-SOP starter, "not applicable" groups get signed off. |
| Handover | `#handover` | Locked until every case is owned and every "not applicable" is signed; then ER cases pre-filled for the Detailed Assessment, SOP requests, and the audit log. |

Colours: red = applies, no SOP · orange = SOP exists, not assessed · purple = unclear, needs expert · green outline = not applicable, sign-off needed · green = done.

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
| X3 / MX100 battery (Li-ion 10.8 V, 21.6 Wh) | P | [philips.lv, HC989803196521](https://www.philips.lv/healthcare/product/HC989803196521/intellivue-x3-mx100-battery) |
| Efficia user-changeable batteries | P | Efficia patient monitoring brochure |
| Battery facts for MX750, MX850, MX40, Avalon CL, EarlyVue VS30, MR400, MR Portal 5000 | A (Assumed) | Product family; no public source matched yet |
| Art. 13(1), 13(4), 14(1) excerpts | R (Regulation) | Reg. (EU) 2023/1542, as quoted in REMATIQ's demo |
| Art. 13(6) excerpt | R | Reg. (EU) 2023/1542, matches several secondary sources; verify |
| Art. 3, 11, 48, 77, producer registration | R | Placeholders; exact text still to be pasted from [EUR-Lex](https://eur-lex.europa.eu/eli/reg/2023/1542/oj) |
| Requirement dates | R | Regulation timeline |
| SOP library (7 SOPs) and SOP search results | I (Illustrative) | Invented for the demo, not Philips data |
| People (Anke, Jonas, Mei, Sara, Lukas, Tobias) | I | Fictional |
| "Not applicable" Toy Safety alert | I | Illustrative example only |
| AI reasoning, confidence, SOP outlines, Jonas's sign-off | S (Simulated) | Fixed rules and text in the page; no model call |

## Open PAS: TODO items

From `index.html` (search for `PAS: TODO`):

- [ ] Paste the exact Art. 3 portable battery definition from EUR-Lex.
- [ ] Paste the exact Art. 11(1) and 11(3) text from EUR-Lex.
- [ ] Paste the exact Art. 48 text (as amended by Reg. 2025/1561) from EUR-Lex.
- [ ] Paste the exact Art. 77 text from EUR-Lex.
- [ ] Confirm the article for producer registration and take-back (shown as "Art. 55 ff. (verify)") and paste its text.
- [ ] Verify the Art. 13(6) QR code wording against EUR-Lex.
- [ ] Check whether the X3 battery, sold as a spare part, counts as user-replaceable under Art. 11 (it would turn R5 green for X3 and MX100).
- [ ] Link the Efficia brochure PDF directly instead of the catalogue page.
- [ ] Confirm that Philips calls the function "Q&R".
- [ ] Generic: placeholder evidence cards show until the EUR-Lex text is pasted into `DATA.evidence`.

Also from the PRD: match SKUs for MX750, MX850, Avalon CL and EarlyVue VS30, or keep them marked "not matched".
