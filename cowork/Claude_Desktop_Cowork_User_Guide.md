# Claude Desktop Cowork — The Complete User Guide

*Your comprehensive guide to working with Claude as a digital coworker, from first launch to advanced automation.*

---

## What is Cowork?

For years, using an AI assistant meant typing a question and reading an answer. You might copy a paragraph into a document, paste a code snippet into a file, or manually save an output somewhere useful. The conversation was helpful, but the actual *work* — the organizing, formatting, creating, and delivering — still fell on you.

Cowork changes that. It is a feature built into the Claude Desktop application that gives Claude direct access to files on your computer, the ability to execute multi-step tasks autonomously, and the intelligence to coordinate complex work across parallel workstreams. You describe an outcome, step away, and come back to finished deliverables — formatted Word documents, Excel spreadsheets with working formulas, PowerPoint presentations, organized file structures, synthesized research reports, and more.

Think of it less like chatting with an assistant and more like delegating a task to a capable colleague. You leave a message describing what you need, and when you return, the work is done.

Cowork is built on the same agentic architecture that powers Claude Code, Anthropic's command-line tool for developers. The difference is that Cowork wraps that power in a friendly desktop interface that requires no terminal knowledge, no command-line expertise, and no technical setup. If you can describe what you want in plain language, you can use Cowork.

> **Current Status:** Cowork is available as a **research preview**. Anthropic is actively iterating on it based on user feedback, and capabilities will expand over time.

---

## Who is Cowork For?

Cowork is designed for knowledge workers of all kinds. If your day involves documents, spreadsheets, presentations, research, data analysis, file management, or any combination of these, Cowork can help. It is particularly well-suited for professionals who find themselves spending significant time on repetitive organizational tasks, document creation, or synthesis work that could be delegated.

You do not need any programming knowledge to use Cowork. Under the hood, Claude writes and executes code inside an isolated virtual machine on your computer — but you never need to see or understand that code. You simply describe what you want in natural language.

---

## Requirements and Availability

Before getting started, make sure you have the following in place.

