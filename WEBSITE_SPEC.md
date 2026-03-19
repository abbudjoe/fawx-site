# Fawx Website Spec — fawx.ai

**Target:** Complete website for Fawx launch. Replaces the current single-page site.
**Audience:** Developers and power users who want a local-first AI agent.
**Design base:** Existing `index.html` design language (cream/charcoal/orange, Inter + JetBrains Mono, dark mode via prefers-color-scheme).
**Deployment:** Static HTML/CSS/JS on Vercel (already configured).
**No frameworks.** Plain HTML + CSS. No React, no Tailwind, no build step. Keep it like the current site.

---

## Sitemap

```
fawx.ai/
├── index.html          — Landing page (hero, features, demo, download CTA)
├── download.html       — Download page (DMG link, system reqs, quick start)
├── about.html          — Vision and philosophy
├── docs/
│   ├── index.html      — Docs hub / getting started overview
│   ├── setup.html      — Setup wizard walkthrough
│   ├── tools.html      — Built-in tools reference
│   ├── skills.html     — WASM skill system
│   ├── fleet.html      — Multi-machine fleet setup
│   └── security.html   — Kernel safety architecture
```

---

## Global Design System

### Already established (keep these):
- **Palette:** `--bg: #F5F0EB`, `--accent: #E8622B`, `--text: #1A1A1A`, `--terminal-bg: #1E1E2E`, `--terminal-green: #A6E3A1`
- **Fonts:** Inter (body), JetBrains Mono (code/mono)
- **Dark mode:** `prefers-color-scheme: dark` with inverted palette
- **Nav:** Fixed top bar with blur backdrop, logo + links + CTA button
- **Sections:** `.section-tag` (small caps label), `.section-heading` (large h2), `.section-sub` (muted description)
- **Terminal blocks:** Dark rounded card with colored syntax
- **Cards:** White/raised cards with subtle border and shadow
- **Max width:** 1200px container

### New additions needed:
- **Docs sidebar layout:** Left sidebar nav (240px) + main content area. Sidebar fixed on desktop, collapsible on mobile.
- **Docs content styling:** Prose-optimized (max 720px content width within the main area), larger line-height (1.8), code blocks with copy button.
- **Breadcrumbs:** `Docs > Setup` style, small text above page title on doc pages.
- **Nav updates:** Add links for Download, Docs, About. Remove GitHub link (no public repo). Keep the accent CTA button for Download.

---

## Page Specs

### 1. index.html — Landing Page

**Purpose:** First impression. Explain what Fawx is, show it working, make them want to download it.

**Sections (in order):**

#### Hero
- **Headline:** "Your AI runs here." (or similar — emphasize local-first, your hardware)
- **Subhead:** One sentence: agentic engine, Rust, tools, memory, your API keys, your machine.
- **CTA buttons:** "Download for macOS" (primary, links to /download) + "Read the docs" (secondary, links to /docs/)
- **Visual:** The fawx-new.png mascot stays. Consider adding a small terminal mockup showing a real interaction.
- **Remove:** The "Star on GitHub" button/link. No public repo.

#### Features grid
- Keep the existing 6-card grid (Rust, Memory, Tools, WASM, Kernel Safety, Multi-Channel)
- **Update copy** to reflect current state:
  - Multi-Channel → mention native macOS + iOS app alongside TUI and Telegram
  - WASM → mention signed plugins, hot-reload, marketplace
  - Kernel Safety → mention capability-space model (AX-first), not permission prompts
- Add a 7th card if needed: "Native Apps" — macOS + iOS with SwiftUI

#### Demo / "See it work"
- Keep the terminal demo block
- **Update the demo content** to show a realistic interaction: user asks something, Fawx thinks, calls a tool, returns a result
- Should feel real, not contrived

#### Architecture
- Keep the 3-layer diagram (kernel / loadable / shells)
- Update description to reflect AX-first model: "The kernel defines boundaries, not checkpoints. Actions within your capability space execute instantly. Cross a boundary and the kernel journals it silently. Only irreversible actions get hard blocks."

#### Getting Started
- **Rewrite for macOS app install** (not `cargo install`):
  1. Download the DMG
  2. Open Fawx → Setup wizard walks you through provider auth
  3. Start chatting
- Keep it to 3 steps max. The wizard handles complexity.

#### Skills / Ecosystem
- Keep the WASM skills section
- Note: community skills coming soon, link to docs/skills.html for details

#### Footer
- Links: Download, Docs, About
- Remove GitHub link
- "Built by Joe." or similar

---

### 2. download.html — Download Page

