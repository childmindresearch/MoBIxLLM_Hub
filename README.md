# MoBIxLLM_Hub

Central hub for the **MoBI × LLM** project (MSM-MoBI): a study of physiological and behavioral responses to interacting with large language models, run both in the MoBI lab and online via Prolific.

This repo does two jobs:

1. **Map.** It indexes every MoBIxLLM repository under the [`childmind`](https://github.com/childmind) org.
2. **Source of truth.** It holds the shared resources (LLM stances, vignettes and probes, randomization schemes, safety checks), the cross-system analyses, and the project's development discussion (as Issues).

> ⚠️ **No participant data in this repo or any MoBIxLLM repo.** This includes transcripts, Prolific IDs, physiological recordings, and anything else linked to a participant. Data lives in: `<approved storage location>`.

---

## Repository map

All repos follow the naming convention **`MoBIxLLM_<Name>`**.

| Repo | What it is | Setting | Status | Owner |
|---|---|---|---|---|
| [MoBIxLLM_Hub](https://github.com/childmind/MoBIxLLM_Hub) | This repo: index, shared resources, analyses, discussion | — | Active | `@owner` |
| [MoBIxLLM_LabStructured](https://github.com/childmind/MoBIxLLM_LabStructured) | Structured LLM-interaction UI for in-lab sessions *(formerly MoBI-MSM)* | In-lab | `Active / Piloting` | `@owner` |
| [MoBIxLLM_LabUnstructured](https://github.com/childmind/MoBIxLLM_LabUnstructured) | Free-form LLM-interaction UI for in-lab sessions | In-lab | `Status` | `@owner` |
| [MoBIxLLM_ProlificStructured](https://github.com/childmind/MoBIxLLM_ProlificStructured) | Web-based structured UI for online data collection | Prolific | `Status` | `@owner` |
| [MoBIxLLM_ProtocolRunner](https://github.com/childmind/MoBIxLLM_ProtocolRunner) | Wizard that guides RAs through the in-lab session protocol | In-lab | `Status` | `@owner` |

**Status key:** `Active` in use for data collection · `Piloting` in testing, not yet collecting study data · `Dev` under development · `Archived` retired, kept for reference

---

## How the pieces fit

```
                  ┌──────────────────────────────┐
                  │        MoBIxLLM_Hub          │
                  │  shared/  (source of truth)  │
                  └──────────────┬───────────────┘
                                 │  tagged releases (e.g., pool-v3)
        ┌───────────────┬────────┴───────┬──────────────────┐
        ▼               ▼                ▼                  ▼
  LabStructured   LabUnstructured   ProlificStructured   ProtocolRunner
```

Each app repo consumes a **pinned, tagged version** of the shared resources and logs that version with every session. That way, for any participant, we can say exactly which stances, vignette pool, randomization scheme, and safety checks they got.

---

## Repo structure

```
MoBIxLLM_Hub/
├── README.md
├── shared/
│   ├── llm-stances/
│   │   ├── README.md              # definitions and goals of each stance
│   │   ├── prompts/               # system prompts used in sessions, by version
│   │   └── generation-prompts/    # prompts used to generate/refine the stance prompts
│   ├── vignettes-probes/
│   │   ├── README.md              # definitions, goals, inclusion criteria
│   │   ├── current/               # active pool
│   │   ├── archive/               # past pools (pool-v1/, pool-v2/, ...)
│   │   └── generation-prompts/
│   ├── randomization/
│   │   └── README.md              # schemes, arms, counterbalancing logic
│   └── safety-checks/
│       └── README.md              # what is checked, when, and escalation steps
├── analyses/
│   ├── exploratory/               # vibe-coded; fast iteration, no guarantees
│   └── validated/                 # reviewed and reproducible; basis for any reported result
└── docs/
    └── protocol/                  # IRB-approved protocol versions, SOPs
```

---

## Versioning shared resources

- **Changes go through Issues and PRs.** Every change to `shared/` should reference the Issue that motivated it.
- **Tag releases** when a version is ready for use in an app. Use a tag per resource type:
  - `stances-v2`
  - `pool-v3`
  - `randomization-v1`
  - `safety-v2`
- **Archive, don't delete.** When a vignette pool is retired, move it to `archive/` rather than overwriting it. Past data depends on it.
- **Apps log the tags.** Every session record should include the tags of the shared resources in use.

**Currently deployed versions:**

| Resource | LabStructured | LabUnstructured | ProlificStructured |
|---|---|---|---|
| LLM stances | `stances-v?` | `stances-v?` | `stances-v?` |
| Vignette pool | `pool-v?` | n/a | `pool-v?` |
| Randomization | `randomization-v?` | `randomization-v?` | `randomization-v?` |
| Safety checks | `safety-v?` | `safety-v?` | `safety-v?` |

---

## Analyses

| Folder | Purpose | Standard |
|---|---|---|
| `analyses/exploratory/` | Quick looks, pilot checks, vibe-coded scripts | Anything goes. Date-prefix folders (`2026-09-29_stance-effects/`). |
| `analyses/validated/` | Anything that informs a decision, report, or paper | Code reviewed, reproducible from raw data, pinned dependencies, README per analysis |

**Promotion rule:** an exploratory analysis moves to `validated/` once its result will be cited or acted on, and not before it's been reviewed.

---

## Development discussion (Issues)

All design discussion lives in this repo's **Issues**, including feedback and direction from leadership. This keeps rationale searchable and linked to the changes it drove.

**Labels:**

| Label | Use for |
|---|---|
| `area:stances` | LLM stances and prompts |
| `area:vignettes` | Vignettes, probes, pools |
| `area:randomization` | Randomization schemes |
| `area:safety` | Safety checks |
| `area:analysis` | Analyses (exploratory or validated) |
| `app:lab-structured` · `app:lab-unstructured` · `app:prolific` · `app:protocol-runner` | Issues specific to one app (cross-linked to that app's repo) |
| `source:leadership` | Direction or feedback from leadership (e.g., emails) |
| `type:decision` | A settled decision. Close with a one-line summary of what was decided |

**Guidelines for email-sourced Issues:**
- Summarize the substance and the ask.
- Don't paste full email threads.
- Include the date and sender.

---

## Getting started

1. Request access to the `childmind` org and the MoBIxLLM repos from `@owner`.
2. Read `shared/*/README.md` for the current study design.
3. Check the **Currently deployed versions** table before making changes to any app.
4. Never commit API keys or `.env` files. Use `<secrets manager / instructions>`.

---

## Contacts

| Role | Person |
|---|---|
| Project lead | `@name` |
| Lab systems | `@name` |
| Prolific / web | `@name` |
| Analysis | `@name` |
