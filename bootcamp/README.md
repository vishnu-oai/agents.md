# Codex + Scaffolding Bootcamp (45 min) — `agents.md`

This bootcamp starts from a **bare-bones** `agents.md` repo (we removed the existing `AGENTS.md` on purpose), then progressively adds just enough structure to ship features safely with Codex.

## What you will do

- **Phase 1**: Create a high-quality `AGENTS.md`, add `.codex/config.toml`, and create a plan template `docs/PLAN.md`
- **Phase 2**: Use Codex to add a top-level **navbar** with 4 pages
- **Phase 3**: Write a **Skill** for “add a new page” (planning, styling, validation, dependency hygiene)
- **Phase 4**: Use your Skill to ship a **new page end-to-end** (and update the navbar)
- **Phase 5**: Run the **full scaffolding bootstrap** (understanding-only) and skim the key artifacts

## Repo context

This repo is a small Next.js (Pages Router) site in the repo root.

You’ll use:
- `pnpm dev` (iteration)
- `pnpm lint` (lint)
- `pnpm exec tsc --noEmit` (typecheck)

Important workflow rule for agent sessions:
- **Iterate with the dev server. Do not run `pnpm build` during interactive agent sessions.**

---

## Phase 0 — Setup (5 min)

### Run locally

```bash
cd ~/code/agents.md
pnpm install
pnpm dev
# open http://localhost:3000
```

### Success criteria
- Site loads locally.

---

## Phase 1 — Repo guidance + Codex config + plan template (12 min)

### Task A — Create a high-quality `AGENTS.md` (required)

Create a new `AGENTS.md` at the repo root. Keep it concise and operational.

Your `AGENTS.md` must include:

- **Project summary (2 lines)**: what this repo is + what the agent should optimize for.
- **Key entrypoints (paths)**:
  - `pages/index.tsx`
  - `pages/_app.tsx`
  - `components/`
  - `styles/globals.css`
- **Dev workflow**:
  - `pnpm install`
  - `pnpm dev`
- **Validation workflow**:
  - `pnpm lint`
  - `pnpm typecheck` (you will add this script below)
- **Agent guardrails** (explicit):
  - Use the dev server for iteration.
  - **Do not run `pnpm build` during interactive agent sessions.**
  - Keep diffs small and reviewable.
  - If you add/update deps: update lockfile and restart dev server.
- **Definition of done** checklist:
  - lint + typecheck pass
  - manual smoke tested in browser (record what you verified)
  - PR-ready summary + test plan written

Tip: You may try Codex `/init` to generate a first draft, but you must tailor it to this repo.

### Task B — Create `.codex/config.toml` (required)

Create `.codex/` at repo root and add `config.toml` configured for:

- model: **`gpt-5.2-codex`**
- reasoning: **medium**
- sandbox permissions: **dangerously allow**
- web search: **enabled**

Create:

`./.codex/config.toml`

```toml
model = "gpt-5.2-codex"
reasoning = "medium"

[sandbox]
permissions = "dangerously_allow"

[tools]
web_search = true
```

If your Codex installation expects slightly different field names, adjust as needed — but the **intent must match** (model, medium reasoning, dangerously-allow sandbox, web search enabled).

### Task C — Add a plan template: `docs/PLAN.md` (required)

Create `docs/PLAN.md`. This is a template you will **fill in before implementing** Phase 4’s page feature.

`docs/PLAN.md` must include these sections:

- **Purpose**
- **Scope**
- **Non-goals**
- **Files to touch**
- **Plan of work** (ordered steps)
- **Validation** (exact commands)
- **Manual smoke test**
- **PR summary**
- **PR test plan**

### Task D — Add a `typecheck` script (required)

Update `package.json` scripts to include:

- `"typecheck": "tsc --noEmit"`

### Validate (required)

```bash
pnpm lint
pnpm typecheck
```

### Success criteria
- `AGENTS.md` is actionable and repo-specific.
- `.codex/config.toml` exists and matches the required intent.
- `docs/PLAN.md` exists and is usable as a template.
- `pnpm typecheck` works.

---

## Phase 2 — Add a top-level navbar + pages (10 min)

### What to build (required)

Add a top-level navbar visible on **all pages**.

Navbar items (exact):
- **Home** → `/`
- **About** → `/about`
- **Contact Us** → `/contact`
- **Docs** → `/docs`

Implementation requirements:
- Create `components/NavBar.tsx`.
- Render it from `pages/_app.tsx` (so it appears on every page).
- Create destination pages:
  - `pages/about.tsx`
  - `pages/contact.tsx`
  - `pages/docs/index.tsx`
