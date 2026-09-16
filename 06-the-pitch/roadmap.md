# Three-Horizon Roadmap & Board Pitch

## Roadmap

Built from a 32-item backlog assembled from the commitments in the five components, mapped to a component and a horizon, then thinned. The cadence is the AI-compressed one: H1 is four weeks, H2 one to three months, H3 three to six. One founder builds all of it, so H1 is held to what gates everything else and nothing more.

### Horizon 1 — Now (0-3 months)
*Quick wins. Ship with existing capabilities.*

Four weeks, nine items. Everything here either gates the backtest or has to exist before the first partner's data arrives.

| Initiative | Component | Metric | Confidence |
|-----------|-----------|--------|-----------|
| Analytics connector for the first design partner's platform, OAuth read-only | Bet | First partner's full experiment history read end to end | H |
| Split craft knowledge from customer context at the schema | Moat | Cross-account reads impossible by construction, verified by test | H |
| Override capture: a stated reason the user goes on record with, both sides on the scoreboard | Moat | Override-with-reason rate at or above 70% of overrides | H |
| Read-out delivery: the result finds the person who made the call, one action to close | Moat | Loop-close rate at or above 80% within seven days of read-out | H |
| Attribution grade on every read-out: A controlled, B rollout, C launch | Moat | Every call carries a grade; grade C never enters the hit rate | H |
| Data-use and sub-processor terms: Anthropic zero-retention, no training, pooling limited to objection-type outcomes | Guardrails | Signed by every partner before their connector is enabled | H |
| Retention and deletion terms, stated at signup | Guardrails | IP hashes 30 days, call records 24 months, deletion within 30 days | H |
| Golden set to 100 rows, with a calibration check published alongside the run | Contract | 100 rows; predicted confidence against observed accuracy reported | M |
| Customer ROI one-liner: reviews x objection rate x hit rate x experiment cost, over $9,000 | Margin | The buyer-side number exists before the first buyer conversation | H |

Two of the nine are documents, not code. The override and read-out metrics are the ones the moat rests on, because a record of unexplained dismissals and unresolved predictions compounds nothing.

### Horizon 2 — Next (3-9 months)
*Bets. Requires new capabilities or integrations.*

One to three months. Each row carries a hypothesis and the condition under which it stops.

| Initiative | Component | Hypothesis | Kill criteria | Confidence |
|-----------|-----------|------------|---------------|-----------|
| Pre-registered backtest on two or three design partners | Bet | Brief-only calls with history cut at date beat the team's own: flagged experiments succeed at least 20 points less often than unflagged | If the gap is under 20 points on two partners with at least 12 flagged each by week 8 after first connection, stop and publish the miss | M |
| Ten buyer conversations at $500 a month plus $60 a review | Margin | Heads of product at teams running 50+ experiments a year pay the hybrid price and grant pre-sale data access | If fewer than 3 of 10 say yes to both price and access by week 4, reprice or drop the entry gate before recruiting anyone | M |
| Design-partner program, three to five teams | Bet | Teams will sign pooling terms and connect analytics before any subscription starts | If fewer than two teams are connected under signed terms by week 8, stop recruiting; the bet is unfunded | M |
| Recursive Learning return path: the record calibrates confidence at review time | Guardrails | Returning resolved calls by objection type lowers calibration error without suppressing objections | If calibration error is not lower on the same golden run by week 10, or objection rate falls, keep the record display-only | M |
| Cascade: triage, retrieval and daily help to small models and embeddings, 96/4 | Margin | 96% of requests run on small models with no loss against the golden set, worth 19.5 margin points | If golden pass on cascaded routes falls more than 2 points below frontier-only by week 6, roll routes back up one tier at a time | M |
| Prompt and model change gate in CI, plus the `decline-only` runtime state | Guardrails | A bad release is blocked without a human present, and a fabricated citation degrades the product to silence rather than confident error | If the gate produces more than one false block per ten releases by week 8, loosen the thresholds rather than the gate | H |
| Confidence interval field on read-outs and the ambiguity rule | Guardrails | Ambiguous read-outs route to manual resolution and none is auto-scored | If any grade A read-out with the CI spanning the threshold is auto-scored, the rule is not enforced | H |
| Record prominence in the objection panel: cited experiments and per-type hit rate inline, plus a line at submission that preflight is free | Guardrails | Users stop re-checking the coach against another model when the evidence is in front of them | If more than half of partners still report re-checking in interviews by week 8, the trust gap is somewhere else | M |
| Secret and PII screen on brief input before transmission | Guardrails | Nothing sensitive leaves the boundary through a pasted brief | Zero secrets in partner transmission logs; no kill, this is a control | H |
| Provider abstraction and routing layer, with the swap gate | Moat | A model swap is a two-week job and the gate catches a bad one | If a candidate model is not within 15 points on three pooled backtests, stay pinned | M |
| Record export: a shareable decision-quality view, aggregated by decision, never by person | Guardrails | The team-level record is what carries the renewal, and it can be shared without exposing anyone | If no partner shares an export outside the product within six weeks of shipping, drop it | M |

