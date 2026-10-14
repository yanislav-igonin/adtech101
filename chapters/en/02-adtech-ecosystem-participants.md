---
id: ch-02
type: chapter
part: I
chapter: 2
slug: adtech-ecosystem-participants
title: "AdTech Ecosystem Participants"
language: en
status: reviewed
toc_requirements: ["2.1", "2.2", "2.3", "2.4", "2.5", "2.6", "2.7", "2.8", "2.9", "2.10", "2.11", "2.12", "2.13", "2.14", "2.15", "2.16", "2.17"]
prerequisites: [ch-01]
---

# AdTech Ecosystem Participants

## The Core Idea: roles, not boxes

In the first chapter we saw the two economic sides of the market: `advertiser`[^g-advertiser] creates demand[^g-demand], while `publisher`[^g-publisher] creates supply[^g-supply]. Many systems may sit between them, but the map of AdTech[^g-adtech] becomes clear once you look not at company names but at **roles** — logical functions in an advertising deal.

`Role`, `company`, and `product` are different levels:

- **role** — the function performed here;
- **company** — the organization that signs the contract; it may perform several roles;
- **product** — a specific offering of that company: a UI, an API, a managed service, or a set of tools.

Therefore a logo cannot be placed in one cell of the map forever: one product suite may buy media, sell access to inventory[^g-inventory], deliver ads, and build reporting, while one role may be split by the advertiser between its own team and several providers.

To analyze any role, use a single card (role card):

| Question | What it clarifies |
|---|---|
| What problem does the role solve? | The reason it exists |
| Who is the customer? | Who uses the product or service |
| Who is the beneficiary? | Who receives the economic benefit |
| Who is the payer?[^g-payee-payer] | Who pays for media or the service under contract |
| What data comes in and goes out? | The technical boundaries of the function |
| What decision is made or executed? | The actual work, not a marketing label |
| How does money move? | Media money, a separate fee, or no payment in this flow |

Customer, beneficiary, and payer may not coincide: a media buyer[^g-media-buyer] works in a platform's UI, the advertiser receives the benefit, and the agency[^g-agency] pays the invoice. Without this distinction, contracts, data flows, and reports are hard to read.

Let's fill in the card for the main economic participant. The advertiser wants to change the knowledge or behavior of an audience, funds the campaign[^g-campaign], hands over the goal, the budget, and the **creative**[^g-creative] — the ad material itself: an image, a video, or text — and receives outcomes and reporting. The advertiser is usually the beneficiary and the source of money, but may delegate the operational work and the payment of specific invoices to an agency. In a specific campaign some roles will be absent and others will hide behind a single contract — which is why the card is more useful than a linear diagram of seventeen mandatory boxes.

## Who sets the goal and who executes the purchase

**Advertiser** — an organization that funds advertising for the sake of a business outcome. For an app with a paid subscription, the outcome may be immediate — a trial or a paid subscription — or more delayed: knowledge of the product and the willingness to consider it later. The advertiser defines the goal, the acceptable spend, the audience, and the success criteria; on its own or through contractors, it decides where to buy media.

This gives rise to two advertising orientations:

- **brand advertising**[^g-brand-advertising] primarily changes awareness, consideration, or perception — knowledge of the product, consideration of it, and attitude toward it;
- **performance advertising**[^g-performance-advertising] is driven around a measurable action or outcome and the cost of obtaining it: registrations, trials, installs, or purchases.

These are not two mutually exclusive kinds of companies. One subscription app may simultaneously run a video campaign to introduce the brand and an acquisition campaign optimized for trials. Moreover, a single user may first encounter the product through brand advertising and later respond to performance advertising. What differ above all are the goal, the evaluation horizon, and the expected evidence of results.

**Publisher** — an organization that owns or operates a media environment where advertising opportunities[^g-ad-opportunity] arise: a website, an app, a game, or a video service. The publisher defines placements[^g-placement] and serving rules, provides context and access to inventory, receives delivery information, and earns publisher revenue[^g-publisher-revenue]. Its interest is to sell opportunities profitably enough while preserving the quality of the product and the user experience.

Between the advertiser's business goal and the technical purchase there often stand people and service organizations:

- **agency** — a contractor company that plans or executes marketing and media work on behalf of the advertiser. It may develop strategy, prepare creatives, choose channels, launch campaigns, manage reporting, and sometimes handle payments;
- **media buyer** — a person, team, or function that chooses media, platforms, and purchase terms, allocates spend, and sets up campaigns. A media buyer may work inside the advertiser, inside the agency, or inside another buying organization.

