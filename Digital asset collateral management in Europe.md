# Digital asset collateral management for the European market: steps and viability

*Research date: 10 November 2026. Subject: [TomaszWaszczyk/digital-asset-collateral-management-system](https://github.com/TomaszWaszczyk/digital-asset-collateral-management-system).*

## Verdict

**Not worth building as a general product for European banks today. Worth a cheap, time-boxed validation of one narrow wedge.**

The idea is sound and the timing looks attractive, but four facts work against a new entrant:

1. **Banks get no capital relief.** Bitcoin is not eligible collateral under EU bank capital rules, so a bitcoin-secured loan is capitalised like an unsecured one. The bank's motive is client acquisition and real-world loss protection, not balance-sheet efficiency. That keeps volumes small.
2. **The seat is partly taken.** Sopra Financial Technology, which already runs IT for German cooperative banks, has a "Crypto Lending Pilot" middleware and a live pilot with VR Bank Bayern Mitte and 21bitcoin. US vendors (Membrane Labs) and custodians (Zodia, Fireblocks, Taurus) cover the institutional end.
3. **The market is shrinking, not growing.** Global crypto-collateralised lending was $56.2bn at end-June 2026, down 40% from its Q3 2025 peak. European bank volumes are a rounding error within that.
4. **The rules are unsettled until at least mid-2027.** The Commission's MiCA review report, which decides whether crypto lending is regulated at EU level, is due 30 June 2027.

What is in favour: bank interest is real and recent (Jeonbuk in Korea, VR Bank in Germany, Sygnum's MultiSYG in Switzerland), a small startup (Debifi) did win a bank as a partner, and no vendor yet owns Central and Eastern Europe.

The repository today is a concept note: a README and a hand-drawn diagram, with no code. Everything below assumes building from zero.

## What the repository describes

The README documents the Jeonbuk Bank model from October 2026:

- A corporate borrower places bitcoin with a licensed third-party custodian.
- The bank lends won and holds only a claim, never the coins.
- On default the bank asks a court to sell the coins. That route exists because Korea's amended civil enforcement rules, in force since 1 October 2026, cover virtual assets.
- The bank values the pledge with its own multi-exchange price index and books the loan in its ordinary collateral systems.

Press coverage confirms this structure. Loan size, rate, loan-to-value and the custodian's name are undisclosed, and no court-supervised sale has been reported yet. The model is therefore untested at the point that matters most.

## The Korean design does not transfer one-to-one

The court sale is a Korean workaround, not a feature to copy. European pilots already use contractual liquidation: Sopra's middleware issues a margin call when a sub-wallet falls below a threshold and liquidates if the client does not top up. A European system should be designed around a pledge plus a three-party control agreement with the custodian, with the court as fallback only.

How enforceable that is depends on the country, because bitcoin sits outside the EU Financial Collateral Directive:

| Country | Position | Confidence |
|---|---|---|
| France | Dedicated crypto pledge regime since the DDADUE law of May 2025 (Code monétaire et financier L. 226-5). Created by signed declaration, custodian issues a pledge attestation, enforcement terms set by contract. An implementing decree was still pending in the source I read. | Medium |
| Germany | No statute. Crypto is seizable as "other property rights" under § 857 ZPO (Kammergericht, 6 Dec 2023), and sold by private sale or via a bailiff's trust account. A live bank pilot exists. | Medium |
| Poland | Bailiff enforcement against crypto is accepted in practice under art. 909 KPC. Whether a registered pledge can be taken over crypto is unsettled. Poland still has no national MiCA act after three presidential vetoes, so there are no Polish-licensed custodians. | Low |
| Switzerland | Outside the EU but the most mature market: Sygnum, AMINA, and SIX's Digital Collateral Service. | Medium |

## Regulatory map

| Area | What it means for this product |
|---|---|
| MiCA | Does not regulate lending. Custody, exchange and transfer of the collateral are regulated services, so whoever holds keys or sells coins must be a licensed crypto-asset service provider (CASP). ESMA Q&A 2883 (June 2026) confirms general conduct duties apply to CASPs involved in lending. |
| Lending licence | National law. In Germany, lending as a business needs a banking licence, which pushes a newcomer into the vendor role. |
| Capital rules (CRR3 Art. 501d, Basel SCO60) | 1,250% risk weight applies if the bank *holds* bitcoin. In this model it does not, so the loan is an ordinary corporate exposure. Bitcoin is not on the list of eligible financial collateral, so it does not reduce the capital charge. **This is my reading; I could not confirm it from a primary source and it needs a regulatory lawyer.** |
| DORA | A software supplier to a bank is an ICT third-party provider. Expect mandatory contract clauses (Art. 30): audit rights, exit plans, incident reporting, sub-outsourcing controls. |
| Consumer credit | The new Consumer Credit Directive applies from 20 November 2026. Stay corporate-only at first, as Jeonbuk did. |
| AML | Source-of-funds checks on the pledged coins, Travel Rule on transfers to and from the custodian, and the new AML Regulation from July 2027. |
| MiCA review | The EBA (Sept 2026) recommended a cost-benefit analysis of adding intermediated crypto lending to MiCA, with suitability tests and leverage limits. Its focus is lending *of* crypto, not fiat loans *against* crypto, but scope could widen. |

## Market and competition

**Size.** Galaxy Research puts crypto-collateralised lending at $56.16bn at end-June 2026, of which centralised lenders hold $22.98bn. Europe's share is not published. The best European data points are Swiss: Sygnum's loan book was CHF 235m and AMINA's CHF 103m at end-2024. More than one in five Sygnum clients now has a Lombard loan, and bitcoin is over 80% of pledged collateral.

**Corporate demand in the EU is thin.** The largest listed European bitcoin holders are small: Bitcoin Group SE with about 3,605 BTC and Capital B with about 3,135 BTC. The natural borrowers are private companies, miners, and wealthy individuals, who are harder to reach and partly excluded by a corporate-only design.

**Who is already there:**

| Player | Role | Why it matters |
|---|---|---|
| Sopra Financial Technology (DE) | White-label middleware between core banking and custodians | Direct competitor with existing bank distribution |
| 21bitcoin (AT) | MiCA-licensed broker handling custody and client experience in the VR Bank pilot | Shows the partner structure banks accept |
| Debifi | Multi-signature loan platform behind Sygnum's MultiSYG (Oct 2026) | Proof a small firm can land a bank |
| Membrane Labs (US) | Loan and collateral management software; $20m Series A; claims over $10bn in bookings; integrated with Zodia, BitGo, Fireblocks, Copper | Owns the institutional segment |
| Zodia, Taurus, Fireblocks | Custody platforms adding collateral features | Can bundle your product's function for free |
| Firefish (CZ), Lendasat, Lygos | Bitcoin-native peer-to-peer and non-custodial lending | Compete for the same borrowers outside banks |
| Nexo, Blockrise, Bit2Me | Non-bank euro loans against bitcoin | Already serve retail and SME demand |

JPMorgan was reported in 2025 to be planning loans against bitcoin held with a third-party custodian. I found no confirmation that it launched.

## Steps to deliver

**Phase 0: validate before building (6–8 weeks)**

1. Choose the role. Recommended: software vendor to lenders. Becoming the lender needs a banking licence in key markets; becoming the custodian needs a CASP licence.
2. Run 15–20 discovery calls with cooperative banks, small private banks, and non-bank lenders in one country. Ask who owns the budget and what blocks them.
3. Talk to two or three MiCA-licensed custodians about a three-party control agreement and API access.
4. Buy one legal opinion for one jurisdiction covering pledge creation, out-of-court sale, borrower insolvency, and capital treatment.

**Phase 1: legal and partner structure (2–4 months)**

5. Pick the launch country. Germany has live demand and case law. France has the clearest statute. Poland is a weak first market until it has a national MiCA act.
6. Draft the document pack: loan agreement, pledge, control agreement, liquidation mandate to a CASP.
7. Sign a design-partner bank and a custodian before writing production code.

**Phase 2: build the minimum product (4–6 months)**

8. Custodian adapters with on-chain verification that pledged coins exist and have not moved.
9. Price index from several exchanges, with a documented methodology and stress haircuts.
10. Loan-to-value monitoring, margin-call workflow, and cure periods.
11. Liquidation orchestration that instructs the CASP. The system must never hold keys or client funds, or it becomes a regulated service itself.
12. Core-banking integration, immutable audit trail, and risk reporting for the bank's supervisor.

**Phase 3: become buyable by a bank (parallel, 6–12 months)**

13. ISO 27001 or SOC 2, penetration tests, business continuity and exit plans, DORA-ready contract terms.
14. Support the bank's new-product approval process and its conversation with the supervisor.

**Phase 4: pilot and scale**

15. Pilot with a capped book, bitcoin only, corporate only, conservative loan-to-value (the German pilot illustrates 50%).
16. Run a default drill end to end, including the court fallback.
17. Add a second country only after the first legal template is proven.

## Economics (my estimates, not sourced)

- A small bank's pilot book might be €10–50m. At a fee of 20–50 basis points of book, that is €20–250k a year per bank.
- Reaching €1m in annual revenue therefore needs roughly 5–10 live banks.
- Bank sales cycles for a new, supervised product typically run 12–24 months.
- Realistic time to that revenue is three years or more, with certification and legal costs up front.

## Conditions that would change the verdict

Proceed if, within the validation window, you get any of these:

- A bank or lender signs a paid pilot or a letter of intent.
- A custodian agrees to co-sell.
- The legal opinion confirms out-of-court enforcement in your launch country.

Stop if discovery calls show interest but no budget owner, or if banks say they will wait for Sopra, their core-banking provider, or the MiCA review.

A lower-risk variant is to sell integration and advisory work to banks running their first pilot, and productise only what repeats.

## The wider European digital-collateral market

Bitcoin-secured bank loans are the small corner of this market. The large and fast-moving part in Europe is **tokenised traditional collateral**: government bonds, money market fund shares and central bank money moved on distributed ledgers. That is where European policy is heading, and it is what the ECB quote in the repository's README is actually about.

**What is live in 2026**

| Development | Status |
|---|---|
| Eurosystem accepts DLT-issued securities as collateral | Since 30 March 2026, for marketable assets issued in central securities depositories. |
| ECB Pontes | Launched 21 September 2026. Links market DLT platforms to TARGET so tokenised trades settle in central bank money. 13 participants at launch, including Deutsche Bank, Santander, Société Générale and the EIB. Four DLT operators: Axiology, Cashlink, Clearstream and SWIAT. |
| First large Pontes settlement | A €1bn European Stability Mechanism benchmark bond issued on DLT, per an ECB speech of 5 November 2026. |
| Eurex Clearing with HQLAx | First clearing house to take DLT-mobilised collateral as margin; first live transaction in July 2025 (J.P. Morgan for the pension fund PGGM). BaFin gave non-objection. |
| BlackRock tokenised money market funds | Tokenised share classes of European cash funds managing $311bn, launched August 2026 on J.P. Morgan's Kinexys. Collateral use is a stated aim. |
| Broadridge DLR | Tokenised repo platform averaging about $350–365bn a day through 2026, mostly US Treasuries, now extending to G7 securities. |

**What is still open**

- **Clearing-house rules.** ESMA opened a call for evidence on tokenised collateral at EU clearing houses on 9 October 2026, with responses due 15 January 2027. It does not propose new eligible collateral types. It asks whether tokenised assets can be reached and turned into cash in a default. ESMA reportedly said HQLAx is the only operational DLT collateral solution it has seen in supervision.
- **DLT Pilot Regime.** The Commission proposed in December 2025 to raise the cap from €6bn to €100bn and open it to all financial instruments. Finance ministers want €300bn. New rules are not expected to apply before 2027.
- **Tokenised funds as margin.** The UK regulator confirmed in April 2026 that tokenised money market funds can be eligible collateral for uncleared trades. I found no equivalent EU statement.
- **Pontes limits.** Operating hours are 8:00–16:00 CET on business days. Round-the-clock operation is planned by 2028. Smart-contract features come later.
- **Crypto as cleared margin.** I found no European clearing house accepting bitcoin or crypto funds as margin. US rules allow it.

**Scale, for comparison**

- European repo market: €13.65tn outstanding in the ICMA survey published March 2026.
- Tokenised money market funds worldwide: about €7bn in February 2026, up 110% in 2025, per a figure attributed to the ECB.
- Crypto-collateralised lending worldwide: $56bn (see above).

**What this means for the product** (my inferences)

- Tokenised collateral is a much bigger market than bitcoin lending, but it belongs to infrastructure owners: Deutsche Börse and HQLAx, Euroclear with Digital Asset, Broadridge, J.P. Morgan. Established collateral software such as CloudMargin already markets itself as ready for tokenised assets. A new vendor cannot enter at the centre.
- The realistic openings are at the edges: tooling for the smaller DLT operators connected to Pontes, adapters between bank collateral systems and those platforms, and valuation and monitoring for tokenised fund shares.
- A bitcoin collateral system built now should treat bitcoin as the first asset type, not the only one. The same engine (custodian adapters, valuation, margin calls, liquidation instructions) applies to tokenised funds and bonds, where European banks do get capital recognition.
- Crypto-native collateral networks already exist for trading firms. Copper's ClearLoop reports $3bn of monthly off-exchange settlement and added loans with FalconX in June 2026. These serve exchanges and funds, not bank lending.

## Is it worth building anywhere else?

Yes: the United States, and possibly South Korea. Everywhere else I checked is either crowded or has no bank demand yet. This section rests on one quick round of searches per region, and the sources are weaker than for the European sections.

| Place | Worth it? | Why |
|---|---|---|
| United States | Best candidate | The only market with real bank volume. Wells Fargo and JPMorgan are reported to lend against bitcoin, Coinbase had $2.3bn in crypto-backed loans outstanding in October 2026, and Fannie Mae began accepting crypto-backed mortgages in March 2026. One source says the US has not proposed implementing the Basel crypto capital rules. |
| South Korea | Good timing, hard entry | Jeonbuk launched on 12 October 2026 and CoinDesk reports the product could spread to other banks under existing law. No second bank has followed yet, so vendors are not entrenched. A foreign vendor faces language, local-custodian and procurement barriers. |
| Switzerland | Proven but taken | Sygnum, AMINA and SIX already do this in-house or with chosen partners. |
| UAE | Too early | Clear licensing, but only pilots (Standard Chartered with OKX), no bank loan product. |
| Japan, Hong Kong, Singapore | Too early | Activity is from non-bank lenders such as CRYL in Japan. I found no regulator announcement on bank lending. |
| Latin America | Wrong customer | Demand is real because local credit is expensive, but it is served by exchanges and non-banks such as Lemon in Argentina, not banks. |

Two caveats on the US:

- **The big banks are not the customer.** They build in-house or use large custodians, and Membrane Labs already sells this software to institutions. The open segment would be community banks, credit unions and mortgage lenders. I found no evidence either way on whether they are buying.
- **The Fannie Mae opening is narrower than headlines suggest.** Reports conflict on how far it has been implemented, and most lenders cannot yet accept crypto as a qualifying asset.

Geography matters less than whether a lender is willing to pilot. A signed design partner in Poland or Czechia beats a better market with no contacts. With no such contact anywhere, the US mortgage and community-bank niche is the first place to run discovery calls.

## What I could not verify

- Whether US community banks, credit unions or mortgage lenders are buying this kind of software.
- The reports that Wells Fargo and JPMorgan have live bitcoin-backed lending, against a primary source.
- Whether any Korean bank other than Jeonbuk plans a similar product.

- The CRR collateral-eligibility conclusion, from a primary text.
- Whether the Commission has adopted the EBA's technical standards on crypto exposures.
- The current status of the VR Bank pilot and of Poland's crypto-assets bill after September 2026.
- Whether a Polish registered pledge can cover crypto-assets.
- The ECB speech was read only through a summary; it does not address bitcoin as collateral. The ECB's on-chain collateral work concerns tokenised securities.

## Sources

**Korean model**
- [FinanceFeeds: Jeonbuk Bank opens bitcoin-backed won loans](https://financefeeds.com/jeonbuk-bank-breaks-ground-with-bitcoin-lending/)
- [Crypto Times: Jeonbuk Bank rolls out first bitcoin-backed loans](https://www.cryptotimes.io/2026/10/13/south-koreas-jeonbuk-bank-rolls-out-first-bitcoin-backed-loans/)
- [crypto.news: What happens if BTC falls?](https://crypto.news/a-south-korean-bank-is-lending-against-bitcoin-what-happens-if-btc-falls/)

**EU regulation**
- [Latham & Watkins: Cryptoasset lending in the gaps, ESMA Q&A 2883](https://www.fintechanddigitalassets.com/2026/08/cryptoasset-lending-in-the-gaps-mica-esma-qa-2883-and-the-regulatory-future-of-cryptoasset-lending/)
- [EBA response to the Commission's MiCA review consultation (PDF)](https://eba.europa.eu/sites/default/files/2026-09/12cb4f01-0d51-46bf-a561-165ac486698f/EBA%20response%20to%20EC%20targeted%20consultation%20on%20MiCA%20review.pdf)
- [Cointelegraph: EBA calls for crypto lending rules under MiCA](https://cointelegraph.com/news/eu-eba-crypto-lending-defi-mica-rules)
- [White & Case: CRR III prudential treatment of crypto exposures](https://www.whitecase.com/insight-alert/crr-iii-prudential-treatment-crypto-exposures)
- [EBA final report on crypto exposure RTS, Art. 501d(5) (PDF)](https://www.eba.europa.eu/sites/default/files/2025-08/616d6b06-cdcf-4246-a7cc-2173dfd32fa6/Draft%20RTS%20on%20crypto%20asset%20exposures%20Article%20501d-5.pdf)
- [Basel Framework SCO60 (PDF)](https://www.bis.org/committees/bcbs/basel-framework/81561/chapter.pdf)
- [ECB: Schnabel, "Central banks on-chain", 28 Aug 2026](https://www.ecb.europa.eu/press/key/date/2026/html/ecb.sp260828~fe9afc86e8.en.html)
- [ECB: DLT-based assets as eligible Eurosystem collateral](https://www.ecb.europa.eu/press/pr/date/2026/html/ecb.pr260127_1~a946167ce1.en.html)
- [Bastion: DORA contractual requirements](https://bastion.tech/learn/dora/contractual-requirements)

**National law**
- [DLA Piper: French DDADUE law and the crypto pledge regime](https://www.dlapiperintelligence.com/investmentrules/blog/articles/2025/french-ddadue-law-establishes-a-legal-regime-for-pledging-crypto-assets)
- [Noerr: Krypto-Vollstreckung, developments in case law](https://www.noerr.com/de/insights/krypto-vollstreckung-aktuelle-entwicklungen-in-der-rechtsprechung)
- [Egzekucja i zabezpieczenia: Egzekucja z kryptowalut](https://egzekucjaizabezpieczenia.pl/2023/10/19/egzekucja-z-kryptowalut/)
- [Polsat News: Sejm vote on the crypto-assets veto, 4 Sep 2026](https://www.polsatnews.pl/wiadomosc/2026-09-04/ustawa-o-kryptowalutach-sejm-zdecydowal-ws-prezydenckiego-weta/)
- [Dudkowiak: President's new crypto-assets bill](https://dudkowiak.pl/blog/prezydent-zlozyl-nowy-projekt-ustawy-o-rynku-kryptoaktywow-co-to-oznacza-dla-branzy)

**Market and competitors**
- [Crypto Briefing: Galaxy reports $11bn decline in crypto lending, Q2 2026](https://cryptobriefing.com/galaxy-crypto-lending-q2-2026-decline/)
- [Sygnum: MultiSYG launch with Debifi](https://www.sygnum.com/news/sygnum-and-debifi-launch-multisyg-as-bitcoin-client-collateral-exceeds-80-up-30-since-2023/)
- [finews: Sygnum vs AMINA loan books](https://www.finews.com/news/english-news/67701-sygnum-amina-2024-comparison-crypto-banks)
- [21bitcoin: pilot project for bitcoin-backed lending](https://21bitcoin.app/en/blog/21bitcoin-launches-pilot-project-for-bitcoin-backed-lending)
- [Payment & Banking: Crypto-backed lending and the Crypto Lending Pilot](https://paymentandbanking.com/crypto-backed-lending-wenn-bitcoin-zur-kreditsicherheit-wird/)
- [Börsen-Zeitung: VR Bayern Mitte to accept bitcoin as collateral](https://www.boersen-zeitung.de/banken-finanzen/vr-bayern-mitte-will-bitcoin-als-kreditsicherheit-akzeptieren)
- [Post Trade 360: Zodia Custody and Membrane Labs](https://posttrade360.com/news/infrastructure/zodia-custody-and-membrane-labs-give-leg-up-to-institutional-collateral-management/)
- [Yahoo Finance: Membrane Labs raises $20m](https://uk.finance.yahoo.com/news/crypto-prime-broker-membrane-labs-130000808.html)
- [Ledger Insights: SIX supports crypto as tri-party collateral](https://www.ledgerinsights.com/stock-exchange-group-six-now-supports-crypto-as-collateral-for-triparty/)
- [Blockrise: bitcoin-backed loans](https://www.blockrise.com/en/services/bitcoin-backed-loans)
- [Decrypt: JPMorgan to accept bitcoin and ether as collateral (report)](https://decrypt.co/345831/jpmorgan-to-let-clients-use-bitcoin-and-ether-as-collateral-for-loans-report)
- [Spaziocrypto: 174 public companies holding 1.18m BTC](https://en.spaziocrypto.com/bitcoin/bitcoin-treasury-2026-174-companies-1-18m-btc/)

**Wider European digital collateral**
- [ECB: Eurosystem brings central bank money to tokenised finance (Pontes launch), 21 Sep 2026](https://www.ecb.europa.eu/press/pr/date/2026/html/ecb.pr260921~e754847a7b.en.html)
- [ECB: Shaping the future of money, speech of 5 Nov 2026](https://www.ecb.europa.eu/press/key/date/2026/html/ecb.sp261105~6495a0df6f.en.html)
- [ECB: Tokenised money market funds, Macroprudential Bulletin](https://www.ecb.europa.eu/press/financial-stability-publications/macroprudential-bulletin/html/ecb.mpbu202604_04.en.html)
- [FinTech Futures: ECB launches Pontes](https://www.fintechfutures.com/tokenisation/ecb-launches-pontes)
- [Eurex: first CCP to launch DLT-enabled collateral mobilisation](https://www.eurex.com/ex-en/find/news-center/news/Eurex-Clearing-becomes-first-CCP-globally-to-launch-DLT-enabled-collateral-mobilization-service-4593252)
- [Markets Media: Eurex members mobilise collateral on DLT](https://www.marketsmedia.com/eurex-members-mobilize-collateral-on-dlt/)
- [Ledger Insights: HQLAx gets SEC no-action letter](https://www.ledgerinsights.com/dlt-collateral-mobility-platform-hqla%E1%B5%A1-gets-sec-no-action-letter-for-us-activity/)
- [ESMA: call for evidence on tokenisation of CCP collateral, 9 Oct 2026 (PDF)](https://www.esma.europa.eu/sites/default/files/2026-10/ESMA91-1505572268-4934_-_Call_for_evidence_tokenisation.pdf)
- [The Industry Spread: ESMA's call does not expand CCP collateral categories](https://theindustryspread.com/esma-call-does-not-expand-ccp-collateral-categories/)
- [FCA PS26/7: Progressing fund tokenisation (PDF)](https://www.fca.org.uk/publication/policy/ps26-7.pdf)
- [Taylor Wessing: DLT Pilot Regime reform](https://www.taylorwessing.com/en/insights-and-events/insights/2026/06/dlt-pilot-regime-reform)
- [Ledger Insights: finance ministers want DLT Pilot Regime cap raised to €300bn](https://www.ledgerinsights.com/eu-finance-ministers-wants-dlt-pilot-regime-cap-raised-to-e300bn-lagarde-objects/)
- [CoinDesk: BlackRock debuts tokenised access to $311bn of money market funds in Europe](https://www.coindesk.com/business/2026/08/04/blackrock-debuts-tokenized-access-to-usd311-billion-of-money-market-funds-in-europe)
- [The Fintech Times: Broadridge DLR monthly repo volume](https://thefintechtimes.com/broadridge-dlr-hits-8trn-monthly-repo-volume-with-28-yoy-growth/)
- [Finance Magnates: Broadridge expands tokenised repo platform to G7 securities](https://financemagnates.com/institutional-forex/broadridge-expands-351-billion-a-day-tokenised-repo-platform-to-g7-securities)
- [Canton Network: cross-border collateral mobility working group](https://www.canton.network/canton-network-press-releases/cantons-industry-working-group-advances-cross-border-collateral-mobility-on-canton)
- [Euroclear: pilot tokenising gold, gilts and Eurobonds](https://cf.euroclear.com/newsandinsights/en/Format/Whitepapers-Reports/dlt-to-enhance-collateral-mobility.html)
- [ICMA: European repo market surveys](https://www.icmagroup.org/market-practice-and-regulatory-policy/repo-and-collateral-markets/repo-market-surveys/)
- [CloudMargin: digital assets](https://www.cloudmargin.com/insights/cloudmargin-digital-assets)
- [Crowdfund Insider: Copper and FalconX introduce ClearLoop Loans](https://www.crowdfundinsider.com/2026/06/286008-copper-falconx-partner-to-introduce-clearloop-loans-merging-financing-with-off-exchange-settlement/)

**Other regions**
- [Crypto Briefing: Coinbase crypto-backed loans hit $2.3bn](https://cryptobriefing.com/coinbase-crypto-backed-loans-tokenized-deposits/)
- [First Citizens: The Bitcoin lending renaissance](https://innovation.firstcitizens.com/industry-insights/fintech/bitcoin-backed-lending)
- [The Real Deal: Fannie Mae opens door to crypto-backed mortgages](https://therealdeal.com/national/2026/03/27/fannie-mae-opens-door-to-crypto-backed-mortgages)
- [The Block: FHFA directs Fannie and Freddie to consider crypto](https://www.theblock.co/post/359708/fhfa-directs-fannie-mae-and-freddie-mac-to-explore-cryptocurrency-as-an-asset-for-mortgages)
- [The Industry Spread: Basel crypto capital rules split EU, UK and US](https://theindustryspread.com/basel-crypto-capital-rules-split-eu-uk-us-2026/)
- [CoinDesk: South Korea's first bank loans backed by bitcoin](https://www.coindesk.com/business/2026/10/12/south-korea-just-got-its-first-traditional-bank-loans-backed-by-bitcoin)
- [CoinDesk: Bank of Korea surveys banks on crypto shock exposure](https://www.coindesk.com/business/2026/11/03/south-korea-asks-its-biggest-banks-how-a-major-crypto-hack-would-hit-them)
- [Gulf Business: Standard Chartered and OKX crypto collateral pilot](https://gulfbusiness.com/?p=308348)
- [Cointelegraph: Japan's CRYL launches bitcoin-backed loans](https://cointelegraph.com/news/japan-cryl-bitcoin-backed-loans-6-million)
- [Cointelegraph: Lemon's bitcoin-backed credit card in Argentina](https://cointelegraph.com/news/bitcoin-backed-credit-card-argentina-lemon)

---

# Appendix: research notes

Raw findings behind the report, grouped by topic. Each note separates what sources said from what I inferred and what I could not find. Most findings come from search-result summaries; only the pages marked "read in full" were fetched and read.

## Notes: the repository

- Three files: `README.md`, `LICENSE`, `IMG_1464.JPG`. Fifteen commits, all README edits. No code.
- The diagram shows three parties: borrower (company or individual), custodian (holds bitcoin), bank (lends fiat). Handwritten note: on default the court sells the bitcoin; the coins are placed in custody as collateral, not sold to the custodian; "the only path to cash runs through the court".
- The README's roadmap line links the model to central banks adopting DLT, quoting the ECB speech of 28 August 2026.

## Notes: Jeonbuk Bank (South Korea)

**Findings**
- Jeonbuk Bank, a JB Financial Group unit, started bitcoin-backed won loans on 12 October 2026 ([CoinDesk](https://www.coindesk.com/business/2026/10/12/south-korea-just-got-its-first-traditional-bank-loans-backed-by-bitcoin)).
- A registered third-party custodian holds the bitcoin. The bank holds a credit claim only.
- Default is handled by court-ordered sale under revised civil enforcement rules in force from 1 October 2026. One outlet attributes the rules to the Supreme Court.
- Corporate borrowers only, bitcoin only, proceeds limited to operating funds.
- Collateral is valued with a weighted average of prices across several global exchanges.
- A bank representative told Chosun that at least one loan had been made. The borrower was not named.
- The Bank of Korea surveyed 18 banks and 13 brokerages on the impact of an exchange halt or price crash, with responses due 4 November 2026 ([CoinDesk](https://www.coindesk.com/business/2026/11/03/south-korea-asks-its-biggest-banks-how-a-major-crypto-hack-would-hit-them)).

**Gaps**
- Loan amount, rate, loan-to-value, custodian identity and technology supplier are all undisclosed.
- Sources use "Civil Execution Rules" and "Civil Enforcement Rules" interchangeably.
- No court-supervised liquidation has been reported.
- No second Korean bank has announced a similar product.
- Most coverage is crypto press; the bank has not issued an official statement.

## Notes: EU regulation of crypto lending

**Findings**
- MiCA recital 94 says the regulation should not address lending and borrowing of crypto-assets and does not prejudice national law. Article 142 requires the Commission to assess whether to regulate it.
- ESMA Q&A 2883, published 18 June 2026, confirms lending is not a MiCA service but general duties apply to CASPs that offer it: Art. 66(1) and (2) on fair conduct and communications, Art. 70(1) on safeguarding. Use of client assets needs prior express consent. Read in full via [Latham & Watkins](https://www.fintechanddigitalassets.com/2026/08/cryptoasset-lending-in-the-gaps-mica-esma-qa-2883-and-the-regulatory-future-of-cryptoasset-lending/), 17 August 2026.
- The Commission opened its MiCA review consultation on 20 May 2026. Part 4 covers DeFi, staking, and lending and borrowing. The Article 140 report is due 30 June 2027 and may come with a legislative proposal.
- The EBA responded on 24 September 2026. Under question 67 it recommends a cost-benefit analysis of (a) adding intermediated borrowing and lending to MiCA services and (b) rules for CASPs that give access to DeFi lending. Proposed measures: suitability tests, leverage limits, extra disclosure, possible prohibitions for some assets, and a certification regime for DeFi lending protocols. Lending passages extracted from the [PDF](https://eba.europa.eu/sites/default/files/2026-09/12cb4f01-0d51-46bf-a561-165ac486698f/EBA%20response%20to%20EC%20targeted%20consultation%20on%20MiCA%20review.pdf).
- The EBA notes two stablecoins dominate borrowing and lending, and lists risks: leveraged market making, collateral chains, contagion, consumer losses.

**Inferences**
- The EBA text is about lending *of* crypto-assets and stablecoins. A bank lending euros against pledged bitcoin is not its target, so that activity stays under national banking and credit law for now.

**Gaps**
- The Latham article names no national lending regimes.
- Sources disagree on the consultation deadline (31 August vs 30 September 2026). Law-firm sources say 31 August.

## Notes: bank capital rules

**Findings**
- CRR3 Article 501d transitional treatment: 250% risk weight for asset-referenced tokens, 1,250% for other crypto-assets including bitcoin, with exposure to that group capped at 1% of Tier 1 capital.
- The EBA published its final draft technical standards (EBA/RTS/2025/04) on 5 August 2025. For derivatives and securities financing, the counterparty's risk weight applies rather than the crypto weights.
- Basel SCO60 took effect 1 January 2026. The Basel Committee announced an expedited targeted review in November 2025 and said in February 2026 that it was progressing. No revised text found.
- One source says the US has proposed no SCO60 implementation and the UK implements Basel 3.1 from 1 January 2027 ([The Industry Spread](https://theindustryspread.com/basel-crypto-capital-rules-split-eu-uk-us-2026/)).
- Deutsche Bank's Pillar 3 report for June 2026 appeared in results, which suggests banks now disclose crypto exposures; I did not read it.

**Inferences**
- A bank that only holds a claim secured on bitcoin at a custodian has no direct crypto exposure, so the 1,250% weight should not apply to the loan.
- Bitcoin is not in the CRR list of eligible financial collateral, so it should give no capital relief.
- Both points are my reading and need a regulatory lawyer.

**Gaps**
- No confirmation that the Commission adopted the EBA standards as a delegated regulation.
- No BaFin or EBA statement on pledged crypto as credit risk mitigation.

## Notes: enforcement and pledge law by country

**France** (DLA Piper, read in full, dated 20 May 2025)
- DDADUE Law 5 published 2 May 2025. Articles: L. 211-38 (crypto-assets as collateral for financial obligations), L. 226-5 (pledge regime), modelled on the securities-account pledge in L. 211-20.
- Created by a signed declaration of the owner, which may be executed by smart contract. Effective between the parties and against third parties.
- The creditor can get a pledge attestation from its MiCA CASP. Pledges must be notified to the service providers.
- Enforcement terms can be agreed by contract or follow a Conseil d'Etat decree. Successive pledges rank by declaration date. The creditor has a right of retention.
- Not stated: whether out-of-court sale or appropriation is allowed, and whether the decree has been issued.

**Germany** (Noerr, read in full, dated 6 September 2024)
- Crypto-assets are "other property rights" under § 857 ZPO with §§ 829 ff.
- Kammergericht, 6 December 2023, 24 W 36/23: first appellate confirmation that crypto is seizable.
- OLG Düsseldorf, 19 January 2021, 7 W 44/20: transfer obligation enforceable under § 887 ZPO.
- OLG Köln, 26 June 2024, 11 W 15/24: transfer from wallets only the debtor controls is enforced under § 888 ZPO, with fines capped at €25,000 and coercive detention beyond that.
- Assets at a custodian or exchange: the transfer claim is seized by serving the order on the third party. Identifying and serving a foreign provider can be hard.
- Sale is normally by private sale (§ 857(5), § 844 ZPO). The court can order transfer to a bailiff's trust account for conversion to euro.
- A Bundestag research paper (WD 7-3000-010/25) points to a gap in §§ 929, 398, 413 BGB for crypto.
- Not stated: how long enforcement takes; whether reform is planned (Noerr said none was in sight in 2024).

**Poland**
- Crypto is not money and not a thing under art. 45 of the Civil Code. Practice treats it as a property right, enforceable under art. 909 ff. KPC ([Egzekucja i zabezpieczenia](https://egzekucjaizabezpieczenia.pl/2023/10/19/egzekucja-z-kryptowalut/)).
- A 2019 case study describes a bailiff seizing bitcoin by serving exchanges.
- Art. 805¹ KPC covers registered pledges found during enforcement but does not mention crypto.
- The President vetoed the crypto-assets act three times, the last on 11 June 2026; the Sejm failed to override on 4 September 2026. A law-firm blog says the President filed his own bill with KNF as supervisor.
- Not found: whether a registered pledge can be created over crypto; status of the President's bill.

**EU level**
- Bitcoin is outside the Financial Collateral Directive. The Commission's 2021 review consultation raised crypto eligibility; respondents cited legal uncertainty over possession and enforcement. No later outcome found.

## Notes: ECB and DLT

- Isabel Schnabel, "Central banks on-chain", Jackson Hole, 28 August 2026. Argues central banks should go on-chain; stablecoins complement but cannot replace central bank money because they cannot expand liquidity in stress.
- Smart contracts could automate collateral substitution, margin and returns.
- Pontes was due to launch in September 2026, linking TARGET services to market DLT platforms. Appia is a long-term programme with no date.
- The Eurosystem has accepted DLT-issued marketable assets in CSDs as collateral since 30 March 2026 ([ECB](https://www.ecb.europa.eu/press/pr/date/2026/html/ecb.pr260127_1~a946167ce1.en.html)).
- The speech does not address bitcoin or crypto-assets as collateral.
- Caveat: the fetch returned only a summary of the speech body, not the verbatim text.

## Notes: market size

- Galaxy Research, end-June 2026: total crypto-collateralised lending $56.16bn, down $11.33bn (16.78%) on the quarter and 40.13% from the $78.69bn peak in Q3 2025.
- Centralised lenders: $22.98bn, down 9.62%, mainly from a fall in Tether's secured loans.
- DeFi: $20.43bn, down 27.61%, third consecutive quarterly fall. Preliminary July figure about $21.94bn.
- Separate from that total: about $16.1bn of corporate debt used to buy digital asset treasuries.
- Figures come from secondary coverage of the Galaxy report, not the report itself.
- Corporate holders: 174 listed companies held 1,187,898 BTC on 12 May 2026 (Bitwise), of which Strategy held 818,869. In Europe: Bitcoin Group SE about 3,605 BTC, Capital B 3,135 BTC (May 2026), a Dutch listed company 1,111 BTC, Bitcoin Treasury Capital (Sweden) 174 BTC.
- One tracker lists 32 Western European companies with 113.5K BTC; methodology unclear, probably includes Gibraltar and Jersey entities.

## Notes: European lenders and pilots

- **Sygnum (CH).** Launched MultiSYG with Debifi on 23 October 2026: each borrower's collateral sits in a dedicated multi-signature wallet. More than one in five clients has a Lombard loan. Bitcoin is over 80% of pledged collateral, up from 63% in 2023. Loan book CHF 235m at end-2024, up from CHF 84m. Signing threshold not confirmed; an earlier plan said three of five.
- **AMINA (CH).** Loan book CHF 103m at end-2024, up from CHF 62m. Uses an Austrian entity for MiCA passporting.
- **Xapo Bank (Gibraltar).** Retail-focused bitcoin-backed loans. Europe is 56% and Latin America 29% of its loan volume.
- **VR Bank Bayern Mitte, 21bitcoin, Sopra Financial Technology (DE/AT).** Announced 20 October 2025 as Europe's first institutional, fully regulated bitcoin-backed loan product. 21bitcoin (FIOR Digital GmbH, MiCA-authorised by the Austrian FMA) handles client experience, custody and settlement. Sopra supplies the white-label platform. Illustrative example: €100,000 of bitcoin for a €50,000 loan. The bank's CEO said a permanent offer was not yet decided. 21bitcoin post read in full.
- **Sopra "Crypto Lending Pilot".** Described in a 12 September 2025 article by Sopra's product owner (read in full): middleware between core banking, custodians and trading venues; sub-wallets per client; real-time price monitoring; margin call, then top-up or liquidation; supports early repayment, refinancing and collateral swaps. No pricing, loan-to-value, bank names or legal mechanics given.
- **Non-bank euro lenders.** Blockrise (NL, parent MiCA-authorised by the AFM), Bit2Me (ES), Nexo (50% loan-to-value listed for bitcoin; custody through BaFin-authorised partners), Firefish (Prague, peer-to-peer, EUR/CZK/CHF/USDC, $1.8m seed), Debifi (non-custodial aggregator, 1.5% fee on collateral), Lendasat (founded 2024, seed March 2026).
- No major EU bank launch found. The 12-bank Qivalis consortium is a euro stablecoin project.

## Notes: software and infrastructure vendors

- **Membrane Labs (US).** Loan management with real-time loan-to-value tracking, margin-call workflows and audit trails; collateral monitoring across custodians. $20m Series A in October 2023 from Brevan Howard Digital, Point72 Ventures, Jane Street and others. Claims over $10bn in loan bookings. Integrated with Anchorage, BitGo, Fireblocks, Copper, Coinbase, Kraken and Zodia. Partnered with BitGo (February 2025) and Zodia Custody (11 August 2025). Added a risk engine in July 2025.
- **Trident Digital (US).** $8m seed in September 2023. Secured lending conduit built on Fireblocks, with a position portal and liquidation engine. Current status not verified.
- **Lygos Finance.** Emerged August 2025 by acquiring Atomic Finance. Non-custodial loans using discreet log contracts; aimed at institutions and wealthy individuals.
- **Zodia Custody.** Collateral Protect (2024) with Digital Prime's Tokenet: collateral in segregated cold wallets, with a notice-of-exclusive-control mechanism for the secured party. Backers include Standard Chartered and Northern Trust.
- **Fireblocks.** Reported 2,400+ clients and 80+ banks in production (third-party figures).
- **Taurus (CH).** Bank-focused platform covering custody, tokenisation and collateral management.
- **SIX (CH).** Digital Collateral Service accepts crypto alongside conventional collateral, mainly for bilateral and OTC trades.

## Notes: wider European digital collateral

**Central bank infrastructure**
- Pontes launched 21 September 2026 per the ECB press release; one trade publication says 23 September. 13 market participants and four DLT operators (Axiology, Cashlink, Clearstream, SWIAT); more are committed to connect.
- Settlement is through cash tokens on the platform or directly in T2. Cash finality stays in TARGET for now; DLT-based finality is planned later.
- Hours are 8:00–16:00 CET on business days, moving toward 24/7/365 by 2028.
- An ECB speech of 5 November 2026 says Pontes settled a €1bn ESM benchmark bond issued on DLT and that the World Bank and others are preparing DLT issuance.
- Eurosystem collateral eligibility for DLT-issued assets (from March 2026) covers only assets issued in CSDs. Tokenised fund shares are not covered.

**Clearing and collateral mobility**
- Eurex Clearing with HQLAx: first live transaction July 2025. HQLAx does not tokenise the asset; it locks it in place and issues a transferable digital collateral receipt. Clients of clearing members need not join HQLAx.
- HQLAx is backed by Deutsche Börse and banks including BNP Paribas, BNY, Citi, Goldman Sachs, HSBC and J.P. Morgan. It received an SEC no-action letter in May 2026 and plans to move from R3 Corda to Canton.
- Eurex said in June 2026 that tokenisation is "in production". A report says DLT-issued securities, including ESM bonds, would trade in Eurex Repo's GC Pooling and qualify as margin; launch date not confirmed.
- LCH has no announced tokenised collateral programme. It clears bitcoin derivatives through LCH DigitalAssetClear, which is not crypto collateral.
- Euroclear, Digital Asset and the World Gold Council ran a pilot tokenising gold, gilts and Eurobonds: 27 participants, 14 Canton nodes, 500 transactions, showing intraday margin calls can be met outside settlement hours. Sources date it to 2024. In February 2026 a Canton working group completed a cross-border intraday repo with tokenised gilts. Euroclear and Digital Asset have started a first phase on a Canton "Global Collateral Network".

**Regulation in motion**
- ESMA call for evidence ESMA91-1505572268-4934, 9 October 2026, responses by 15 January 2027. No new eligible categories proposed. Lists tokenised central bank money, stablecoins, e-money tokens and tokenised deposits as possible settlement assets, noting stablecoins may not be equivalent to cash.
- An EFAMA guide reads EMIR as not disallowing tokenised money market funds as collateral. That is an industry view.
- FCA PS26/7 (April 2026) confirms eligibility under UK EMIR for uncleared trades.
- Market Integration and Supervision Package, 4 December 2025: DLT Pilot Regime cap from €6bn to €100bn, all financial instruments in scope, simplified regime up to €10bn, exemptions from parts of MiFID II, MiFIR and CSDR. The Council wants €300bn with a possible rise to €500bn, and €50bn rather than €10bn for bank-run DLT settlement schemes. The ECB President is reported to object. Until adoption, Regulation (EU) 2022/858 limits apply.
- US comparison: the CFTC lets clearing organisations accept crypto-assets including stablecoins as initial margin under a minimal-risk standard.

**Tokenised funds**
- BlackRock, 4 August 2026: tokenised share classes of Institutional Cash Series funds ($311bn combined), built with J.P. Morgan Kinexys.
- Spiko (EUTBL, USTBL, UKTBL) and Franklin Templeton's Luxembourg fund together about $716m, roughly a quarter of European assets with a public token, per a secondary tracker.
- ECB Macroprudential Bulletin: tokenisation makes fund shares more usable as collateral; about 75% of EU-domiciled tokenised money market funds invest in European government bonds. A market-report site cites the ECB for global capitalisation of €7bn by February 2026.
- UBS Asset Management's uMINT was used as off-exchange collateral on Bybit in June 2026, a crypto-venue use.

**Vendors and volumes**
- Broadridge DLR 2026: average daily repo volume $351–368bn, monthly $6.9–8.0tn. No European breakdown and no named European bank volumes found.
- CloudMargin: won Risk.net's 2026 collateral management product award; markets its platform as ready for tokenised assets; earlier partnership with Ivno on tokenised cash and HQLA; a $15m Series B with Citi, Deutsche Bank and Deutsche Börse (undated in the source).
- Copper ClearLoop: company-reported $105bn monthly notional protected and $3bn monthly off-exchange settlement; ClearLoop Loans with FalconX announced June 2026; Kraken's FCA-authorised venue is connected.
- European repo market: €13,651.1bn in ICMA's 50th survey (published 26 March 2026, 59 respondents), up 9.8% from €12.4tn in June 2025. The figure is a sample-based minimum.

**Gaps**
- No 2026 volume figures for HQLAx or Eurex digital collateral.
- Nothing found on Fnality, SWIAT's commercial traction, Komainu Connect or Fireblocks Off Exchange.
- Tri-party collateral outstanding in Europe is in the full ICMA report, which I did not access.
- The ESMA paper itself was not read; points above come from coverage of it.
- No confirmed European bank accepting a tokenised money market fund as loan collateral.

## Notes: DORA

- Articles 28–30 govern ICT third-party risk. Article 30(2) sets baseline contract content; 30(3) adds requirements for critical or important functions, including unrestricted access, inspection and audit rights for the bank and its supervisor.
- The first 19 critical ICT providers were designated on 18 November 2025. A small software vendor would not be designated but still faces the Article 30 clauses.
- Sources are compliance-vendor blogs. Effect on sales cycles is my inference.

## Notes: other regions

**United States**
- Reports say Wells Fargo launched bitcoin-backed loans for institutional and wealth clients in Q4 2025, and that JPMorgan lends dollars against bitcoin and ether. Both rest on weak secondary sources. Earlier reporting (Bloomberg, September 2025) described the JPMorgan plan with a third-party custodian; JPMorgan already lent against bitcoin ETFs.
- Coinbase: $2.3bn in crypto-backed loans outstanding on 17 October 2026; fixed-rate, fixed-term bitcoin loans from 22 September 2026.
- Ledn closed a $188m bitcoin-backed asset-backed security with an investment-grade rating.
- FHFA directed Fannie Mae and Freddie Mac in June 2025 to consider crypto held at US-regulated exchanges as a reserve asset. In March 2026 Better Mortgage and Fannie Mae were reported to allow borrowing against Coinbase-held crypto for a down payment. Newrez launched non-agency crypto mortgages in February 2026. Other sources say formal guidelines still require conversion to dollars and most lenders cannot yet accept crypto.
- Nothing found on community banks, credit unions, OCC guidance or which vendors small lenders use.

**Asia and Middle East**
- Japan: CRYL offers bitcoin-backed loans up to ¥1bn; Daiwa Securities has referred clients to Fintertech's digital-asset-backed loans since October 2025. Both are non-banks.
- Singapore: Sygnum Singapore is the main bank route, per an affiliate-style guide.
- Hong Kong: only a promoted platform (Lendary) and a planned HashKey bank.
- UAE: Standard Chartered holds collateral in the DIFC for an OKX trading-collateral pilot. First Abu Dhabi Bank signed an MoU in December 2024 on lending against tokenised real-world assets. Bitcoin is on ADGM's accepted virtual assets list. No bank loan product found.

**Latin America**
- Lemon launched a bitcoin-backed Visa card in Argentina. Argentina's central bank was reviewing bank crypto services in early 2026; outcome not confirmed.
- Brazil: only comparison guides, no bank launch.
- El Salvador: an undated report of a state bank lending $1.5m against 200 bitcoin ATMs.
