# Existing App Redesign Prompt

You are redesigning an existing production web application.

This is **not** a greenfield project. This is a constrained UI/UX modernization of a working product. Preserve the app’s current product behavior while improving clarity, consistency, polish, and usability.

---

## 1. Primary Goal

Create a modern, consistent, and product-specific design system for the existing application, then apply it across the app without changing backend behavior or product logic.

This should be a real redesign, not a light reskin. Do not stop at changing fonts, colors, border radius, or button styles. Reconsider layout structure, information architecture, interaction patterns, visual metaphors, navigation, empty states, and the overall product storytelling while preserving what the app actually does.

Optimize for:

- A bold, memorable visual direction that feels specific to the product name, product purpose, and target user
- Visual consistency across every page and state
- Clearer information hierarchy and stronger page composition
- Better usability for real users
- A user experience that makes sense for the product’s actual audience, workflow, emotional context, and level of complexity
- Creative but usable layout, navigation, and component patterns
- Cleaner, more premium, modern UI
- Reusable components instead of one-off page styling
- Accessibility, responsive behavior, and empty/loading/error states

Do **not** change what the product does. Change how clearly, memorably, and beautifully it presents the existing product.

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

### Step 2 — Product-Specific Creative Strategy

Before choosing a style direction, define the creative strategy behind the redesign.

Analyze:

- Product name and what it implies visually or conceptually
- What the product actually helps users do
- Target user, emotional context, and desired confidence level
- Any user-requested style preference, such as “pinky,” “editorial,” “calm,” “playful,” “serious developer tool,” or “premium”
- Product-specific metaphors that could inform the interface without becoming gimmicky

Output:

- 2–3 possible creative concepts tied to the product name/purpose
- Which concept best fits the product and why
- How the user’s requested style preference should influence color, typography, surfaces, layout, motion, and tone
- What would count as a shallow reskin for this product and must be avoided

### Step 2.5 — User Experience and Product Fit

Before proposing final style directions, evaluate whether the product experience itself makes sense for real users. Do not judge the redesign only by visual polish.

Analyze:

- What the main user is trying to accomplish and what they need to understand first
- Whether the current main flow is obvious, confusing, too slow, too dense, or missing helpful guidance
- Whether each page makes the next action clear without overwhelming the user
- Whether the information hierarchy matches the user’s real decision-making order
- Whether navigation, layout, and grouping fit the product category and workflow
- Whether empty, loading, error, disabled, success, and permission/auth states help the user recover or continue
- Whether the tone and interaction model match the product’s audience, emotional context, and trust level
- Whether the redesign reduces confusion and cognitive load instead of adding decoration

Output:

- 3–5 user experience principles for this specific product
- The most important user flow improvements to preserve in the redesign
- Product-fit risks where a visually interesting idea might make the product harder to use or less trustworthy
- What the redesign should make easier, clearer, faster, calmer, or more confidence-building for users

### Step 3 — Style Direction Exploration

Before defining the final design system, propose style directions for the redesign.

If design inspiration, screenshots, brand assets, or a `design-inspiration/` folder are provided, use them as reference material. Do not copy another product exactly; extract principles such as density, hierarchy, mood, rhythm, typography, and interaction posture.

If no inspiration is provided, generate 3 possible directions:

1. **Evolutionary** — improves the current product while still changing layout and hierarchy meaningfully; safest implementation.
2. **Strong-fit bold** — your best recommendation for this product, audience, workflow, name, and requested style.
3. **Revolutionary** — a more distinctive, memorable, and opinionated redesign that changes the composition, interaction model, and product storytelling while preserving behavior.

At least one direction must be meaningfully bold. “Same layout with new fonts and colors” is not acceptable as the strongest recommendation unless the user explicitly asks for a conservative refresh.

For each direction, include:

- Name
- 3–5 words describing the feel
- Best-fit audience/product rationale
- Product-name/product-purpose connection
- User experience rationale: why this direction makes the product easier, clearer, more trustworthy, or more enjoyable to use
- Visual principles: typography, color posture, spacing/density, surfaces, motion
- Structural changes: navigation, page composition, hero/dashboard model, data visualization using existing frontend-available fields only, and frontend interaction patterns using existing routes, data, permissions, and actions only
- Signature moments: 2–3 memorable UI ideas that make the product feel distinctive without implying unsupported functionality
- What it intentionally avoids
- Implementation complexity: low/medium/high