Agency and media buyer are not synonyms: the former is an organization and a contractual role, the latter an operational function. A media buyer is also not a DSP[^g-dsp]: a human formulates and configures decisions, while a DSP executes part of the buying workflow at scale.

| Role | Problem and beneficiary | Typical payer | Data in | Decision or result |
|---|---|---|---|---|
| Advertiser | Achieve a business outcome; the advertiser itself receives the benefit | Source of media spend[^g-media-spend] and many service fees | Business goal, constraints, customer data | Campaign goal, budget, success criteria |
| Publisher | Monetize the media environment; the publisher receives the benefit | Usually not a payer in the media sale; may pay technology providers | Placements, context, inventory rules | Available opportunities, delivery rules, publisher revenue |
| Agency | Perform the work for which the advertiser does not build a team or expertise | Advertiser; sometimes the agency acts as payer on downstream invoices | Brief, budget, creatives, results | Plan, settings, execution, and reporting |
| Media buyer | Turn the goal and budget into concrete purchases | Not a separate payer as a function; paid by employer/client | Campaign goals, available channels, reports | Choice of media and platforms, allocation, and settings |

The advertiser may buy media with its own team (in-house), hand the buying entirely to an agency, or split the responsibility. This determines the control boundary: who has access to the account, raw data, and the contract; who is responsible for setup mistakes; and who can reallocate spend.

## Who connects demand and supply

Neither the advertiser nor the publisher can negotiate every short-lived impression with thousands of counterparties by hand. The next group of roles solves the scale problem, but does so from different sides:

```text
advertiser ───────────── direct buying ─────────────→ publisher
advertiser ───────────── ad network ────────────────→ publisher
advertiser / buyer → DSP ⇄ exchange / SSP functions → publisher

advertiser ad server and publisher ad server can support different branches;
no single line is a mandatory universal pipeline.
```

**Ad network**[^g-ad-network] aggregates supply and/or demand and sells a managed media offering. The buyer usually chooses the available offer, the goal, and the constraints, while the network takes on a significant share of traffic distribution and publisher relationships. The pricing axis belongs to the network: it usually sets its own price for the buyer and itself decides from which publisher, and at what price, to take the impression, so the purchase price is opaque to the buyer. The network usually accepts media money and settles with supply partners; the specific commercial model depends on the contract.

**DSP (Demand-Side Platform)** — a buying platform that helps a media buyer evaluate and purchase opportunities from several supply sources according to campaign rules. The customer is an advertiser, an agency, or another buyer. The key trait: the decision is made for each incoming opportunity separately and in real time — in programmatic[^g-programmatic] this is a bid[^g-bid] in an auction[^g-auction]; the deep comparison with networks is in chapter 16, auction mechanics in chapter 18.

**SSP (Supply-Side Platform)**[^g-ssp] — a sell-side platform for the publisher. It describes available opportunities, gives demand sources access to inventory, and helps manage its sale. The publisher is the primary customer and beneficiary, although the SSP often takes its payment within the media settlement[^g-settlement] — the actual movement of money between participants, as distinct from the invoice as the issued claim.

**Ad exchange**[^g-ad-exchange] — a transaction layer or function that connects buyers and sellers and performs matching or an auction. An exchange is not necessarily a separate company between DSP and SSP: exchange and SSP functions are often combined in one product. A useful distinction is this: the SSP represents the publisher's sell-side workflow, while the exchange performs the automated transaction function between the parties themselves.

**Ad server**[^g-ad-server] selects, delivers, and records ads according to given campaign or inventory rules. It is not just a CDN with files: a CDN may deliver creative bytes, while an ad server applies rules and creates an observable point of delivery.

- An advertiser ad server helps the buyer side manage creatives, their delivery, and event recording independently of the specific place of purchase.
- A publisher ad server matches available demand sources and manages delivery on the publisher's inventory.

Detailed `order`, `line item`, priorities, and serving mechanics will appear in chapter 11.

| Role | Primary customer | Data in | Decision or result | Money relationship |
|---|---|---|---|---|
| Ad network | Advertiser/agency; also needs supply partners | Campaign constraints, creatives, aggregated supply | Managed distribution and reporting | Usually a principal[^g-principal-agent]: sets its own price for the buyer, accepts media money, and settles with publishers itself at a price opaque to the buyer |
| DSP | Advertiser, agency, media buyer | Campaign settings, creatives, opportunity signals | Buying decision, access to supply, reports | Paid by the buyer: media cost plus a platform fee, usually a percentage of spend |
| SSP | Publisher | Inventory rules, opportunity and context signals | Access to demand, sale decision metadata, reports | Paid by the seller side: usually retains a share (revenue share[^g-revenue-share]) of the clearing price (the final auction price) before paying the publisher |
| Ad exchange | Buyers and sellers or their platforms | Opportunity descriptions and buying responses | Matching/transaction result | Usually a share of the clearing price on the sell side; if the exchange is combined with the SSP, this is one deduction, not two |
| Ad server | Advertiser or publisher | Campaign/inventory rules, creatives, delivery signals | Selection, delivery, and event registration | Usually a separate license or usage fee from its own customer; media money usually does not pass through the ad server |

