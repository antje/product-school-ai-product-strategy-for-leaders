# Golden Dataset & Reliability Contract

## The contract

What product-coach promises, how it is measured, and what happens when it breaks.

| Metric | Target | Measurement | Alert Threshold |
|--------|--------|-------------|-----------------|
| Accuracy | 90% | Weekly, full golden set, rule judge, segmented by `prompt_version`, `model` and call type | <85% pages the founder, triggers gold-set audit |
| Hallucination rate | <1% | Same weekly run. Cited ids checked against the corpus deterministically, plus a safety rubric on misdescribed results, invented numbers and unsupported mechanism claims | >2% routes all reviews to decline-only, pages the founder |
| Latency p95 | <20s | Continuous, per review. 60s function ceiling, and a timed-out review is a failed review | >30s p95, or completion below 97% over 20 reviews, pages the founder |
| Drift velocity | <5pp decay per 4 weeks | 4-week rolling pass rate on the full golden set, against a frozen prompt version and model id | >10pp decay pins to the last verified model, triggers gold-set audit |

**HITL architecture:** a fabricated citation on write, an endorsement whose precedents disagree, or a 4-week pass rate decaying more than 10 points routes to the founder. Refusals and declines never escalate. Reviewer corrections feed back into the weekly gold-set audit.

**Defensible bands:** Accuracy 88 to 93 (not 99) · Hallucination <1% · Latency <20s · Drift <5pp per 4 weeks

**Consequence patterns:** Page the founder · Route to decline-only · Pin to last verified model · Gold-set audit

**Golden set:** 300 rows at v1, 10 today. The gap is the main risk in this document and the arithmetic is below.

**One thing this contract does not promise.** It says nothing about whether the advice is good. Accuracy above measures whether the coach makes the call the golden set expects, against a corpus we built. The product's commercial claim, that its predictions beat a team's own judgment, needs a customer's real history and is not asserted here.

---

## What is real here, and what is synthetic

Everything below rests on this, so it goes first.

**Synthetic.** The 50 experiments, the company they belong to, every hypothesis, and every "actual lift" figure. They describe a fictional bookkeeping product. So does the rule that decides their outcomes, which was written by the same person building the coach.

That last point is the one that matters. The coach is being tested against an answer key its own author wrote. When it finds the pattern, that means it found a pattern someone planted, not that it understands how products behave.

**Real.** The model calls. Fifteen of them on 2026-08-29, logged with model, cost and outcome. The objections the coach produced, the declines it produced, and the fact that its output could be mechanically scored without a human interpreting it. Those are real behaviours of a real system on fake inputs.

**What follows from that split.** A synthetic corpus can test whether the machinery works. It cannot test whether the advice is any good. An accuracy number computed against your own answer key measures obedience to yourself, which is why the contract above reports accuracy and withholds the hit rate.

The judgment backtest, on a customer's real history, is the gate that unlocks the commercial claim. It does not exist yet.

### The assumptions this exercise runs on

| Assumption | Why it is being made | What it costs |
|---|---|---|
| The corpus reflects how early-funnel experiments actually behave | No real corpus is available, and the exercise needs labelled outcomes | If the planted rule does not resemble reality, the coach is being trained and tested on a fiction |
| One hidden rule is enough structure | A single rule can be verified by recomputation, so the test is reviewable | Real product histories have many overlapping effects and much more noise |
| The rule judge is the right grader | An objection carries an explicit metric, direction and threshold, so it can be checked without interpretation | It only works because the corpus supplies a clean actual lift. Real read-outs are messier |
| 50 corpus experiments and 10 golden rows are enough to test behaviour | It is what exists today | The contract's targets need 300 rows to be enforceable. At 10 the alert thresholds sit inside the noise |
| The coach never sees the rule | It is stated in a comment, never placed in a prompt or on a record | Verified by inspection, not enforced by a test. A future refactor could leak it |

### The ground-truth rule, stated openly

Outcomes in the corpus were assigned from this rule. It is written in the corpus file so the evaluation is reviewable, and it is never placed in a prompt, never passed to the model, and never stored on an experiment record. The coach receives only the fields a real analytics export would carry.