Then recommend one direction and explain why. If the user requested a bold, creative, or revolutionary redesign, prefer the strongest safe direction over the most conservative one.

### Step 4 — Design System Definition

After style direction is chosen or recommended, extract and define a unified design system that fits the product.

Include:

- Design direction: 3–5 words describing the desired feel
- Core concept: how the design expresses the product name, product purpose, and requested style preference
- Typography scale and usage rules
- Color system, including semantic colors for success/warning/error/info
- Spacing scale
- Border radius rules
- Shadow/elevation rules
- Layout grid and page width rules
- Navigation and information architecture rules
- Data visualization and dashboard composition rules using existing frontend-available fields only, if relevant
- Icon style rules
- Motion/transition rules, if used
- Responsive behavior rules
- Accessibility rules: contrast, focus states, keyboard usability, reduced motion

Important: define tokens and rules first. Do not jump directly into page mockups.

### Step 5 — Core Component System

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

### Step 6 — Page-by-Page Redesign Plan

Only after the design system and components are defined, plan each page.

For every page/route, provide:

- Current purpose of the page
- Main user action on the page
- User experience goal: what should feel easier, clearer, faster, calmer, or more confidence-building for the user
- Structural layout changes, not just styling changes
- Information hierarchy changes: what becomes more prominent, grouped, collapsed, or sequenced differently
- Product-specific creative treatment: metaphor, visual motif, data/storytelling model using existing frontend-available fields only, or signature interaction using existing routes/actions only
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
- Avoid “reskin-only” plans. Every major page should include at least one meaningful improvement to layout, hierarchy, composition, interaction, or storytelling unless the existing structure is already ideal.
- Do not hide or de-emphasize critical controls, legal/compliance content, permission/auth states, destructive actions, pricing/billing information, errors, or required workflow steps.

### Step 7 — Implementation Sequencing

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

### Step 8 — Consistency, Creativity, and Safety Validation

Before final output, check for:

- Reskin-only changes where the layout, hierarchy, and interaction model stayed essentially the same
- Weak connection between the visual direction and the product name, product purpose, target user, or requested style
- Product-fit issues where the UI looks interesting but makes the real user flow harder to understand or complete
- User experience gaps where the next action, system state, recovery path, or success state is unclear
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
2. **Product-Specific Creative Strategy**
3. **User Experience and Product Fit**
4. **Style Direction Options and Recommendation**
5. **Chosen/Recommended Design Direction**
6. **Design System Definition**
7. **Component Library Specification**
8. **Page-by-Page Redesign Plan**
9. **Implementation Phases for Claude Code**
10. **Creativity, UX, and Reskin Check** — explain why this is more than fonts/colors/palette, what structurally changes, and how the experience becomes clearer or better for users.
11. **Claude Code HANDOFF.md** — create a separate concise redesign-specific handoff artifact/file for the Claude Design export named `HANDOFF.md`. Include the approved design direction, key tokens, component specs, page-by-page implementation notes, structural changes, visual fidelity requirements, verification checklist, and product-logic risks.
12. **Validation Checklist**
13. **Backend/API/Product-Logic Risks** — only include real risks; otherwise say “None identified.”

---

## 6. Success Criteria

The redesign plan is successful if:

- The app remains functionally the same
- The UI has one coherent design system
- The creative direction is tied to the product name, product purpose, target user, and requested style preference
- The user experience makes sense for the product’s real audience, workflow, emotional context, and complexity
- The redesign makes important user flows easier to understand, complete, recover from, or trust
- The redesign changes more than fonts, colors, and palette; it improves layout, hierarchy, composition, interaction, or product storytelling
- Shared components are redesigned before pages
- Every page uses the shared system instead of ad-hoc styling
- Empty, loading, error, disabled, hover, focus, and mobile states are covered
- Any missing backend data or API limitation is flagged instead of faked
- The implementation plan is concrete enough for Claude Code to execute safely