## Who measures and verifies

A platform that sold or bought media sees only its own measurement[^g-measurement] points and is at the same time interested in the outcome of the deal. Therefore advertisers and publishers may connect cross-cutting providers. They are not a mandatory link in the commercial chain, although their code may execute inside creative delivery: integrations receive events and return separate conclusions.

**Attribution provider**[^g-attribution] matches available advertising touchpoints — for example, an impression[^g-impression] or a click[^g-click] — with outcomes such as a registration or a purchase, and applies rules for assigning credit. The result answers the question "to which source, under the chosen rules, is this conversion[^g-conversion] attributed?", not "was the advertising the true cause of the action?" Attribution does not prove causality.

**MMP (Mobile Measurement Partner)**[^g-mmp] — a mobile-specialized category of measurement and attribution providers for app acquisition, installs, and in-app outcomes. Its primary role is to match available acquisition signals with app events and to give the advertiser a consistent picture across all media sources. The motive is clear: without an independent party, each network attributes the install to itself under its own rules, and the sum of self-reported installs usually exceeds the real number; an MMP applies uniform rules to all sources. An MMP is not a synonym for product analytics: product analytics primarily studies behavior inside the product, whereas an MMP links acquisition to advertising sources. Technical details of SDKs, install matching, postbacks, and platform privacy restrictions belong to chapters 27–29.

**Verification provider**[^g-verification] creates a separate point for evaluating the conditions and quality of ad delivery. Depending on the integration, it may analyze available delivery, render, placement, context, and quality signals and return verification results to the advertiser, the publisher, or a platform. Verification is broader than fraud detection alone — the questions may also concern the serving environment — but it is not absolute truth: the completeness of its conclusions depends on the environment, the available signals, and the methodology.

For a single app ad, the systems may receive partially overlapping events:

```text
impression / click signals ─┬→ buying and selling platform reports
                            ├→ attribution provider / MMP
delivery / context signals ─┴→ verification provider

install / subscription events → MMP and the advertiser's systems, if integrations allow it
```

Discrepancies between reports are not necessarily an error. Platform reporting answers what the platform itself observed; the MMP applies its own attribution rules to acquisition and app events; the verification provider evaluates the delivery conditions available to it. These are different questions and different measurement boundaries.

## Who supplies, organizes, and connects data

The word `data` hides several different tasks. Supplying an external dataset, managing an audience segment[^g-audience-segment], storing a customer record, and matching identifiers are not one role. A separate operation is **activation**[^g-activation]: handing data or a segment to a system that will apply it to real impressions, for example a buying platform for targeting[^g-targeting]; before activation, a segment remains a record in storage.

| Role | Customer and data in | Persistent state | Result and activation | What the role itself does not do |
|---|---|---|---|---|
| **Data provider**[^g-data-provider] | Advertiser, publisher, or platform; its own or collected datasets | Datasets, attributes, or segments | Data for permitted activation, decisioning, or analysis | Not required to store its client's customer record or make media decisions |
| **DMP**[^g-dmp] | Advertising/marketing team; audience data and campaign signals | Audience profiles and segments in the chosen product model | Segmentation and activation through advertising integrations | Not required to be the system of record for the full customer lifecycle |
| **CDP**[^g-cdp] | Advertiser; first-party events and customer data from the product, CRM, and other systems | Persistent unified customer record | Customer profiles, events, and segments made available to downstream systems | Not required to buy media or assign attribution credit |
| **Identity provider**[^g-identity-provider] | Advertiser, publisher, or platform; identifiers from permitted sources | A mapping or identity graph within the specific solution | Linked or translated identifiers for activation and measurement | Does not create consent, does not register all events, and does not prove the identity of a real person |

**Data provider** sells or provides datasets, attributes, or audience segments. The customer pays for an additional signal: for example, a context classification or an audience attribute that can be used legally and technically.

**DMP (Data Management Platform)** — an advertising-oriented system for managing, segmenting, and activating audience data. **CDP (Customer Data Platform)** maintains a persistent unified customer record and makes customer data available to downstream systems. The historical rule "DMP — cookies and anonymous data only; CDP — PII only" is unreliable: modern products and deployment models overlap. The working boundary lies in the primary task and the record model — advertising audience activation versus a durable customer record.