- **Early funnel** (activation for new workspaces, trial conversion). Mechanisms that change how a user *feels* (personalization, social-proof, urgency, incentive) land flat or negative. Mechanisms that remove work between the user and their own data (reduce-steps, time-to-value, defaults) land solidly positive.
- **Established accounts** (retention, renewal, expansion, reactivation). The same feeling-led mechanisms work fine here.
- **education, notification, pricing-display** are noise, mixed both ways.

Recomputed from the data rather than asserted, by `node scripts/check-corpus.mjs`:

| Slice | n | Mean actual lift |
|---|---|---|
| new-workspaces x activation, feeling-led | 12 | -0.18pp |
| new-workspaces x activation, friction-led | 12 | +4.14pp |
| established accounts, feeling-led | 6 | +3.35pp |

**Separation on the early funnel: 4.33pp.**

That third row is why the corpus tests something rather than nothing. A coach that concludes "personalization is bad" has overfit to the planted rule, and the corpus catches it, because the same mechanism works on established accounts. Catching that is a real property of the test. It still says nothing about whether the coach would read a real company's history correctly.

## The four outcomes, defined

The rows below use four words for what the coach can do, and they are not interchangeable.

| | When it happens | Model called | Prediction made | Ledger effect |
|---|---|---|---|---|
| **Refuse** | The brief is not reviewable: no read date fixed before launch, volume cannot power the effect, a guardrail with no numeric bound, or a target asserted rather than derived | No | No | Nothing recorded |
| **Object** | The history contradicts the hypothesis. Carries a metric, a direction and a numeric threshold | Yes | Yes, lands below X | Scorable. Resolves right or wrong |
| **Endorse** | The history supports the hypothesis, on named precedent | Yes | Yes, lands above X | Scorable. Resolves right or wrong |
| **Decline** | The history says nothing either way | Yes | No | Recorded `not-scored`. Never moves the hit rate |

Refuse is a judgment about the input, and it costs nothing because it is arithmetic. Object and Endorse are both commitments that get graded. Decline is a pass.

### Why Endorse exists, and why it is not just "accept"

The obvious fourth state is "accept, this looks fine." That state is dishonest, because it would rest on the *absence* of a contradiction. Absence of evidence supports no claim, and a prediction built on it would enter the hit rate carrying nothing.

Endorse is narrower. It fires only on **positive precedent**: prior experiments in this team's history with the same mechanism and the same audience that landed above the threshold. Named, counted and cited, exactly as an objection cites the cases that contradict.

**The bar is deliberately higher than for objecting**, because the failure is worse. A wrong objection costs a team an experiment they should have run. A wrong endorsement manufactures confidence and costs them one they should not have, which is the Air Canada shape. Conditions:

1. At least three prior experiments match on mechanism and audience.
2. Their mean lift is above the threshold being predicted.
3. No matching experiment in the same slice contradicts.
4. If any condition fails, the outcome is Decline, never Endorse.

### What it changes

Run against the 49 parsed corpus experiments:

| | Object only | With Endorse |
|---|---|---|
| Object | 31% | 31% |
| Endorse | not available | 33% |
| Decline | 37% | 37% |
| **Scorable share of reviews** | **31%** | **63%** |

The ledger fills **2.1x faster**, and that is the point. A hit rate near 70% needs about 36 labelled calls. At 31% scorable, a 50-experiment customer backtest yields about 15 labels, so three customers are needed. At 63% it yields 31, so roughly one.

It also changes what a review is worth. Roughly a third of reviews previously returned nothing, and "clear to proceed" is thin. A cited endorsement is the evidence a product manager needs to defend a decision in a review, which is the second value stream the pricing rests on.

## Golden Dataset Spec

Ten rows drawn from the synthetic corpus rather than written fresh for this exercise, so the inputs at least match what the running product actually processes. Each is a brief the coach is shown blind, with the read date withheld. Expected output is the call a correct reading produces. Every row is scored by the rule judge in `lib/ledger/scoring.ts` unless stated otherwise.

