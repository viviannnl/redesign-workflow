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
| `claude-code/commands/redesign.md` | Claude Code | Optional installable `/redesign` slash command so users do not need to paste the full handoff prompt every time. |
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

## Recommended Claude Code Setup: Install as a Command

If you use Claude Code often, you can install this workflow as a project command.

Copy:

```text
redesign-workflow/claude-code/commands/redesign.md
```

into your app:

```text
your-app/.claude/commands/redesign.md
```

Beginner-friendly terminal version from your app root:

```bash
mkdir -p .claude/commands
cp path/to/redesign-workflow/claude-code/commands/redesign.md .claude/commands/redesign.md
```

Then place your downloaded Claude Design export at:

```text
your-app/redesign-reference/claude-design-export/
```

You can create the folder from your app root with:

```bash
mkdir -p redesign-reference/claude-design-export
```

Open Claude Code from your app root and run:

```text
/redesign
```

The command instructs Claude Code to use the local design export, create a redesign branch, implement the UI, verify it in a browser when available, push the branch, and open a PR if the repo and local tooling allow it.

This is the recommended way to use the Claude Code handoff because it avoids repeatedly pasting the full handoff prompt. You can still use `redesign-handoff.md` manually if you do not want to install the command.

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
I want a bold, creative redesign that is specific to the product name, what the product does, and my preferred style direction, if any: [calm / playful / premium / editorial / pinky / serious developer tool / etc.]. Do not only change fonts and colors; rethink layout, hierarchy, interaction patterns, and product storytelling while preserving existing functionality.
```

Expected output:

- Existing app audit
- Product-specific creative strategy
- Design direction
- Optional style direction options
- Design system definition
- Component library specification
- Page-by-page redesign plan
- Creativity and reskin check explaining what changed beyond fonts/colors/palette
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

### Step 4: Download the Claude Design ZIP

Once the design is approved, download the project/artifact ZIP from Claude Design.

Do this instead of handing Claude Code only a Claude Design share link. The ZIP gives Claude Code actual local files it can inspect, open, and compare against the implemented app.

Recommended setup:

```text
your-app/
  redesign-reference/
    claude-design-export/
      [unzipped Claude Design files]
```

You can name the folder whatever you want, but keep the exported design files inside the app/repo directory so Claude Code can read them directly.

### Step 5: Hand the approved design files to Claude Code

After the ZIP is downloaded and unzipped into the app directory, the recommended Claude Code path is to run the installable `/redesign` slash command.

You can still paste `redesign-handoff.md` manually, but installing the command is more convenient because users only need to run `/redesign` from the app root.

Give Claude Code:

- The approved Claude Design output/notes
- The local path to the unzipped Claude Design export, for example `redesign-reference/claude-design-export/`
- The app repo
- The installed `/redesign` command or `redesign-handoff.md`
- Local browser access so it can inspect the rendered app
- Screenshot and screen-recording capability, if available

Recommended Claude Code command usage:

```text
/redesign
```

If your design export is somewhere else, pass the path as an argument:

```text
/redesign use the local Claude Design export at path/to/design-export
```

Manual fallback prompt:

```text
Implement this approved redesign in the existing app. Use the handoff prompt. The Claude Design ZIP has been downloaded and unzipped locally at: [path to redesign-reference/claude-design-export]. Use those local files as the design reference, not only a share link. Preserve all backend/API/auth/product behavior. Start by creating a new redesign branch from the up-to-date default branch. Work in phases: tokens, shared components, then pages. Verify with lint/typecheck/build. Then use local browser access to open the app, compare the actual rendered UI against the local Claude Design export, check the browser console, and capture screenshots or a short screen recording for visual verification when possible. After verification, push the branch and open a pull request for the redesign.
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

1. **Evolutionary** — improves the current product while still changing layout and hierarchy meaningfully.
2. **Strong-fit bold** — the best balanced recommendation for your product name, audience, workflow, and requested style.
3. **Revolutionary** — more distinctive and opinionated; useful when you want a very creative redesign that changes composition, interaction patterns, and product storytelling while preserving behavior.

The goal is not just a new palette. A strong redesign should connect the visual system to what the product does and should change layout, hierarchy, components, states, and interaction patterns where that makes the product clearer or more memorable.

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