- Each new page must have:
  - `<h1>` with the page title
  - 2–4 short paragraphs of real placeholder content (not empty)
- Styling:
  - Use the repo’s existing Tailwind conventions
  - Must look acceptable in light/dark mode
  - Must remain usable on narrow screens (stacking is fine)

### Validate (required)

```bash
pnpm lint
pnpm typecheck
```

### Manual smoke test (required)
- Navbar appears on `/` and all new pages.
- Each link navigates correctly.
- Narrow window: navbar remains usable.

### Success criteria
- Navbar works globally and pages exist.
- Lint + typecheck pass.

---

## Phase 3 — Write a Skill: “add a new page end-to-end” (7 min)

### Task (required)

Create a Skill at:

`./.codex/skills/add_new_page/SKILL.md`

This Skill must tell Codex how to add a new page **end-to-end** in *this* repo, including:

- making an implementation plan (using `docs/PLAN.md`)
- matching styling (Tailwind + dark mode)
- updating the navbar
- validation (lint + typecheck + smoke test)
- dependency hygiene (lockfile, restart dev server)
- producing commit-ready output (PR summary + test plan, and a “ready to commit” checklist)

Your Skill should contain (at minimum):

- **Purpose**
  - Add a new page to this Next.js repo end-to-end.
- **When to use**
  - Any time you add a new route/page and need consistent UX + validation.
- **Inputs**
  - Page name, route, navbar label
  - Content requirements
  - Acceptance criteria
- **Plan requirement (mandatory)**
  - Before coding: **fill in `docs/PLAN.md` for the specific change**
  - Plan must include: files, non-goals, steps, validation, smoke test, PR text
- **Implementation checklist (ordered)**
  - Create `pages/<route>.tsx` (or `pages/<route>/index.tsx` as appropriate)
  - Ensure page uses consistent layout/typography patterns
  - Update `components/NavBar.tsx` to link to the new page
  - Add/adjust any shared components (keep minimal)
  - If deps are needed: update `package.json` + lockfile, restart dev server
- **Testing & validation**
  - Run `pnpm lint`
  - Run `pnpm typecheck`
  - Manual smoke checklist (route loads, navbar link works, dark mode OK)
- **Outputs**
  - List of files changed
  - PR-ready **Summary** (2–3 bullets)
  - PR-ready **Test plan** (commands + manual steps)
  - “Ready-to-commit” checklist

### Success criteria
- The Skill is a runnable recipe (checklist + commands), not an essay.
- It references constraints from `AGENTS.md` (dev server; don’t run build).
- It explicitly requires updating `docs/PLAN.md` before implementation.

---

## Phase 4 — Use your Skill to ship a new page (6 min)

### Feature (required)

Add a new page:

- **Name**: Guides
- **Route**: `/guides`
- **Navbar label**: Guides (add as a 5th nav item)

Guides page content requirements:
- `<h1>Guides</h1>`
- Section: “How to write a good AGENTS.md” (3–5 bullets)
- Section: “What matters in this repo” referencing real paths/commands (from your `AGENTS.md`)
- Links to:
  - `/docs`
  - `/` (Home)

### Process requirement (mandatory)

Follow your Skill workflow exactly:

1) Fill `docs/PLAN.md` for this specific change first (do not skip)
2) Implement the page + navbar update
3) Validate + smoke test
4) Produce PR-ready summary + test plan (wherever your cohort is collecting it)

### Validate (required)

```bash
pnpm lint
pnpm typecheck
```

### Manual smoke test (required)
- Navbar includes Guides.
- `/guides` loads; content is present; links work.
- Dark mode doesn’t break readability.

### Success criteria
- You followed your Skill (plan → implement → validate → PR-ready output).
- Lint + typecheck pass.

---

## Phase 5 — Run full scaffolding bootstrap (understanding-only)

This is purely to understand the broader scaffolding baseline. You do not need to fully adopt it today.

### Clone the bootstrap repo into `agents.md/` (local-only)

Visit the Repo at - https://github.com/openai/codex-scaffolding-bootstrap
Go through the README and fully understand what this repo does and how it can be helpful to your development!


### Run the bootstrap interview

Follow:
- `_bootstrapper_reference/codex-scaffolding-bootstrap/prompts/bootstrap/BOOTSTRAP.md`

### What to skim after it runs (10 min max)
- `AGENTS.md` (what it adds/changes)
- `docs/conventions/README.md`
- `docs/PLANS.md`
- `docs/meta/TECH_DEBT.md`
- `.codex/skills/`

### Deliverable

Write 5 bullets:
- 2 artifacts you’d keep long-term for `agents.md`
- 2 artifacts that feel like overhead today
- 1 thing you learned about working with Codex more effectively