**Platform support.** Cowork requires the Claude Desktop application, available for macOS (Intel and Apple Silicon) and Windows. Note that while Claude Desktop is available on both Windows x64 and ARM64, Cowork is currently supported on Windows x64 only. It is not available on the web interface or mobile apps. Download the latest version at [claude.com/download](https://claude.com/download).

**Subscription.** Cowork is available to all paid Claude plans: Pro ($20/month), Max ($100/month and $200/month tiers), Team, and Enterprise. Free-tier users cannot access Cowork.

**Internet connection.** An active internet connection is required throughout each Cowork session.

**App must remain open.** The Claude Desktop app must stay open while Claude is working. If you close the app or your computer goes to sleep, the session ends.

---

## Getting Started: Your First Task

### Step 1 — Open Cowork

Launch the Claude Desktop app. Near the top of the interface, you will see a mode selector with two tabs: **Chat** and **Cowork**. Click the **Cowork** tab to switch into task mode. The interface changes to reflect the task-oriented nature of Cowork: instead of a conversation thread, you will see a workspace where you can describe tasks and monitor their progress.

### Step 2 — Choose a Folder

Cowork operates on files stored in folders you explicitly grant it access to. When you begin a session, you can attach a folder from your computer. Claude can then read, edit, create, and organize files within that folder.

A critical best practice: **create a dedicated working folder** rather than pointing Claude at your entire Documents directory or home folder. A folder like `~/Cowork-Projects/` or `~/Claude-Work/` keeps things contained and limits what Claude can access. Copy the files you want Claude to work with into this folder, and keep backups of anything important.

### Step 3 — Describe Your Task

Type a clear description of what you want Claude to accomplish. Unlike regular chat, where you might ask a question and get an answer, Cowork is designed for *delegation*. Tell Claude what the finished product should look like, provide any necessary context, and mention constraints or preferences.

For example, instead of asking "Can you help me organize my files?", write something like: *"Organize the files in this folder by type. Create subfolders for PDFs, images, spreadsheets, and documents. Rename each file using the format YYYY-MM-DD followed by a brief description. Do not delete any files."*

### Step 4 — Review the Plan

After receiving your task, Claude analyzes the request and formulates a plan. It will present this plan to you, describing the steps it intends to take and the approach it will follow. This is your opportunity to review, refine, or redirect before execution begins. If the plan looks right, let Claude proceed. If something needs adjustment, provide feedback and Claude will revise its approach.

### Step 5 — Let Claude Work

Once you approve the plan, Claude begins executing. You will see progress indicators showing what Claude is doing at each step. You can monitor the work in real time, step in to course-correct, or simply step away and come back when it is finished. Tasks can run for extended periods depending on complexity — from a few minutes for simple file organization to much longer for research synthesis or multi-document creation.

When Claude finishes, it delivers the results directly to your file system. The outputs appear in the folder you granted access to, ready for you to review and use.

---

## Understanding How Cowork Works Under the Hood

When you assign a task, Claude follows a structured process. First, it analyzes your request and creates an execution plan. If the work is complex, it breaks the task into subtasks. It then executes the work inside a sandboxed Linux virtual machine on your computer. This means your files are mounted into a contained environment, separate from your main operating system, which provides a layer of security.

For particularly complex tasks, Claude may spin up multiple sub-agents that work on different parts of the job simultaneously. For example, if you ask Claude to research five competitors, it might create five parallel workstreams — one for each company — and coordinate their outputs into a unified deliverable. This parallel execution is one of the features that distinguishes Cowork from standard chat interactions.

Throughout the process, Claude surfaces its reasoning and approach so you can follow along. It will ask for your explicit permission before taking any potentially destructive actions, such as permanently deleting files.

---

## Configuring Cowork to Match Your Workflow

### Model Selection

You can choose which Claude model powers your Cowork session. Different models offer different trade-offs between speed, cost, and capability. For most complex tasks, the default model works well, but you may want to select a faster model for simpler or more routine work to conserve usage. Model selection is available at the start of a session.

### Global Instructions

Global instructions are standing directives that apply to every Cowork session. They allow you to specify your preferences once and have them honored consistently. Common uses include specifying a preferred tone for written output, defining standard formatting conventions, providing background about your role or organization, and setting default behaviors (such as "always create backups before modifying files").

To set global instructions, navigate to **Settings > Cowork** within Claude Desktop, click **Edit** next to "Global instructions," type your preferences, and save.

For example, you might write: *"I am a marketing director at a mid-size SaaS company. When creating documents, use a professional but approachable tone. Format all reports with an executive summary at the top. Use metric units. Always create a backup copy before modifying any existing file."*

### Folder Instructions

Folder instructions add project-specific context that activates whenever you work in a particular folder. This is useful when different projects have different requirements. Claude can also update folder instructions on its own during a session if it discovers important context about the project.

For example, a folder containing client deliverables might have instructions specifying the client's brand guidelines, while a folder for internal analysis might have instructions about your company's preferred chart styles and data sources.

### Shortcuts

Shortcuts let you create reusable automations that you can trigger on demand or run on a schedule. If you find yourself repeating the same task regularly, such as generating a weekly status report, processing a batch of incoming files, or pulling data from a connector every morning, you can save it as a shortcut. This turns a multi-step Cowork task into a one-click action, making it easy to build lightweight workflows without writing any code.

---

## Working with Plugins

Plugins are pre-built packages that customize how Claude works for specific roles, teams, or workflows. Each plugin bundles together skills (specialized capabilities like document formatting), connectors (links to external services), slash commands (quick actions you can invoke), and preconfigured workflows that can take advantage of Cowork's parallel execution capabilities.

### Pre-Built Plugins

Anthropic provides a library of plugins for common knowledge work functions. These include plugins for **Productivity** (task management, calendars, daily workflows), **Enterprise Search** (finding information across company tools), **Sales** (prospect research, deal preparation), **Finance** (financial analysis, model building, metric tracking), **Data** (querying, visualization, interpretation), **Legal** (document review, risk flagging, compliance tracking), **Marketing** (content drafting, campaign planning, launch management), **Customer Support** (issue triage, response drafting), **Product Management** (spec writing, roadmap prioritization), and **Biology Research** (literature search, result analysis, experiment planning).

### Installing a Plugin

Open Claude Desktop and navigate to the Cowork tab. Click **Plugins** in the left sidebar to browse the available library. Click on any plugin to install it. You can also click **Upload plugin** to install a custom plugin from a file. All plugins are saved locally on your machine.

### Using Plugins in a Session

Once installed, plugins add commands you can invoke during a Cowork session. Type `/` or click the **+** button to see the available commands from your installed plugins. Each command triggers a specialized workflow tailored to that plugin's domain.

### Creating Custom Plugins

Anthropic provides a special plugin called **Plugin Create** that helps you build custom plugins from scratch. If the pre-built options do not match your needs, you can use Plugin Create to design a plugin tailored to your specific role, team, or company. The full collection of Anthropic-built plugins is also available as open source on [GitHub](https://github.com/anthropics/knowledge-work-plugins), which you can use as templates for your own creations.

### Customizing Existing Plugins

After installing a plugin, you can click the **Customize** button in the upper right corner while viewing it. This generates a Cowork prompt that walks you through customizing the plugin to better fit your specific workflow. Click "Let's go" and Claude will help you tailor it interactively.

---

## Connecting External Services

### Connectors (MCP)

Connectors link Claude to external services and data sources using the Model Context Protocol (MCP). While connectors have been available in regular Claude chat for some time, Cowork gives them a new dimension: because Claude has filesystem access, a connector that pulls data from an external service can now save that data locally as a file, or use local files as input for actions on external platforms.

To browse available connectors, go to **Settings > Connectors > Browse connectors**. The catalog offers two types: **Web connectors** (which operate through browser-based APIs) and **Desktop extensions** (which run locally on your machine and tend to have deeper system access). The catalog includes hundreds of options covering cloud services, workflow automation, observability tools, meeting management, and much more. Each connector is reviewed by Anthropic, and you can also add custom connectors if your tool is not listed.

### Claude in Chrome Integration

If you have Claude in Chrome installed, Cowork can leverage it to complete tasks that require browser access — such as researching information on the web, filling out online forms, or interacting with web applications. This significantly expands what Cowork can accomplish, though it also introduces additional security considerations (discussed in the Safety section below). To enable this integration, install the Claude in Chrome extension from the Chrome Web Store and ensure it is connected to the same Claude account you use in the Desktop app.

---

## Use Cases: From Simple to Advanced

### Everyday File Management

One of the most immediately satisfying uses of Cowork is taming a messy file system. Point Claude at your Downloads folder (after copying it to your working directory) and ask it to sort files by type and date, rename them with consistent conventions, and identify duplicates. What might take you an hour of manual sorting can be finished while you get coffee.

**Example prompt:** *"Go through every file in this folder. Create subfolders named Documents, Images, Spreadsheets, Audio, Video, and Other. Move each file into the appropriate subfolder. Within each subfolder, rename files using the format YYYY-MM-DD_original-name. Create a summary log file listing every file and where it was moved."*

### Expense Reports from Receipt Photos

Drop a collection of receipt photos or scanned PDFs into a folder. Ask Claude to extract the vendor name, date, amount, and category from each receipt, then compile everything into a formatted Excel spreadsheet with category totals, date sorting, and a summary row.

**Example prompt:** *"This folder contains photos and scans of business expense receipts from January 2026. Extract the date, vendor, amount, and expense category from each receipt. Create an Excel spreadsheet with one row per receipt, sorted by date. Add a summary section at the bottom showing totals by category. Flag any receipts where the amount or date could not be confidently determined."*

### Research Synthesis

Cowork excels at pulling together information from multiple sources into a coherent narrative. You can combine web searches, local notes, and uploaded documents into a single synthesized report. Claude will read through everything, identify themes and contradictions, and produce a structured deliverable.

**Example prompt:** *"I need a competitive landscape report on the top five project management tools for enterprise teams. Search the web for the latest pricing, features, and customer reviews for each tool. Cross-reference what you find with the notes in this folder, which contain feedback from our internal evaluation. Produce a Word document with an executive summary, individual tool profiles, a comparison matrix, and a recommendation section."*

### Document Creation from Messy Inputs

Cowork can transform scattered, rough, or incomplete inputs into polished professional documents. Voice memo transcripts, handwritten note images, bullet-point outlines, and previous draft fragments can all serve as raw material for a final deliverable.

**Example prompt:** *"This folder contains my rough notes, two voice memo transcripts, and a half-written outline for a quarterly board presentation. Create a PowerPoint presentation with 12 to 15 slides covering our Q4 results, key wins, challenges, and Q1 outlook. Use a clean, professional style. Include speaker notes for each slide. Where data is missing, insert placeholder text marked with [TBD] so I know what to fill in."*

### Data Analysis and Visualization

For datasets stored as CSV, Excel, or other tabular formats, Cowork can perform statistical analysis, detect outliers, build cross-tabulations, run time-series analysis, generate charts, and produce written summaries of findings.

**Example prompt:** *"Analyze the sales data in this folder (sales_2025.xlsx). Calculate monthly revenue by region, identify the top 10 customers by lifetime value, and flag any months with unusual drops or spikes. Create a new Excel workbook with three tabs: a summary dashboard, detailed monthly breakdowns, and a chart sheet with line charts for each region's revenue trend."*

### Batch Document Processing

When you have dozens or hundreds of files that all need the same treatment, Cowork's ability to work systematically through a queue is invaluable. This could mean extracting key sections from a set of contracts, standardizing the formatting across a collection of reports, or converting a folder of Markdown files into formatted Word documents.

**Example prompt:** *"This folder contains 30 PDF contracts. For each contract, extract the parties involved, the effective date, the termination clause, and the total contract value. Compile all extracted information into a single Excel spreadsheet with one row per contract. Flag any contracts where a field could not be found."*

### Parallel Research with Sub-Agents

For tasks that are naturally parallelizable, you can instruct Claude to use sub-agents. Each sub-agent works independently on a portion of the task, and Claude coordinates the results.

**Example prompt:** *"Research these five companies in parallel: Acme Corp, Betaworks, Citadel Systems, DeltaForce Inc, and Echo Labs. For each, find their latest revenue figures, employee count, key products, recent news, and primary competitors. Create a separate analysis file for each company, plus a summary comparison document that ranks them across all dimensions."*

### Meeting Transcript Analysis

After a meeting, drop the transcript (or audio file, if you have a transcription plugin) into a Cowork folder. Ask Claude to extract action items, key decisions, open questions, and a concise summary. Claude can format the output as a meeting minutes document and even draft follow-up emails.

**Example prompt:** *"This folder contains the transcript from today's product planning meeting. Extract all action items with assigned owners and deadlines. List the key decisions that were made. Note any open questions or unresolved debates. Create a meeting minutes document in Word format and draft a follow-up email summarizing the outcomes for the team."*

### Personal Knowledge Management

Over time, many professionals accumulate a sprawling collection of notes, journal entries, bookmarks, and research fragments. Cowork can analyze this personal knowledge base to surface patterns, connections, and insights you might have missed.

**Example prompt:** *"This folder contains my research notes from the past six months — a mix of Markdown files, text files, and PDFs. Read through all of them and identify the recurring themes, key insights, and areas where my thinking has evolved. Create a synthesis document that maps out the major threads, highlights contradictions or gaps, and suggests three areas worth deeper exploration."*

---

## Writing Effective Task Descriptions

The quality of Cowork's output is directly tied to the quality of your input. Because Cowork operates with more autonomy than a standard chat interaction, clear task descriptions matter more than ever.

**Describe the finished product.** Rather than giving step-by-step instructions, paint a picture of what "done" looks like. What format should the output be in? How long or detailed should it be? Who is the audience?

**Provide context.** Tell Claude about your role, the purpose of the work, and any relevant background. The more context Claude has, the better it can tailor its approach.

**State constraints explicitly.** If there are things Claude should *not* do — deleting files, accessing certain subfolders, making assumptions about missing data — say so upfront. Claude cannot read your mind about limits you have not stated. A safe default is to always include "do not delete any files" unless you specifically want deletions.

**Specify the output format.** If you want a Word document, say so. If you want Excel with formulas, say so. If you want a PowerPoint with speaker notes, say so. Cowork's built-in skills produce real, professional-grade files in these formats — not just text that looks like a spreadsheet.

**Anticipate edge cases.** What should Claude do if a receipt is illegible? What if a data field is missing? What if a file is corrupted? Providing guidance for these situations prevents Claude from making assumptions you would not agree with.

---

## Managing Usage

Working on tasks with Cowork consumes more of your subscription's usage allocation than standard chat. This is because complex, multi-step tasks are compute-intensive and require significantly more processing tokens. A single Cowork session that coordinates sub-agents across a large research task might consume as much usage as dozens of regular chat messages.

To manage your usage effectively, consider batching related work into single sessions rather than running many small ones. Use standard chat for simpler tasks that do not require file access or extended execution — things like quick questions, brainstorming, or short text edits are better suited to chat mode. Monitor your usage in **Settings > Usage** at [claude.ai/settings/usage](https://claude.ai/settings/usage) (sign-in required; you can also navigate there from within the app).

If you find yourself hitting limits frequently, you may want to evaluate whether a higher-tier Max subscription ($200/month) would better suit your workflow.

---

## Safety and Security

Cowork is powerful precisely because it can take real actions on your computer — and that power demands thoughtful use. Anthropic has built multiple layers of protection into the system, but as a research preview, Cowork carries risks that you should understand.

### How Cowork Protects You

Claude operates inside an isolated virtual machine that is separate from your main operating system. This sandboxed environment provides a boundary between Claude's execution environment and the rest of your system. Claude also requires your explicit permission before permanently deleting any files — you will always see a confirmation prompt before any deletion occurs.

Claude is trained through multiple techniques, including reinforcement learning from human feedback, to recognize and refuse potentially harmful instructions. Content classifiers also scan untrusted content entering Claude's context to flag potential prompt injection attempts before they affect behavior.

### Your Responsibilities

Despite these safeguards, you remain responsible for all actions Claude takes on your behalf. This includes any content published, messages sent, purchases made, data accessed or modified, and respect for third-party terms of service.

### Best Practices for Safe Use

**Be selective about file access.** Only grant Claude access to the specific folders and files it needs for the task at hand. Keep sensitive materials — financial documents, credentials, personal records, API keys — in separate folders that Cowork never touches.

**Monitor for unexpected behavior.** You do not need to validate every individual command Claude executes, but watch for patterns that seem wrong: Is Claude accessing files or websites you did not mention? Is the scope of the task creeping beyond what you asked? If something feels off, stop the task immediately.

**Limit browser and web access to trusted sources.** If you use Claude in Chrome with Cowork, restrict access to sites you trust. Web content is the primary vector for prompt injection attacks, where malicious instructions hidden in web pages attempt to hijack Claude's behavior.

**Use verified connectors.** Stick to MCPs from the Claude Desktop directory and carefully evaluate the permissions each connector requests before installing.

**Report anything suspicious.** If Claude starts discussing unrelated topics, attempts to access unexpected resources, or requests sensitive information unprompted, stop the task and use the in-app feedback button or email usersafety@anthropic.com.

---

## Current Limitations

As a research preview, Cowork has some boundaries you should be aware of.

**No memory between sessions.** Each Cowork session starts fresh. Claude does not remember what you worked on in previous sessions. This means you should save effective task descriptions for reuse, and provide necessary context at the start of each session. (Note that folder instructions do persist between sessions, since they are saved to the folder itself. This provides a lightweight form of continuity for project-specific context.)

**No sharing.** Cowork sessions cannot be shared with other people. The conversation history is stored locally on your machine.

**Desktop only.** Cowork is available exclusively in the Claude Desktop app and does not sync across devices. If you switch computers, your sessions and history do not follow.

**Session persistence requires the app to stay open.** As noted in the Requirements section, if you close the Claude Desktop app, your computer goes to sleep, or you lose your internet connection, the session ends. Make sure the app remains open for the duration of any task.

**Not captured in audit logs.** For Team and Enterprise users, Cowork activity is not currently captured in Audit Logs, the Compliance API, or Data Exports. Do not use Cowork for regulated workloads until this changes. Organization owners can enable or disable Cowork organization-wide via Admin Settings > Capabilities, but granular per-user or per-role controls are not available during the research preview. See the [Cowork for Team and Enterprise](https://support.claude.com/en/articles/13455879-cowork-for-team-and-enterprise-plans) support article for the latest updates on enterprise features.

---

## Troubleshooting Common Issues

**"Setting up Claude's workspace" appears when starting Cowork.** This is normal. It means Cowork is updating to the latest version to incorporate recent fixes and improvements. Allow it a moment to complete.

**Claude stopped working on a task.** The most common cause is the Claude Desktop app being closed or the computer going to sleep during execution. Ensure the app remains open and your computer stays awake throughout the task.

**Hitting usage limits quickly.** Cowork is significantly more compute-intensive than standard chat. Reserve it for complex, multi-step work and use regular chat for simpler interactions. Batching related work into fewer, more comprehensive sessions also helps.

**Files are not appearing where expected.** Verify that you granted Claude access to the correct folder. Review the output location Claude specified when completing the task — sometimes outputs are placed in a subfolder Claude created during execution.

**Cowork tab is not visible.** Make sure you are using the latest version of Claude Desktop. Download the newest version from [claude.com/download](https://claude.com/download) and restart the app.

---

## Tips from Experienced Users

**Start small.** Run your first few tasks on non-critical files in a dedicated test folder. This lets you build intuition for how Claude interprets instructions and where it might need more guidance.

**Build a prompt library.** When a task produces excellent results, save the exact prompt you used. Over time, you will develop a personal collection of proven task descriptions that you can reuse and adapt.

**Maintain a consistent folder structure.** Keeping your working folders organized the same way across sessions helps Claude navigate predictably, even without memory of past sessions.

**Use the "do not delete" safety net.** Until you are fully confident in how Claude handles a particular type of task, include an explicit instruction not to delete any files. This single habit prevents most accidental data loss.

**Leverage parallel work for large jobs.** If your task involves multiple independent subtasks — researching several companies, processing many files, or creating several documents — tell Claude to work on them in parallel. This takes full advantage of Cowork's sub-agent coordination and finishes the job faster.

**Pair Cowork with standard chat.** Use regular chat for brainstorming, quick questions, and iterating on ideas. Once you have a clear picture of what you need, switch to Cowork to execute. This combination keeps your usage efficient while getting the best of both modes.

---

## Quick Reference

| Feature | Details |
|---|---|
| **Access** | Claude Desktop app (macOS; Windows x64 for Cowork) |
| **Plans** | Pro, Max, Team, Enterprise |
| **Pricing** | Included with paid subscription; consumes more usage than chat |
| **File Access** | Read, write, create, delete (with permission) in designated folders |
| **Output Formats** | .docx, .xlsx, .pptx, .pdf, .md, .csv, and more |
| **Parallel Work** | Sub-agents for independent subtasks |
| **Model Selection** | Choose which Claude model powers each session |
| **Plugins** | Pre-built library + custom creation |
| **Shortcuts** | Reusable on-demand or scheduled automations |
| **Connectors** | Hundreds of MCP integrations (web and desktop) |
| **Browser** | Via Claude in Chrome |
| **Memory** | None between sessions (folder instructions persist) |
| **Sharing** | Not currently supported |
| **Global Instructions** | Settings > Cowork > Global instructions |
| **Folder Instructions** | Set per-folder context for project-specific behavior |
| **Safety** | VM isolation, deletion protection, content classifiers |

---

## Further Resources

For additional information, visit the following resources.

- **Getting Started with Cowork** — [support.claude.com](https://support.claude.com/en/articles/13345190-getting-started-with-cowork)
- **Using Cowork Safely** — [support.claude.com](https://support.claude.com/en/articles/13364135-using-cowork-safely)
- **Cowork for Team and Enterprise** — [support.claude.com](https://support.claude.com/en/articles/13455879-cowork-for-team-and-enterprise-plans)
- **Anthropic's Plugin Collection on GitHub** — [github.com/anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins)
- **Claude Desktop Download** — [claude.com/download](https://claude.com/download)
- **Introducing Cowork (Blog Post)** — [www.claude.com/blog/cowork-research-preview](https://claude.com/blog/cowork-research-preview)

---

*Last updated: February 2026. Cowork is a research preview and features are subject to change. Refer to Anthropic's official documentation for the most current information.*
