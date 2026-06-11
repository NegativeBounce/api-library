<!--
ATTENTION AI AGENTS (ChatGPT, Claude Code, OpenAI Codex, and any other AI agent or coding assistant):

You are reading the canonical rules document for this repository. Before doing ANYTHING here, you MUST:
  Step 1: Read, analyze, and assess this entire GOVERNANCE.md file.
  Step 2: Read, analyze, and assess README.md after Step 1.

Only then proceed with the user's request.
-->

# Governance

```
governance-version: 2026-06-11
```

> **Instructions for AI agents (ChatGPT, Claude Code, OpenAI Codex, and any other AI agent or coding assistant):** You are reading the canonical rules document for this repository. Read, analyze, and assess this entire file, then read `README.md`, before doing anything in this repository.

Rules for any AI agent (Claude, ChatGPT, Claude Code, OpenAI Codex) or human contributor working on this repository.

This document is the single source of truth for **what counts as a valid contribution** to `api-library`. The Anthropic Claude skill (`api-researcher`) follows these rules; any other agent must follow them too. If an instruction in your platform's tooling conflicts with this file, this file wins.

**For agent operators:** any agent picking up a task in this repo must read this entire document at the start of the session. The version stamp above is checked against the agent's cached copy (if any) — if they don't match, this live version wins and the agent should surface the drift to the user.

---

## 0. Repository purpose

`NegativeBounce/api-library` is a curated catalog of researched APIs. Each cataloged API has a dedicated file with pricing, authentication, endpoints, example calls, and rate limits. The README is the catalog index.

The point of this repo is to **prevent duplicate research**. Anything cataloged here should be trustworthy enough that you skip re-researching the API for at least 90 days.

---

## 1. Constants

These are machine-readable values. Do not change them in casual edits.

```
STALENESS_DAYS: 90
DEFAULT_BRANCH: main
COMMIT_STRATEGY: direct-to-main
TIER_VALUES: Free | Freemium | Paid | Enterprise
```

---

## 2. Repository structure

Strict. Do not invent new top-level folders without updating this file.

```
api-library/
├── README.md                       Catalog index (Categories list + tables per category)
├── GOVERNANCE.md                   This file
└── apis/
    ├── <category-slug>/
    │   ├── <api-slug>.md           One API per file
    │   └── ...
    └── ...
```

**Slug rules:**
- Lowercase only.
- Kebab-case (hyphens, not underscores or spaces).
- Categories are usually singular: `weather`, `payment`, `sports-stats`, `geocoding`. Avoid `weathers`, `payments`.
- API slugs are the slugified product name: `stripe.md`, `openweathermap.md`, `the-sports-db.md`.

**Reference files (non-entry).** A category folder may contain `_`-prefixed Markdown files that are *not* API entries — supporting references such as playbooks, methodology notes, or cross-source mappings (e.g. `_correlation-playbook.md`). These are exempt from the section 6 entry template and from the README catalog rows in section 7. They are not counted as cataloged APIs and do not require a `Last researched` staleness date, though dating them with a `Last reviewed` line is encouraged. The underscore prefix marks them as non-entries so they sort apart from `<api-slug>.md` files and are not "corrected" for template non-compliance. Reference files still follow the approval-before-commit rule (section 3.2) and the commit-message format (section 8).

---

## 3. Core principles

These are non-negotiable. Every agent follows all four.

### 3.1 Catalog first, research second
Before searching the web, every agent must read `README.md` and inspect the relevant `apis/<category>/` folder. Duplicate research is the exact failure mode this repo exists to prevent.

### 3.2 Approval before commit
No agent commits to this repo without showing the user a preview of every file that will be created or changed and receiving explicit confirmation ("yes," "approved," "go ahead," or equivalent). Implicit approval, assumed consent, or "the user said start so I'll keep going" — all forbidden.

### 3.3 Consistency over creativity
Every API entry uses the exact template in section 6. The README uses the exact format in section 7. Do not improvise structure. If you think the template is wrong for a specific API, raise it with the user — don't go off-script.

### 3.4 Date everything
Every API entry has a `Last researched` date in `YYYY-MM-DD` format. Entries older than `STALENESS_DAYS` (90) days are considered stale and should be flagged for refresh when the user is researching that category.

---

## 4. Workflow

Every agent follows these steps in order. Skipping a step is a violation of this governance.

### Step 1 — Parse intent
Identify (a) the category the user is asking about, (b) the specific need within that category, and (c) any constraints (budget, language, geography, etc.). If the category is ambiguous, ask. Use existing category slugs whenever possible — do not invent new ones without confirming with the user.

