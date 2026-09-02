---
type: Analysis
title: Knowledge Collaboration Workflow
description: Summary of how the team organizes per-topic knowledge vaults using Hermes + OKF template
status: stable
generated: { by: human:user, at: 2026-09-02T00:00:00Z }
sources:
  - id: conversation
    resource: this conversation
    title: Team knowledge collaboration discussion
    author: human:user
    last_modified: 2026-09-02T00:00:00Z
---

# Knowledge Collaboration Summary

## Conversation Overview
This page summarizes the team's approach to organizing per-topic knowledge vaults using Hermes Agent + the OKF v0.2 knowledge template.

## Key Decisions

1. **Per-topic vaults** — Each coworker works in their own topic sub-vault under a shared `knowledge_kb/` root:
   - `electrical/` — electrical engineering, wiring, circuits
   - `conservation/` — energy conservation, sustainability
   - `rl/` — reinforcement learning, policy gradients
   - `ml/` — machine learning, neural networks
   - `code/` — programming, functions, APIs
   - `devops/` — CI/CD, Kubernetes, Docker

2. **Hermes profiles per user** — Each team member runs Hermes with their own isolated profile (`alice/`, `bob/`, `carol/`), preventing topic↔vault map clashes.

3. **knowledge-manager skill** — Auto-detects topics in conversation and routes the agent to the correct vault. Falls back to `unsorted` when no keyword matches.

4. **Keyword registry** — Each user's skill instance has a keyword→vault mapping:
   - Alice: `electrical`→electrical-vault, `conservation`→conservation-vault
   - Bob: `rl`→rl-vault, `ml`→ml-vault
   - Carol: `code`→code-vault, `devops`→devops-vault

5. **Auto-creation** — When a new topic is mentioned and its vault doesn't exist, the skill auto-creates it from `knowledge_template/` scaffold.

6. **Fallback** — Unknown topics route to `knowledge_unsorted/` with the same scaffold.

## Workflow per Topic

### New topic first mention
```
User: "I'm working on three-phase motor winding"
→ Hermes (Alice's profile) detects "electrical" keyword
→ Checks ~/knowledge_kb/electrical-vault/ → doesn't exist
→ Creates from scaffold: cp -r ~/knowledge_template ~/knowledge_kb/electrical-vault
→ Runs: python3 tools/okf.py lint
→ Agent ingests from electrical-vault onwards
```

### Unknown topic
```
User: "I'm thinking about medieval pottery"
→ No keyword match → falls back to unsorted
→ Creates ~/knowledge_kb/unsorted-vault/ from scaffold if missing
→ User can later refine classification
```

## CLI Commands

```bash
# Set active vault manually
hermes knowledge set-vault electrical-vault

# Check current state
hermes knowledge status
# Output: Active vault: electrical-vault | Topic map: electrical→...

# List all known topic mappings (from memory)
hermes memory show
```

## Technical Details

- **Template**: `~/knowledge_template/` — OKF v0.2 scaffold (AGENTS.md, tools/okf.py, templates/)
- **Vault layout**: `~/knowledge_kb/<topic>-vault/` with standard OKF dirs (wiki/concepts/, wiki/sources/, wiki/entities/, wiki/analyses/)
- **Validation**: `python3 tools/okf.py lint` enforces: type field, ## Summary ≥40 chars, kebab-case filenames, ≤300 lines, no orphans
- **Index rebuild**: `python3 tools/okf.py rebuild-index` after each ingest
- **Audit log**: wiki/log.md tracks all changes in `YYYY-MM-DD | ACTION | path | note` format
- **Cross-links**: OKF bundle-relative links (`/concepts/...`, `/sources/...`) enable navigation across vaults

## Benefits

- **Isolated per-user context** — Hermes memory is profile-scoped, no map clashes
- **Zero-config start** — New topics auto-created from scaffold
- **OKF conformance** — Lint ensures quality as vault grows
- **Git-backed** — Full version history in `knowledge_kb/` git repo
- **Scalable** — Add more topics/keywords as team expands

## Future Extensions

- Add topic: `concept-engineering` → new vault + keyword
- Cross-vault Dataview queries for inter-topic insights
- Shared `overview.md` in each vault listing related topics from other vaults
- Git branch per topic for parallel development
- Automated cross-vault citation suggestions when agents ingest new sources