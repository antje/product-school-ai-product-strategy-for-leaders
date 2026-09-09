# product-coach: An AI Product Strategy

> Decision review for product teams, and the strategy behind it.
>
> Product managers work without the review layer engineers take for granted. product-coach reads a team's repository, tracker, analytics, and customer feedback, objects to a decision using that team's own numbers, and then records whether its own call was right.
>
> A living strategy built across six sessions. Each module adds one component. By Module 6 this repo is the strategy, version-controlled and portable.

**Prototype:** [product-coach.vercel.app](https://product-coach.vercel.app/) · **Author:** Antje Barth · AI Product Strategy for Leaders, Product School

---

## Strategy at a Glance

| Component | Module | Status | Key Artifact |
|-----------|--------|--------|-------------|
| **The Bet** | M1 | Done | [`01-the-bet/`](01-the-bet/): vulnerability diagnostic and working prototype |
| **The Moat** | M2 | Done | [`02-the-moat/`](02-the-moat/): data flywheel and kill switch audit |
| **The Margin** | M3 | Done | [`03-the-margin/`](03-the-margin/): cost curve, pricing and board story |
| **The Contract** | M4 | Done | [`04-the-contract/`](04-the-contract/): golden dataset, confidence UX, reliability contract |
| **The Guardrails** | M5 | Done | [`05-the-guardrails/`](05-the-guardrails/): compounding system, governance policy, shadow AI audit |
| **The Pitch** | M6 | [ ] | `06-the-pitch/` |

---

## The Bet (M1)

**What we're building, for whom, why now.**

- **Product:** product-coach, decision review for product teams. It connects to the repository, tracker, analytics, and customer feedback, objects using the team's own numbers, and then records whether its own calls were right.
- **AI Value Archetype:** Copilot, with an Orchestrator trajectory once it proposes experiments rather than only reviewing them.
- **Vulnerability Scores:** Moat 4/5 · Data 4/5 · Platform 2/5
- **Top Risk:** The product is sold on keeping score, so if the coach's calls do not beat the team's own judgment, it will have collected the evidence against itself and published it.
- **Confidence:** M
- **Prototype:** [product-coach.vercel.app](https://product-coach.vercel.app/)
- **Kill Criteria:** Backtest the coach over about fifty of a team's completed experiments. If the calls it would have flagged do not underperform the ones it would have passed by a clear margin, there is no judgment worth selling and the bet stops.

→ Details: [`diagnostic.md`](01-the-bet/diagnostic.md) · [`prototype.md`](01-the-bet/prototype.md)

---

## The Moat (M2)

**Why this won't get copied in 6 months.**

- **Data Flywheel Score:** 9/20 (Correction 4 · Preference 2 · Domain Context 1 · Network 2)
- **Weakest Loop:** Domain Context. Left at 1 deliberately, because covering more decision types means covering ones where nobody can check the advice afterwards. The investment goes to Network instead.
- **Competitive Position:** ChatPRD scores 8/20 on the same loops, so the category has no flywheel. The whole difference is the Correction loop: their corrections say a user changed the wording, these say the user was wrong.
- **Encroachment Defense:** The most dangerous attacker is the experimentation platforms, not the AI writing tools, because the beachhead sits on a surface they already own. What they cannot see is the decision itself, the objection, and the override.
- **Vendor Portability:** Partial. Eval is strong because the product already scores its own advice, so the usual blocker is solved. Provider, abstraction and routing are all High risk and about two weeks of ordinary work away.

→ Details: [`data-flywheel.md`](02-the-moat/data-flywheel.md) · [`kill-switch.md`](02-the-moat/kill-switch.md)

---

## The Margin (M3)

**Will this make money or bleed it?**

- **Gross Margin (current):** 74.3% at a $30 seat price. COGS is $7.72 per seat per month, and 65% of it is human onboarding rather than inference.
- **Gross Margin (AI-adjusted):** 94.9% in year one on the proposed pricing, 97.8% by year three once onboarding drops out.
- **Pricing Model:** Hybrid, sold self-serve. $500 per team per month plus $60 per experiment reviewed, so $9,000 in year one. Outcome units were rejected because a resolved call would let the vendor decide the invoice, and because any unit tied to warnings shrinks as the coach teaches the team to stop repeating itself.
- **Cascading Strategy:** 96% of requests to small models and embeddings, 4% to mid and frontier. A task moves up a tier only when a smaller model actually fails at it and being wrong costs something. Worth 19.5 points of gross margin.
- **Break-even at:** A review costs 0.7% of the $25,000 experiment it checks. CAC payback is 1.7 months self-serve, against 28.7 months at seat pricing with a rep.

→ Details: [`cost-curve.md`](03-the-margin/cost-curve.md)

---

## The Contract (M4)

**Why users will trust a probabilistic system.**

- **Reliability Target:** Accuracy 90% (alert <85%), hallucination <1% (alert >2%), latency p95 <20s, drift <5pp per 4 weeks. Measured weekly against the golden set, segmented by prompt version, model and call type. Accuracy proves consistency against a corpus we built; the commercial claim that predictions beat a team's own judgment needs a customer's real history and is not asserted.
- **Golden Dataset:** 10 rows today, 300 at v1, 4 adversarial and 6 edge cases. At 10 rows a 90% measurement carries ±18.6 points, so the contract is not enforceable until the set grows. The path to 300 is corpus rows, reworded variants, refusal cases and the first three customer backtests.
- **Confidence UX:** Four outcomes rather than one answer. Refuse before any model call on an unreviewable brief, Object when history contradicts, Endorse on named positive precedent, Decline when history is silent. Below 90% confidence an endorsement degrades to Decline, because encouragement costs more to get wrong than caution does.
- **HITL Architecture:** A human is reached only on a fabricated citation or an endorsement whose precedents disagree. Refusals and declines never escalate, so review volume tracks failures rather than usage and the queue shrinks as the corpus grows.
- **Failure Mode Coverage:** Four coverage gaps named, and one real failure kept rather than fixed. The live coach misread ex-044's mechanism from its prose and was wrong by 9.2pp. Softening the corpus to hide it would be the self-grading failure the product exists to avoid.

→ Details: [`golden-dataset.md`](04-the-contract/golden-dataset.md)

---

## The Guardrails (M5)

**What breaks when this scales, and what compounds.**

- **Compounding System:** Three loops, none compounding today, for three different reasons. Recursive Learning is the one defect: the product records every override and resolves every prediction, then never returns the record to the reasoning. Cross-Domain Transfer is declined on purpose, because A/B tested decisions are the only ground where a prediction can be checked against a control. Network Intelligence is gated on having customers. Six design commitments follow, the first being that the record is the product and the advice is how we earn the right to keep it.
- **Freeze Test:** Frozen for a quarter with every competitor on the same model, product-coach is the only asset in the comparison that grows. Templates, content breadth and in-experiment optimization all go static. A verified record of predictions and outcomes cannot be bought, scraped or generated, because it requires having been present at the decision, the override and the read-out.
- **Governance Posture:** The coach argues, it never acts, and holds no write path into any customer system. Two decisions need human approval: scoring a prediction when the read-out is ambiguous, defined as the 95% CI containing the objection's threshold, and shipping any prompt or model change, gated at 90% golden-set pass and 1% hallucinated citations. `decline-only` is the named degraded state, entered automatically on a fabricated citation or a 10-point pass-rate drop.
- **Shadow AI Status:** 6 workarounds found, triaged to 4 build, 1 partner, 1 ignore. $35 per PM per month in adjacent spend. Dominant signal is trust, which reframes the audit: users double-checking output against another model are reporting a credibility problem, not requesting a feature.
- **Agent Boundaries:** Four components, three of which call a model, plus one designed and unbuilt. Each row separates what code enforces from what policy merely asks, because a reader cannot otherwise tell which limits survive a bug. No component calls another's tools and there is no chain, so there is no handoff to own.
- **Regulatory Exposure:** EU AI Act limited risk, conditionally. It holds only while a person's coaching profile stays private to that person; exposing it upward is Annex III performance monitoring and moves the product to high risk. The decision is to keep it private, which costs the per-person visibility that was one reason a leader would buy, and keeps the team-level decision record that carries the renewal.

→ Details: [`05-the-guardrails/`](05-the-guardrails/)

---

## The Pitch (M6)

**How you get this funded, shipped, and adopted.**

- **Horizon 1 (Now):**
- **Horizon 2 (Next):**
- **Horizon 3 (Bet):**
- **Board Narrative:** [1-sentence thesis]
- **Key Metric:**

→ Details: [`06-the-pitch/`](06-the-pitch/)
