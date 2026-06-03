# Skill LGPD SaaS Brasil Compliance

Skill em pt-BR para orientar agentes de engenharia na auditoria técnica e documental de LGPD, privacidade, cookies, SDKs, rastreadores, retenção, incidentes, fornecedores, transferências internacionais e controles mínimos de segurança em SaaS no Brasil.

## Autor

- Nome: Anobyzy
- Email: anobyzy@gmail.com
- Revisão do pacote: 2026-06-03
- Versão: 2.0.1

## Instalação

Para uso como skill local, mantenha a pasta com o mesmo nome do frontmatter:

```powershell
git clone git@github.com:Anobyzy/skill-lgpd-brasil.git
```

Depois aponte o agente para `SKILL.md` ou instale a pasta no diretório de skills do seu ambiente.

## Uso recomendado

```text
Use $lgpd-saas-brasil-compliance-skill para auditar este repositório. Mapeie dados pessoais, cookies, SDKs, fornecedores, transferências internacionais, riscos de segurança, direitos do titular e lacunas LGPD. Gere ou atualize artefatos em .lgpd/ e privacy/. Corrija o que for técnico e bloqueie o release se houver risco crítico.
```

## Conteúdo

- `SKILL.md`: instruções principais da skill.
- `agents/openai.yaml`: metadados de interface para ambientes que suportam skills.
- `references/`: referência normativa resumida.
- `privacy/`: templates CSV e Markdown para inventários, bases legais, retenção, riscos, cookies, DSAR, LIA, ROPA, fornecedores e PR review.
- `security/`: templates de incidentes e controles de segurança.
- `.lgpd-templates/`: modelos para artefatos vivos em `.lgpd/`.
- `MANIFEST.json`: manifesto gerado com hashes SHA-256 dos arquivos do pacote.

## Publicação no GitHub por SSH

Se o repositório remoto ainda não existir, crie um repositório vazio no GitHub e publique com:

```powershell
git init
git add .
git commit -m "release: prepare lgpd compliance skill"
git branch -M main
git remote add origin git@github.com:Anobyzy/skill-lgpd-brasil.git
git push -u origin main
```

Se preferir outro nome de repositório, ajuste apenas a URL do `git remote add origin`.

## Limite

Este pacote não é parecer jurídico. Ele é uma skill técnica e documental para reduzir risco, gerar evidências e apontar quando revisão jurídica humana é necessária.

## Fontes oficiais verificadas

Verificação feita em 2026-06-03:

- ANPD, regulamentações vigentes: https://www.gov.br/anpd/pt-br/acesso-a-informacao/institucional/atos-normativos/regulamentacoes_anpd
- Planalto, Lei nº 15.211/2025: https://www.planalto.gov.br/ccivil_03/_ato2023-2026/2025/lei/l15211.htm
- Planalto, Decreto nº 12.880/2026: https://www.planalto.gov.br/ccivil_03/_ato2023-2026/2026/decreto/d12880.htm
- Planalto, Lei nº 15.352/2026: https://www.planalto.gov.br/ccivil_03/_ato2023-2026/2026/lei/l15352.htm
