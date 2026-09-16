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

Written for a seed investor or funding committee, the audience whose yes funds twelve months. A board cares about defensibility and economics first, so the case leads with the record and the risks lead with the kill.

**Thesis (1 sentence):** Product teams will pay for a coach that argues with their decisions using their own data and keeps score on whether it was right, and the score is the asset no competitor can backfill.

**The case:**
1. Why now: Two things became true in the last two years. Agents can read a team's live systems instead of being told about them, and experimentation platforms log hypotheses and results well enough that the coach can be graded on a buyer's own history before they buy. At the same time, producing product artifacts became free, so the only thing left worth paying for is whether the decision behind them was right. Nothing in the category measures that.
2. What's defensible: The record of predictions and outcomes. Freeze the product for a quarter with every competitor on the same model and it is the only asset in the comparison that grows, because it requires having been present at the decision, the override and the read-out. The coach sits upstream of the experimentation platforms, at the moment a decision is written, and reads from all of them, so a native review step inside one platform sees only the slice that reached it. ChatPRD can copy the objection next quarter; it cannot copy a record of whether objections were right. Pooled objection-type priors across customers are what nobody else can reach, and they are sequenced first.
3. The economics: $9,000 per team in year one, $500 a month plus $60 per experiment reviewed, at 94.9% gross margin. Contribution is $8,537 per team, inference is $116 of the $463 cost to serve, and the cascade is worth 19.5 margin points. A review costs 0.7% of the $25,000 experiment it checks. From year two the motion is self-serve with a 1.7-month payback; year one is founder-led design partners, priced at full rate once their backtest passes.

**The risks:**
1. Trust / failure modes: The coach might not beat the team's own judgment, in which case the product has collected the evidence against itself. The pre-registered backtest answers this before any money is spent on a customer: flagged experiments must succeed 20 points less often than unflagged, on two or three named partners, within eight weeks, published either way. A confident wrong citation is the other failure, and it degrades the product to decline-only rather than to confident error. The golden set is 10 rows today and 100 in the first four weeks; no reliability number ships to a buyer until it comes from a real history.
2. Scale / governance: One person holds every audit role, which is a stated single point of failure; the per-call invariants and daily golden run are automated, and the first hire is an eval owner at the first paying customer. Customer briefs are sent to Anthropic, so zero-retention and no-training terms are the first Guardrails item, signed before any partner connects. The person layer stays private to the individual, which keeps the EU AI Act tier at limited and costs one selling point.
3. Competitive: Statsig, Eppo or Amplitude could ship native pre-launch review within a year; the upstream position and the pooled priors are the answer, and the Network loop is sequenced ahead of everything else for that reason. ChatPRD copying the mechanism is expected and not a kill: the answer is collecting outcomes faster than they do.

**The ask:** Twelve months of one founder full-time and a design-partner program of three to five teams. Modelled at $250,000 loaded founder cost, an assumption the founder replaces with the real figure, plus $25,000 for outside counsel on data-use terms and platform, the ask is **$275,000**. Break-even at that cost is 30 teams at $8,537 contribution each. What the money buys by month three is the backtest result, published whether it passes or not, and the kill point is week eight after the first partner connects. If it fails, the spend to that point is under a quarter of the ask.

## M1 Baseline vs. Now
*Your 3-sentence AI strategy from Module 1 vs. what you'd say now:*

**M1 baseline:**

> AI made producing product artifacts basically free, so the scarce thing isn't output anymore, it's judgment about what's worth building. We're going after the judgment layer, the decision itself, before anything gets written. We win it by coaching inside the system where the work already lives, so the reasoning gets committed instead of lost, and the decisions that pay off become the signal that makes the coaching better.

**Now:**

> Every team can generate product artifacts for free, so the only thing left worth paying for is whether the decision behind them was right, and nothing in the category measures that. We build a coach that argues with a team's decisions at the moment they are written down, using the team's own history, attaches a falsifiable prediction to every objection, and keeps score when the read-out arrives, graded by how good the counterfactual was. The asset is the record, not the advice: a competitor with the same model can copy the objection next quarter but cannot backfill a quarter of predictions and outcomes, and that record is what makes the coach right more often and the renewal an executive decision.

The delta. Module 1 said "judgment layer" and "the signal that makes the coaching better," both of which were aspirations. The version above names the mechanism (a scored prediction), where it fires (the moment a decision is written, upstream of any experimentation platform), how honesty is kept as the surface widens (attribution grading), the asset (the record) and why it holds (it cannot be backfilled). Module 1's third sentence promised compounding. Module 5 found the loop open and Module 6 sequenced what closes it.
