# AI-Assisted iOS Development

**A Step-by-Step Guide**

Building a Complete iOS App with Cowork, Claude Agent & GitHub

Example Project: StreakPal — A Simple Habit Tracker

iOS 26+ · SwiftUI · Xcode 26.3

February 2026

---

## Introduction

This guide walks you through building a complete iOS app from idea to App Store submission, using an AI-assisted workflow built on three tools: Cowork (Claude Desktop), Claude Agent (Xcode 26.3), and GitHub.

Rather than explaining the workflow abstractly, we follow a concrete example: StreakPal, a simple habit tracker app. The app is small enough to build in a few sessions, but complex enough to exercise every part of the workflow.

**What you will build:** StreakPal lets users create daily habits, check them off, and track streaks. It uses SwiftUI for the interface, persists data with SwiftData, and follows MVVM architecture. No backend, no accounts, no external dependencies.

**How the tools divide the work:** Cowork handles planning, product specs, task tracking, and session memory. Claude Agent in Xcode handles all code implementation, building, testing, and visual verification. GitHub connects the two through issues, branches, and pull requests.

## What You Need Before Starting

**Claude Desktop with Cowork mode.** Cowork requires a paid Claude subscription (Pro, Max, Team, or Enterprise) and the Claude Desktop app for macOS or Windows x64. Download the latest version at claude.com/download. Once installed, install the following plugins from the Plugins sidebar: Productivity, Product Management, and Marketing.

**Xcode 26.3 with Claude Agent.** Xcode 26.3 introduced native support for agentic coding through the Claude Agent SDK. You need an active Apple Developer Program membership and an Anthropic account with API access. In Xcode, open Settings, navigate to Coding Agents, enable Claude Agent, and authenticate with your Anthropic account. Select a model — Claude Sonnet 4.5 is a good default for most implementation work; use Claude Opus 4.6 for complex architectural tasks.

**A GitHub account** with a personal repository for the project.

**Basic familiarity** with Swift, SwiftUI, and Git. You do not need to be an expert — the AI tools will handle most of the implementation — but you should understand enough to review the code they produce.

## How This Guide Is Organized

The guide has four parts: a setup phase that prepares the project infrastructure, followed by three development phases that build the app feature by feature. The development phases (1 through 3) align directly with the roadmap you will create, so there is no ambiguity about which phase you are in.

| Section | Tool | What Happens |
|---|---|---|
| Setup | Cowork + GitHub | Memory system, PRD, roadmap, repo, Xcode project |
| Phase 1: Foundation | Cowork → GitHub → Claude Agent | Data models, services, ViewModels, navigation |
| Phase 2: Core Features | Cowork → GitHub → Claude Agent | Habit list UI, check-off logic, streaks, calendar |
| Phase 3: Polish & Launch | Cowork + Claude Agent | Onboarding, settings, marketing, App Store |

---

## Understanding the Tools

Before diving into the workflow, it helps to understand what each tool does and where its boundaries are.

**Cowork** is a feature of the Claude Desktop app that gives Claude direct access to files on your computer and the ability to execute multi-step tasks autonomously. It runs inside an isolated virtual machine on your machine, which provides a layer of security. Cowork has no built-in memory between sessions — each session starts fresh. The Productivity plugin works around this limitation by storing structured files (CLAUDE.md, TASKS.md, and a memory/ directory) in your project folder, which Claude reads at the start of every new session. This file-based memory system is the foundation of the multi-session workflow described in this guide.

When you give Cowork a task, it will analyze your request and present a plan before executing. This plan review step is a key quality gate — it is the right moment to catch misunderstandings or redirect the approach before any work begins. Always review the plan before letting Cowork proceed.

**Claude Agent in Xcode** is an autonomous coding partner, not a line-by-line autocomplete tool. When you describe a goal, the agent analyzes your entire project structure, searches Apple's developer documentation, plans which files to create or modify, writes code across multiple files, builds the project, runs tests, and even captures Xcode Previews to visually verify the UI. It iterates autonomously until the task is complete or it needs your input. Xcode automatically creates milestones each time the agent makes a change, so you can revert to any prior state if the output is not what you wanted.

**GitHub** serves as the bridge between the two tools. Cowork drafts specifications that become GitHub Issues. Claude Agent implements those issues on feature branches. Pull requests provide a review checkpoint before code reaches the main branch.

### A Note on Costs

This workflow uses both tools heavily across multiple sessions, so understanding the cost model matters.

