# Validation Brief

> Module 2 · Validation. Frame the riskiest assumption, then build to test it. **This locks your scenario, no switching after M2.**
Project: Signal — The Dashboard Nobody Reads. Status: hypothesis-testing prototype deployed; behavioral validation is still pending. The scenario metrics and quotes below are supplied context, not independently verified research findings or measured prototype outcomes.
## Scenario
The Dashboard Nobody Reads — Usability.

An analytics product has a 60% bounce rate. Its data exists, but decision-makers struggle to find the insight that tells them what to do next. The target users are marketing managers, growth analysts, product leads, and PMMs who need to turn analytics into a decision.

This scenario concerns abandonment of the analytics dashboard itself, not acquisition-channel bounce on a marketing website. The revised prototype follows that distinction.
_____

## Riskiest assumption

_The one belief that, if false, sinks the idea._

People leave mainly because the dashboard does not make the important insight and next action clear—not because the underlying data is irrelevant, untrusted, or too weak to support a decision.

If this assumption is false, simplifying the first screen may attract clicks without helping users make a useful decision. The test must therefore examine both behavior and whether users understand the recommended action._____

## Hypothesis

> We believe **[change]** will cause **[outcome]** for **[user]**. We'll know we're right when **[signal]**.
> We believe a first screen that leads with one headline metric, a plain-language takeaway, and one recommended action will cause users to act on the dashboard instead of bouncing for marketing managers, growth analysts, product leads, and PMMs who make decisions from analytics. We'll know we're right when bounce rate drops below the supplied 60% baseline and users click the recommended action, while demonstrating that they understand the next step.

Operational definitions
- Bounce: a completed visit lasting strictly less than 15 seconds with no interaction. A visit of exactly 15 seconds does not qualify. Click/tap, keyboard, and wheel/touch interaction are recorded as interaction; passive pointer movement is not.
- Recommended-action click: a visit in which the user clicks Start the focused-view test. Click rate is visits with that click divided by visits started. Repeated clicks do not inflate the number of clicked visits.
- Secondary signal: a saved test plan with a next step, hypothesis, owner, and review date. Saving a plan records intent; it does not launch an experiment or prove decision quality.
- Comprehension check: after the silent walk, ask the participant to explain the priority, the recommended next step, and why they chose it, using their own words.
What the prototype tests
The core flow has two screens:
1. Decision overview: the supplied 60% bounce rate, a plain-language takeaway, one recommended action, supporting 12-chart/6-click context, and both user quotes.
2. Focused-view test plan: an editable next step, hypothesis, owner, and review date, followed by a saved confirmation when the backend write succeeds.
Open the prototype. It is private and requires ChatGPT sign-in. Ensure intended participants have permitted access before testing; login friction must be considered separately from the dashboard experience.

## Risk type

- [ ] Value (do they want it?)
- [1] Usability (can they use it?)
- [ ] Feasibility (can we build it?)
- [ ] Viability (should we?)
 The primary risk is usability: whether users can recognize a priority and act without guidance. If comprehension improves but the recommended action still feels irrelevant, the next investigation should examine value and metric relevance.

## Kill switch

_The result that would make you stop or pivot._

Proposed formative pilot rule: conduct a silent first-use test with five representative decision-makers. If three or more cannot identify and explain the intended next action without help, stop expanding the feature set and revise the first-screen hierarchy or wording.

If participants understand the screen but say the metric or recommended action is not useful, investigate metric relevance, trust, and action value rather than assuming another visual polish pass will solve it.

For the behavioral test, do not declare success if a sufficiently sized, comparable evaluation shows bounce at or above 60% and little or no meaningful recommended-action uptake. Agree the sample size, evaluation window, and minimum useful click rate before that test; these have not yet been set. Missing measurement is inconclusive, not evidence of failure or success.

The five-person pilot is a proposed qualitative usability check. It is not a statistically powered conversion experiment, and its thresholds are planning decisions rather than observed results._____

## The three ingredients

- **Real data (domain metrics):** 60% — Bounce rate: sessions under 15s with no interaction.
12 — Charts on the default landing view.
6 clicks — To reach the most-requested metric.
These are the supplied scenario baselines. They appear on screen as context and must not be presented as live trial results._____
- **User voice (verbatim quotes):** “I open it, see twelve charts, and have no idea which one I'm supposed to act on. So I close it.” — Marketing manager
“The number I need is in there, but it takes six clicks and three filters to find it.” — Growth analyst
Both quotes appear on the overview. They were supplied with the scenario; no new interviews are claimed._____
- **Hypothesis (above):** ✓
one clear metric, takeaway, and action should improve engagement and help users identify a useful next step.