**Identity provider** links or translates identifiers for permitted activation, measurement, and adjacent use cases. For example, one integration may know the advertiser's customer ID while another knows a platform-specific ID; the identity function helps establish a permissible correspondence.

Distinguish four operations:

```text
identity    → links users, devices, or their identifiers
tracking    → records events
attribution → assigns conversion credit according to rules
consent     → expresses permission or a choice in a separate governance/legal context
```

An identity provider does not create legal permission merely by matching. Specific identifiers, resolution algorithms, and privacy rules will be covered in chapters 24 and 40–42.

In the running example, the subscription app sends first-party trial and subscription events to the CDP to maintain the customer record. A DMP or platform integration can form and activate a permitted audience segment. An identity provider helps link the necessary identifiers between permitted environments, and an external data provider can enrich the segment with an additional attribute.

## One campaign: data and money kept separate

Let's assemble the roles in one scenario. A subscription app is advertised inside a mobile game. The advertiser has hired an agency; a media buyer at the agency runs acquisition through a DSP. The game's publisher provides the opportunity through an SSP whose product also includes an exchange function (in mobile in-app, this sell-side role is often performed by a mediation platform or an SDK network — chapter 12). An MMP measures mobile acquisition, a verification provider optionally evaluates delivery, and the data/identity functions are connected only where they are needed and permitted.

This is one possible composition, not a mandatory chain: the advertiser could have bought media directly or through an ad network, and several roles could have belonged to one company or been absent altogether.

### Data flow

```text
advertiser / media buyer
  ── campaign goal, settings, creative metadata ──→ buying and serving systems

publisher app
  ── opportunity, placement, format, permitted context ──→ sell-side and decision systems

decision systems
  ── the selected ad + delivery metadata ──→ publisher app

publisher app and participating systems
  ── impression / click / delivery events ──→ reporting, MMP, verification

subscription app / advertiser backend
  ── install, trial, subscription events ──→ MMP, CDP, and advertiser reporting
```

Not every participant receives every event: the set depends on integrations, the environment, contracts, and privacy/platform restrictions. The event flow is often bidirectional and asynchronous; it need not repeat either the creative path or the financial relationships.

### Money flow

The direction is the same as on the map in chapter 1: the advertiser's media spend goes through the buying channel to media sellers and becomes publisher revenue, while technology providers receive separate fees. What is new here is who exactly pays whom in a typical programmatic setup:

| Who pays | Whom | For what | Kind of money |
|---|---|---|---|
| Advertiser | Agency | Planning and running campaigns | Usually a fee or a percentage of spend; sometimes inside the media invoice |
| Advertiser or agency | DSP | Purchased media and use of the platform | Media cost plus a platform fee, usually a percentage of spend |
| DSP | Exchange / SSP | Won opportunities at the clearing price | Media money |
| Exchange / SSP | Publisher | Sold opportunities | Publisher payout[^g-publisher-payout]: clearing price minus the sell-side revenue share |
| Advertiser | MMP | Attribution and acquisition measurement | SaaS[^g-saas-pricing] or usage fee |
| Advertiser | Verification provider | Evaluation of delivery conditions | Usage fee, usually by volume of measured impressions |
| Publisher or advertiser | Its own ad server | Selecting, delivering, and recording ads | Usage or SaaS fee |
| Advertiser or agency | Data provider | Audience segments or attributes | Often a data CPM[^g-cpm] — a surcharge on media cost, billed through the DSP |

The advertiser is the economic source of media spend, but the contractual payer on the DSP's invoice is often the agency: the advertiser sees one consolidated invoice, while the money is then distributed across several contracts. Invoice and settlement also differ: the former is the issued claim, the latter the actual payment, and the amounts may not match because of adjustments. The deductions of intermediaries[^g-intermediary] at each step and the path of a hypothetical `$100` are the subject of chapter 4.

Finally, the **invoice path**, the actual **settlement path**, the creative delivery path, and the HTTP/event path may have different endpoints: the creative may come from an ad server or a CDN, and a conversion event may go asynchronously to the MMP and never return through the SSP.

## Why one company occupies several places on the map

Companies combine roles because of acquisitions, shared infrastructure and data, and the desire to offer a managed service, a single workflow, reporting, and contract. When one company controls several consecutive levels of the value chain, this is called **vertical integration**[^g-vertical-integration]; in this course we also speak of combining roles.

For the customer, combining roles means fewer integrations, lower operational overhead, faster data exchange, and one UI for setup and reports. But the same properties create risks:

- a conflict of incentives when one side simultaneously represents buyer and seller;
- opacity of fee boundaries and internal money transfers;
- an advantage for its own supply or demand in decisioning;
- self-measurement, when the executor of the deal evaluates its quality itself;
- difficulty exporting data and comparing external alternatives.

Imagine a hypothetical Platform X: it sells a packaged media offering, gives the media buyer DSP-style controls, delivers creatives, and shows an attribution report in one UI. Calling it merely a "DSP" is not enough. Let's break the suite into functions:

| Platform X function | Separate role card |
|---|---|
| Packages and sells access to media | Ad network-like managed offering |
| Selects opportunities according to campaign rules | DSP-like buying/decisioning |
| Delivers the creative and records delivery | Ad serving |
| Links touchpoints with outcomes | Attribution/measurement |

A shared login and a shared invoice do not make these functions one role. This is the way to analyze an unfamiliar AdTech company: first list the roles it performs, then fill in for each one `problem → customer → payer → data in/out → decision → money` and ask where the fee arises and whose interests it may conflict with. Only then does it make sense to compare vendors by their labels.

## Common Confusions

- **"A brand advertiser and a performance advertiser are different kinds of companies."** No: these are orientations of activity. One company can run both.
- **"Ad network is the old name for a DSP."** A network sells managed media aggregation at its own price; a DSP leaves the decision on each opportunity to the buyer's rules. Real suites may combine both functions.
- **"An SSP and an exchange must be different companies" or "they are complete synonyms."** Both extremes are wrong: the sell-side workflow and the transaction function are distinguishable, but often combined in one product.
- **"An MMP knows the true reason for an install, and a verification provider sees the absolute truth of an impression."** Both work with available measurement points and methodologies. Attribution credit is not causality; a verification result is limited by the integration.
- **"Data provider, DMP, CDP, and identity provider are four names for the user base."** They respectively supply data, organize audience activation, maintain the customer record, and link identifiers.

## What to Remember

1. The AdTech map describes logical roles, not a mandatory list of companies.
2. The advertiser funds advertising for the sake of an outcome; the publisher creates the media environment and opportunities.
3. Brand and performance are orientations of goals and measurement that one advertiser may combine.
4. An ad network sells media at its own price; a DSP decides on each opportunity with a bid under the buyer's rules and charges the buyer a platform fee; an SSP serves the sell-side workflow and usually retains a share of the clearing price; an exchange performs the transaction function.
5. Advertiser-side and publisher-side ad servers apply different sets of rules, although both roles select, deliver, and record ads.
6. MMP/attribution, verification, data, and identity are cross-cutting functions, not mandatory links in the commercial chain; they usually receive a fee for their function rather than a share of media money.
7. The data flow, the delivery path, the invoice path, and the settlement path need not coincide.
8. One company may perform several roles; vertical integration reduces integration friction but raises questions about incentives, fees, data boundaries, and measurement independence.

## Check Yourself

1. Why can a subscription app simultaneously be a brand and a performance advertiser?
2. How does a media buyer differ from an agency and from a DSP?
3. Why might a publisher use an SSP and a publisher ad server in one flow without considering them one role?
4. A hypothetical suite offers publishers an SSP, a publisher ad server, and verification in one UI under one invoice. Which separate role cards need to be filled in, and where does such a combination create a conflict of interest?

## Sources and Further Reading

1. [IAB Tech Lab — Programmatic Auction Definitions](https://iabtechlab.com/programmatic-auction-definitions/)
2. [UK Government — Online Advertising Programme consultation](https://www.gov.uk/government/consultations/online-advertising-programme-consultation/online-advertising-programme-consultation)
3. [Competition and Markets Authority — Intermediation in open display advertising](https://www.gov.uk/find-digital-market-research/online-platforms-and-digital-advertising-market-study-appendix-m-intermediation-in-open-display-advertising-2020-cma)
4. [Adjust — What is a Mobile Measurement Partner](https://www.adjust.com/glossary/mobile-measurement-partner-mmp/)
5. [IAB Tech Lab — Open Measurement SDK](https://iabtechlab.com/standards/open-measurement-sdk/)
6. [IAB Tech Lab — Identity Solutions Guidance and Recommended Practices](https://iabtechlab.com/wp-content/uploads/2024/05/Identity-Solutions-Guidance-FINAL.pdf)
7. [CDP Institute — What is a CDP?](https://www.cdpinstitute.org/what-is-a-cdp/)
8. [Oracle Marketing Cloud — CDP vs CRM vs DMP](https://blogs.oracle.com/marketingcloud/cdp-vs-crm-vs-dmp)