Cowork usage is included in your Claude subscription but consumes more of your usage allocation than standard chat. A single Cowork session that coordinates multiple sub-agents can consume as much usage as dozens of regular chat messages. Reserve Cowork for planning, spec writing, and task tracking — use standard Claude chat for quick questions and brainstorming.

Claude Agent in Xcode is billed based on API consumption through your Anthropic account. To manage costs, use focused prompts that minimize unnecessary exploration, and choose the appropriate model tier for each task. Claude Haiku works well for simple implementation tasks, Sonnet for moderate complexity, and Opus for complex architectural reasoning.

### A Note on Safety

Since this workflow grants both tools access to your project folder, follow a few safety practices. Keep sensitive materials — API keys, certificates, provisioning profiles — in a separate folder that neither tool accesses. Cowork will ask for your explicit permission before deleting any files, but it is still good practice to maintain backups of anything important. When reviewing Claude Agent's work in Xcode, use the transcript to understand the agent's reasoning, not just its final output. Treat agent-generated code the way you would treat a pull request from a colleague: review it thoroughly before merging.

---

## Setup: Project Initialization

Everything starts in Cowork. Before writing a single line of Swift, you establish the project's infrastructure: plugin-based memory, product requirements, a roadmap, and the repository.

### Step 0.1 — Initialize the Productivity System

Open Claude Desktop and switch to the Cowork tab. Select your project folder (create an empty one if needed — something like `~/Projects/StreakPal/`). Then invoke the Productivity plugin:

> `/start`

This is a command provided by the Productivity plugin (not a built-in Cowork feature). It creates the file-based memory system that provides continuity across sessions:

