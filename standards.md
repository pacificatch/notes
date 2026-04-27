# Project Standards

Standards for writing project documentation. One section per document type. Add new sections as standards are established.

## Contents

- [features.md](#features.md)
- [roadmap.md](#roadmap.md)
- [architecture.md](#architecture.md)

---

## features.md

### Purpose

features.md is a living document that lists every feature in the product. Its primary audience is executives and non-technical stakeholders. Everything in it must be readable by someone who has never seen the code.

Secondary audiences: the developer uses it to track build status; the customer uses it to understand what is built and what is coming.

---

### Who Reads It

Write every sentence as if the reader is a senior executive who understands the business but does not know what a database, API, or webhook is. If a technical term is unavoidable, replace it with a plain-English equivalent.

- Do not say: "The webhook triggers background processing via a queue worker."
- Say: "As soon as a file is uploaded, the system begins processing it in the background without any manual trigger."

---

### Document Structure

**Title**

```
# [Project Name] — Feature List
```

**Opening block**

Always include this immediately after the title. Customize the milestone list to match the project.

```
> This document is intended for executive review. Every feature includes a plain-English description of what it does and why it matters.
>
> Status legend: 🔲 Planned | 🔄 In Progress | ✅ Done | 🔮 Future version | ❓ Pending Decision
>
> Milestone legend: **Scaffold** → **Alpha** → **Beta** → **Launch** → **V2** → **V3** → **V4**
```

**Sections**

Group features into logical categories. Each section has a number, a title, and an italicized tagline.

```
## 1. Section Title
*One sentence describing what this section covers.*
```

Separate sections with a horizontal rule (`---`).

---

### Feature Format

Each feature is a single bullet point:

```
- [status emoji] **Feature name.** Plain-English description. → *Milestone*
```

Rules:
- The feature name is in bold and ends with a period.
- The description is in plain English, in complete sentences.
- The description explains both what the feature does AND why it matters.
- The milestone tag (`→ *Alpha*`) goes at the end, after the description.

Example:

```
- 🔲 **Duplicate file prevention.** Before doing any work, the system checks whether the same file has already been processed — even if it was uploaded under a different name. If it is a duplicate, the system skips it, records the event, and notifies the user, saving time and cost. → *Alpha*
```

---

### Status Emojis

| Emoji | Meaning |
|-------|---------|
| 🔲 | Planned but not started |
| 🔄 | Currently in progress |
| ✅ | Complete |
| 🔮 | Planned for a future version (V2, V3, etc.) |
| ❓ | Pending a decision before it can be built |

Do not invent new emojis. Use exactly these.

---

### Milestone Tags

Every feature must have a milestone tag at the end:

```
→ *Scaffold* / → *Alpha* / → *Beta* / → *Launch* / → *V2* / → *V3* / → *V4* / → *Post-launch*
```

If a feature collects data early but shows it in a UI later, note both:

```
→ *V3 (data collected from Alpha)*
```

---

### Special Elements

**Build blockers**

Use when a feature cannot be built until an external decision or deliverable is complete. Place as a blockquote below the section heading, before the first feature bullet.

```
> ⚠️ **Build blocker:** [What must be decided or delivered before this section can be built.]
```

**Decision notes**

When a contested design decision was made, document the alternatives and the reason for the choice. Place as an indented blockquote inside the relevant feature bullet.

```
  > **Decision note:** Three approaches were considered — (A) ...; (B) ...; (C) .... Option A was chosen because [reason]. This decision may be revisited.
```

**Tables**

Use when a feature has a defined set of states, colours, or categories. Follow the table with the milestone tag on its own line.

**Status timelines**

For complex workflows with time-ordered states, use a code block to draw a plain-text timeline. Label each state clearly and note any branching conditions.

---

### Content Rules

1. **Plain English only.** No jargon or technical terms without explanation. Widely understood terms (API, PDF, URL) are acceptable.
2. **What and why.** Every description must answer: what does it do, and why does it matter?
3. **Complete sentences.** No fragments.
4. **No em dashes.** Replace with a colon, comma, semicolon, or period.
5. **Active voice.** "The system detects the upload" — not "The upload is detected."
6. **Mark future features clearly.** Features tagged 🔮 must always be clearly marked.
7. **Keep it honest.** If a decision has not been made, use ❓ and link to the GitHub Issue where it is tracked.

---

### Section Ordering Suggestions

1. How data enters the system (ingestion, upload, intake)
2. How the system processes data (AI extraction, calculation, transformation)
3. How data is stored and managed (database, history, corrections)
4. Reference data management (main lists, lookup tables)
5. Lifecycle and status tracking
6. Notifications and alerts (email, in-app)
7. Dashboard and reporting
8. User interface and management screens
9. User and access management
10. Infrastructure and technology

For multi-module apps, use a horizontal rule and a new top-level heading to separate modules:

```
---

# [Module Name]

> Brief description of this module and its audience.
```

---

### Minimal Template

```markdown
# [Project Name] — Feature List

> This document is intended for executive review. Every feature includes a plain-English description of what it does and why it matters.
>
> Status legend: 🔲 Planned | 🔄 In Progress | ✅ Done | 🔮 Future version | ❓ Pending Decision
>
> Milestone legend: **Scaffold** → **Alpha** → **Beta** → **Launch** → **V2**

---

## 1. [Section Title]
*[One-sentence tagline describing this section.]*

- 🔲 **[Feature name].** [Plain-English description of what it does and why it matters.] → *[Milestone]*

---

## 2. [Section Title]
*[One-sentence tagline.]*

- 🔲 **[Feature name].** [Plain-English description.] → *[Milestone]*
```

---

## roadmap.md

### Purpose

roadmap.md defines the build sequence for the project, milestone by milestone. It is the developer's primary working document during the build. Every step that needs to be built is listed here in the order it should be done.

Secondary audiences: the admin and customer use it to understand what has been done and what is coming.

---

### Document Structure

**Title**

```
# [Project Name] — Roadmap
```

**Opening block**

Customize the owner list to match the project's roles.

```
> This document defines the build sequence for [Project Name], milestone by milestone.
> Feature prioritization and milestone definitions: see [FEATURES.md](FEATURES.md) and [ARCHITECTURE.md](ARCHITECTURE.md).
>
> Status: 🔲 Not started | 🔄 In progress | ✅ Done | ⏸ Blocked | 🔮 Future
>
> Owner: **Engineer** = [developer name] | **Admin** = customer IT | **Executive** = customer executive | **Manager** = customer operations
```

**Table of Contents**

Always include a table of contents immediately after the opening block. List every milestone and top-level section.

```
## Table of Contents

- [Milestone Overview](#milestone-overview)
- [Module Name](#module-name)
  - [Scaffold](#scaffold)
  - [Alpha](#alpha)
  - [Beta](#beta)
  - [Launch](#launch)
  - [V2](#v2)
- [Pending Before Building](#pending-before-building)
```

**Milestone Overview table**

Always include this after the table of contents. One row per milestone.

```
| Milestone | Who has access | Goal |
|-----------|---------------|------|
| Scaffold | Engineer only | Infrastructure live — blank app renders, login works |
| Alpha | Engineer + Admin | Core loop works |
| Beta | Engineer + Admin + Manager + Viewers | Integration testing ready |
| Launch | Full team | All roles live |
```

---

### Step Format

Steps are rows in a numbered table with four columns:

```
| # | Description | Owner | Status |
|---|-------------|-------|:------:|
| 1 | [What to build and why, in plain technical terms] | Engineer | 🔲 |
```

Rules:
- Number restarts from 1 at every milestone.
- For multi-module apps (e.g. fuel tracking), prefix steps with a module letter: F1, F2, etc.
- Sub-steps use a letter suffix: 17a, 17b.
- Owner can be a combination: `Engineer + Admin`.
- Status is always centered: `:------:`.
- Description is technical and specific — enough for the engineer to know exactly what to build.

---

### Status Emojis

| Emoji | Meaning |
|-------|---------|
| 🔲 | Not started |
| 🔄 | In progress |
| ✅ | Done |
| ⏸ | Blocked |
| 🔮 | Future version (V2, V3, etc.) |

---

### Owner Names

Use consistent owner labels throughout the document. Define them in the opening block. Common names:

| Label | Who |
|-------|-----|
| Engineer | The developer |
| Admin | Customer IT administrator |
| Executive | Customer executive or decision maker |
| Manager | Customer operations manager |

---

### Milestone Sections

Each milestone gets a `###` heading and an italicized tagline that describes what is achieved by the end of that milestone.

```
### Alpha
*Engineer + Admin only. Core loop works — files in, AI extracts, data saved, list shows.*
```

Within a milestone, group steps into sub-sections using `####` headings:

```
#### Database
#### Backend — [topic]
#### Frontend — [topic]
#### Testing checkpoint
```

Always end every milestone with a testing checkpoint sub-section containing at minimum:
- Run full automated test suite and confirm all passing
- Complete USER-TESTING.md checklist for that milestone

For milestones with a large frontend build, add a `/simplify` step before the testing checkpoint.

---

### Special Elements

**Pre-milestone prerequisites**

When one milestone depends on work from another section being done first, add a blockquote note before the milestone heading:

```
> **Before starting [Milestone]:** [What must be completed first and why.]
```

**Account migration section**

For projects that will be handed over to a customer, include an "Account migration" sub-section at the start of the Beta milestone. Reference HANDOVER.md for full steps.

**Module separation**

For apps with multiple independent modules, use `##` to separate modules:

```
## [Module Name]

### [Module] — MVP
*Description of what this milestone achieves.*
```

Number steps within each module separately using a prefix (e.g. F1, F2 for fuel).

**Pending Before Building section**

Always add this as the final section. It lists sessions or decisions that must happen before certain features can be built. Format:

```
## Pending Before Building

| Session | What happens | Owner | Status |
|---------|-------------|-------|--------|
| [Name] | [What must be decided or delivered, and what it unblocks.] | Executive | ❓ Not started |
```

---

### Content Rules

1. **Descriptions are technical.** Unlike features.md (which is for executives), roadmap.md descriptions are written for the engineer. Be specific about what to build, what tables or APIs are involved, and what the acceptance condition is.
2. **One step = one deployable unit.** Each step should be completable and testable on its own. Do not bundle unrelated work into one row.
3. **Testing checkpoints are mandatory.** Every milestone must end with an automated test run and a manual testing checklist step.
4. **Blocked steps use ⏸.** If a step cannot be started because of an external dependency, mark it ⏸ and add a note in the description explaining what is blocking it.
5. **Future steps use 🔮.** Steps in V2, V3, and beyond use 🔮 instead of 🔲 so they are visually distinct from near-term planned work.
6. **No em dashes.** Replace with colon, comma, semicolon, or period.

---

### Minimal Template

```markdown
# [Project Name] — Roadmap

> This document defines the build sequence for [Project Name], milestone by milestone.
> Feature prioritization and milestone definitions: see [FEATURES.md](FEATURES.md) and [ARCHITECTURE.md](ARCHITECTURE.md).
>
> Status: 🔲 Not started | 🔄 In progress | ✅ Done | ⏸ Blocked | 🔮 Future
>
> Owner: **Engineer** = [name] | **Admin** = customer IT | **Executive** = customer executive | **Manager** = customer operations

## Table of Contents

- [Milestone Overview](#milestone-overview)
- [Scaffold](#scaffold)
- [Alpha](#alpha)
- [Pending Before Building](#pending-before-building)

---

## Milestone Overview

| Milestone | Who has access | Goal |
|-----------|---------------|------|
| Scaffold | Engineer only | Infrastructure live |
| Alpha | Engineer + Admin | Core loop works |

---

### Scaffold
*Infrastructure only — nothing works yet.*

| # | Description | Owner | Status |
|---|-------------|-------|:------:|
| 1 | [First step] | Engineer | 🔲 |

---

### Alpha
*[Who has access. What is achieved by end of milestone.]*

#### Backend

| # | Description | Owner | Status |
|---|-------------|-------|:------:|
| 1 | [Step] | Engineer | 🔲 |

#### Testing checkpoint

| # | Description | Owner | Status |
|---|-------------|-------|:------:|
| 2 | Run full automated test suite — confirm all tests passing | Engineer | 🔲 |
| 3 | Complete USER-TESTING.md Alpha checklist | Engineer | 🔲 |

---

## Pending Before Building

| Session | What happens | Owner | Status |
|---------|-------------|-------|--------|
| [Name] | [What must be decided and what it unblocks.] | Executive | ❓ Not started |
```

---

## architecture.md

### Purpose

architecture.md records every architecture and product design decision made during planning, along with the reasoning behind each decision. It is the authoritative reference for why the system is built the way it is.

Secondary audiences: a new developer joining the project uses it to understand why the code is structured the way it is, without having to dig through git history or ask the original developer.

---

### Who Reads It

Write for a technical developer who is new to this specific project but already knows how to code. Assume they understand concepts like databases, APIs, and background workers — but explain every design choice as if they are reading it cold, with no prior context.

---

### Document Structure

**Title**

```
# [Project Name] — Architecture Design Decisions
```

**Opening block**

```
> This document records every architecture and product design decision made during planning, along with the reasoning behind each decision. It is the authoritative reference for why the system is built the way it is.
```

**Table of Contents**

Always include a full table of contents. Every section in the document must be linked. This is a long document — navigation is essential.

```
## Table of Contents

- [Build Framework](#build-framework)
- [Stack](#stack)
- [Section Name](#section-name)
...
- [Page Inventory](#page-inventory)
```

**Fixed opening sections (always include these in order):**

1. Build Framework — current status in the vibecoding phases, session order
2. Milestones — milestone overview table (same as in roadmap.md)
3. Pending Sessions — decisions or sessions that must happen before building
4. Stack — technology choices with reasons

After these, add one section per design decision area.

---

### Section Format

Each section covers one design area. Lead with the decision, then explain why.

```
## Section Name

[State the design decision in one or two sentences — what was chosen and what the key constraint is.]

**Why:** [The reasoning. What alternatives were considered. What made this the right call for this project.]
```

For complex decisions, add sub-sections using `###`:

```
## Section Name

### Sub-topic
[Decision]

**Why:** [Reasoning]

### Another Sub-topic
```

---

### Stack Table Format

The Stack section always uses this table format:

```
| Layer | Technology | Reason |
|-------|-----------|--------|
| Frontend | [Technology] | [One sentence reason] |
| Backend | [Technology] | [One sentence reason] |
| Database | [Technology] | [One sentence reason] |
| AI | [Technology] | [One sentence reason] |
```

---

### Build Framework Table Format

The Build Framework section tracks the current project status against the vibecoding phases:

```
| Framework Phase | Steps | Project Activity | Status |
|----------------|-------|-----------------|--------|
| Phase 1 — Project Setup | Steps 1–5 | [What was done] | ✅ Complete |
| Phase 2 — Infrastructure | Steps 6–10 | [What was done] | 🔄 In progress |
| Phase 3 — Feature Milestones | M0–M8 | [What will be done] | 🔲 Not started |
```

---

### Special Elements

**Pipeline steps**

For ordered processing pipelines, use a numbered code block:

```
```
1. Step name     → outcome if check fails
2. Step name     → outcome if check fails
3. Step name     → outcome if check fails
```
```

**SQL schemas and views**

Include key SQL inline when it is essential to understanding the design. Use a code block with the `sql` language tag.

**Option comparison tables**

When a technology or approach was chosen over alternatives, use a table to show the comparison:

```
| | Option A | Option B | Option C |
|---|---|---|---|
| Cost | $X | $Y | $Z |
| Complexity | Low | High | Medium |
```

**Decision notes**

When a decision may be revisited, add a forward-looking note:

```
**V2:** If [condition changes], [what will be done differently].
```

**Why labels**

Use `**Why:**` consistently to label the reasoning paragraph in every section. This makes it easy to scan the document for justifications.

---

### Page Inventory

Always include a Page Inventory as the last section. It lists every page and sub-section of the app, who can see it, and what it contains. This is used to keep docs/USER-FLOWS.md and docs/ARCHITECTURE.md in sync.

```
## Page Inventory

| Page | Sub-section | Visible to | Notes |
|------|-------------|------------|-------|
| [Page name] | [Sub-section or —] | [Roles] | [Key detail] |
```

---

### Content Rules

1. **Lead with the decision, not the background.** State what was chosen first. The reasoning follows.
2. **Always include a Why.** Every design decision must have an explanation. "Because it was simpler" is acceptable if true — but it must be stated.
3. **Document alternatives considered.** If other options were evaluated and rejected, say so briefly. This prevents future developers from re-litigating settled decisions.
4. **Be specific about constraints.** Name the actual constraint: cost, scale, team size, integration availability. Vague reasoning ages poorly.
5. **Flag decisions that may change.** If a decision is provisional or expected to be revisited in a future milestone, say so explicitly.
6. **No em dashes.** Replace with colon, comma, semicolon, or period.
7. **Keep technical terms.** Unlike features.md, architecture.md is for developers. Use correct technical terms without apology.

---

### Section Ordering Suggestions

1. Build Framework
2. Milestones
3. Pending Sessions
4. Stack
5. Data ingestion and processing pipeline
6. AI design (if applicable)
7. Data model and database design
8. Status and lifecycle design
9. Authentication and sessions
10. Notifications and email
11. Navigation and UI structure
12. Roles and access control
13. Scale and performance
14. Observability and error tracking
15. Mobile
16. Page Inventory (always last)

---

### Minimal Template

```markdown
# [Project Name] — Architecture Design Decisions

> This document records every architecture and product design decision made during planning, along with the reasoning behind each decision. It is the authoritative reference for why the system is built the way it is.

---

## Table of Contents

- [Build Framework](#build-framework)
- [Stack](#stack)
- [Page Inventory](#page-inventory)

---

## Build Framework

### Current Status: [Phase Name]

| Framework Phase | Steps | Project Activity | Status |
|----------------|-------|-----------------|--------|
| Phase 1 — Project Setup | Steps 1–5 | [Activity] | ✅ Complete |
| Phase 2 — Infrastructure | Steps 6–10 | [Activity] | 🔲 Not started |

---

## Milestones

| Milestone | Who has access | Goal |
|-----------|---------------|------|
| Scaffold | Engineer only | Infrastructure live |
| Alpha | Engineer + Admin | Core loop works |

---

## Stack

| Layer | Technology | Reason |
|-------|-----------|--------|
| Frontend | [Technology] | [Reason] |
| Backend | [Technology] | [Reason] |
| Database | [Technology] | [Reason] |

---

## [Design Decision Section]

[State the decision.]

**Why:** [Reasoning. Alternatives considered. Why this was the right call.]

---

## Page Inventory

| Page | Sub-section | Visible to | Notes |
|------|-------------|------------|-------|
| [Page] | — | [Roles] | [Notes] |
```
