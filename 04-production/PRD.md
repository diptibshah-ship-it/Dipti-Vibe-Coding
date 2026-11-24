# Living PRD

> Module 4 · Production Specs. Refactor for readability; extract a living PRD that stays true as the build evolves.

## Problem

_What user problem does this solve? Tie to the validated hypothesis._

Decision-makers have access to analytics but struggle to identify the insight that matters and the action to take. The supplied scenario describes 60% bounce, 12 charts on the default landing view, and six clicks to reach the most-requested metric.

Signal tests the hypothesis that one headline metric, a plain-language takeaway, and one recommended action will help users act instead of leaving.

Validation status: This hypothesis is not yet validated. The figures and user quotes are supplied scenario evidence. No representative-user study, measured bounce reduction, or confirmed improvement in decision quality has been recorded. Passing implementation tests does not establish product validation._____

## Users & jobs

- **Primary user:** A marketing manager who uses analytics to decide what needs attention and what to do next._____
- Secondary users: Growth analysts, product leads, and PMMs. The prototype does not provide role-specific experiences.
- **Job to be done:** “When I open my analytics dashboard, help me quickly understand what matters, why it matters, and what I should do next—without exploring multiple charts and filters.”_____
Current limitation: The recommended action creates a usability-test plan. Whether that represents a useful business action for these users remains an open question.
## Scope

- **In:** Decision Overview: One headline metric, takeaway, recommended action, supporting metrics, and both supplied user quotes.
Focused-view Test Plan: Editable next step, hypothesis, owner, and review date.
A saved-plan confirmation following a successful server response.
An expandable measurement panel within the overview.
Navigation between overview and plan using URL fragments.
ChatGPT authentication and server-enforced record ownership.
Persistent storage for plans and prototype-session signals.
Request timeouts, save-error messages, retry controls, and tab-local draft preservation.
Responsive layouts._____
- **Out (explicitly):** Separate Evidence Detail and Test Results screens; these were proposed in the prompt chain but have not been implemented.
External analytics integrations.
Automatically generated insights or causal diagnosis.
Randomized A/B testing or production experiment deployment.
Cross-participant research reporting.
Shared workspaces, invitations, or collaborator permissions.
Supabase email/password authentication or PostgreSQL RLS.
Automated measurement of decision quality.
A comprehensive skeleton-loading system._____
The earlier channel-data backend remains in the project, but its broader analytics interface is outside v3’s core flow.
## Requirements

| # | Requirement | Priority | Acceptance criteria |
|Priorities express intended importance. Acceptance criteria describe the current implementation; they do not imply every behavior has passed live production testing.
Requirement	Priority	Acceptance criteria
Present a focused first screen	P0	Overview displays the supplied 60% bounce rate, its definition, a plain-language takeaway, and one primary recommended-action button.
Ground the screen in context	P0	Both supplied user quotes and the 12-chart/six-click metrics appear on screen. They are labeled as scenario evidence rather than live results.
Connect the recommendation to an action	P0	Clicking Start the focused-view test opens the plan screen and records an action-click signal when tracking succeeds.
Capture a test plan	P0	User can edit the next step and hypothesis, enter an owner, and choose a review date. Required values are validated before saving.
Persist the plan	P0	A successful backend response produces a confirmation containing the saved owner and review date. Saving does not launch an experiment or send invitations.
Protect user records	P0	APIs require authenticated identity and scope record access to that user. Ownership is enforced server-side.
Record prototype behavior	P0	Backend supports session duration, interaction, recommended-action click, plan-save, and exit signals. Repeated events do not create duplicate sessions.
Show measurement honestly	P0	Panel displays counts and denominators. Zero completed visits produces No completed visits, not a 0% bounce rate. Tracking failures display an unavailable state.
Recover from failed saves	P1	Requests time out after ten seconds. Save errors preserve entries and offer Retry or sign-in. Save controls are disabled while pending.
Preserve drafts	P1	Form input is retained in tab-local session storage when available and removed after a successful save.
Support navigation and responsive use	P1	Users can move between overview and plan and return after saving. Layout adapts to nar---|---|---|---|
| 1 | Present a focused first screen_____ | Must P0| 	Overview displays the supplied 60% bounce rate, its definition, a plain-language takeaway, and one primary recommended-action button._____ |
| 2 | Ground the screen in context_____ | Should P0 | 	Both supplied user quotes and the 12-chart/six-click metrics appear on screen. They are labeled as scenario evidence rather than live results._____ |

## Data & events

_What gets stored, what gets tracked._
Supplied or predefined content
- 60%: Baseline bounce rate.
- 12: Charts on the original default landing view.
- Six clicks: Path to the most-requested metric.
- Both scenario quotes.
- The takeaway, recommended action, and initial plan text.
These are real interface content, but they are not live analytics findings or newly collected research.

Persistent data
Table	Purpose
action_plans	Stores user-owned next steps, hypotheses, owners, review dates, and reporting scopes.
prototype_sessions	Stores account-scoped session IDs, variation, duration, interaction flags, action clicks, saved-plan signals, and exit status.
channels	Retained user-owned channel records from the earlier build.
daily_metrics	Retained dated analytics records from the earlier build.


Identity comes from ChatGPT sign-in; the application does not maintain its own password store.

Event definitions
- Session started: A recorded authenticated visit for variation focus-v1.
- Interaction: Click/tap, keyboard, or wheel/touch input. Passive pointer movement does not count.
- Recommended action clicked: The primary overview button was clicked.
- Plan saved: The backend confirmed a successful plan save.
- Session ended: An exit event was delivered when the page was left.
Calculations
- Bounce rate: Completed sessions under 15 seconds without interaction ÷ completed sessions.
- Action-click rate: Sessions with a recommended-action click ÷ sessions started.
- Saved-plan signal: Number of sessions containing a successful plan save—not the number of distinct saved plans.
Measurement limits

Exit delivery is best effort. Incomplete sessions are excluded from bounce, which may bias results. Reports cover the signed-in account only. There is no randomized control, and unavailable events cannot be interpreted as zero activity.

Twelve automated data-layer tests previously passed. Live signed-in measurement, real two-account testing, network stress testing, and representative-user validation remain unverified.
_____

## Open questions

1. Is unclear presentation the main cause of abandonment, or are relevance, trust, and data quality more important?
2. Does creating a usability-test plan satisfy the user’s actual business job?
3. Can unfamiliar users explain the priority and next step without guidance?
4. What sample size, evaluation window, and minimum useful click rate should determine success?
5. Is the supplied 60% baseline comparable to the prototype’s audience and measurement method?
6. How will exit-event losses and incomplete sessions affect bounce-rate interpretation?
7. How will participant access and results collection work without mixing accounts or compromising privacy?
8. What evidence would show that clicks led to useful decisions, rather than merely following a prominent button?
9. Should Evidence Detail and Test Results become separate screens, or would that recreate the navigation burden the prototype is trying to reduce?_____
