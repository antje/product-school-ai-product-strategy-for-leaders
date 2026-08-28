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
| **The Margin** | M3 | [ ] | `03-the-margin/` |
| **The Contract** | M4 | [ ] | `04-the-contract/` |
| **The Guardrails** | M5 | [ ] | `05-the-guardrails/` |
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

- **Gross Margin (current):**
- **Gross Margin (AI-adjusted):**
- **Pricing Model:**
- **Cascading Strategy:**
- **Break-even at:**

→ Details: [`03-the-margin/`](03-the-margin/)

---

## The Contract (M4)

**Why users will trust a probabilistic system.**

- **Reliability Target:**
- **Golden Dataset:** __ rows, __ adversarial
- **Confidence UX:** [approach]
- **HITL Architecture:**
- **Failure Mode Coverage:**

→ Details: [`04-the-contract/`](04-the-contract/)

---

## The Guardrails (M5)

**What breaks when this scales — and what compounds.**

- **Compounding System:** [describe feedback loops]
- **Governance Posture:** [approach]
- **Shadow AI Status:** __ tools found, __ triaged
- **Agent Boundaries:**
- **Regulatory Exposure:**

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
