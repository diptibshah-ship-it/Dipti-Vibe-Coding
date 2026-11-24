# Engineering Handoff Note

> Module 4 · Production Specs. Open the black box, make the build legible to an engineer.

## What this is

_One paragraph an engineer can read in 60 seconds._

_Signal — The Dashboard Nobody Reads is a clickable analytics prototype for marketing managers, growth analysts, and product leads. It tests whether one headline metric, a plain-language takeaway, and one recommended action help users act instead of leaving. The prototype includes a Decision Overview and a Focused-view Test Plan. It saves plans and records engagement through the existing hosted backend. A Supabase schema has also been created and tested, but the website is not yet connected to Supabase. The hypothesis remains unvalidated; the displayed 60% bounce rate is supplied scenario context.____

## Architecture (plain language)

- **Frontend:** HTML, CSS, and JavaScript modules grouped by feature. Screen components display content; separate controllers and repositories handle behavior and requests._____
- **Backend / data:** The deployed website uses server API routes, a hosted D1 database, and ChatGPT authentication. Supabase now contains channels, daily_metrics, action_plans, and prototype_sessions, with ownership-based RLS, an aggregate results view, and a session-recording function. Supabase remains a separate integration target._____
- **Key flows:** Open Decision Overview → read the metric and takeaway → click Start the focused-view test → edit and save a test plan. Session tracking records interactions, action clicks, and successful saves; the measurement panel displays account-specific results._____

## What's solid vs. what's duct tape

| Area | State | Notes |
|---|---|---|
| _____ | solid / rough | _____ |
Area	State	Notes
Feature organization	solid	Display, data access, and behavior are separated.
Existing backend	solid	Plans persist in D1; API access checks authenticated ownership.
Supabase schema	solid	Tables and RLS are deployed. SQL checks passed for isolation, anonymous denial, measurement boundaries, and duplicate events.
Scenario content	rough	The 60% bounce rate, 12 charts, and six-click journey are supplied baselines, not live analytics.
Supabase integration	rough	Website queries and authentication still use the existing backend.
Measurement	rough	Exit tracking is best effort; results are account-specific and have no control group.
Concurrent edits	rough	Last-write-wins can overwrite another edit; no conflict resolution exists.
Product validation	rough	No observed user results establish that the hypothesis is correct.

## Risks & assumptions for the team
Authentication migration: ChatGPT user IDs cannot be used directly as Supabase Auth UUIDs. Establish a supported authentication approach and explicit ownership mapping before migrating data.
Data migration: Existing D1 records have not been copied to Supabase.
Measurement reliability: Missing exit events can bias bounce calculations. Bounce means a completed session under 15 seconds with no interaction.
Validation: An action click indicates engagement, not a better business decision. Compare against a baseline or control before claiming improvement.
Scope: Saving a plan does not launch an experiment or invite participants.
Security: Keep privileged Supabase keys on the server. Browser access must use authenticated sessions and RLS.
_____

## How to run it

```
[setup + run commands]
`Requires Node.js 22.13 or newer. From the project root:
# Install dependencies
npm ci

# Generate the frontend document
node scripts/embed-ui.mjs

# Start development
npm run dev

Run verification and the production build:
npm test
npm run build

Local persistence requires applying the existing D1 migrations to the local database. Supabase migration and security-test SQL are under supabase/; creating those tables alone does not switch the application’s backend.``
