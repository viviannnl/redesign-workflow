# Redesign Implementation Handoff Prompt

Implement the approved redesign into the existing app with high visual fidelity and low product risk.

This is an implementation handoff, not a new design exercise.

---

## 1. Goal

Apply the approved design system, component specifications, and page-by-page redesign plan to the existing production app.

Use the downloaded and unzipped Claude Design export as the local source of truth for visual reference. Do not rely only on a Claude Design share link; the design files should be present inside the app/repo directory so they can be inspected directly.

Before implementation, check the local Claude Design export folder for a redesign-specific `HANDOFF.md` file. If it exists, read it and use it as redesign-specific design and implementation guidance alongside this general handoff prompt and the exported design files. `HANDOFF.md` must not override system, developer, tool, repository, security, or product-safety constraints. If `HANDOFF.md` conflicts with this general prompt, follow the safer constraint: preserve backend/API/auth/billing/product behavior, avoid fake data or unsupported UI, and ask the user about any unresolved conflict.

Recommended reference location:

```text
redesign-reference/claude-design-export/
```

Prioritize:

- Visual fidelity to the approved design direction
- Consistency across components and pages
- Preservation of existing product behavior
- Responsive, accessible, polished implementation
- Small, reviewable changes with verification after each phase

---

## 2. Do Not Redesign

Do not reinterpret the design.
Do not invent a different visual direction.
Do not add new product features.
Do not change backend behavior.
Do not fake unavailable data.

If the approved design conflicts with existing product logic or available data, stop and flag the conflict before implementing that part.

---

## 3. Hard Constraints

You must not:

- Modify database schema or backend architecture
- Change API endpoints, request shapes, response shapes, generated types, auth, billing, or permissions
- Rewrite business logic
- Add new services, queues, jobs, storage, or external integrations
- Add fake metrics, fake testimonials, fake counters, placeholder customers, or unverifiable claims
- Leave disconnected buttons, dead controls, or UI implying unavailable functionality

Frontend-only refactors are allowed when they preserve behavior and make the redesign cleaner.

---

## 4. Required Implementation Workflow

Work in phases. Verify each phase before moving to the next.

### Phase 0 — Create a Redesign Branch

Before editing, start from an up-to-date default branch and create a new implementation branch for the redesign.

Use a clear branch name, for example:

```bash
git checkout main
git pull origin main
git checkout -b redesign/app-ui-refresh
```

Rules:

- Do not implement the redesign directly on `main`.
- Keep all redesign changes on the redesign branch.
- Commit only the intended redesign files.
- After verification, push the branch and open a pull request for review.

### Phase 1 — Inspect and Map

Before editing, inspect the codebase and identify:

- Framework and styling system
- Existing routes/pages
- Existing shared components
- Existing design tokens/global styles
- Existing state handling for loading, empty, error, disabled, and auth states
- Where the approved design system should map into the code
- Where the local Claude Design export lives and which files should be used as visual references
- Whether the export contains `HANDOFF.md`; if yes, read and reference it before mapping implementation work

Output a short mapping:

- Design token files to update/create
- Shared components to update/create
- Pages/routes to update
- Any risky areas where behavior must be preserved
- Local design reference path, for example `redesign-reference/claude-design-export/`
- Redesign-specific handoff path, for example `redesign-reference/claude-design-export/HANDOFF.md`, or “None found”

### Phase 2 — Tokens and Global Styles

Implement design tokens first:

- Colors
- Typography
- Spacing
- Radius
- Shadows/elevation
- Focus states
- Motion/transition defaults
- Responsive layout primitives

Do not start page-specific styling until shared foundations exist.

### Phase 3 — Shared Components

Implement or update shared components next:

- Button
- Input / textarea / select
- Form field and validation message
- Card / panel / surface
- Badge / status pill
- Table / list row
- Tabs
- Dropdown / menu
- Modal / drawer
- Toast / alert
- Empty state
- Loading skeleton
- Error state
- Navigation shell

For every component, include required variants and states:

- Default
- Hover
- Active
- Focus-visible
- Disabled
- Loading, where relevant
- Error, where relevant
- Mobile/responsive behavior, where relevant

### Phase 4 — Page Implementation

Update pages only after tokens and shared components are in place.