**Purpose:** Get the app installed. Fast, clear, no friction.

**Content:**

#### Download hero
- macOS DMG download button (big, obvious, primary accent color)
- Version number + release date
- "Requires macOS 14+ (Sonoma or later)" — system requirements below the button

#### Quick start (3 steps)
1. Open the DMG, drag Fawx to Applications
2. Launch Fawx — the setup wizard walks you through connecting your AI provider
3. Start chatting (or run `fawx` in terminal for TUI mode)

#### What's included
- Fawx engine (single Rust binary)
- Native macOS app (SwiftUI)
- Terminal UI (ratatui)
- 13+ built-in tools
- WASM skill runtime
- Encrypted credential store

#### System requirements
- macOS 14+ (Sonoma)
- Apple Silicon or Intel
- API key for Claude, ChatGPT, or compatible provider
- Optional: Tailscale for fleet/multi-machine setup

#### iOS
- "iOS app coming soon" with a brief note. Don't overpromise.

#### Previous versions / changelog
- Link to release notes (can be a simple section or future page)

---

### 3. about.html — About / Vision

**Purpose:** Why Fawx exists. What makes it different. The philosophy.

**Content (narrative, not bullet points):**

#### The thesis
- AI assistants today run on someone else's server, through someone else's interface, with someone else's rules.
- Fawx runs on YOUR hardware, with YOUR API keys, under YOUR control.
- It's not a chatbot wrapper — it's an agentic engine. It thinks, plans, calls tools, and remembers.

#### What makes Fawx different
- **Local-first:** Your data never leaves your machine unless you explicitly ask it to.
- **Agent, not assistant:** Fawx doesn't just respond — it plans multi-step actions, uses tools, and learns from outcomes.
- **Kernel safety:** A compiled safety layer the AI cannot modify, inspect, or bypass. Not prompt-based guardrails — real enforcement.
- **Self-extending:** WASM skill plugins let Fawx learn new capabilities without rebuilding.
- **Multi-surface:** Same engine powers the TUI, the native app, Telegram, and HTTP API.

#### Where it's headed (vague, no proprietary details)
- Fleet: distribute work across multiple machines
- Local models: on-device inference, zero cloud dependency
- More platforms (iOS shipping, Android planned)

#### Who built this
- Brief note. Don't need a full bio — just enough to be human.

---

### 4. docs/index.html — Docs Hub

**Purpose:** Entry point for all documentation. Getting started guide + links to detailed pages.

**Layout:** Sidebar nav (links to all doc pages) + main content.

**Content:**

#### Getting started (inline, not a separate page)
- What Fawx is (2 sentences)
- Install (link to /download)
- First run: setup wizard overview
- Your first conversation
- Next steps: link cards to setup, tools, skills, fleet, security pages

#### Quick reference cards
Grid of cards linking to each doc page with a one-liner:
- **Setup** — Provider auth, permissions, configuration
- **Tools** — What Fawx can do out of the box
- **Skills** — Extend with WASM plugins
- **Fleet** — Multi-machine setup
- **Security** — How the kernel keeps things safe

---

### 5. docs/setup.html — Setup Guide

**Content:**

#### Setup wizard walkthrough
- Step 1: Choose your AI provider (Claude, ChatGPT, or API key)
- Step 2: Authentication flow for each provider
  - Claude: setup token or API key
  - ChatGPT: OAuth PKCE flow (browser opens, you authorize)
  - API key: paste your key, it's encrypted locally (AES-256-GCM)
- Step 3: Permission preset (Open / Standard / Restricted)
  - Explain what each means in plain language
  - Default is Standard (capability space with boundaries)

#### Configuration
- Config file location: `~/.fawx/config.toml`
- Key settings: model, thinking level, tools, permissions
- Hot-reload: change config, Fawx picks it up (SIGHUP)

#### Multiple providers
- How to add additional providers after initial setup
- Model switching mid-conversation (`/model` command)

---

### 6. docs/tools.html — Tools Reference

**Content:**

#### What are tools?
- Brief explanation: tools are actions Fawx can take autonomously
- The agent decides when and how to use them based on your request

