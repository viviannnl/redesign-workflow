# Redesign Workflow Prompts

A two-prompt workflow for redesigning an existing production app with AI while keeping product logic safe.

The key idea is to separate **design exploration** from **implementation handoff**:

1. Use `redesign-prompt.md` with **Claude Design** to create the redesign direction, design system, component specs, and page-by-page plan.
2. Use `redesign-handoff.md` with **Claude Code** to implement the approved design in the real app without changing backend behavior or product logic.

This is meant for existing apps, not brand-new greenfield projects.

---

## Files

| File | Use it with | Purpose |
| --- | --- | --- |
| `redesign-prompt.md` | Claude Design | Explore and define the redesign. Produces the visual direction, design system, component library, page-by-page plan, and implementation phases. |
| `redesign-handoff.md` | Claude Code | Implement the approved design in the existing codebase. Keeps changes frontend-focused and verifies behavior stays intact. |
| `design-inspiration/README.md` | You + Claude Design | Optional place to collect style references, links, screenshots, and notes before running the design prompt. |

---

## Tooling Expectation for Claude Code

For the handoff step, Claude Code should have access to:

- A local dev server for the app
- A local browser it can control or inspect
- Screenshot capture
- Screen recording, when available

This matters because visual fidelity cannot be verified from code alone. Claude Code should open the actual rendered app, compare it against the approved Claude Design artifact, check responsive states, and capture visual evidence when possible.

---

## Recommended Workflow

### Step 1: Prepare your app context

Open your existing app/repo and gather anything useful:

- Link to the GitHub repo
- Screenshots of the current app
- Screenshots or links to design inspiration, if you have any
- Notes about what feels outdated, confusing, or inconsistent
- Any constraints Claude must preserve, such as auth, billing, API contracts, or important user flows

If you do not have design inspiration yet, that is okay. Claude Design can still propose style directions based on the product, audience, and current UI.

### Step 2: Run the design prompt in Claude Design

Use `redesign-prompt.md` first.

Tell Claude Design something like:

```text
Use this prompt to redesign my existing app. The app is here: [repo/link/context].
Please audit the current UI, propose style directions, then create the design system and page-by-page redesign plan.
```

Expected output:

- Existing app audit
- Design direction
- Optional style direction options
- Design system definition
- Component library specification
- Page-by-page redesign plan
- Implementation phases for Claude Code
- Validation checklist
- Backend/API/product-logic risks, if any

Do not skip this step. The design prompt is where taste, style, hierarchy, and system decisions should happen.

### Step 3: Pick or refine the design direction

Before implementation, choose the direction you actually want.

Useful things to say:

```text
I like option 2, but make it warmer and less enterprise-looking.
```

```text
Keep the layout structure from option 1, but use the typography and surfaces from option 3.
```

```text
This feels too generic SaaS. Make it more editorial, calmer, and more founder-tool focused.
```

The goal is to reach an approved design direction before Claude Code touches the app.

### Step 4: Hand the approved design to Claude Code

Once the design is approved, use `redesign-handoff.md` with Claude Code.

Give Claude Code:

- The approved Claude Design output
- Any generated design file/artifact
- The app repo
- `redesign-handoff.md`
- Local browser access so it can inspect the rendered app
- Screenshot and screen-recording capability, if available

Tell Claude Code something like:

```text
Implement this approved redesign in the existing app. Use the handoff prompt. Preserve all backend/API/auth/product behavior. Start by creating a new redesign branch from the up-to-date default branch. Work in phases: tokens, shared components, then pages. Verify with lint/typecheck/build. Then use local browser access to open the app, compare the actual rendered UI against the approved Claude Design artifact, check the browser console, and capture screenshots or a short screen recording for visual verification when possible. After verification, push the branch and open a pull request for the redesign.
```

Expected output:

- Frontend-only implementation
- A dedicated redesign branch, not direct work on `main`
- Shared design tokens/components first
- Page updates using the approved system
- Browser-based comparison of the rendered UI against the approved design
- Screenshots or screen recording when available
- Verification results
- A pull request link for human review
- Notes about any limitations or conflicts

---

## How to Decide the Style Direction

You do not need to know the exact style upfront. A good redesign process can discover it.

If you are unsure, ask Claude Design for 3 directions:

1. **Conservative** — closest to the current app; safest implementation.
2. **Strong-fit** — the best balanced recommendation for your product and audience.
3. **Divergent** — more distinctive and opinionated; useful for finding taste boundaries.

Then react to what you see. You can say what feels right or wrong in normal language:

- “too corporate”
- “too playful”
- “too dark”
- “too generic SaaS”
- “more premium”
- “more minimal”
- “more editorial”
- “more like a serious developer tool”
- “more warm and founder-friendly”

Claude Design should translate that taste feedback into tokens, components, and layout rules.

---

## Optional: Design Inspiration Folder

The `design-inspiration/` folder is optional. Use it when you have references.

You can add:

- Screenshots
- Product links
- Notes about what you like or dislike
- Color or typography references
- Existing brand assets

Do not copy another product exactly. Use references to describe principles: density, hierarchy, mood, interaction patterns, typography, or layout rhythm.

---

## Important Safety Rules

This workflow is intentionally strict because redesigns can accidentally break real products.

Claude should not:

- Change backend architecture
- Change database schema
- Change API contracts
- Change auth, billing, or permission logic
- Add fake metrics, fake testimonials, or fake social proof
- Invent product features that do not exist
- Add disconnected buttons or UI that implies unsupported functionality

If a desired design requires missing data or backend work, Claude should flag it instead of faking it.

---

## Who This Is For

This workflow is useful if you have:

- A working app that looks inconsistent or outdated
- A product you want to polish without changing backend logic
- A Claude Design artifact that needs to become production frontend code
- A Claude Code implementation that needs stronger guardrails

---

## License

MIT
