# PROMPTS.md: Living Prompt Pack

> Module 3 · Prompt Chaining. Re-architect the build with prompt chains; capture the reusable ones here.

## How to use this pack

_Each prompt is a reusable step. Chain them: the output of one becomes the input to the next._

## Prompt chain: [Signal-From Insight to Action]

### Step 1: [Expand-Add evidence and results screens]
```
[Inspect the existing Signal project and its README.

Build the next phase in this strict sequence:

1. Add the "{{screen_a}}" screen.
   Display the supplied 60% bounce-rate baseline, its definition
   (sessions under 15 seconds with no interaction), the 12-chart
   and 6-click context, and both supplied user quotes.

   Separate observations, hypotheses, and missing evidence.
   Label supplied scenario data separately from measured results.

2. Add the "{{screen_b}}" screen.
   Use the existing account-scoped measurement service to show:
   - Sessions started and completed.
   - Bounce rate among completed sessions.
   - Recommended-action click rate.
   - Saved-plan signals.

   Show the counts and denominators behind percentages.
   Explain that incomplete visits are excluded from bounce,
   results cover the signed-in account, and there is no
   randomized control. Do not imply individual-plan attribution.

3. Add navigation.
   Link the overview to "{{screen_a}}" through a secondary
   View evidence link. Link "{{screen_a}}" to "{{screen_b}}".
   Provide a route back to the overview from both screens.
   Offer View results after the existing plan-save confirmation.

Preserve the overview's single primary recommended action:
Start the focused-view test.

Reuse the existing design, authentication, database, and
measurement definitions. Do not connect to GitHub.

Finish by summarizing the screens, routes, queries, and any
remaining mocked or incomplete behavior.]
```
**Expects in:** The existing Signal project, README, authentication, measurement service, and supplied scenario evidence._____
**Produces out:** Two connected screens and an implementation summary identifying data sources and remaining gaps._____

### Step 2: [Make data states explicit]
```
[Use the screens and implementation summary from Step 1.

Harden the "{{screen_b}}" data flow:

- Loading: show skeletons that match the metric and result
  layouts. Do not display temporary zero values.
- Empty: show "{{empty_message}}" with an Open decision overview
  CTA that takes the user to the prototype's starting screen.
- Failure: show "{{error_message}}" inline with Retry.
  Retry must repeat the failed query without reloading the app.
- Success: display actual values with their denominators.
  Zero completed sessions means bounce is unavailable, not 0%.
- Authentication: distinguish signed-out or denied access from
  an empty dataset. Use the existing sign-in flow.
- Slow/offline: use a bounded request timeout. Keep the page
  usable and label any retained results as stale.
- Recovery: discard outdated responses when navigation or
  account identity changes. A failed data request must not
  clear a valid session.

Never replace failed live requests with demo data.
Preserve existing plan drafts, ownership rules, event definitions,
and the overview's primary action.

Verify each state and report passed, failed, and unrun checks.
Do not claim a state works solely because its UI exists.]
```
**Expects in:** The connected screens, queries, and implementation summary from Step 1._____
**Produces out:** Explicit loading, empty, error, recovery, and success states, plus a verification record._____

### Step 3: [Refine — Polish one screen only]
```
[Polish typography and spacing on "{{screen_b}}" only, using
"{{reference_screen}}" as the visual reference.

First, list the three biggest typography and spacing gaps.
Then make a focused refinement pass:

- Match the reference screen's heading hierarchy.
- Make metric values, labels, and denominators easy to scan.
- Align metric cards and standardize their internal spacing.
- Keep body text at least 16px and regular labels at least 14px.
- Preserve readable layouts on narrow screens.

Change only typography, spacing, and alignment on this screen.
Do not alter copy, calculations, queries, event tracking,
navigation, authentication, or the states from Step 2.

Do not redesign other screens or add features.
Finish with a short before/after summary of the visual changes.]
```
**Expects in:** The functioning Test Results screen from Step 2 and the existing Decision Overview as a visual reference._____
**Produces out:** A visually consistent results screen with unchanged behavior and a scoped change summary._____

## Reusable techniques learned

- Sequence dependencies: Establish screens and navigation before adding recovery behavior or visual polish._____
- Specify observable states: Define exactly what users see during loading, empty results, failure, and success._____
- Set boundaries: Name what each prompt may change and what it must preserve.
- Separate evidence from assumptions: Supplied baselines, measured results, and hypotheses need distinct labels.
- Require verification: Capture what was tested and what remains unverified after each step.
## What broke (and the fix)
The initial build looked complete but interpreted the scenario as marketing-site bounce rather than abandonment of the analytics dashboard. It also recommended nearly the same landing-page change for every channel without establishing the cause.

That exposed the weakness of a broad build request: visual completeness can hide incorrect product logic.
_Where a single mega-prompt failed and chaining fixed it._

_This chain addresses the problem by separating structure, behavior, and refinement into reviewable steps. The chain has not yet been executed, so its effectiveness remains to be verified.____
