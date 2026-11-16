# Reporting Portal: Handoff Prompts and Spec

Nov 16, 2026 · @Usha

## Using this inside a secure client platform

Build it code-first with your internal coding agent, using Abyss's own AI skills. Use Figma Make only if your org has it enabled with the Abyss library. In both cases you carry over only the text in this doc, never code or data.

**What is safe to bring over.** Everything here is a spec and prompts written outside your client's systems. It uses invented sample data, with no PHI, no internal code and no credentials. Even so, follow your company's rules for bringing outside content in. If you're unsure, ask your manager or security team, or retype the prompts. Never paste internal code, real tokens or real data back into a personal AI account.

**Why the internal agent is the better route.** The Abyss CLI installs Abyss "skills" into supported AI coding agents (Claude Code, GitHub Copilot, Windsurf, Codex and others) and Copilot instructions (`npx @uhg-abyss/cli skills find`, `skills add <name>`, `instructions`). An agent with those installed reads the real Abyss components and tokens from inside the secure network. That closes the gap the mockup has: it only approximates the tokens.

| Route | Where it runs | What you give it | What you get | Use when |
| --- | --- | --- | --- | --- |
| 1. Internal coding agent + Abyss skills (recommended) | Your secure IDE | The coding-agent prompt below + this spec | Working React + Vite + TanStack app on real Abyss components and tokens | You are building it yourself, which you are |
| 2. Figma Make | Your org's Figma | The Figma Make prompt below + mockup screenshots | A clickable prototype to review with stakeholders | You need sign-off on the design before coding |
| 3. Both | Both | Figma first, then the agent | Approved design, then code | Stakeholders want to see it first |

**Taking the mockup screens with you.** The mockup canvas is private on claude.ai, and your client network may block that site. To give the agent or Figma Make a picture, export the three screens as PNG or PDF from the canvas's Share menu. Then bring those files in under the same rules as above.

