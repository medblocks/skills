# Medblocks Skills

[Medblocks](https://medblocks.com) gives applications the easiest way to access a patient's longitudinal health data in a clean, normalized format with their consent, across EHRs, payer APIs, health information networks, and clinician workflows, through a single API.

These skills teach coding agents how to build with Medblocks. They cover integration best practices, Patient Access flows, and FHIR record export, grounded in the live docs and the Medblocks SDK.

Authored internally under `ai/plugins/` and mirrored to the public `medblocks/skills` repo by `.github/workflows/agent-skills-publish.yml` on merge to main.

The public repo mirrors the Better Auth shape:

```text
.claude-plugin/
medblocks/
  .claude-plugin/
  best-practices/
  patient-access/
  export-fhir/
```

`SKILL.md` folders are the portable skill surface. The root `.claude-plugin/marketplace.json` and `medblocks/.claude-plugin/plugin.json` files are Claude-specific packaging metadata.

## Install (end users, from the public mirror)

Recommended one-liner. Works across agents (Claude Code, Cursor, Codex, and others):

```bash
npx skills add medblocks/skills
```

Claude Code native plugin install (adds update tracking via `claude plugin marketplace update`):

```bash
claude plugin marketplace add medblocks/skills
claude plugin install medblocks-skills@medblocks
```

## Maintenance rules

- Patient Access docs or `docs/src/lib/prompts.ts` (`patient-access-build`) changes require reviewing `medblocks/patient-access/SKILL.md`.
- `/records`, FHIR export, or data-out docs changes require reviewing `medblocks/export-fhir/SKILL.md`.
- SDK or API behavior changes require reviewing `medblocks/best-practices/SKILL.md`.
- Keep only stable primitives and semantic rules inlined in the skills. Do not copy full endpoint, parameter, payload, or event references into skills; link out for high-churn details.
- Keep public skills product-facing. Do not include private Medblocks codebase internals.
- Mirroring requires the `AGENT_SKILLS_DEPLOY_TOKEN` repo secret (fine-grained PAT with contents write on `medblocks/skills`).