### Horizon 3 — Bet (9-18 months)
*Moonshots. High uncertainty, high potential.*

Three to six months. The vision these serve: a new team's first objection is already better than a general model's because it carries what every other team's record taught, the backtest runs without anyone from us in the room, and the coach proposes the next experiment instead of only reviewing the one in front of it. Each row names what has to be true before it starts.

| Initiative | Component | What must be true first | Confidence |
|-----------|-----------|-------------------------|-----------|
| Pooled cold-start layer: craft priors for a new account's first thirty days | Moat | Schema split enforced, pooling terms signed by at least three partners, grades flowing, and a minimum account count stated before any statistic leaves an account. This is the asset a native review step inside an experimentation platform cannot reach, and it is the one to protect if budget is cut | M |
| Self-serve onboarding: the backtest runs on OAuth without a person | Margin | Five partners onboarded by hand, the backtest passing unattended on at least two platforms, the connector generalized. Year two by design; moves CAC to $1,200 and payback to 1.7 months | M |
| Monitoring add-on: watch metrics and draft candidate experiments | Bet | The backtest passed, the return path working, and a hit rate that beats the team. Proposing experiments before the calls are proven is the Orchestrator step taken too early | L |
| Person layer: a coaching profile visible only to the individual | Guardrails | The team-level record exists, and never-upward is enforced in code rather than policy, or the EU AI Act tier flips | L |

### Dropped

**ChatPRD deep link.** The shadow audit chose partner over build for drafting. The roadmap review found the specific integration pushes the coach's sharpened hypothesis into the one competitor with a Correction loop, in exchange for a trust signal that record prominence already answers. The generic action stays: the user can open the sharpened hypothesis in whatever drafting tool they use. No partner integration with any drafting tool is built.

### Unmapped

| Initiative | Why it's unmapped | Decision |
|---|---|---|
| `/jtbd`, `/product-status`, `/board-review`, `/decision` coaches | Items from the local skills toolkit. None produces a scorable prediction or feeds a loop, so none touches a component | Cut from this backlog. They belong to the toolkit's own queue |

The four rows exposed a decision the strategy had not made: what the toolkit is to the product. The answer is that the toolkit is the free top of the funnel and not part of the product. Fifteen coaching skills run locally inside a product manager's own agent, store nothing and cost us nothing, which is why the governance scope excludes them. A person who reviews decisions with the toolkit is the person who will want the review that keeps score. The toolkit keeps its own backlog, stays free, and every skill ends by pointing at the product for the one thing it cannot do: remember whether it was right.

## AI Evaluation

A cold evaluation of the README, run against the six lenses from the course, before the Module 6 revision.

