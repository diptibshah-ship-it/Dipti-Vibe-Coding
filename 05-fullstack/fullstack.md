# Full-Stack: Data, Access Rules, Edge Cases, Deploy

> Module 5 · Full-Stack. Add data schemas, access rules, and edge cases; stress-test and deploy.

## Deployed link

_The working, shareable link that survives real users._

_____

## Data schema

| Entity | Key fields | Notes |
|---|---|---|
| _Profiles ____ | _	user_id UUID primary key; display_name TEXT; created_at TIMESTAMPTZ____ | user_id references auth.users(id). Stores the authenticated user's display information._____ |
Channels |	id UUID primary key; user_id UUID; name TEXT; created_at and updated_at TIMESTAMPTZ | User-owned acquisition channels. Unique (user_id, name) and (user_id, id).
daily_metrics	id UUID primary key; user_id UUID; channel_id UUID; metric_date DATE; sessions BIGINT; bounced_sessions BIGINT; signup_sessions BIGINT; timestamps	Unique (user_id, channel_id, metric_date). Composite foreign key (user_id, channel_id) references channels(user_id, id), preventing cross-account channel relationships.
action_plans	id UUID primary key; user_id UUID; nullable channel_id UUID; period_start and period_end DATE; title, hypothesis, next_step, owner_label TEXT; due_date DATE; status TEXT; timestamps	User-owned investigation plans. Optional channel must belong to the same user. Status: planned, in_progress, or completed. owner_label is descriptive and does not grant access.
## Access rules

_Who can see / do what? Where are the auth boundaries?_
Proposed rules; no application authentication or database RLS is currently implemented.
- Signed-out visitors can access signup, login, and password recovery; they cannot access private analytics or plans.
- A signed-in user can access only their own profile, channels, metrics, and plans. This iteration does not include shared workspaces or administrator roles.
- Enable RLS on every exposed application table and grant only the operations each role needs. Enforce ownership against the authenticated session ID in the database, not only through frontend filters.
- For inserts, validate the new row's ownership. For updates, validate both existing and resulting ownership. Prevent changing ownership or referencing another account's channels.
- Ensure aggregate queries, evidence views, and exports obey the same access boundaries. Never place privileged database credentials in browser code.
- Restore valid sessions after refresh. On logout or account switching, clear private cached data, cancel pending requests, and discard late responses from the previous account.
- Verify with two accounts and direct data requests: account B must not read, modify, delete, or reference account A's records. These checks are pending.
_____

## Edge cases hardened

| Case | Before | After |
||
| Empty / first-run state |	The fixed dataset always displays populated metrics. There is no new-account onboarding, filtered-empty state, or zero-denominator handling. _____ | Planned: show “No analytics yet. Add your first channel and daily metrics.” with Get Started. Provide Clear Filters when no records match. Distinguish missing records from zero activity. Show “Not enough data” for undefined rates and “No comparison data” when historical records are absent._____ |
| Bad / malicious input |The plan form requires an owner and date and rejects whitespace-only owner names. There is no backend validation, authentication, ownership model, or cross-account access enforcement. _____ | Planned: validate required text, count ranges, dates, and relationships in the database as well as the UI. Enforce RLS and reject forged ownership. Render entered text safely. Use stable record IDs, unique constraints, and duplicate-submit protection for retry-safe writes._____ |
| Failure / offline | No application data requests exist, so backend failure handling is untested. A localStorage write failure displays an error, but in-memory plan state is changed before persistence succeeds. No loading skeletons, request timeouts, or Retry controls exist._____ | Planned: show skeletons while loading; use bounded timeouts and inline errors with Retry. Preserve unsaved drafts, keep successful sections usable, and label stale data. Confirm saves only after server success. Do not log out because a data request fails. Discard outdated filter/account responses._____ |

## Stress test results

_What you threw at it, and what held / broke._

Full-stack stress tests: not run. No pass is claimed for database persistence, account isolation, network recovery, pagination, or simultaneous editing.
Test	Expected result	Current result
Create a database record and refresh	Record survives and metrics reflect it	Not run; backend connection not confirmed
Change stored metric counts	Cards, evidence, and export update consistently without code changes	Not run
Two-account isolation	Account B cannot access account A's rows or aggregates	Not run; application auth and RLS absent
Forge ownership or channel IDs	Backend rejects cross-account reads and writes	Not run
Throttle the network	Skeletons appear; interface remains usable; valid session survives	Not run
Block a data request	Inline error and Retry appear; valid session remains intact	Not run
Disconnect during a save	Draft survives; no false success; retry creates one record	Not run
Rapidly change filters	Latest selection wins; stale responses are discarded	Not run against backend requests
Switch accounts during a request	No previous-account data appears	Not run
Load more than 25 records	Stable pagination works; totals include all matching records	Not run
Edit one plan in two sessions	Last database-ordered write persists after refresh	Not run
Submit invalid or empty records	Database rejects invalid input; correct empty states appear	Not run


Earlier prototype checks confirmed that channel filtering, evidence dialogs, and browser-local plan persistence work. Those checks do not establish full-stack readiness or improved decision-making.
Deployment completion gate
Confirm the hosted backend, apply the schema, add authentication and RLS, implement edge states, run the tests above, and record actual outcomes before calling the deployment full-stack complete. Work in the build tool without connecting it to GitHub; transfer this worksheet manually to 05-fullstack/fullstack.md._____
