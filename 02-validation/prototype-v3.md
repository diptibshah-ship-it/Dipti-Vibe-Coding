# Prototype (v3): The Build That Tests the Hypothesis

> Module 2 · Validation. The prototype is a hypothesis test, not a demo.

## Link

The Dashboard Nobody Reads — Signal v3_____

## What it tests

_Tie it back to the validation brief: which assumption does this prototype put in front of a user?_

The prototype tests whether users leave because the dashboard fails to make the important insight and next action clear.

The first screen presents one headline metric, a plain-language takeaway, and one recommended action: “Start the focused-view test.” That action opens an editable test plan with an owner and review date.

We will look for:
- Fewer completed sessions under 15 seconds with no interaction.
- Clicks on the recommended action.
- Users explaining the priority and next step without guidance.
- Saved plans as a secondary signal of intent.
Tracking is implemented, but the hypothesis is not yet validated. The supplied 60% baseline is separate from observed prototype results; there is no randomized control._____

## Context injected (no placeholders)

- **Real user quotes on screen:** “I open it, see twelve charts, and have no idea which one I'm supposed to act on. So I close it.”
— Marketing manager

“The number I need is in there, but it takes six clicks and three filters to find it.”
— Growth analyst_____
- **Domain metrics on screen:** - 60%: Bounce rate—sessions under 15s with no interaction.
- 12: Charts on the default landing view.
- 6 clicks: To reach the most-requested metric.
All three are labeled as scenario baselines, not live trial results._____

## Iteration log (v1 → v3)

| Version | Change | Why |
|---|---|---|
| v1 | Built a dashboard with demo acquisition metrics, channel filters, evidence dialogs, and predefined recommendations._____ | Made the idea clickable, but interpreted bounce as marketing-site performance and recommended fixes before establishing causes._____ |
| v2 |Added persistent metrics and plans, ChatGPT authentication, server-enforced ownership, data entry, pagination, and error handling. Replaced premature fixes with investigation language. _____ | Made the product functional beyond a polished mockup and improved the credibility of its recommendations._____ |
| v3 | 	Refocused on dashboard abandonment. Built two core screens with the supplied quotes and metrics, one recommended action, and session, bounce, click, and saved-plan tracking._____ | Made the prototype test a specific usability assumption: whether a clearer first screen helps decision-makers understand what matters and take a next step._____ |