| Dimension | Score |
|---|---|
| Bet Validation | 4/5 |
| Capability Assessment | 3/5 |
| Impact Analysis | 3/5 |
| Defensibility | 3/5 |
| Pricing Alignment | 3/5 |
| Trust & Reliability | 4/5 |
| Governance & Scale | 4/5 |
| Gap Identification | 4/5 |
| **Overall** | **3/5** |

The summary line: "unusually disciplined thinking with unusually thin evidence. The reasoning earns a 4; the evidence holds it at 3."

**Biggest risk named:** the backtest is the whole bet and, as specified, could be passed by accident or softened after the fact. No numeric threshold, no leakage control, no named data source, no date.

**Four findings changed the strategy.** The encroachment defense failed as written: an experimentation platform adding a review step inside its own flow would see the brief, the objection, the override and the read-out natively, so the coach moved upstream to the brief and roadmap stage and the platforms became read-out sources. The A/B-only scope made the market small, so read-outs are now graded by attribution quality and flag rollouts enter the record as grade B. "Sold self-serve" contradicted a cost model where 65% of COGS is human onboarding, so year one is a founder-led design-partner program and self-serve is year two. And every subscription now starts only when the team's own pre-registered backtest passes, which answers willingness to pay by making the first dollar conditional on proof.

**Two findings are accepted and open.** Customer-side ROI is unquantified and the segment is unsized; both are H1 and H2 items above. Data-use terms with the model provider are absent; that is the first Guardrails item in H1.

**One finding is contested.** The evaluation reads the backtest as a prediction claim rather than a decision-change claim. It is, and the Contract says so: accuracy measures the call against a known answer, the hit rate measures whether predictions come true, and the commercial claim that the coach beats a team's judgment is not asserted until a real customer's history says so.

## Board Pitch

