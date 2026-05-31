# Redesign Implementation Handoff Prompt

Implement the approved redesign into the existing app with high visual fidelity and low product risk.

This is an implementation handoff, not a new design exercise.

---

## 1. Goal

Apply the approved design system, component specifications, and page-by-page redesign plan to the existing production app.

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

### Phase 1 — Inspect and Map

Before editing, inspect the codebase and identify:

- Framework and styling system
- Existing routes/pages
- Existing shared components
- Existing design tokens/global styles
- Existing state handling for loading, empty, error, disabled, and auth states
- Where the approved design system should map into the code

Output a short mapping:

- Design token files to update/create
- Shared components to update/create
- Pages/routes to update
- Any risky areas where behavior must be preserved

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

- Layout structure
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

If exact fidelity is impossible because of existing constraints, explain the constraint and implement the closest safe version.

---

## 6. Verification Requirements

Run the project’s relevant checks, such as:

- Targeted tests for changed behavior/components, if available
- Full relevant test suite, if practical
- Lint
- Typecheck
- Production build

For UI changes, also manually verify:

- Main updated pages load successfully
- Core user flows still work
- Empty/loading/error states render correctly where possible
- Keyboard focus states are visible
- Mobile/responsive layout works at common breakpoints
- Browser console has no new relevant errors

If a check cannot be run, say exactly why.

---

## 7. Final Response Format

When finished, report:

1. **What changed**
2. **Files changed**
3. **Behavior preserved**
4. **Design fidelity notes**
5. **Tests/checks run and results**
6. **Manual UI verification performed**
7. **Known limitations or follow-up risks**

Do not claim completion until implementation has been verified.