| # | Input | Expected Output | Edge Case? | Judge Type |
|---|-------|----------------|-----------|-----------|
| 1 | ex-004, personalized dashboard hero, personalization, new-workspaces, activation, expects +8.0pp | Object. Predict activation lands below +2.0pp. Cite the feeling-led early-funnel pattern | N | rule |
| 2 | ex-007, reduce-steps on new-workspace activation, expects +3.0pp | **Endorse.** Predict above +2.0pp. Cite the friction-led early-funnel precedent | N | rule |
| 3 | ex-026, urgency banner, new-workspaces, activation, expects +5.0pp | Object. Predict below +2.0pp. Actual was -2.4pp | N | rule |
| 4 | ex-046, referral credit for invites, incentive, established accounts | **Endorse.** Feeling-led works on accounts that already get value, so the early-funnel pattern must not be generalised | **Y** | rule |
| 5 | ex-015, time-to-value, new-workspaces, expects +5.0pp | **Endorse.** Predict above +2.0pp. Actual +6.1pp | N | rule |
| 6 | ex-064, urgency, new-workspaces, expects +3.0pp, read out inconclusive | Object, and the prediction must still be scorable. Inconclusive is not a get-out | **Y** | rule |
| 7 | **ex-044**, sample data replaced by the user's first import. Labelled time-to-value, but the hypothesis text reads as a presentation change | **Endorse.** The mechanism is friction removal despite the wording. The live coach objected instead and was wrong by 9.2pp | **Y adversarial** | rule |
| 8 | A brief with no read date fixed before launch | Refuse before any model call. `no-read-date` | **Y adversarial** | rule |
| 9 | A brief whose weekly volume cannot power the stated effect inside the window | Refuse before any model call. `underpowered`, with the arithmetic shown | **Y adversarial** | rule |
| 10 | A brief on `education` mechanism, which the corpus treats as noise | Decline. No pattern exists to object from, and inventing one is the failure mode | **Y adversarial** | rule + LLM |

**Edge cases:** 6 of 10 (rows 4, 6, 7, 8, 9, 10). **Adversarial:** 4 of those (rows 7, 8, 9, 10). The Golden Dataset Builder scores this Strong on coverage at a 90/10 rule-to-LLM judge mix.

### Why these rows

Row 4 is the anti-overfit case. A coach that learned "personalization is bad" fails it.

Row 7 is a miss the live product actually made, though against a synthetic answer key. On 2026-08-29 the coach objected to ex-044, predicted the lift would land below +2pp, and it landed +7.2pp. Recorded **Wrong** in the ledger. The reasoning was substantive rather than lazy, distinguishing mechanisms that create value from ones that present it, which is what makes the miss worth keeping. It also exposed a genuine ambiguity: the experiment is labelled `time-to-value` but its hypothesis text describes a presentation change, so the coach reasoned from the prose while the hidden rule scored by the label. **Left unfixed on purpose.** Softening the corpus so the coach looks better is the self-grading failure this product exists to avoid, and it is a live temptation precisely because the corpus is ours to edit.

Rows 8 and 9 test the refusal layer rather than the judgment layer, and they must fire without a model call.

Row 10 tests the hardest behaviour to get right: declining when there is no pattern. A coach that always finds something to say is worse than useless, because every objection carries a prediction that enters the hit rate.

**Coverage gaps identified:**

1. No row covers a brief where the mechanism label and the audience both sit in the noise category. Expected behaviour is undefined.
2. No row covers two experiments in the corpus that contradict each other. The coach's behaviour under conflicting precedent is untested.
3. All rows are single-metric. Briefs with a primary metric and a guardrail metric that move in opposite directions are not covered.
4. The corpus is one fictional company with one hidden rule. It tests whether the coach can find a pattern, not whether it can find a *different* pattern in a different company. That gap closes only with real customer backtests.

**Growth path:** 10 rows today, 300 at v1. New rows arrive without anyone writing them. Every resolved call in the ledger is a labelled row by construction. Every customer backtest contributes about 50 rows, of which roughly 32 are scorable once endorsements count.

## Confidence UX Design

**Approach:** all three, in a fixed order. A deterministic refusal layer runs first, then tiered confidence on what survives, then a human trigger on the bottom tier.

The order matters because the refusals cost nothing and never vary. A brief that cannot be reviewed should not reach a model, and the product's opinions should be identical every time rather than varying with sampling temperature. A refusal that only fires sometimes is not a refusal.

**Layer 0, before any model call.** Four deterministic checks, implemented as arithmetic in `lib/coach/preflight.ts`:

| Code | Fires when | Shown to the user |
|---|---|---|
| `no-read-date` | No read date fixed before launch | The check, the remedy |
| `underpowered` | Weekly volume cannot detect the stated effect in the window | The check, the remedy, and the sample-size arithmetic |
| `guardrail-without-boundary` | A guardrail is named with no numeric bound | The check, the remedy |
| `undevised-target` | The success target is asserted rather than derived | The check, the remedy |

Sample size per arm uses n ≈ 16·p(1−p)/δ², the standard planning approximation at 80% power and 5% two-sided significance. The arithmetic is shown so the PM can check the work.

**High confidence (>90%):** the call is stated directly with its prediction and the cited past experiments. No hedging. The coach's hit rate appears here only once it comes from that customer's own resolved calls, never from the synthetic corpus. This applies to both objections and endorsements, and the prediction is written into the ledger either way.

**Medium confidence (70-90%):** the call is shown with the confidence figure visible. Copy shifts from "this will land below X" to "on this team's history this pattern has landed below X in n of m cases." The prediction is still recorded and still scored. Softening the language does not soften the accountability.

**Endorsements are held to a higher bar than objections at this tier.** A hedged objection is a caution, which is cheap to be wrong about. A hedged endorsement is encouragement, which is not. Below 90% confidence an endorsement degrades to Decline rather than softening.

**Low confidence (<70%):** **decline, do not hedge.** The coach says it has nothing to go on and names what it looked at. No prediction is made, and per `lib/ledger/scoring.ts` a decline is recorded as `not-scored` and never moves the hit rate.

A low-confidence call still carries a prediction, and a prediction entered at low confidence pollutes the only number the product sells. Declining is cheaper than being wrong.

**User control surface:**

| Control | Available | Detail |
|---|---|---|
| Adjust the threshold | No, not at v1 | A customer-tunable threshold makes the published hit rate incomparable across accounts |
| See the reasoning | Yes | Every objection shows the past experiments it drew on, with their results |
| Correct and override | Yes | Accept the sharpened hypothesis or keep the original. Both are recorded |
| Corrections feed the model | Yes, indirectly | Overrides plus outcomes become labelled rows. They tune retrieval and objection-type priors, not a per-customer model |

## Why these numbers

**The contract needs 300 rows and today there are 10.** That is the gap to close before any of the targets above can be enforced.

| Rows | Precision on a 90% measurement | One flip moves the rate |
|---|---|---|
| 10 | ±18.6 points | 10.0 points |
| 50 | ±8.3 points | 2.0 points |
| 150 | ±4.8 points | 0.7 points |
| **300** | **±3.4 points** | **0.3 points** |

At ten rows the alert threshold sits inside the noise. Three hundred also allows segmenting by call type at about 100 each, which matters because a coach that classifies objections well and endorsements badly would post a fine blended number.

Three hundred is the same figure the worked support-copilot example uses, and the module's guidance is 100 to 500.

**Where the 300 come from**, all but the last available without a customer:

| Source | Rows | How |
|---|---|---|
| Corpus experiments as they stand | 50 | One row each, already labelled |
| Reworded variants | 50 | The same experiment with prose that points away from its mechanism, which is the ex-044 failure class |
| Refusal cases | 40 | Four preflight codes, ten variations each |
| Constructed adversarial | 30 | Overfit traps, contradicting precedent, conflicting guardrails |
| Resolved ledger calls | accumulating | Every scored call is a labelled row by construction |
| Customer backtests | ~50 each, ~32 scorable | The first three close the gap |

**Accuracy and hit rate are two different numbers.**

Accuracy above is whether the coach made the *correct call* on a golden row, where the correct call is known. That is the same kind of measurement as a support copilot's 92%, and 90% is the right band. It is not 99% because the coach already misreads a brief whose wording contradicts its category, which row 7 records.

The **hit rate** is different: of the predictions the coach commits to, how many come true. That runs near 70%, and it is not a weak number. Predicting how an experiment lands is genuinely uncertain, and a product manager working unaided is close to a coin flip. Seventy percent on forecasts and 90% on classification are both strong, and they are measuring different things.

The hit rate is the product's commercial claim and it is deliberately not in this contract, because it cannot be measured against a corpus we wrote.

**Why hallucination is under 1% and not zero.** A fabricated citation is only one kind, and it is the easy one: an id either exists or it does not, so that sub-check is deterministic and does run at zero tolerance on write. The harder kinds are a real id described wrongly, an invented number, or a mechanism claim the cited rows do not support. Those need a rubric and cannot be driven to zero. 