A slide version of this section is at [`final-presentation.html`](../final-presentation.html) in the repo root, served live at [antje.github.io/product-school-ai-product-strategy-for-leaders/final-presentation.html](https://antje.github.io/product-school-ai-product-strategy-for-leaders/final-presentation.html), eight slides with arrow-key navigation. The text below is the spoken version.

For a partner at a seed fund writing $500k to $1M first checks into B2B software, an ex-product leader who has run experiments and has passed on a dozen AI copilots for PMs. They lead the deal and sell it to two partners on a Monday, so the thesis has to survive without the founder in the room.

**Thesis (1 sentence):**
Product teams will pay for a reviewer that objects to their decisions before they ship and keeps score on whether it was right, because a verified record of calls and outcomes is the one asset neither a foundation model nor an experimentation platform can ship as a feature.

**The case:**
1. Why now: Two things became true in the last two years. Agents can read a team's live systems instead of being told about them, and experimentation platforms log hypotheses and results well enough that the coach can be graded on a buyer's own history before they buy. Neither was true before, and the second is what makes a scoreboard something you can sell on rather than promise. Demand is already priced: ChatPRD sells AI coaching to product managers at $15 a seat, and the category has no flywheel, because ChatPRD scores 8/20 on the same data loops. The window is twelve months: the experimentation platforms could add a review step inside their own flow within a year, and once they do, the only position left is upstream of them. And the asset is time-gated. A record of predictions and outcomes cannot be bought, scraped or generated after the fact; it requires having been present at the brief, the override and the read-out. Every quarter of read-outs that goes unrecorded is gone.
2. What's defensible: The Correction loop and the record it produces (M2, Data Flywheel 9/20, Correction 4 of 5). Every other copilot's corrections say a user changed the wording; ours say the user was wrong, and the read-out proves it. The freeze test is the argument for the Monday partners: freeze every competitor on the same model for a quarter and product-coach is the only asset in the comparison that grows, because templates, content breadth and in-experiment optimization all go static. On "why won't Statsig ship this": they can ship a review step, and they probably will, inside a year. What a native step cannot reach is what we sit on: decisions made without an experiment, the cross-source context around each one, and pooled objection-type priors across customers. The coach sits at the brief and roadmap stage, reads from every platform, and treats them as read-out sources. The honest caveat: Domain Context is 1 of 5 today because the record holds only controlled experiments. The fix is attribution grading, so rollouts and flagged releases enter as grade B, which grows the scorable surface about tenfold, and it is a Horizon 1 item rather than a shipped one. The moat is a design and a sequence today, not a stock of data.
3. The economics: 94.9% gross margin in year one at $9,000 per team per year, 97.8% by year three once onboarding is self-serve (M3). COGS is $463 per five-seat team per year, and inference is only $116 of it; 65% is human onboarding, which is the founder's time in year one. Revenue per inference dollar is about 78x. The floor: at the rejected $30-a-seat price the margin is 74.3%, so pricing can be wrong by a lot and the business still clears. Pricing is $500 per team per month plus $60 per experiment reviewed; a review costs 0.7% of the $25,000 experiment it checks. Ninety-six percent of requests run on small models and embeddings, worth 19.5 margin points; only the priced review goes to frontier. No sales team: year-one CAC is founder time, and from year two self-serve payback is 1.7 months against 28.7 at seat pricing with a rep. Contribution is $8,537 per team per year. The model does not carry a salary, so break-even is 30 teams at a $250k loaded founder cost. The number still missing is the customer's ROI one-liner (reviews x objection rate x hit rate x experiment cost); it is Horizon 1 and exists before the first buyer conversation.

**The risks:**
1. Trust / failure modes: The front-page version: the coach objects to an experiment citing a precedent that never existed, the team kills a $25,000 test on the strength of it, and the fabricated citation is found later. The contract (M4) is built around exactly that. Hallucinated citations under 1%, alert at 2%; accuracy 90%, alert under 85%; drift under 5 points per four weeks; measured weekly against the golden set. A fabricated citation is the one event that always reaches a human, and it drops the product into decline-only automatically, so a bad model degrades to silence rather than confident error. Below 90% confidence an endorsement degrades to Decline, because encouragement costs more to get wrong than caution. Two things not softened: the golden set is 10 rows today, so a 90% measurement carries ±18.6 points and the contract is not enforceable until it reaches 100 in Horizon 1 and 300 at v1. And the live coach has already been wrong: it misread ex-044's mechanism from its prose and missed by 9.2 points. That miss stays in the corpus, because hiding it would be the self-grading failure the product exists to prevent.
2. Scale / governance: At 10x usage the cost that breaks is not inference, it is the human onboarding that is 65% of COGS; that is why year one is capped at three to five hand-onboarded teams and self-serve is a year-two design decision rather than a hope. The review queue does not scale with usage: only fabricated citations and disagreeing precedents escalate, refusals and declines never do, so the queue tracks failures and shrinks as the corpus grows (M5). The coach argues and never acts; it holds no write path into any customer system, no component calls another's tools, and there is no agent chain to own. Two decisions stay human: scoring an ambiguous read-out and shipping any prompt or model change, gated at 90% golden pass and 1% hallucinated citations in CI. EU AI Act: limited risk, on the condition that a person's coaching profile stays private to that person. Exposing it upward is Annex III performance monitoring, so we gave up the per-person visibility a leader would buy and kept the team-level decision record that carries the renewal. The named defect: Recursive Learning does not compound yet. The product records every override and resolves every prediction, then never returns the record to the reasoning. That return path is a Horizon 2 item with its own kill rule.
3. Competitive: There is no competitive kill criterion in the strategy, and it is better to say that than dress one up. The scenario that kills us is not a platform shipping a review step; it is the backtest failing, because a coach whose calls do not beat the team's own judgment loses to any native step on the same model, sitting closer to the data. So the kill is the pre-registered backtest: brief-only calls, history cut at the brief date, on two or three named design partners, at least 12 flagged experiments each; flagged experiments must succeed at least 20 points less often than unflagged, by week eight after first connection. Under 20 points on two partners, we stop and publish the miss. Two earlier gates precede it: fewer than 3 of 10 heads of product saying yes to both the price and pre-sale data access by week four means reprice or drop the entry gate; fewer than two teams connected under signed terms by week eight means stop recruiting, the bet is unfunded. The backtest is also the commercial gate: no subscription starts until a team's own backtest passes, so the customer's first dollar is conditional on proof, and the founder's kill decision precedes the spend on both sides.

**The ask:**
$275,000, one founder, twelve months. $250,000 is the modelled loaded founder cost, an assumption the founder replaces with the real figure, and the ask moves with it; $25,000 is outside counsel on data-use and sub-processor terms plus platform. It is sized to the test, not to the fund, and deliberately below this partner's usual check so a week-eight kill is a cheap write-off rather than a fund story. Quarter one runs the pre-registered backtest on two or three named design partners and publishes the result by month three whether it passes or not. If it fails, under a quarter of the money is spent. If it passes, the remaining nine months build the loop inputs (override capture, read-out delivery, attribution grades, the schema split), the Recursive Learning return path, and the design-partner program to five teams at $9,000 a year each once their own backtest clears. Paused if funded: the monitoring add-on that proposes experiments, the person-level coaching layer, and self-serve onboarding, which waits until five partners have been onboarded by hand. No sales hire, in this round or the plan. Two things the strategy cannot give you today: the first five customers are not named, and the coach has not yet been shown to beat any team's judgment. The round exists to settle both by week eight.

### Presenter notes

**Opening line, said first:** "Every AI copilot for PMs you have passed on sells advice; we sell the scoreboard, and no customer pays a dollar until our calls beat their own judgment on their own experiment history."

**If there are only sixty seconds:** We review a product team's decisions before they ship, using the team's own numbers, and we record whether we were right when the read-out arrives, which is the one asset a foundation model or an experimentation platform cannot ship as a feature because it requires having been in the room. The risk is that we have not yet proven our calls beat the team's, the golden set is 10 rows, and the first five customers are not named, so the whole bet is a pre-registered backtest on two or three design partners with a 20-point threshold and a week-eight stop. $275k funds one founder for twelve months; if the backtest fails you find out by month three with under a quarter of it spent.

**The first question they will ask:** "Name the first five customers." The answer that holds: "I cannot name five today, and I have written the gate instead of pretending: ten heads of product at teams running fifty-plus experiments a year by week four, at least three saying yes to both the price and pre-sale data access or I reprice, and at least two connected under signed terms by week eight or I stop recruiting and the bet is unfunded."

**Handle before the meeting, not in it:** the ask is below this partner's check size. Say up front that the round is sized to the test so a kill is cheap, or the meeting opens on check size instead of the thesis.

## M1 Baseline vs. Now
*Your 3-sentence AI strategy from Module 1 vs. what you'd say now:*

**M1 baseline:**

> AI made producing product artifacts basically free, so the scarce thing isn't output anymore, it's judgment about what's worth building. We're going after the judgment layer, the decision itself, before anything gets written. We win it by coaching inside the system where the work already lives, so the reasoning gets committed instead of lost, and the decisions that pay off become the signal that makes the coaching better.

**Now:**

> Every team can generate product artifacts for free, so the only thing left worth paying for is whether the decision behind them was right, and nothing in the category measures that. We build a coach that argues with a team's decisions at the moment they are written down, using the team's own history, attaches a falsifiable prediction to every objection, and keeps score when the read-out arrives, graded by how good the counterfactual was. The asset is the record, not the advice: a competitor with the same model can copy the objection next quarter but cannot backfill a quarter of predictions and outcomes, and that record is what makes the coach right more often and the renewal an executive decision.

The delta. Module 1 said "judgment layer" and "the signal that makes the coaching better," both of which were aspirations. The version above names the mechanism (a scored prediction), where it fires (the moment a decision is written, upstream of any experimentation platform), how honesty is kept as the surface widens (attribution grading), the asset (the record) and why it holds (it cannot be backfilled). Module 1's third sentence promised compounding. Module 5 found the loop open and Module 6 sequenced what closes it.
