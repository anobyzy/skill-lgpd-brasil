# Skill LGPD SaaS Brasil Compliance

Skill em pt-BR para orientar agentes de engenharia na auditoria técnica e documental de LGPD, privacidade, cookies, SDKs, rastreadores, retenção, incidentes, fornecedores, transferências internacionais e controles mínimos de segurança em SaaS no Brasil.

## O Que Ela Faz

A skill instrui o agente a mapear tratamentos de dados pessoais no código, documentação, infraestrutura e fornecedores, gerar evidências de conformidade e apontar bloqueadores técnicos antes de release.

Ela cobre, entre outros pontos:

- inventário de dados pessoais, sensíveis e de crianças/adolescentes;
- bases legais, legítimo interesse, consentimento e retenção;
- cookies, SDKs, analytics, publicidade e rastreadores;
- DSAR, ROPA, RIPD, LIA, incidentes e transferência internacional;
- fornecedores, subprocessadores, logs, segurança e controles de acesso;
- alinhamento entre código, política de privacidade e artefatos de auditoria.

## Quando Usar

Use esta skill ao implementar, revisar ou auditar funcionalidades que tratem dados pessoais em SaaS, aplicativos web, aplicativos móveis, APIs, checkout, billing, suporte, CRM, analytics, anúncios, IA, automações, integrações, webhooks, logs, cookies ou SDKs.

Também use quando o pedido envolver LGPD, privacidade, cookies, DPO, ANPD, privacy by design, relatório de impacto, incidentes, direitos do titular ou revisão de política de privacidade.

## Instalação

Clone o repositório:

```powershell
git clone ssh://git@github.com/anobyzy/skill-lgpd-brasil.git
```

Para instalação local, use a pasta como skill no ambiente do agente ou aponte o agente diretamente para `SKILL.md`.

O nome da skill no frontmatter é:

```text
lgpd-saas-brasil-compliance-skill
```

## Como Usar

Prompt recomendado:

```text
Use $lgpd-saas-brasil-compliance-skill para auditar este repositório. Mapeie dados pessoais, cookies, SDKs, fornecedores, transferências internacionais, riscos de segurança, direitos do titular e lacunas LGPD. Gere ou atualize evidências em .lgpd/ e documentos auxiliares em privacy/ quando necessário. Corrija o que for técnico e bloqueie o release se houver risco crítico.
```

## Saídas Esperadas

Quando aplicável, a skill orienta o agente a gerar ou atualizar:

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

## Estrutura Do Pacote

- `SKILL.md`: instruções principais da skill.
- `agents/openai.yaml`: metadados de interface para ambientes que suportam skills.
- `references/`: referência normativa resumida.
- `privacy/`: templates CSV e Markdown para inventários, bases legais, retenção, riscos, cookies, DSAR, LIA, ROPA, fornecedores e PR review.
- `security/`: templates de incidentes e controles de segurança.
- `.lgpd-templates/`: modelos para artefatos vivos em `.lgpd/`.
- `MANIFEST.json`: manifesto com hashes SHA-256 dos arquivos do pacote.

## Limite

Esta skill não substitui revisão jurídica humana e não é parecer jurídico. Ela reduz risco por meio de evidência técnica, minimização, governança, rastreabilidade e correção de lacunas verificáveis.