The stakes are still the Air Canada stakes, and worse in one respect. Air Canada's bot invented a policy. This product would be inventing a fact about the customer's own history and handing it back to them as evidence.

**Why drift is measured as decay rather than flips.** Ten rows is a coarse instrument, since one flip moves the pass rate ten points. A rolling four-week trend absorbs single-run noise and still catches a provider changing behaviour behind a stable model name. It gets sharper as the row count grows toward 300.

**Why there is no auto-rollback.** There is no second qualified model to roll back to until the vendor swap gate from the kill-switch audit has been run. What fires instead is routing every review to decline-only, which is degraded-safe.

**What the synthetic corpus limits.** Accuracy is measured against a rule we wrote, so it proves consistency rather than correctness. No accuracy figure ships to a customer or a sales conversation until it comes from a real backtest on a history nobody here authored. The other three metrics hold either way, because they are properties of the system rather than of the answers.

## HITL Architecture

**Trigger conditions**, evaluated in order. The first match wins.

1. Any preflight refusal fires. Return to the PM with the check and the remedy. No model call, no human.
2. Confidence below 70%. Decline, recorded as `not-scored`. No human.
3. A fabricated citation is detected on write. Block the call, route every review to decline-only, page the founder.
4. An endorsement clears its three-precedent bar but the precedents disagree with each other. Downgrade to Decline and queue for audit.
5. The 4-week rolling pass rate decays more than 10 points. Pin to the last verified model id and page the founder.
6. A resolved call comes back Wrong on a golden row. Add to the weekly audit queue.

**Who the human is.** At current scale, the founder. That is honest rather than embarrassing, and it is what makes the queue-shrinking design a requirement rather than a preference.

**Why the queue shrinks rather than scaling with usage.** Only conditions 3, 4 and 5 reach a person, and all three are rare by construction. Condition 1 is arithmetic and condition 2 is a decline, so the two highest-volume paths never touch a human. Review volume therefore tracks failures rather than usage, which is the difference between the crutch pattern and the feature pattern.

**Corrections feed back.** Every human review produces a labelled row that joins the gold set. This is the same mechanism as the Correction loop in the moat work, and it is the only place a human touching the system makes the system permanently better rather than just fixing one output.

## Red-Team Findings

**Found by the product itself, though against a synthetic answer key.** The coach objected to ex-044 and was scored wrong by 9.2 percentage points. The failure was not sloppiness. It read the hypothesis prose, which describes replacing demo numbers with real ones, as a presentation change, when the corpus labels the mechanism as friction removal. The distinction it was reasoning about is the right one and it applied it to the wrong side.

**Why this one survives the synthetic problem.** Most findings from invented data are worthless, because they only show the coach disagreeing with its author. This one is different. The failure is that the coach classified a mechanism from natural language and got it backwards, and that failure mode does not depend on the labels being true. Any brief whose wording and category disagree will break it, and real briefs are written by people who do not think in mechanism categories at all.

**The fix, not yet built.** Classify mechanism as an explicit intermediate step with its own confidence, rather than inferring it inside the call. When the classifier's confidence is low, decline. That converts a silent wrong answer into a visible decline.

**Adding Endorse makes this failure worse before it makes it better.** ex-044 should now be an endorsement, and the coach objected. Under the old three-state design a mechanism misread produced a wrong objection. Under four states it can produce a wrong endorsement, which is the more expensive direction. That is why the endorsement bar is three matching precedents and 90% confidence rather than the 70% floor everything else uses.

**A second finding, from reading the contract above.** The decline-rate band of 30 to 50% had no empirical basis. It was derived from the corpus flag rate, which is a property of the rule we planted rather than of anything real. It has been moved out of the enforceable contract and into the list of things that need a customer.

**What has not been red-teamed, and this is the honest headline.** Nobody outside has tried to break this. Every coverage gap listed above was found by inspecting a corpus I wrote, against a rule I wrote, using a judge I wrote. That is the weakest form of red-teaming there is, and no amount of care inside that loop escapes it.

The first genuine test is a customer backtest on a history whose pattern nobody here planted. Until that runs, this document describes a system that behaves correctly, and says nothing about whether it is right.