- **CLAUDE.md** — working memory that Claude reads at the start of every session
- **TASKS.md** — task tracker organized into Active, Up Next, Waiting On, Someday, and Done sections
- **memory/** — long-term storage for people, projects, glossary, and tools

When Cowork presents its plan, review it, then provide your project description:

> I'm building StreakPal, a simple habit tracker for iOS.
> SwiftUI only, iOS 26+, Xcode 26.3. Paid app on the App Store.
> Solo developer. Using Claude tools exclusively.
> MVVM architecture, SwiftData for persistence, no external dependencies.

**Why this matters:** Every future Cowork session reads CLAUDE.md first. The more accurate your initial context, the less you need to re-explain later. Because Cowork has no built-in memory between sessions, these files are the only thing that carries context forward. Treat updating them like committing code.

### Step 0.2 — Write the PRD

With the memory system initialized, draft your Product Requirements Document using the Product Management plugin:

> `/write-spec`

Describe StreakPal to the spec writer:

> StreakPal is a habit tracker app. Users can:
> - Create daily habits with a name and optional emoji
> - Check off habits each day
> - See their current streak for each habit
> - View a simple weekly calendar showing completion
>
> No accounts, no sync, no backend. All data stored locally using SwiftData.
> 4 tabs: Today, Habits, Stats, Settings.
> Target: $1.99 paid app on the App Store.

Cowork will present a plan, then generate a structured PRD with user stories, acceptance criteria, and priority levels (P0 = must-have, P1 = nice-to-have, P2 = future). Review it carefully — this document drives every implementation decision downstream. Ask for adjustments if needed, and save it as `docs/PRD.md`.

**Prompt tip:** Be specific about what is NOT in scope. Saying "no accounts, no sync" prevents the PRD from including features you don't want to build. Explicit exclusions save more time than detailed inclusions.

### Step 0.3 — Build the Roadmap

Convert the PRD into a phased development plan:

> `/roadmap-update`

> Create a development roadmap based on docs/PRD.md.
> I'm a solo developer working ~30 hrs/week.
> 3 phases, each ~1–2 weeks:
> Phase 1: Foundation (project setup, models, services, navigation)
> Phase 2: Core Features (habit CRUD, check-off, streaks, UI)
> Phase 3: Polish & Launch (onboarding, settings, App Store prep)
> Include definition of done for each phase.

Save as `docs/ROADMAP.md`. This document defines what gets built when. Each phase becomes a batch of GitHub issues, and the phase numbers in this guide (1, 2, 3) match the roadmap directly.

### Step 0.4 — Create the GitHub Repository

Create a repo on GitHub (or use the `gh` CLI) and clone it locally. Then set up context files that Claude Agent will read when it opens the project in Xcode. Ask Cowork:

> Set up context files for Claude Agent in Xcode.
> Create .claude/rules/ with:
> - project-context.md (what StreakPal is, key specs, doc locations)
> - conventions.md (SwiftUI only, MVVM, naming conventions, SwiftData)
> - architecture.md (rules for updating ARCHITECTURE.md, tiered format)

The `.claude/rules/` directory is a convention from the Claude Agent SDK (the same framework that powers both Claude Code and Xcode's Claude Agent integration). Files placed here are automatically loaded as context whenever Claude Agent opens the project, giving it the same background knowledge that Cowork has from CLAUDE.md.

Also create a PR template at `.github/pull_request_template.md`:

```markdown
## Summary
<!-- What does this PR do and why? -->

## Phase
<!-- Which roadmap phase does this belong to? -->

## Changes
<!-- List the key changes -->

## Out of Scope / Deferred
<!-- What was intentionally NOT included? Reference roadmap phase if applicable. -->

## Testing
<!-- How was this tested? What tests were added? -->
```

**Recommended workflow convention:** To avoid confusion about which tool should edit which files, establish clear ownership boundaries. Cowork manages CLAUDE.md, TASKS.md, memory/, PRD, and ROADMAP. Claude Agent manages all Swift code, .claude/rules/, and ARCHITECTURE.md. Both tools read the shared docs/ directory but only write to what they own. This is a convention you enforce, not a platform feature — neither tool has built-in access controls.

### Step 0.5 — Create the Xcode Project

This is your first run through the feature cycle that you will repeat for every feature in the app.

**Spec** (Cowork):

> Draft an issue spec for the Xcode project setup.
> Save it to docs/github-issues/001-xcode-project-setup.md.
> It should cover: creating the iOS 26+ SwiftUI project,
> folder structure (Models/, ViewModels/, Views/, Services/),
> SwiftData model container setup, .gitignore, and initial commit.

**Issue** (GitHub): Post the spec as a GitHub Issue. You can do this manually, or ask Cowork to use the `gh` CLI if it is available on your system. Add labels (`setup`, `P0`).

**Implement** (Claude Agent in Xcode):

> Implement GitHub Issue #1 (Xcode project setup).
> Read docs/github-issues/001-xcode-project-setup.md for details.

Claude Agent will analyze the spec, create the project structure, configure the build settings, and set up the initial SwiftData model container. Watch the transcript as it works — it shows every file explored, every decision made, and every build triggered. If the agent takes a wrong turn, you can pause it and redirect.

**Review and merge:** Create a feature branch (`setup/xcode-project-issue-1`), open a PR using the template, review the changes, squash-merge to main, and delete the branch. When reviewing, check the Xcode transcript to understand not just what changed but why the agent made each decision.

**Track** (Cowork):

> The Xcode project setup is done. PR merged to main.
> Update TASKS.md and memory.

**The feature cycle:** This is the core loop you will repeat for every feature: Spec (Cowork) → Issue (GitHub) → Implement (Claude Agent) → PR Review → Merge → Track (Cowork). The rest of this guide is variations on this cycle.

---

## Phase 1: Foundation

With the project scaffolded, build the invisible infrastructure: data models, services, ViewModels, and navigation. This phase has no visible UI — it is all architecture.

### Step 1.1 — Plan Phase Deliverables

Open a new Cowork session, select your project folder, and plan the phase. Because each session starts fresh, Claude will read CLAUDE.md and TASKS.md to pick up where you left off.

> We're starting Phase 1 (Foundation) from the ROADMAP.
> Break it into individual features for issue specs:
> 1. Core data models (Habit, CompletionRecord, etc.)
> 2. Services & business logic (PersistenceService, HabitService)
> 3. ViewModels & state management
> 4. Navigation shell (4-tab TabView)

Cowork adds these to TASKS.md as ordered tasks. Each one will go through the full feature cycle.

### Step 1.2 — Feature Cycle: Data Models

**Spec** (Cowork):

> Draft an issue spec for core data models.
> Save to docs/github-issues/002-core-data-models.md.
> Models needed: Habit (id, name, emoji, createdDate, isArchived),
> CompletionRecord (habitId, date), HabitStats (computed streaks).
> Use SwiftData @Model macro. Include unit test file list.
> Reference the PRD for acceptance criteria.

Cowork writes a detailed spec with exact file paths, model definitions, relationships, and test scenarios. It cross-references the PRD to ensure nothing is missed.

**Issue** (GitHub): Post the spec as a GitHub Issue. Add labels (`phase-1`, `models`, `P0`).

**Implement** (Claude Agent in Xcode):

> Implement GitHub Issue #N (core data models).
> Read docs/github-issues/002-core-data-models.md.
> Create all model files and unit tests.
> Run tests before marking as done.

Claude Agent will create the model files, write unit tests, build the project, and run the tests. If any tests fail, it will iterate and fix them autonomously. Watch the transcript to follow along, and check that the agent used the SwiftData `@Model` macro rather than falling back to plain `Codable` structs.

**Review and merge:** Create a feature branch (`feature/core-data-models-issue-N`), open a PR, review the code and the transcript, squash-merge to main, delete the branch.

**Track** (Cowork):

> Core data models PR merged. Update TASKS.md and memory.

### Step 1.3 — Repeat for Remaining Foundation Features

Follow the same cycle for each remaining feature. The order matters because of dependencies:

| Feature | Key Contents | Depends On |
|---|---|---|
| Services & business logic | PersistenceService, HabitService, ServiceContainer | Data models |
| ViewModels & state management | HabitListVM, TodayVM, StatsVM, SettingsVM | Services |
| Navigation shell | 4-tab TabView, ServiceContainer wiring, stub views | ViewModels |

Each feature produces one issue spec (Cowork), one GitHub Issue, one feature branch, one PR, and one squash merge. The Foundation phase typically produces 4–5 PRs.

For each spec, Cowork should reference both the PRD and the ARCHITECTURE.md file (which Claude Agent updates during implementation) to ensure consistency.

### Step 1.4 — Phase Completion Checkpoint

When all Foundation features are merged, run a checkpoint in Cowork:

> `/update`

> Phase 1 (Foundation) is complete. All PRs merged.
> Run a completion checkpoint:
> - Confirm all deliverables from the ROADMAP are done
> - Update CLAUDE.md phase status
> - Update memory/projects/
> - Identify any gaps or issues before starting Phase 2

Review Cowork's checkpoint report. It compares TASKS.md against reality, flags stale items, and identifies memory gaps. Once everything checks out, clean up: delete all merged feature branches (local and remote) to reduce noise.

---

## Phase 2: Core Features

Now the app gets its visible functionality. This is where users will spend their time — creating habits, checking them off, and watching streaks grow.

### Step 2.1 — Plan Core Feature Deliverables

> We're starting Phase 2 (Core Features) from the ROADMAP.
> Break it into issue specs:
> 1. Habit list UI (create, edit, delete, reorder habits)
> 2. Today view (daily check-off interface)
> 3. Streak calculation & display
> 4. Weekly calendar view

### Step 2.2 — Feature Cycle: Habit List UI

UI features require more detailed specs than architecture features, because they define layout, interactions, and edge cases that affect the user experience directly.

**Spec** (Cowork):

> Draft an issue spec for the habit list UI.
> Save to docs/github-issues/005-habit-list-ui.md.
> Covers: list of habits with emoji + name, swipe to delete,
> add button opens a sheet, edit by tapping, empty state message.
> Reference PRD user stories for acceptance criteria.
> Describe what the user sees, what they can do,
> edge cases, and what is NOT included in this issue.

A good UI spec addresses four things: what the user sees (layout, components, visual states), what the user can do (interactions, gestures, navigation), edge cases (empty state, very long habit names, 50+ habits), and what is NOT included (explicitly list deferred features to prevent scope creep).

**Implement** (Claude Agent in Xcode):

> Implement GitHub Issue #N (habit list UI).
> Read the issue spec for full details.
> Build on the existing HabitListViewModel and Habit model.
> Use Xcode Previews to verify the layout visually.
> Run on simulator and verify all interactions work.

This is where Claude Agent's visual verification capability shines. The agent can capture Xcode Previews after writing or modifying a view, analyze the visual output for layout issues, and iterate on its own code based on what it sees. For UI work, this feedback loop produces results that are much closer to your intent on the first attempt.

**Review:** When reviewing the PR, pay special attention to accessibility. Check that VoiceOver labels are present, Dynamic Type is supported, and interactive elements are reachable. If Claude Agent missed accessibility requirements, ask it to do a targeted pass before merging.

### Step 2.3 — Continue the Cycle

Repeat for each core feature. The order matters — each feature builds on the previous:

1. **Habit list UI** — CRUD interface for managing habits
2. **Today view** — daily check-off screen (depends on habit list)
3. **Streak logic** — calculation engine and display (depends on completion records)
4. **Weekly calendar** — visual grid of completions (depends on streak logic)

After each PR merge, return to Cowork to track progress. After all features merge, run another phase checkpoint with `/update`.

### Step 2.4 — Phase 2 Completion Checkpoint

> Phase 2 (Core Features) is complete. All PRs merged.
> Run a completion checkpoint.
> Verify all PRD user stories marked P0 are implemented.
> Plan Phase 3 tasks.

---

## Phase 3: Polish & Launch Prep

The app works. Now make it ready for real users and the App Store.

### Step 3.1 — Onboarding & Settings

Follow the same feature cycle for polish features:

- **Onboarding flow** — welcome screen, first habit creation tutorial
- **Settings screen** — data management, app version, support link
- **Empty states and error handling** — across all views
- **Accessibility pass** — VoiceOver labels, Dynamic Type, reachable interactive elements

For the accessibility pass, you can give Claude Agent a single focused prompt:

> Audit the entire app for VoiceOver accessibility.
> Add missing labels and hints to all interactive elements.
> Ensure Dynamic Type is supported on all text.
> Test with the Accessibility Inspector in Xcode.

Claude Agent will scan every view in the project, identify gaps, and implement fixes — exactly the kind of project-wide task it excels at.

### Step 3.2 — Marketing Preparation

Switch to the Marketing plugin in Cowork:

> `/draft-content`

Draft your App Store presence:

> Draft App Store copy for StreakPal.
> Include: app name, subtitle, description, keywords,
> promotional text, and what's new for v1.0.
> Tone: friendly, motivational, simple.
> Target audience: people who want to build daily habits
> without complex apps or subscriptions.

You can also use the Marketing plugin for:

- `/brand-review` — check consistency across all copy
- `/campaign-plan` — plan your launch strategy (social media, Product Hunt, etc.)

**Parallel work:** Marketing prep can happen alongside development. You do not need to wait until the app is finished to write App Store copy or plan your launch. This is a good use of Cowork sessions during periods when you are waiting for PR reviews or iterating on implementation.

### Step 3.3 — Testing & App Store Submission

Final steps before submission:

1. Run all unit tests in Xcode — fix any failures with Claude Agent
2. Test on a physical device, not just the simulator
3. Profile with Instruments for memory leaks and performance issues
4. Create your App Store Connect listing using the marketing copy from Cowork
5. Take screenshots on required device sizes
6. Archive in Xcode and submit for App Store review

Use Cowork to close out the project:

> App submitted to App Store review.
> Update TASKS.md. Mark Phase 3 complete.
> Write a project summary to memory/projects/.

---

## Quick Reference

### The Feature Cycle

Every feature follows this loop:

| Step | Where | What You Do | Output |
|---|---|---|---|
| 1 | Cowork | Draft issue spec | docs/github-issues/NNN-feature.md |
| 2 | GitHub | Post issue from spec | GitHub Issue #N |
| 3 | Xcode | Claude Agent implements | Feature branch with code + tests |
| 4 | GitHub | Open PR, review carefully, merge | Squash merge to main |
| 5 | Cowork | Mark done, update memory | TASKS.md + CLAUDE.md updated |

### Plugin Commands

These commands are provided by the Cowork plugins, not by Cowork itself. The short form is shown here; if you have multiple plugins installed that share a command name, use the fully qualified form (e.g., `/productivity:start`).

| Command | Plugin | When to Use |
|---|---|---|
| `/start` | Productivity | First session — initializes memory system |
| `/update` | Productivity | After merging PRs, completing phases, or resuming work |
| `/write-spec` | Product Management | Creating or updating the PRD |
| `/roadmap-update` | Product Management | Creating or adjusting the development roadmap |
| `/draft-content` | Marketing | App Store copy, blog posts, social media |
| `/brand-review` | Marketing | Checking copy against brand voice |
| `/campaign-plan` | Marketing | Planning launch or marketing campaigns |

### File Map

The "Managed by" column indicates which tool should create and update each file. This is a recommended convention, not an enforced access control.

| File | Managed by | Purpose |
|---|---|---|
| CLAUDE.md | Productivity plugin (Cowork) | Working memory — read at session start |
| TASKS.md | Productivity plugin (Cowork) | Task tracker with status sections |
| memory/ | Productivity plugin (Cowork) | Long-term storage (people, projects, glossary) |
| docs/PRD.md | Product Mgmt plugin (Cowork) | Product requirements |
| docs/ROADMAP.md | Product Mgmt plugin (Cowork) | Phased development plan |
| docs/ARCHITECTURE.md | Claude Agent (Xcode) | Architecture decisions, updated during implementation |
| docs/github-issues/ | Cowork | Issue specs drafted before posting to GitHub |
| .claude/rules/ | Cowork (initial), shared thereafter | Auto-loaded context for Claude Agent (via Agent SDK) |
| .github/ | Shared | PR template, CI workflows |

### Claude Model Selection (Xcode)

| Task Type | Recommended Model | Why |
|---|---|---|
| Simple implementation, boilerplate | Claude Haiku | Fast, cost-effective |
| Feature implementation, UI work | Claude Sonnet 4.5 | Good balance of speed and reasoning |
| Complex architecture, multi-file refactors | Claude Opus 4.6 | Deepest reasoning, best for nuanced decisions |

---

## Troubleshooting

**Cowork doesn't remember the project.** Cowork has no built-in memory between sessions. Continuity comes entirely from the files created by the Productivity plugin (CLAUDE.md, TASKS.md, memory/). Check that these files exist and are up to date. Run `/update` to resync. If specific facts are wrong, edit the memory files directly — they are just Markdown files in your project folder.

**Claude Agent implements the wrong thing.** The issue spec was probably ambiguous. Go back to Cowork, refine the spec, update the GitHub Issue, then re-implement. Do not patch unclear specs with code fixes — you will carry the ambiguity forward into future features. Use the Xcode transcript to understand where the agent's interpretation diverged from your intent.

**Claude Agent uses deprecated APIs.** The agent has direct access to Apple's developer documentation, but occasionally its training data may favor older patterns. If you see deprecated APIs, tell the agent explicitly: "Use the current API for [feature]. Check Apple's documentation for the latest approach." The agent will search the docs and correct course.

**PR reviewer flags deferred work.** Add an "Out of Scope / Deferred" section to your PR description using the template. Reference which roadmap phase handles the flagged item. Automated reviewers (like Gemini Code Assist) will flag anything that looks incomplete — the deferred section preempts false positives.

**Session ends unexpectedly.** Cowork requires the Claude Desktop app to stay open and an active internet connection throughout the session. If the app closes or your computer sleeps, the session ends. Your project files (including CLAUDE.md and TASKS.md) are safe — they live in your project folder on your actual file system — but you will need to start a new session and let the Productivity plugin reload context.

**Everything feels out of sync.** Run `/update` in Cowork. It compares TASKS.md against the actual state of your project folder, flags stale items, identifies memory gaps, and suggests corrections. Run it freely — there is no penalty for running it often, and it is designed to be the primary recovery mechanism.

---

## Principles

**Specs before code.** Every feature starts as a written spec in Cowork before any Swift gets written. This catches scope issues and edge cases while they are still cheap to fix. A 10-minute spec review saves hours of reimplementation.

**One feature, one issue, one branch, one PR.** Keep the unit of work small and traceable. Each merged PR represents exactly one feature from one issue spec. This makes code review manageable, keeps the git history clean, and makes it easy to revert a single feature if needed.

**Memory is a deliverable.** Updating CLAUDE.md, TASKS.md, and memory/ after each merge is not housekeeping — it is what makes the next session productive. Skip it once and the next session starts with stale context, leading to confusion and wasted time.

**Review the work, not just the output.** Claude Agent's Xcode transcript shows every file it explored, every documentation page it consulted, every build it triggered, and every decision it made. Reviewing the transcript is as important as reviewing the code. It tells you whether the agent understood the spec correctly, used the right APIs, and made sound architectural decisions — things you cannot tell from a diff alone.

**AI tools are collaborators, not magic.** Claude Agent writes better code when given clear specs. Cowork manages better when its memory is accurate. Your inputs determine their output quality. The workflow in this guide works because it structures the collaboration — removing that structure does not make things faster, it makes them less predictable.

**Keep the human in the loop.** Some steps are intentionally manual: reviewing Cowork's plans before execution, reviewing PRs before merging, making go/no-go decisions at phase checkpoints. These are where you apply judgment that AI tools cannot. As Apple noted when introducing agentic coding in Xcode: treat the agent as a highly capable colleague whose work you review, not as a replacement for engineering judgment.
