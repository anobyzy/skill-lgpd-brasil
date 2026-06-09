# Skill LGPD SaaS Brazil Compliance

Portuguese-Brazilian skill that guides engineering agents through technical and documentation audits for LGPD, privacy, cookies, SDKs, trackers, retention, incidents, vendors, international transfers, and minimum security controls for SaaS products in Brazil.

## What It Does

The skill instructs the agent to map personal data processing across code, documentation, infrastructure, and vendors, generate compliance evidence, and identify technical blockers before release.

It covers, among other topics:

- inventory of personal, sensitive, and child/adolescent data;
- legal bases, legitimate interest, consent, and retention;
- cookies, SDKs, analytics, advertising, and trackers;
- DSAR, ROPA, RIPD, LIA, incidents, and international transfers;
- vendors, subprocessors, logs, security, and access controls;
- alignment between code, privacy policy, and audit artifacts.

## When To Use

Use this skill when implementing, reviewing, or auditing features that process personal data in SaaS products, web apps, mobile apps, APIs, checkout, billing, support, CRM, analytics, ads, AI, automations, integrations, webhooks, logs, cookies, or SDKs.

Also use it when the request involves LGPD, privacy, cookies, DPO, ANPD, privacy by design, impact reports, incidents, data subject rights, or privacy policy review.

## Installation

Clone the repository:

```powershell
git clone ssh://git@github.com/anobyzy/skill-lgpd-brasil.git
```

For local installation, use the folder as a skill in the agent environment or point the agent directly to `SKILL.md`.

The skill name in the frontmatter is:

```text
lgpd-saas-brasil-compliance-skill
```

## How To Use

Recommended prompt:

```text
Use $lgpd-saas-brasil-compliance-skill to audit this repository. Map personal data, cookies, SDKs, vendors, international transfers, security risks, data subject rights, and LGPD gaps. Generate or update evidence in .lgpd/ and supporting documents in privacy/ when needed. Fix technical issues and block the release if there is critical risk.
```

## Expected Outputs

When applicable, the skill guides the agent to generate or update:

- `.lgpd/STATUS.md`;
- `.lgpd/data-map.md`;
- `.lgpd/legal-basis.md`;
- `.lgpd/ROPA.md`;
- `.lgpd/lia/`;
- `.lgpd/RIPD/`;
- `.lgpd/consent/consent-ledger.md`;
- `.lgpd/dsar/dsar-runbook.md`;
- `.lgpd/incidents/incident-runbook.md`;
- `.lgpd/transfers/`;
- `.lgpd/vendors/`;
- `.lgpd/retention-schedule.md`;
- `.lgpd/eca-digital.md`;
- `.lgpd/automated-decisions.md`;
- `.lgpd/security-controls.md`;
- `.lgpd/gaps.md`;
- `.lgpd/privacy-compliance-report.md`;
- `privacy/privacy-review-pr-template.md`;
- `privacy/privacy-test-plan.md`.

## Package Structure

- `SKILL.md`: main skill instructions.
- `agents/openai.yaml`: interface metadata for environments that support skills.
- `references/`: summarized regulatory reference.
- `privacy/`: CSV and Markdown templates for inventories, legal bases, retention, risks, cookies, DSAR, LIA, ROPA, vendors, and PR review.
- `security/`: incident and security control templates.
- `.lgpd-templates/`: templates for living artifacts in `.lgpd/`.
- `MANIFEST.json`: manifest with SHA-256 hashes for package files.

## Limitation

This skill does not replace human legal review and is not legal advice. It reduces risk through technical evidence, minimization, governance, traceability, and remediation of verifiable gaps.
