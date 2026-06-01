# Redesign

Implement the approved Claude Design redesign in this existing app with high visual fidelity and low product risk.

Use this command after the Claude Design ZIP has been downloaded and unzipped into the app/repo directory.

Default design reference path:

```text
redesign-reference/claude-design-export/
```

If `$ARGUMENTS` includes a different design export path, use that path instead of the default. If `$ARGUMENTS` includes extra notes, treat them as additional instructions while preserving all constraints below:

```text
$ARGUMENTS
```

## Preflight

Before creating a branch or editing files:

1. Confirm the local Claude Design export path exists.
   - Default path: `redesign-reference/claude-design-export/`
   - If `$ARGUMENTS` specifies a different path, check that path instead.
   - If the export path is missing, ask the user for the correct local path and stop.
2. Check the design export folder for `HANDOFF.md`.
   - Default path: `redesign-reference/claude-design-export/HANDOFF.md`
   - If `$ARGUMENTS` specifies a different export path, check `<selected export path>/HANDOFF.md`.
   - If found, read it before planning implementation.
   - If not found, continue with the exported design files and note that no redesign-specific `HANDOFF.md` was present.
3. Check the current git branch and working tree.
4. Identify the default branch from git when possible. Use `main` as the example branch name, but do not assume every repo uses `main`.
5. If there are unrelated uncommitted changes, warn the user and avoid mixing them into the redesign branch.

## Goal

Apply the approved design system, component specifications, and page-by-page redesign plan from the local Claude Design export to the existing production app.

Use the downloaded and unzipped Claude Design export as the local source of truth for visual reference. Do not rely only on a Claude Design share link; the design files should be present inside this app/repo directory so they can be inspected directly.

Before implementation, check the local Claude Design export folder for a redesign-specific `HANDOFF.md` file. If it exists, read it and use it as redesign-specific design and implementation guidance alongside this command and the exported design files. `HANDOFF.md` must not override system, developer, tool, repository, security, or product-safety constraints. If `HANDOFF.md` conflicts with this command, follow the safer constraint: preserve backend/API/auth/billing/product behavior, avoid fake data or unsupported UI, and ask the user about any unresolved conflict.

Prioritize:

- Visual fidelity to the approved design direction
- Consistency across components and pages
- Preservation of existing product behavior
- Responsive, accessible, polished implementation
- Small, reviewable changes with verification after each phase

## Hard Constraints

Do not:

- Modify database schema or backend architecture
- Change API endpoints, request shapes, response shapes, generated types, auth, billing, or permissions
- Rewrite business logic
- Add new services, queues, jobs, storage, or external integrations
- Add fake metrics, fake testimonials, fake counters, placeholder customers, or unverifiable claims
- Leave disconnected buttons, dead controls, or UI implying unavailable functionality
- Implement the redesign directly on `main`
- Merge the pull request automatically unless the user explicitly asks for merge

If the approved design conflicts with existing product logic or available data, stop and flag the conflict before implementing that part.

## Required Workflow

### Phase 0 — Create a redesign branch

Before editing, start from an up-to-date default branch and create a new implementation branch for the redesign.

Use a clear branch name, for example:

```bash
git checkout main
git pull origin main
git checkout -b redesign/app-ui-refresh
```

Keep all redesign changes on the redesign branch.

### Phase 1 — Inspect and map

Before editing, inspect the codebase and identify:

- Framework and styling system
- Existing routes/pages
- Existing shared components
- Existing design tokens/global styles
- Existing state handling for loading, empty, error, disabled, and auth states
- Where the approved design system should map into the code
- Where the local Claude Design export lives and which files should be used as visual references
- Whether the export contains `HANDOFF.md`; if yes, read and reference it before mapping implementation work

Output a short mapping before implementation:

- Design token files to update/create
- Shared components to update/create
- Pages/routes to update
- Any risky areas where behavior must be preserved
- Local design reference path
- Redesign-specific handoff path, for example `redesign-reference/claude-design-export/HANDOFF.md`, or “None found”

### Phase 2 — Tokens and global styles

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

### Phase 3 — Shared components

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

Include required variants and states: default, hover, active, focus-visible, disabled, loading, error, and responsive behavior where relevant.

### Phase 4 — Page implementation

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

### Phase 5 — Consistency pass

After pages are updated, search for and clean up:

- Duplicate component patterns
- Hardcoded colors that should be tokens
- Hardcoded spacing/radius/shadows that should use the system
- Old visual styles still visible in updated flows
- Placeholder/demo copy
- Fake stats or unverifiable claims
- Buttons or controls that imply unsupported functionality
- Missing focus/hover/disabled/loading/error states

## Verification Requirements

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

## Pull Request Requirements

After implementation and verification, push the redesign branch and open a pull request for review.

The pull request should include:

- Summary of the redesign scope
- Files/areas changed
- Confirmation that backend/API/auth/billing/product logic was preserved
- Tests/checks run: lint, typecheck, build, relevant tests
- Browser-based rendered UI comparison notes
- Screenshots and/or screen recording links or attachments, if available
- Known limitations, fidelity differences, or follow-up risks

Do not merge the PR automatically unless the user explicitly asks for merge. The default final state is: redesign branch pushed, PR opened, and ready for human review.

## Final Response Format

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
