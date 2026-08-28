# Three-Axis Vulnerability Diagnostic

## Product
<!-- Name the product you're diagnosing. Real product at your company — not a hypothetical. -->

**Product:** product-coach, decision review for product teams.

Engineering teams review each other's code before it ships. Product teams do not review each other's decisions. A PRD can rest on an assumption nobody tested. An OKR can measure activity instead of outcome. A roadmap can repeat a bet the team already lost and nobody notices. The cost usually shows up two quarters later.

product-coach is a reviewer for those decisions. It connects to the repository, the issue tracker, the analytics, and the customer feedback channels. Because it reads those systems directly, it can object using the team's own numbers instead of general advice. An objection looks like this: your hypothesis assumes personalization drives activation, here are the last three times this team tested that, and here is what happened each time.

It attaches to review, which product teams already do. Nobody has to adopt a new habit or maintain a new document.

### It keeps score on its own advice

Every objection the coach raises carries an expected effect and a date. The coach then watches the metric and records whether it was right.

No product in this category does that today. They all measure the documents they produce. None of them measures whether those documents led to good decisions. The incentive runs against it, because that measurement can only make the seller look worse.

### Honest scoring needs honest attribution

This constraint decides where the product starts.

Most product outcomes are confounded. A metric moves for several reasons at once, so a coach grading itself on "the metric went up" would produce a scoreboard nobody trusts.

So the product starts on decisions that get A/B tested. An experiment has a control group. The counterfactual is built in, so the verification is clean without any extra work. Experiments also run weekly rather than quarterly, so the record fills faster.

Once there is a track record on ground where the scoring is not arguable, the product can extend to decisions with messier attribution. The earlier record is what makes that extension credible.

### The scoreboard exists before the first sale

A fair objection is that a scoreboard takes months to fill, and a buyer will not wait.

It does not have to. Experiment histories already sit inside analytics platforms, with hypotheses, results, and dates recorded. The coach can run backwards over experiments a team has already completed and show which ones it would have flagged and how those turned out. The proof is computed on the buyer's own history rather than on a reference customer's.

**Where the sample size comes from.** The working number is about fifty experiments, chosen for availability rather than for statistical comfort. A team running weekly tests has roughly a year of history on hand, which is about fifty. Assume the coach flags around a third of them. That splits into 17 flagged and 33 unflagged. Group sizes that small support a directional read, not a precise one. The reason that is acceptable: an effect too small to see across a year of a team's own history is too small to build a product on. The one-third flag rate is an assumption, and it is the first thing the backtest should measure rather than take on faith.

### Then it proposes, and learns

A track record earns the right to propose rather than only to react. At that point the coach reads product metrics as input and suggests the experiment or the bet, then watches what happens.

What updates can be named specifically. Its priors about which objection types matter for this team. Its retrieval over the record of past outcomes. Its weighting of which metrics tend to predict which failures. It does not rewrite itself. It keeps score and adjusts.

**One rule governs the learning: synthetic data generates hypotheses, real data judges them.** Synthetic scenarios are useful for proposing experiments nobody thought of, and for building evaluation coverage on rare cases. They are never a learning signal for what works. A system that learns from a model's beliefs about how products behave becomes self-consistent and confident. A system that also grades itself would then grade itself accurate against its own invented priors. That would remove the only thing the product is selling.

### It calibrates to the person

Beneath the product context and the team context sits a third layer, which is the person using it. Someone six weeks into their first product role and someone eight years in do not need the same thing from a reviewer.

Many product managers arrive from engineering, design, support, or founding a company. For them the coach teaches through the decision in front of them. It explains why this experiment is worth running, and what makes a hypothesis weak, rather than handing over a finished document. The explanation drops away as the person stops needing it.

For people who already know the job, the coach stops explaining and argues instead. The same product works across a career rather than being outgrown after a year.

### What it will not do

