# Connext — Joined-up student support

A complete browser-based prototype using plain HTML, CSS and JavaScript, with ServiceNow-inspired deep green and lime colours. Every name, record and policy is fictional.

## Run

Open `dist/index.html` directly in your browser — no installation or API keys required.

For a local server with reliable cross-tab synchronisation:

```sh
node server.cjs
```

Open http://127.0.0.1:4173. Run commands from this folder. Optional visual fonts use Google Fonts; system fonts work offline.

## Included

- A responsive home page at `#home`, opened by clicking the Connext logo, with role-aware links back into the workspace.
- Overview, urgency-ranked attention queue, live search, department/priority filters and sorting.
- Ten fictional student stories; all twelve departments named; seven primary departments seeded, plus optional Accessibility and Grievance cases.
- Student 360, connected cases, append-only shared timeline, department-specific student database lookup and next-step tasks.
- Configurable detector rules with a visible reason for every flag. Ishita's combined signals and Aanya's priority journey are deliberate demo stories.
- Eight demo roles, full/redacted/hidden view filtering, restricted counselling notes and hidden grievance records.
- Student grievance submission by text, optional browser voice dictation or an editable demo example, with local persistence and status tracking. Students can see their own submissions; staff access is restricted to the Grievance Officer.
- Offline text intake, deterministic routing and task creation, review before creation, related-case warnings and optional browser speech recognition.
- Permission-filtered simulated case briefs, department summaries, daily briefing and a local case copilot.
- Notes, status updates, task completion, follow-up dates and first-appointment booking.
- Pending/accepted warm handoffs, overdue indicators, coordinated fee holds and manual duplicate linking.
- Department dashboards, leadership snapshot, CSV export, fictional reference policies and a searchable knowledge library.
- Local browser persistence, same-origin cross-tab updates and one-click demo reset. Seed dates are relative to the reset date.
- Responsive layout, keyboard navigation, native dialogs and labelled controls.

## Suggested walkthrough

1. Open Overview as the Coordinator; Aanya is first in the attention queue.
2. Open Aanya; read each detector reason, department status and shared timeline.
3. Pause reminders. Switch to Fee Officer and verify the hold and redacted counselling note.
4. Switch to Counsellor and see the authorised note. Open Handoffs and accept Aanya's referral.
5. Return to Coordinator, add a task or note and observe the updated timeline.
6. Review Ishita's connected signals and book Riya's first appointment.
7. Create a request with the example text and review its routing before creation.
8. Use Reset demo to restore the original stories.

## Implementation

- `dist/config.js`: detector thresholds and scoring weights.
- `dist/data.js`: fictional seeded records; stories documented first in `STORIES.md`.
- `dist/model.js`: local state, permissions, detector and mutation/event logic.
- `dist/app.js`: all views, dialogs, interaction flows and simulated AI.
- `dist/styles.css`: visual theme and responsive layouts.
- `tests/model.test.cjs` and `tests/render.test.cjs`: workflow, permission and page-rendering checks (`node --test tests/model.test.cjs tests/render.test.cjs`).

## Demo boundaries

Clerk, Groq, ServiceNow, server authentication, a remote database, email delivery and real RAG are not connected. AI is deterministic and labelled simulated. Voice uses the browser speech-recognition service when available; it may require connectivity and microphone permission.

The permission layer strips restricted fields before UI and simulated-AI rendering. **All seed data still ships to the browser**; this is a presentation demo, not secure access control. Do not use real confidential information. Real deployment would require server-side identity verification, access control, durable persistence and audited API boundaries.

Changes synchronise only across tabs on the same device/browser/origin, not across users or devices. Separate tabs can overwrite simultaneous edits. Reset is intentionally a one-click operation on fictional local data.

Eleven automated checks cover workflows, permission filtering and page rendering. The home page and student grievance submission were also verified in the browser, including saving a demo grievance and displaying its Pending status. Live microphone capture was not exercised; it depends on browser support and permission. The page includes optional feature-detected WebMCP tools; ordinary browsers do not need them.
