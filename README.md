# Medblocks Skills

[Medblocks](https://medblocks.com) gives applications the easiest way to access a patient's longitudinal health data in a clean, normalized format with their consent, across EHRs, payer APIs, health information networks, and clinician workflows, through a single API.

This skill teaches coding agents how to build with Medblocks. It covers integration best practices, Patient Access flows, and FHIR record export, grounded in the live docs and the Medblocks SDK.

Authored internally under `ai/plugins/` and mirrored to the public `medblocks/skills` repo by `.github/workflows/agent-skills-publish.yml` on merge to main.

Everything ships as one skill folder so every install method produces a single `medblocks` entry in the user's skills directory:

```text
.claude-plugin/
  marketplace.json
skills/
  medblocks/
    SKILL.md
    patient-access.md
    export-fhir.md
```

`skills/medblocks/` is the portable skill surface. `SKILL.md` is the entrypoint with the stable integration playbook; agents read `patient-access.md` and `export-fhir.md` on demand for task-specific flows. The root `.claude-plugin/marketplace.json` is Claude-specific packaging metadata (the marketplace root itself is the plugin, so there is no separate `plugin.json`).

## Install (end users, from the public mirror)

Recommended one-liner. Works across agents (Claude Code, Cursor, Codex, and others) and installs a single `medblocks` skill folder:

```bash
npx skills add medblocks/skills
```

Claude Code native plugin install (adds update tracking via `claude plugin marketplace update`):

```bash
claude plugin marketplace add medblocks/skills
claude plugin install medblocks-skills@medblocks
```

Manual install is a plain copy:

```bash
cp -r skills/medblocks ~/.claude/skills/medblocks
```

## Maintenance rules

- Patient Access docs or `docs/src/lib/prompts.ts` (`patient-access-build`) changes require reviewing `skills/medblocks/patient-access.md`.
- `/records`, FHIR export, or data-out docs changes require reviewing `skills/medblocks/export-fhir.md`.
- SDK or API behavior changes require reviewing `skills/medblocks/SKILL.md`.
- Keep only stable primitives and semantic rules inlined in the skill. Do not copy full endpoint, parameter, payload, or event references into it; link out for high-churn details.
- Keep the public skill product-facing. Do not include private Medblocks codebase internals.
- Mirroring requires the `AGENT_SKILLS_DEPLOY_TOKEN` repo secret (fine-grained PAT with contents write on `medblocks/skills`).