It will not compete on document generation. That is the incumbent's ground. Those are also the economics where copies arrive fastest, because a document generator has nothing underneath it that took time to build. Teaching happens inside a live decision, never by producing a polished artifact on request. This product will be worse at writing a PRD than a product that does nothing else, and that is a deliberate choice.

### Who buys it

The product leader who owns decision quality for a team. It is priced per seat, alongside the other tools that team already pays for.

The record that leadership reads is not a second product. It is what makes a renewal an executive decision rather than a team preference.

**Your Role:** Founder, deciding whether to build it.

---

## Scores

| Axis | Score | Where it breaks |
|---|---|---|
| Contextual Moat | 4/5 | The dependency takes quarters to build, so a young account loses nothing by leaving |
| Data Advantage | 4/5 | Team history stays fenced inside each account, and a new customer starts cold |
| Platform Exposure | 2/5 | Coding agents already read the repository, and the product now has infrastructure to unwind |

### Contextual Moat — 4/5
*Workflow depth × switching cost. Would users leave in a weekend if a competitor showed up?*

**Score rationale:**

The score is a 4 because of who ends up reading the record.

A tool that only a product team uses is a team-level decision to remove. A record that leadership relies on to understand why the product is the way it is becomes an organizational dependency. Those get removed slowly, if at all.

Two things accumulate underneath that. The first is the team's verified decision history, which is worth nothing to a competitor and takes years to rebuild. The second is each person's development profile. That one belongs to the individual rather than to the employer, so it travels with them when they change jobs, and they arrive at the new company already wanting the product.

The integrations are not part of that. They make the product work. They do not make it hard to leave, because any competitor can connect the same four sources in a day.

Frequency helps the two assets that do count. The coach attaches to review, so it takes part every time an artifact moves, rather than on the occasions when someone decides to go and ask for advice.

It is a 4 rather than a 5 for two reasons. The dependency is earned over quarters, so a young account can still leave in a weekend without losing anything. And there is no network effect, because the account covers a product team rather than a whole company, even when executives read the output. A 5 would be a product an organization cannot route around when procurement wants it gone.

**What happens if a larger competitor copies the mechanism.** Assume ChatPRD ships review-with-evidence next quarter. The mechanism is not hard to copy, and their team is capable of building it. What they cannot copy on the day they ship is the record itself: which calls were flagged, which were overridden, and how those turned out. That record only accumulates in real time. So the lead is measured in months of collected outcomes rather than in features, and it holds only while this product collects faster than they do. That is the reason for keeping the beachhead narrow. A dense record on one decision type is defensible. A thin record spread across ten is not.

