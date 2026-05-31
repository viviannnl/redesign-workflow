# Existing App Redesign Prompt

You are redesigning an existing production web application.

This is **not** a greenfield project. This is a constrained UI/UX modernization of a working product. Preserve the app’s current product behavior while improving clarity, consistency, polish, and usability.

---

## 1. Primary Goal

Create a modern, consistent design system for the existing application, then apply it across the app without changing backend behavior or product logic.

Optimize for:

- Visual consistency across every page and state
- Clearer information hierarchy
- Better usability for real users
- Cleaner, more premium, modern UI
- Reusable components instead of one-off page styling
- Accessibility, responsive behavior, and empty/loading/error states

Do **not** change what the product does. Change how clearly and beautifully it presents the existing product.

---

## 2. Non-Negotiable Constraints

You must not:

- Modify backend architecture
- Modify database schema
- Modify data models, generated types, or API contracts
- Change API endpoints or request/response shapes
- Change authentication, authorization, billing, or permission logic
- Introduce new backend services, jobs, queues, or storage
- Rewrite business logic
- Replace the product with a different concept
- Add fake product capabilities that do not exist

Assume:

- Existing backend APIs are fixed and production-ready
- Existing data contracts are the source of truth
- All implementation changes must be frontend-only unless explicitly approved
- If a desired UI needs missing data or backend support, flag it as a risk instead of silently implementing fake behavior

---

## 3. Source-of-Truth Rules

Before proposing changes, inspect the existing app and identify:

- Current routes/pages and their purpose
- Existing reusable UI components
- Existing styling approach, design tokens, and CSS framework
- Existing data fields available to the frontend
- Existing loading, empty, and error states
- Existing responsive breakpoints and navigation patterns

When the current app conflicts with the desired redesign, preserve the current product behavior and improve the presentation around it.

Do not invent:

- New metrics
- New integrations
- New user roles
- New workflow steps
- New dashboard cards backed by unavailable data
- New marketing claims, fake testimonials, fake counters, or unverifiable social proof

---

## 4. Required Workflow

Work in this order. Do not skip ahead.

### Step 1 — Product and UI Audit

First, produce a short audit of the existing app:

- What the app appears to do
- Main user flows
- Main pages/routes
- Reusable components already present
- Visual inconsistencies or usability problems
- Risky areas where UI changes could accidentally alter product behavior

Output this audit before proposing the design system.

### Step 2 — Style Direction Exploration

Before defining the final design system, propose style directions for the redesign.

If design inspiration, screenshots, brand assets, or a `design-inspiration/` folder are provided, use them as reference material. Do not copy another product exactly; extract principles such as density, hierarchy, mood, rhythm, typography, and interaction posture.

If no inspiration is provided, generate 3 possible directions:

1. **Conservative** — closest to the current product; safest implementation.
2. **Strong-fit** — your best recommendation for this product, audience, and workflow.
3. **Divergent** — more distinctive and opinionated; useful for discovering taste boundaries.

For each direction, include:

- Name
- 3–5 words describing the feel
- Best-fit audience/product rationale
- Visual principles: typography, color posture, spacing/density, surfaces, motion
- What it intentionally avoids
- Implementation complexity: low/medium/high

Then recommend one direction and explain why.

### Step 3 — Design System Definition

After style direction is chosen or recommended, extract and define a unified design system that fits the product.

Include:

- Design direction: 3–5 words describing the desired feel
- Typography scale and usage rules
- Color system, including semantic colors for success/warning/error/info
- Spacing scale
- Border radius rules
- Shadow/elevation rules
- Layout grid and page width rules
- Icon style rules
- Motion/transition rules, if used
- Responsive behavior rules
- Accessibility rules: contrast, focus states, keyboard usability, reduced motion

Important: define tokens and rules first. Do not jump directly into page mockups.

### Step 4 — Core Component System

Redesign the reusable components before pages.

Define variants, sizes, and states for:

- Button
- Input / textarea / select
- Form field and validation message
- Card / panel / surface
- Badge / tag / status pill
- Table / list row
- Tabs
- Dropdown / menu
- Modal / drawer
- Toast / alert
- Empty state
- Loading state / skeleton
- Error state
- Main navigation and secondary navigation

For each component, specify:

- Purpose
- Variants
- States: default, hover, active, focused, disabled, loading, error where relevant
- Responsive behavior
- Accessibility requirements
- Existing component/file to update if identifiable

### Step 5 — Page-by-Page Redesign Plan

Only after the design system and components are defined, plan each page.

For every page/route, provide:

- Current purpose of the page
- Main user action on the page
- Layout changes
- Component usage from the design system
- Empty/loading/error state treatment
- Responsive behavior
- What must remain unchanged
- Any implementation risks or missing data

Rules:

- Use only the design system components and tokens
- Do not create one-off colors, spacing, shadows, or typography per page
- Do not introduce UI that requires unavailable backend data
- Keep copy clear and specific, but do not change product promises or positioning unless requested

### Step 6 — Implementation Sequencing

Break the work into safe implementation phases:

1. Design tokens and global styles
2. Shared components
3. Layout/navigation shell
4. Highest-impact pages
5. Secondary pages and edge states
6. Responsive/accessibility polish
7. Final consistency pass

For each phase, include:

- Files likely to change, if identifiable
- What to verify before moving on
- Risks to watch for

### Step 7 — Consistency and Safety Validation

Before final output, check for:

- Inconsistent spacing, typography, colors, or radius values
- Duplicate components solving the same UI problem
- Missing hover/focus/disabled/loading/error states
- UI drift away from the design system
- Unverifiable claims, fake stats, fake social proof, or placeholder content
- New UI controls that do not connect to existing functionality
- Changes that appear to require backend/API/auth/business-logic changes
- Accessibility regressions
- Mobile/responsive regressions

Flag unresolved issues clearly.

---

## 5. Output Format

Provide the final answer in this structure:

1. **Existing App Audit**
2. **Style Direction Options and Recommendation**
3. **Chosen/Recommended Design Direction**
4. **Design System Definition**
5. **Component Library Specification**
6. **Page-by-Page Redesign Plan**
7. **Implementation Phases for Claude Code**
8. **Validation Checklist**
9. **Backend/API/Product-Logic Risks** — only include real risks; otherwise say “None identified.”

---

## 6. Success Criteria

The redesign plan is successful if:

- The app remains functionally the same
- The UI has one coherent design system
- Shared components are redesigned before pages
- Every page uses the shared system instead of ad-hoc styling
- Empty, loading, error, disabled, hover, focus, and mobile states are covered
- Any missing backend data or API limitation is flagged instead of faked
- The implementation plan is concrete enough for Claude Code to execute safely