Sources: [Abyss CLI setup](https://abyss.uhc.com/ai-cli/cli-setup) · [Abyss AI skills](https://abyss.uhc.com/ai-cli/skills/overview) · [Abyss Web getting started](https://abyss.uhc.com/web/developers/getting-started)

## Design spec

The app has three screens: Reports home, Build a report and Run a report. They share one app shell, and every color, size and font comes from the Abyss UHC theme, never from hex values.

### Foundations

- Abyss Web v2: wrap the app in `ThemeProvider` with `createTheme('uhc')`. Use Abyss components wherever one exists, and use theme tokens for any custom layout styling. No hardcoded hex, px font sizes or font names.
- Typography: serif display headings for page titles (H1) and section titles (H2), sans for everything else, all from theme text styles.
- Buttons: Abyss primary (filled) for the one main action per area, secondary (outline) for alternatives, tertiary or link for low-emphasis actions.
- Layout: content max width about 1280px, centered, with side gutters. Panels and cards use the theme's surface, border and radius tokens.

### App shell (all screens)

- Header: logo (official Abyss brand asset), app name "Reporting Portal", primary navigation (Home, Report library, Report builder, Schedules, Data sources) with the current page marked, a notifications icon button and an account menu.
- Footer: "Data refreshed nightly at 2:00 AM CT. Reports may contain PHI. Handle according to policy." plus Help and Request data access links.
- Routes (TanStack Router): `/` home · `/reports` library · `/reports/$reportId/run` run · `/builder` new report · `/builder/$reportId` edit · `/schedules`.

### Screen 1: Reports home and quick access

1. Hero band on a light brand tint: H1 "Reports", one line of intro text, and two actions: Build a report (primary, goes to `/builder`) and Browse library (secondary).
2. Search: a labelled field "Search reports" with placeholder "Name, owner, or data source" and a Search button.
3. Quick access: H2 plus a "View all reports" link, then tabs Pinned (6), Recent (3) and Shared with me (2), then a responsive card grid (cards at least 280px wide).
   - Each card has a category badge (Claims, Membership, Provider, Utilization, Pharmacy, Finance), a pin toggle icon button ("Unpin {report name}"), the title, a one-line description, last-run or schedule info, and actions Run (primary, goes to the run page) and Edit (secondary, goes to the builder).
4. Recent runs table: Report (name plus a small detail line), Run by, Started, Status, and an action (Download, View, Retry or Cancel). Status is a badge with an icon and text: Completed, Running, Failed or Queued.
5. Upcoming schedules panel: report name, cadence and delivery method, next run time, and a "Manage schedules" link.

### Screen 2: Build a report

1. Breadcrumb Reports / Build a report. Report name text field. Actions: Save draft (secondary) and Save and run (primary).
2. Stepper: Data source (done), Columns (current), Filters, Group and sort, Schedule and share.
3. Left panel, "Columns":
   - Data source summary (Medical claims, refresh time, Change link), a selected-count label and a field search.
   - Grouped checkboxes: Member (Member ID, Member name, Plan, Line of business), Claim (Claim number, Service date, Claim status, Denial reason), Provider (Provider name, NPI, Specialty), Financial (Billed, Allowed and Paid amount).
4. Center panel, "Live preview": a table that updates as fields are ticked, showing 6 sample rows and "Showing 6 of N rows".
   - Number columns are right-aligned, and member identifiers are masked.
   - With no columns selected, show an empty state.
   - A warning alert reads: "Contains PHI. Member identifiers are masked in the preview; exports are logged."
5. Right panel:
   - Filters as removable chips (Service date: Last 90 days; Claim status: Denied; Line of business: Commercial, Medicare Advantage, Medicaid; Market: Midwest), plus an Add filter button.
   - Group by and Sort by dropdowns, and Output format as a segmented choice: Excel, CSV or PDF.
   - A "Run on a schedule" switch that reveals Frequency and Deliver-to dropdowns, and a "Who can see this report" dropdown.

### Screen 3: Run a report

1. Breadcrumb, H1 with the report name, and a metadata line (owner, data source, last updated). Actions: Share (icon), Schedule and Edit in builder.
2. Left panel, "Run parameters":
   - Service date From and To date fields, plus quick-range chips (Last 90 days, Quarter to date, Year to date).
   - Line of business checkboxes, a Market dropdown and Output format.
   - Run report as a full-width primary button, showing "Running…" and disabled while a run is in progress. Below it, a "Reset to saved defaults" link.
3. Status area with three states:
   - **Running:** progress bar, step text (validating parameters, querying data, aggregating results), percent complete, a Cancel run button and the note "You can leave this page. We'll notify you when it's ready."
   - **Completed:** success alert (time taken, row count, finish time) with Download {format} (primary) and Email results (secondary).
   - **Failed:** error alert with the reason and a Retry button.
4. Results:
   - Four summary tiles (Denied claims, Denial rate, Billed amount denied, Avg. days to decision), each with a change versus the prior period shown as an arrow plus text.
   - Top denial reasons as horizontal bars with count and percent, and a By line of business table with a total row.
   - Detail rows table with a filter field and pagination, and a Run history list with Download links.
   - While a new run is in progress, earlier results are dimmed or replaced with loading placeholders.

### States, accessibility and responsiveness

- Every data area has loading (skeleton), empty (with a next step) and error (with retry) states.
- WCAG 2.1 AA: 4.5:1 contrast for text and 3:1 for icons and borders. Status never relies on color alone. Visible focus everywhere, and tap targets of 44px or more.
- Run progress and completion are announced through a live region (`role="status"`). Tabs, chips and segmented controls work with the keyboard. Tables use real header cells.
- Under about 1024px the builder's three panels stack in order (Columns, Preview, Settings). On phones the navigation collapses into a menu and wide tables scroll inside their box.

## Data and API contract

These endpoints cover all three screens. Runs are asynchronous: start one, poll its status, then download. These are proposed names, so adjust them to your backend's conventions.

| Endpoint | Used on | Returns | TanStack Query key |
| --- | --- | --- | --- |
| `GET /reports?view=pinned\|recent\|shared` | Home quick access | Report cards (id, title, category, description, lastRun, schedule) | `['reports', view]` |
| `GET /runs?limit=5` | Home recent runs | Run rows (id, reportName, runBy, startedAt, status, rowCount, error) | `['runs', 'recent']` |
| `GET /schedules?upcoming=true` | Home schedules | Schedule rows (reportName, cadence, delivery, nextRunAt) | `['schedules', 'upcoming']` |
| `GET /datasources/{id}/fields` | Builder | Grouped fields (id, label, group, type, isPhi) | `['fields', sourceId]` |
| `POST /reports/preview` | Builder live preview | Up to 6 masked rows + total count | `['preview', definition]` (debounce 300 ms) |
| `POST /reports`, `PUT /reports/{id}` | Builder save | Saved report definition | mutation; invalidates `['reports']` |
| `POST /reports/{id}/runs` | Run report | `202` + runId | mutation |
| `GET /runs/{runId}` | Run status | status, progress %, step, rowCount, durationMs, error | `['run', runId]`, `refetchInterval` 1.5 s until terminal |
| `GET /runs/{runId}/file?format=` | Download | File stream (audit-logged) | plain link, not cached |

Run flow:

1. The client posts the parameters and gets a `runId` back.
2. It polls `GET /runs/{runId}`. Status moves from `queued` to `running` to `completed`, or ends at `failed` or `cancelled`.
3. Polling stops at a terminal status. On `completed` the client invalidates `['runs', 'recent']` and the report's summary query.
4. Cancel is `DELETE /runs/{runId}`.

Enforce PHI masking and export permissions on the server, not only in the UI.

## Prompt for your internal coding agent

Paste this into the agent in your secure IDE after installing the Abyss skills, and attach the Design spec and Data and API sections above. It asks for the work in four stages so you can review each one before the next.

```text
You are helping me build an internal "Reporting Portal" web app. I am a backend developer
learning frontend, so explain key decisions briefly in your summaries.

STACK (already chosen, do not change)
- React + Vite + TypeScript, TanStack Router (file-based routes), TanStack Query,
  TanStack Form (or the Abyss form hooks if the Abyss skill recommends them).
- UI: Abyss Web v2 (@uhg-abyss/web) with the UHC theme: ThemeProvider + createTheme('uhc').

DESIGN-SYSTEM RULES (strict)
1. Use the installed Abyss skills/instructions and the Abyss docs as the source of truth.
   Before using a component, confirm its import path and props there. Never invent props.
2. Use an Abyss component wherever one exists (header/navigation, buttons, text fields,
   selects, checkboxes, toggles, tabs, badges, cards, alerts, progress, tables,
   pagination, breadcrumbs, stepper, date inputs, icons).
3. For custom layout styling, use theme tokens via Emotion/the theme only.
   No hex colors, no hardcoded font families, no magic-number font sizes.
4. If Abyss has no component for something (e.g. a horizontal bar list), build a small
   wrapper in src/components using tokens, and tell me which ones you had to build.
5. Accessibility: WCAG 2.1 AA. Status never by color alone, visible focus,
   role="status" for run progress, keyboard-operable tabs/chips/segmented controls.

PROJECT STRUCTURE
src/api (typed client + types) | src/queries (queryOptions per resource) |
src/routes (pages) | src/features/{home,builder,run} | src/components (shared wrappers)
| src/mocks (MSW handlers with sample data, so the UI works before the backend exists).

WORK IN STAGES. Stop after each stage, summarize what you built, and wait for my OK.
Stage 1: App shell (header, nav, footer, ThemeProvider, QueryClient, router), routes:
  /, /reports, /reports/$reportId/run, /builder, /builder/$reportId, /schedules.
  MSW mocks for every endpoint in the API section.
Stage 2: Reports home: hero + search, quick-access tabs and report cards,
  recent runs table with status badges, upcoming schedules. Loading/empty/error states.
Stage 3: Run a report: parameter form, run mutation, polling GET /runs/{runId} with
  refetchInterval until a terminal status, running/completed/failed/cancelled UI,
  summary tiles, denial-reason bars, line-of-business table, paginated detail table,
  run history.
Stage 4: Report builder: stepper, grouped field checkboxes, debounced live preview,
  removable filter chips, group/sort, output format, schedule toggle, visibility, save.

QUALITY BAR
- Vitest + Testing Library tests for each feature's main flow; an axe check per page.
- No `any`. Loading, empty and error states for every query.
- Responsive: builder panels stack under ~1024px; tables scroll inside their container.

The full screen-by-screen spec and the API contract are below. Follow them exactly;
ask me before deviating.

[PASTE "Design spec" AND "Data and API contract" SECTIONS HERE]
```

If your agent can't install Abyss skills, add one line at the top: "Open https://abyss.uhc.com/web/catalog/components and check each component's docs before using it."

## Prompt for Figma Make

Attach the exported mockup screenshots, then paste this prompt. If your Figma org has the Abyss library or an Abyss kit available to Make, select it first. That is the single biggest factor in whether the output uses real Abyss parts.

```text
Create a clickable, responsive 3-screen prototype called "Reporting Portal" for internal
healthcare reporting users (analysts and operations staff).

DESIGN SYSTEM
- Use the attached/connected Abyss (UHC theme) design system library: its components,
  color variables, text styles, spacing and radius. Do not invent colors or fonts.
- If no library is available, approximate the UHC Abyss look: deep navy brand blue for
  headings, primary buttons and active states; white surfaces on a light gray page;
  pale aqua tint for the home hero band; pill-shaped buttons; serif page titles over a
  clean sans-serif body; 1px light-gray borders; 8–12px card corners; green/red/amber
  status badges that always pair color with an icon and a text label.
- Accessibility: WCAG 2.1 AA contrast, visible focus states, 44px minimum tap targets.
- Frames: desktop 1440 wide (content max 1280, centered) and mobile 390 wide.

SHARED SHELL
Header: logo placeholder, app name "Reporting Portal", nav (Home, Report library,
Report builder, Schedules, Data sources) with the current page underlined, a bell icon
button, a round avatar "AB". Footer: "Data refreshed nightly at 2:00 AM CT. Reports may
contain PHI. Handle according to policy." with Help and Request data access links.

SCREEN 1 – REPORTS HOME
- Hero band (pale aqua): H1 "Reports"; text "Run the reports you use most, build new ones
  from governed data sources, and track every run in one place."; buttons "Build a report"
  (primary, goes to Screen 2) and "Browse library" (secondary).
- Search field labelled "Search reports", placeholder "Name, owner, or data source", and
  a Search button inside the pill-shaped field.
- "Quick access" section with tabs Pinned (6) | Recent (3) | Shared with me (2).
  Card grid (3 across on desktop, 1 on mobile). Each card: category badge, filled star
  pin button, title, one-line description, clock icon + last-run text, buttons Run
  (primary, goes to Screen 3) and Edit (secondary, goes to Screen 2). Pinned cards:
  Claims denial summary (Claims) – Last run today, 10:42 AM · Excel
  Member eligibility roster (Membership) – Scheduled daily, 6:00 AM
  Provider network adequacy (Provider) – Last run yesterday · PDF
  Prior authorization turnaround (Utilization) – Running now
  Pharmacy spend trend (Pharmacy) – Last run Oct 26 · Excel
  Premium reconciliation (Finance) – Scheduled monthly, 1st
- "Recent runs" table (left, wide): Report | Run by | Started | Status | action.
  Statuses: Completed, Running, Failed, Queued. Actions: Download, View, Retry, Cancel.
- "Upcoming schedules" panel (right): 4 items with calendar icon, name, cadence +
  delivery, "Next run: …", then a "Manage schedules" link.

SCREEN 2 – BUILD A REPORT (light gray page)
- Breadcrumb "Reports / Build a report". Editable report name field showing
  "Denied claims by market, last 90 days". Buttons: Save draft (secondary),
  Save and run (primary, goes to Screen 3).
- Stepper: 1 Data source (complete, green check) · 2 Columns (current) · 3 Filters ·
  4 Group and sort · 5 Schedule and share.
- Three white panels side by side (stacked on mobile):
  Left "Columns (6 selected)": data-source box "Medical claims – Refreshed today,
  2:00 AM CT · Change", field search, then checkbox groups MEMBER (Member ID, Member
  name, Plan, Line of business✓), CLAIM (Claim number✓, Service date✓, Claim status,
  Denial reason✓), PROVIDER (Provider name✓, NPI, Specialty), FINANCIAL (Billed
  amount✓, Allowed amount, Paid amount).
  Center "Live preview – Showing 6 of 18,204 rows": table with the 6 checked columns
  and 6 sample denied-claim rows (claim numbers like CLM-20931874, dates in Oct 2026,
  money right-aligned). Below it an amber warning: "Contains PHI. Member identifiers are
  masked in the preview. Every export is logged."
  Right "Filters": removable chips (Service date: Last 90 days · Claim status: Denied ·
  Line of business: Commercial, Medicare Advantage, Medicaid · Market: Midwest), "Add
  filter" button, Group by dropdown, Sort by dropdown, Output format segmented control
  (Excel selected | CSV | PDF), "Run on a schedule" toggle ON revealing Frequency and
  Deliver to dropdowns, and a "Who can see this report" dropdown.
- Interaction: ticking a checkbox adds/removes that column in the preview; unticking all
  shows an empty state "No columns selected".

SCREEN 3 – RUN A REPORT (light gray page)
- Breadcrumb "Reports / Claims / Claims denial summary"; serif H1 "Claims denial
  summary"; meta "Owner: Claims Analytics · Source: Medical claims · Updated Oct 20,
  2026"; buttons Share (icon), Schedule, Edit in builder.
- Left "Run parameters" panel: From/To date fields, quick chips (Last 90 days selected,
  Quarter to date, Year to date), Line of business checkboxes, Market dropdown, Output
  format segmented control, full-width primary "Run report" button, "Reset to saved
  defaults" link.
- Right results column:
  Status banner in 3 variants (make them separate frames or component states):
   Running – progress bar 60%, "Running: querying medical claims (step 2 of 3)",
     Cancel run button, note "You can leave this page. We'll notify you when it's ready."
   Completed – green: "Completed in 14 seconds. 12,482 rows · Today, 10:42 AM",
     Download Excel (primary), Email results (secondary).
   Failed – red: reason "Data source timed out" and Retry.
  4 summary tiles: Denied claims 12,482 (▲ 4.1% vs. prior 90 days) · Denial rate 8.4%
  (▲ 0.6 pts) · Billed amount denied $18.6M (▼ 2.3%) · Avg. days to decision 3.2 (▼ 0.4).
  "Top denial reasons" horizontal bars in brand blue with count and %: Missing prior
  authorization 3,412 (27%) · Not medically necessary 2,690 (22%) · Out of network
  1,958 (16%) · Timely filing exceeded 1,487 (12%) · Duplicate claim 1,204 (10%) ·
  Other 1,731 (14%).
  "By line of business" table: Commercial 6,240 / 7.9% · Medicare Advantage 4,118 / 9.1%
  · Medicaid 2,124 / 8.6% · Total 12,482 / 8.4%.
  "Detail rows" table with a filter field and Previous/Next pagination "Showing 1–6 of
  12,482 rows", then a "Run history" list (3 past runs with Download links).
- Interaction: clicking Run report switches the banner to Running, then to Completed.

All data is sample data. Keep labels exactly as written. Use sentence case everywhere.
```

## Review checklist

Check these before you accept each stage from the agent or a Figma Make draft.

- [ ] No hex colors, font names or raw px font sizes in custom code. Search the codebase for `#` and `px` in style code.
- [ ] Every button, field, tab, badge, alert and table is an Abyss component, or a listed wrapper built from tokens.
- [ ] Each screen has its loading, empty and error states, and the run has running, completed, failed and cancelled states.
- [ ] Keyboard only: you can reach and operate everything, and focus is always visible.
- [ ] The axe check shows no serious or critical issues, and status shows as an icon plus text, not color alone.
- [ ] At 390px wide, the builder panels stack, the nav collapses and tables scroll inside their box.
- [ ] Member identifiers are masked in previews, and downloads go through the logged endpoint.
- [ ] Figma Make: confirm it used the Abyss library rather than look-alike styles, by checking that layers link to library components.