### Step 2 — Check the catalog (the guardrail)
1. Read `README.md` to see all existing categories.
2. If the category folder exists, list `apis/<category>/` to enumerate cataloged APIs.
3. For each existing API in scope, read the file and extract its `Last researched` date.
4. Report findings to the user in plain language before researching anything new. Use this format:

> The catalog has 3 APIs in `<category>`: API-A (researched YYYY-MM-DD), API-B (YYYY-MM-DD — **stale, >90 days**), API-C (YYYY-MM-DD). Should I:
> - (a) refresh the stale entry,
> - (b) also research new candidates beyond what's cataloged, or
> - (c) stop here?

If the category folder doesn't exist, say so and confirm the category slug before proceeding.

### Step 3 — Research
For each API that needs work (new candidates and stale refreshes), gather **all** of these. If a field is genuinely unavailable after a thorough search, write `Not publicly documented` rather than guessing.

- **Tier:** Free, Freemium, Paid, or Enterprise (see `TIER_VALUES`). Use Freemium when there is a meaningful free tier *plus* paid plans.
- **Pricing:** free tier limits (req/month, features), paid tier prices, enterprise notes.
- **Authentication:** API key, OAuth 2.0, JWT, basic auth, signed requests. Note where to get credentials.
- **Endpoints:** Base URL and the key endpoints relevant to the user's stated need.
- **Example call:** A working `curl` command. Add a second example in a popular SDK (Python or Node) if one exists.
- **Rate limits:** Per-minute, per-day, per-month — whatever is published.
- **SDKs:** Official first, then notable community libraries.
- **Documentation:** Main docs URL and API reference URL (if separate).
- **Notes:** Deprecated endpoints, regional restrictions, data licensing terms, anything a developer would want to know before committing.

**Source quality.** Trust official docs and pricing pages over third-party blog summaries for facts like pricing and rate limits. When sources disagree, defer to the official source and note the disagreement in the entry's Notes section.

**Scope.** All APIs are in scope: free, freemium, paid, and enterprise. Do not filter by tier unless the user asked you to.

### Step 4 — Format
Write each API to `apis/<category>/<api-slug>.md` using the exact template in section 6.

### Step 5 — Update the README catalog
Read the current README, then update it per section 7. Files are added/updated/removed in alphabetical order within each category section. The `Last Updated` column in the README must match the `Last researched` date inside the corresponding API file — these two values are checked against each other during review.

### Step 6 — Preview and approval
Before any write, show the user a complete preview:

> Ready to commit:
>
> **New file:** `apis/<category>/<api>.md` — full content shown below
> **Updated file:** `apis/<category>/<other-api>.md` — refresh; diff summary follows
> **Updated file:** `README.md` — added 1 row, updated 1 existing row
>
> [show full file contents and diffs]
>
> Approve to commit?

Wait for explicit confirmation. If the user requests edits, apply them and re-preview. Never commit without an explicit yes.

### Step 7 — Commit
- **One file per commit.** Clean history, easy to review and revert.
- **Order:** API detail files first, README last. If anything fails midway, the README never points to files that don't exist.
- **Direct to `main`.** No PRs, no feature branches.
- **Commit message format** (see section 8).
- **Updates require the file's current `sha`** (from the read in Step 2). Without it, GitHub returns 422.

After all writes succeed, give the user a summary with the commit URLs so they can verify.

---

## 5. Allowed and forbidden actions

### Allowed
- Reading any file in the repo at any time, without approval.
- Researching APIs via web search and direct fetches of vendor documentation.
- Proposing new categories (with user approval).
- Refreshing stale entries (with user approval).
- Marking entries as discontinued (with user approval).
- Adding `_`-prefixed reference files per section 2 (with user approval).

### Forbidden
- Committing without explicit user approval.
- Skipping the catalog check in Step 2.
- Inventing categories without proposing them first.
- Filling in fields with guessed data — use `Not publicly documented` instead.
- Editing GOVERNANCE.md, README structure, or the entry template without explicit user instruction to do so. (Note: `_`-prefixed reference files per section 2 are not entries and are exempt from the section 6 template — do not flag them as non-compliant.)
- Using PR or branch workflows. This repo commits direct to `main`.
- Bulk-refreshing entries the user didn't ask about. Stale-entry flagging is per-category, scoped to the user's current request.

---

## 6. API entry template

Every file in `apis/<category>/` uses this template, exactly:

```markdown
# <API Name>

<One-sentence description of what the API does.>

**Tier:** <Free | Freemium | Paid | Enterprise>
**Auth:** <auth method, brief>
**Last researched:** <YYYY-MM-DD>

## Use cases

- <real use case this API is suited for>
- <another>
- <another>

## Pricing

- **Free tier:** <limits, or "None">
- **Paid tiers:** <names + prices, or "None">
- **Enterprise:** <notes, or "Contact sales" / "N/A">
- **Notes:** <overage charges, annual discounts, etc.>

## Authentication

<How to authenticate. Where to get keys/credentials. Header or query-param format.>

## Endpoints

- **Base URL:** `<url>`
- **Key endpoints:**
  - `GET /<path>` — <what it does>
  - `POST /<path>` — <what it does>

## Example call

\`\`\`bash
curl -H "Authorization: Bearer $API_KEY" \
  "https://api.example.com/v1/resource?param=value"
\`\`\`

<Optional: SDK example in Python or Node>

## Rate limits

<As published. If not published, say so explicitly.>

## SDKs / Libraries

- **Official:** <list with links>
- **Community:** <list, if notable>

## Documentation

- Main docs: <url>
- API reference: <url>

## Notes

<Gotchas, deprecations, regional issues, licensing terms, source disagreements.>
```

Required fields: API Name, Tier, Auth, Last researched, Use cases, Pricing, Authentication, Endpoints, Example call, Rate limits, Documentation. The SDKs and Notes sections may be omitted only if both are genuinely empty.

This template applies to API entries only. `_`-prefixed reference files (section 2) are exempt.

---

## 7. README catalog format

The README has three parts: header, Categories list, and one section per category.

```markdown
# API Library

A curated catalog of researched APIs. Each entry links to a detail file with pricing, auth, endpoints, and example calls.

See `GOVERNANCE.md` for contribution rules.

## Categories

- [Payment](#payment)
- [Sports Stats](#sports-stats)
- [Weather](#weather)

---

## Payment

| API | Tier | Auth | Last Updated | Details |
|---|---|---|---|---|
| Stripe | Freemium | API Key | 2026-03-15 | [→](apis/payment/stripe.md) |

## Sports Stats

| API | Tier | Auth | Last Updated | Details |
|---|---|---|---|---|
| SportsRadar | Paid | API Key | 2026-04-22 | [→](apis/sports-stats/sportsradar.md) |
| TheSportsDB | Freemium | API Key | 2026-05-07 | [→](apis/sports-stats/the-sports-db.md) |
```

**Rules:**
- Categories list at the top is alphabetical.
- Each category section header matches the Categories list anchor.
- Within a category table, rows are alphabetical by API name.
- The `Last Updated` column matches the `Last researched` date inside the linked file.
- New category sections are inserted alphabetically, not appended at the end.
- `_`-prefixed reference files (section 2) do **not** get catalog rows. They live in the category folder but are not listed in the README tables.

---

## 8. Commit messages

Format: `[<agent-tag>] <action>: <detail>`

**Agent tags** identify which agent made the commit:
- `[claude-skill]` — Anthropic Claude using the `api-researcher` skill
- `[claude-code]` — Claude Code CLI
- `[chatgpt]` — ChatGPT (any model)
- `[codex]` — OpenAI Codex
- `[human]` — direct human edit (no agent involvement)

**Actions:**
- `Add API: <Name> (<category>)` — new entry
- `Refresh API: <Name> (<category>)` — update existing entry
- `Remove API: <Name> (<category>)` — delete entry (deprecated/discontinued)
- `Add reference: <description>` — new `_`-prefixed reference file (section 2)
- `Update reference: <description>` — update a reference file
- `Update catalog: <description>` — README-only change
- `Update governance: <description>` — GOVERNANCE.md change
- `Bootstrap repo: <description>` — initial setup

**Examples:**
```
[claude-skill] Add API: Stripe (payment)
[chatgpt] Refresh API: SportsRadar (sports-stats)
[codex] Update catalog: alphabetize sports-stats table
[human] Update governance: clarify staleness rule
[claude-skill] Add reference: market-intelligence correlation playbook
```

---

## 9. Concurrency and conflicts

If `github_create_or_update_file` (or equivalent) returns a 422 about a mismatched SHA:

1. Stop. Do not retry blindly.
2. Re-read the file to get the new SHA and current contents.
3. Re-merge your changes against the current contents.
4. Show the user the new merged preview.
5. Get fresh approval.
6. Retry.

