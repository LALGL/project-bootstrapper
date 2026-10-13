# project-bootstrapper

A reusable, **domain-agnostic** skill that bootstraps any multi-session project with a traceable, extensible, handoff-ready scaffold.

It works for anything that spans sessions, has raw data, and must produce auditable deliverables: literature review, paper writing, data analysis, engineering R&D, knowledge-base building.

## Why

Long AI-assisted collaborations rot from three silent failures:
- **Divergent files** — conclusions scattered across reports with no single authority.
- **Lost context** — stale summaries / compressed history silently drift from disk reality.
- **Information dilution** — long chats fill with fluff instead of decisions.

This skill attacks all three up front, on the very first task.

## What it creates

One **single-source-of-truth control document** (`{{PROJECT_NAME}}_项目规范.md`) with fixed sections — including two always-empty slots (integration-contract / known-pitfalls and environment-contract) that each project fills with its own concrete instances — plus a copy-paste **universal startup prompt** you can reuse for any future project.

## The disciplines it enforces

| # | Discipline | One-line rule |
|---|---|---|
| 1 | Single source of truth | One control doc (fixed sections incl. two empty slots); never edit a report without editing the spec. |
| 2 | Semantic raw-data renaming & archival | Archive every input into `data/raw/` on entry; rename to `<type>_<desc>_<n>`; immutable raw, derived copies go to `data/processed/`; record provenance + hash in §4. |
| 3 | Deliverable numbering & lifecycle | Doc projects default `<主题>_<类型>_<版本>_<日期>`; high-volume streams use `YYMMDD-NNN_<semantic>`; superseded files get `_退役_`/`_作废_` markers, kept on disk. |
| 4 | Intermediate vs final-text separation | Ship a paper-ready "成稿文字" alongside reports; one final text per finding. |
| 5 | Verification log + changelog | Independent checks with fact-vs-inference split form the audit chain. |
| 6 | Context-drift correction | After any compression/continuation, re-read disk before editing; never trust stale summaries. |
| 7 | Handover checklist | A permanent "next steps" list so any future self/collaborator can continue. |
| 8 | Process-reply style | Every reply is clear / appropriately detailed / concise / no fluff. |
| 9 | Destructive-write pre-flight gate | Any external-system write/delete needs a named snapshot + DRY_RUN default + rollback artifact in the log. |
| 10 | Attempt budget & escalation ceiling | Fix a retry ceiling + fallback ladder up front; stop and switch tiers instead of re-hammering. |
| 11 | Reusable-script harvesting | Promote a hard-won workaround script into a named, documented tool/skill. |
| 12 | Feasibility tiering | Label each deliverable's production path (automated / semi / manual-browser / human). |
| 13 | Functional folder taxonomy | Assign files to `deliverables/` `workings/` `data/raw/` `data/processed/` `references/` `scripts/` `memory/` by functional attribute; control doc + index stay at root; default layout, adaptable if documented. |

## How to use

1. Trigger the skill: *"start a new project"*, *"set up a project spec"*, *"create a project startup prompt"*, or when a project shows drift.
2. The AI builds the control-document skeleton for you to confirm.
3. Copy the universal startup prompt from `references/bootstrap_template.md` §二 and paste it as the first message of any new project — fill the five `{{...}}` placeholders.

## Install (WorkBuddy)

Drop this folder into your user skills directory:

```
~/.workbuddy/skills/project-bootstrapper/
├── SKILL.md
├── references/bootstrap_template.md
└── README.md
```

Then invoke it by name or by the trigger phrases above.

## Safety

Documentation-only. No executable code, no network calls, no external dependencies.

## License

[MIT](LICENSE) © 2026 LALGL. Free to use, modify, and redistribute.