#### Built-in tools (table or card grid)
For each tool:
- Name
- What it does (one sentence)
- Example usage (what you'd say to trigger it)

Tools to document:
- read_file, write_file, list_directory
- run_command (shell execution)
- web_search, web_fetch
- browser (headless browser control)
- memory_search, memory_write
- git_status, git_commit, git_push
- github_pr_create

#### Tool permissions
- How capability mode affects tool access
- What happens when a tool hits a boundary (capability mode: denied with explanation; prompt mode: asks for approval)

---

### 7. docs/skills.html — Skills / Plugins

**Content:**

#### What are skills?
- WASM plugins that extend Fawx with new capabilities
- Sandboxed execution (WASI runtime)
- Cryptographically signed (Ed25519)
- Hot-reloadable without restart

#### Available skills
- Weather, TTS, Calculator, GitHub
- Brave Search, Web Fetch, Scheduler
- Note: more coming, community contributions welcome soon

#### Installing skills
- `fawx skill install <name>` from marketplace
- Manual: drop `.wasm` file in skills directory

#### Creating skills
- `fawx skill create <name>` scaffolds a new skill project
- Skill SDK overview (Rust → WASM)
- Signing workflow: `fawx auth sign`
- Link to SDK docs (when published)

#### Domain allowlists
- Skills can declare network access requirements
- Per-skill domain restrictions enforced by the kernel

---

### 8. docs/fleet.html — Fleet / Multi-Machine

**Content:**

#### What is Fleet?
- Distribute work across multiple machines over Tailscale
- One primary, multiple workers
- Token-based authentication (HMAC-SHA256)

#### Setup
- Prerequisites: Tailscale installed on all machines, Fawx installed on all machines
- `fawx fleet init` on primary
- `fawx fleet join <primary-url>` on workers
- Verify: `fawx fleet list`

#### How it works
- Primary dispatches tasks to workers
- Workers execute and report results
- Heartbeat monitoring for health
- Capability-based routing (workers declare what they can do)

#### Use cases
- Distributed experiments (run evaluations across machines)
- Build/test on different platforms (macOS + Linux)
- Fleet of agents working on different tasks

---

### 9. docs/security.html — Security Architecture

**Content:**

#### Philosophy
- "Boundaries, not checkpoints" — the AX-first model
- The kernel defines what the agent CAN do, not what it must ask about
- Actions within capability space execute instantly (zero friction)
- Boundaries are enforced silently (tripwire + journal, no modal)
- Only irreversible actions outside the boundary get hard blocks

#### Three layers
1. **Capability space** (Layer 1, visible): What the agent can do freely. Configurable via presets (Open/Standard/Restricted).
2. **Tripwire + Ripcord** (Layer 2, invisible to agent): Silent monitoring within the capability space. If the agent crosses a tripwire, the kernel journals the action and enables atomic rollback. The agent never knows.
3. **Hard boundaries** (Layer 3, visible): Compiled restrictions the agent cannot bypass. Kernel source paths, credential store internals, system auth files.

#### Kernel immutability
- The kernel binary is code-signed and notarized
- No `--unsafe` flag, no env var override, no admin bypass
- The agent cannot read kernel source (compiled path restrictions)
- Safety layer is not prompt-based — it's compiled Rust

#### Encrypted credentials
- AES-256-GCM encryption at rest
- Credentials never exposed to the agent as plaintext
- Scoped access: agent can USE credentials (make API calls) but cannot READ them

#### Capability presets
- **Open:** Full filesystem, network, shell access. For trusted environments.
- **Standard:** Bounded filesystem (project directory), network allowed, shell with restrictions. Default.
- **Restricted:** Read-only filesystem, no shell, no network except allowlisted domains. For untrusted tasks.

---

## Copy Guidelines

- **Tone:** Confident, technical, concise. Not marketing-speak. Fawx is for people who read man pages.
- **No buzzwords:** Don't say "revolutionary," "game-changing," "leverages AI." Just say what it does.
- **Show, don't tell:** Terminal blocks with real commands and real output > bullet points about features.
- **Be honest about state:** If something is "coming soon," say so. Don't imply it ships today.
- **No GitHub references:** There is no public repo. Don't link to GitHub, don't mention stars, don't show a GitHub button.

## Asset Notes

- `fawx-new.png` — existing mascot, keep using it
- Terminal mockups should use the existing terminal block styling (dark bg, colored syntax)
- Consider adding a screenshot of the native macOS app on the landing page or download page
- App icon TBD — use the mascot for now

## Technical Notes

- All pages share the same CSS (inline in each page, or extract to a shared `style.css` — implementer's choice, but keep it zero-build-step)
- Dark mode must work on all pages
- Mobile responsive: nav collapses to hamburger (existing pattern), docs sidebar collapses
- No JavaScript required for core content. JS only for: mobile nav toggle, copy-to-clipboard on code blocks, docs sidebar toggle
- Vercel handles routing — `docs/setup` serves `docs/setup.html`