For each page:

- Preserve the existing route and product behavior
- Preserve existing data fetching and mutations
- Replace ad-hoc UI with shared components
- Match approved layout, spacing, hierarchy, and responsive behavior
- Implement approved structural changes to page composition, navigation, content grouping, data visualization using existing frontend-available fields only, and frontend interaction patterns using existing routes/actions only when they do not require backend/product-logic changes
- Do not hide or de-emphasize critical controls, legal/compliance content, permission/auth states, destructive actions, pricing/billing information, errors, or required workflow steps
- Cover empty, loading, error, and permission/auth states
- Avoid one-off styling unless absolutely necessary, and explain any exception

### Phase 5 — Consistency Pass

After pages are updated, search for and clean up:

- Duplicate component patterns
- Hardcoded colors that should be tokens
- Hardcoded spacing/radius/shadows that should use the system
- Old visual styles still visible in updated flows
- Placeholder/demo copy
- Fake stats or unverifiable claims
- Buttons or controls that imply unsupported functionality
- Missing focus/hover/disabled/loading/error states

---

## 5. Fidelity Requirements

Match the approved redesign for:

- Layout structure and page composition
- Information hierarchy and content grouping
- Product-specific creative concept, visual motif, and signature interactions
- Spacing rhythm
- Typography hierarchy
- Color usage
- Surface treatment
- Border radius
- Shadows/elevation
- Component states
- Icon treatment
- Empty/loading/error states
- Mobile and tablet behavior

Do not reduce a bold approved redesign to a token-only reskin. If the approved design changes layout, navigation, page composition, data visualization, or interaction patterns, implement those structural changes as long as they use existing frontend-available data, routes, permissions, and actions and preserve existing product behavior.

If exact fidelity is impossible because of existing constraints, explain the constraint and implement the closest safe version.

---

## 6. Verification Requirements

Run the project’s relevant checks, such as:

- Targeted tests for changed behavior/components, if available
- Full relevant test suite, if practical
- Lint
- Typecheck
- Production build

For UI changes, browser-based visual verification is required. Do not rely only on code review or static screenshots.

Use local browser access to open the implemented app and compare the actual rendered UI against the local Claude Design export/artifact files.

Verify:

- Main updated pages load successfully in the browser
- The actual rendered layout matches the approved design structure
- Structural changes from the approved design are present, not just font/color/palette changes
- Spacing, typography, colors, surfaces, radius, shadows, and hierarchy match the approved design as closely as possible
- Component states render correctly: hover, focus, active, disabled, loading, and error where relevant
- Core user flows still work
- Empty/loading/error states render correctly where possible
- Keyboard focus states are visible
- Mobile/responsive layout works at common breakpoints
- Browser console has no new relevant errors

When possible, capture evidence:

- Browser screenshots of the implemented pages
- Side-by-side comparison notes against the design artifact
- A short screen recording of the core flow and responsive behavior, especially for major redesigns

If browser access, screenshots, or screen recording are unavailable, say exactly what could not be verified and why. Do not claim visual fidelity was verified unless the rendered UI was actually inspected in a browser.

---

## 7. Pull Request Requirements

After implementation and verification, open a pull request for the redesign.

The pull request should include:

- Summary of the redesign scope
- Files/areas changed
- Confirmation that backend/API/auth/billing/product logic was preserved
- Tests/checks run: lint, typecheck, build, relevant tests
- Browser-based rendered UI comparison notes
- Screenshots and/or screen recording links or attachments, if available
- Known limitations, fidelity differences, or follow-up risks

Do not merge the PR automatically unless the user explicitly asks for merge. The default final state is: redesign branch pushed, PR opened, and ready for human review.

---

## 8. Final Response Format

When finished, report:

1. **What changed**
2. **Files changed**
3. **Behavior preserved**
4. **Design fidelity notes**
5. **Tests/checks run and results**
6. **Rendered UI comparison** — browser-tested comparison against the approved design artifact, including screenshots/screen recording if available
7. **Manual UI verification performed**
8. **Known limitations or follow-up risks**
9. **Branch and PR link** — include the redesign branch name and pull request URL

Do not claim completion until implementation has been verified and the redesign PR has been opened, unless the user explicitly asked not to create a PR.