**Named attacker (from partner challenge):** [ChatPRD](https://www.chatprd.ai/), at $15 per seat and $29 per seat for teams. It already ships team workspaces, shared projects, comments, and Linear, Slack, and Google Drive integrations. Those integrations move documents between tools. These integrations feed evidence into a judgment. That is a real difference in purpose, but it is one product decision away from being copied by a company that already has the seats.

---

### Data Advantage — 4/5
*Proprietary signal that compounds with usage. What do you see that OpenAI doesn't?*

**Score rationale:**

The unit of data is one prediction with a measured outcome attached to it.

Starting on experiments is what makes that outcome attributable rather than merely observed, and that distinction is where the value sits. Many systems can log what a metric did. Almost nothing links a specific piece of advice to a controlled result. Doing so requires being present when the decision is made, present when it is overridden, and watching the experiment when it reads out. OpenAI sees none of those three moments. Lenny's archive holds what practitioners say worked in hindsight, which is a much weaker signal than a record of what a team was warned about and chose to do anyway.

The proposal loop raises the collection rate. Experiments run weekly, and a proposed experiment labels itself when it reads out, so the record grows without anyone maintaining it.

A second and different corpus comes from the person layer. It records which coaching interventions actually made someone better, measured against their own work over months. This one has a property the team corpus lacks. How people learn product judgment is not commercially sensitive, so it can be learned in aggregate across customers without touching anyone's private context. That is the part of the flywheel that improves the product for every customer rather than only for the one generating the data.

It is a 4 rather than a 5 for two specific reasons. Team-specific history stays fenced inside each account. And a new customer starts cold, so they get a good general model until enough cycles have run. It becomes a 5 at the point where the shareable slice alone makes a first-day customer measurably better served than a strong general model would.

**Named attackers (from partner challenge):** [ChatPRD](https://www.chatprd.ai/) is the closest, and on this axis it is more dangerous than [Lennybot](https://www.lennysnewsletter.com/cc/lenny-bot). Lennybot has breadth and no outcomes. ChatPRD has thousands of paying teams, so if it attaches judgment to review it will collect the same kind of record faster than a product starting from zero. The proposal loop opens a second front against [Statsig](https://www.statsig.com/), [Eppo](https://www.geteppo.com/), and Amplitude. They already suggest experiments from product metrics, and they own the data pipe this product would be reading. What none of them does is check whether the bet was worth making. They optimise inside a decision somebody else already took.

---

### Platform Exposure — 2/5
*Encroachment risk × pivot speed. If Apple/Google/OpenAI ships your hero feature native — then what?*

**Score rationale:**

This score got worse as the product got more ambitious.

Encroachment risk is high on two fronts. Coding agents already read the repository, which is one of the four context sources, and they are steadily getting better at remembering across sessions. Separately, teaching product fundamentals to a newer product manager is the part of this product a strong general model already does well, because that knowledge is public and well represented in training data. So the teaching mode is more exposed than the challenging mode, and the teaching mode is also what opens the wider market.

Pivot speed used to offset that. The argument was that the coaching logic is portable text with no infrastructure to unwind. That argument no longer holds. Watching metrics continuously, holding a verified record of outcomes, and running a proposal loop all require infrastructure. It also creates dependencies on analytics platforms whose APIs and pricing sit outside this product's control.

What still protects the score is everything a model provider cannot see. The tracker, the analytics, and the customer feedback are not in a coding agent's path. Whether a prediction survived a controlled read-out is not something anyone can bundle into a model.

High exposure that is still rising, and an exit that now costs real money. That is a 2.

**Named attacker (from partner challenge):** the [anthropic/skills](https://github.com/anthropics/skills) repository and the Claude Code plugin marketplace, with more than 2,500 registered marketplaces behind it. The threat is not a free product-management skill pack. It is the coding agent extending from repository context into persistent cross-session product memory, shipped free inside a tool the team already has open.

---

## Top Vulnerability
<!-- One line: what's the single biggest strategic risk? -->

The product is sold on keeping score, so if the coach's calls do not beat the team's own judgment, it will have collected the evidence against itself and published it.

## Confidence Level
<!-- H / M / L — how confident are you in this bet after the diagnostic? -->

**M.**

The demand is proven and the specific wedge is not.

ChatPRD sells AI coaching to product managers at $15 a seat, so the market exists and is already priced. A large share of people doing the job arrived from engineering, design, support, or founding a company, and nothing in the category is built for someone still learning the craft.

**Why not H.** The central claim is untested. Nothing yet shows that a coach with full context makes better calls than the team would have made alone, and everything else rests on that being true and measurable. The design answers the questions around the claim but not the claim itself. Backtesting answers how the product proves itself before anyone buys. Seat pricing under a product leader answers who pays. Neither of those makes the coach right.

**Why not L.** The remaining risks are about accuracy rather than about behaviour, and accuracy is testable. Nothing depends on anyone adopting a habit they have never had, because the coach attaches to review. Nothing depends on anyone maintaining a record, because verification is automatic. Attribution is clean on the beachhead, because experiments carry their own controls. And the product is useful on day one, before any history exists, because the person layer works from cold.

**What would settle it.** Take experiment-shaped decisions and compare two rates. How often the coach's flagged calls turned out to be right, against how often the same team's unflagged calls did. One number, run on a narrow decision type, long before the product is broad.