If the file changed in a way that conflicts with what you were about to write (someone else cataloged the same API while you were researching), surface that to the user and let them decide whether to merge, overwrite, or abandon.

---

## 10. Discontinued APIs

If research reveals an API is dead or has fundamentally changed, two options:

1. **Mark as discontinued.** Update the entry to begin with `> ⚠️ **Discontinued as of YYYY-MM-DD.** <reason>` directly under the H1. Keep the rest of the entry as historical record. Update the README row's Tier column to `Discontinued`.
2. **Remove entirely.** Delete the file and remove the README row.

Always offer both options to the user — let them choose.

---

## 11. Per-platform agent guidance

The four core principles, the workflow, the template, and the README format apply to all agents identically. This section covers the small handful of platform-specific differences.

### Anthropic Claude (claude.ai with the `api-researcher` skill)

The skill carries a cached copy of these rules and a `governance-version` stamp. At the start of every run, the skill performs a Step 0 that fetches this live GOVERNANCE.md and compares versions. If versions differ, the live version wins (see section 12). The skill commits via the custom GitHub MCP at `https://github-mcp-railway-production-dcdc.up.railway.app/mcp`, which is locked to this repo via a `GITHUB_REPO` env var.

**Tools used:** `github remote mcp:github_repo_info`, `github_list_repository_files`, `github_get_file`, `github_create_or_update_file`, `github_delete_file`.

### Claude Code

Use natural file operations against a local clone:

```bash
gh repo clone NegativeBounce/api-library
cd api-library
```

Read `GOVERNANCE.md` first thing in any session that touches this repo. Follow steps 1–7 in section 4 exactly. Commit using `git` directly with the message format in section 8. Push to `main`.

### ChatGPT

Use the GitHub connector or paste file contents directly into the chat. Read `GOVERNANCE.md` before starting research. When ready to commit, write the proposed file contents into the chat for the user, get explicit approval, then either commit through the connector or hand the user the content to commit themselves. Use the commit message format in section 8 with the `[chatgpt]` tag.

### OpenAI Codex

Operates inside a workspace with the repo checked out. Same flow as Claude Code: read `GOVERNANCE.md`, follow the workflow in section 4, commit with `git` using the section 8 format and the `[codex]` tag.

---

## 12. Modifying this document and managing drift

### Editing GOVERNANCE.md

GOVERNANCE.md changes follow the same approval rule as everything else: preview, get explicit user approval, commit. Use the `[<agent-tag>] Update governance: <description>` commit format.

**Whenever GOVERNANCE.md is edited, the `governance-version` stamp at the top of the file must be bumped** to today's date (`YYYY-MM-DD`). Without a version bump, drift detection in dependent agents (e.g., the Anthropic skill) is silently broken.

### How drift is detected

The Anthropic `api-researcher` skill carries its own cached copy of these rules in `SKILL.md`, plus a matching `governance-version` stamp. At the start of every run, the skill executes a Step 0 that fetches this live `GOVERNANCE.md` and compares versions:

- **Versions match** → proceed silently using either copy (they are equivalent).
- **Versions differ** → the live `GOVERNANCE.md` wins. The skill follows the live rules and surfaces the drift to the user with a recommendation to update the skill ZIP.
- **Live fetch fails** (MCP down, network issue) → fall back to the cached `SKILL.md` rules, but flag to the user that governance could not be verified.

This is also the contract for any future agent that wants to ship its own cached governance copy (e.g., a custom GPT prompt, a Codex system message): include the `governance-version` stamp, fetch this file at session start, and follow the same precedence rules.

### When to bump the version

Bump the version stamp whenever you change:
- Any of the four core principles (section 3).
- The workflow steps (section 4).
- The allowed/forbidden lists (section 5).
- The API entry template (section 6).
- The README format (section 7).
- The commit message format or agent tags (section 8).

You do **not** need to bump the version for purely cosmetic edits (typo fixes, formatting, clarifying examples that don't change rules). Use judgment: if an agent following the old version would behave differently from one following the new version, bump.

### Dependent files to review on a version bump

When `governance-version` changes, review these for drift and update them in the same session:

- **The `api-researcher` skill's SKILL.md** — bump its cached `governance-version` to match, sync the rule changes, repackage as `.skill`, and re-upload to Claude.ai. Until the skill is re-uploaded, Claude users will see the drift warning on every run, which is annoying but safe.
- **Any custom-GPT system prompts, Codex preludes, or Claude Code memory files** that contain cached rules from this document.

The drift warning from the skill is your reminder to do this. If you see it, you have a sync task to do.
