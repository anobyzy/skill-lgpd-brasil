---
name: lgpd-saas-brasil-compliance-skill
description: "Use when auditing or implementing LGPD/privacy compliance for Brazilian SaaS, web apps, mobile apps, APIs, cookies, SDKs, analytics, ads, billing, support, logs, AI, DSAR, ROPA, RIPD/LIA, international transfers, incidents, vendors, privacy policies, consent, retention, security controls, or release blockers."
license: "MIT"
metadata:
  version: "2.1.0"
  language: "pt-BR"
  author: "Anobyzy"
  author_email: "anobyzy@gmail.com"
  last_reviewed: "2026-06-03"
  risk_posture: "conservadora"
  intended_agents: "Codex, Claude Code, Gemini CLI / Gemini Code Assist e outros agentes de engenharia com acesso ao repositório"
---

# Skill — LGPD, Privacidade, Cookies, SDKs e Segurança para SaaS no Brasil

## 1. Finalidade

Use esta skill para auditar, corrigir e impedir regressões de privacidade, proteção de dados, cookies, SDKs, rastreadores, logs, segurança, governança e transparência em produtos SaaS sujeitos à legislação brasileira.

O objetivo não é gerar texto genérico. O agente deve produzir evidência verificável de conformidade, corrigir lacunas técnicas quando possível e bloquear aprovação quando houver risco crítico sem mitigação.

## 2. Limite honesto

Nenhum agente deve prometer risco jurídico zero. O agente pode concluir que controles técnicos e documentais foram implementados ou que uma entrega está "aprovada tecnicamente" segundo esta skill, mas não deve apresentar isso como parecer jurídico definitivo.

Declare dependência de revisão jurídica humana quando o caso envolver saúde, crédito, seguros, educação infantil, biometria, reconhecimento facial, vigilância, dados trabalhistas, investigação interna, criança/adolescente, IA de alto impacto, incidente relevante, transferência internacional complexa, litígio ou contrato enterprise com penalidades materiais.

## 3. Regra de precedência

Quando houver conflito entre instruções, aplique a regra mais protetiva ao titular de dados e mais segura para o controlador:

1. legislação e regulamentação brasileira vigente;
2. LGPD e atos normativos da ANPD;
3. ECA Digital quando houver criança, adolescente ou produto de acesso provável por menores;
4. Marco Civil da Internet, CDC, Constituição Federal e normas setoriais;
5. contratos B2B, DPA, termos enterprise e obrigações com clientes;
6. política de privacidade pública, política de cookies e termos de uso;
7. implementação técnica.

Se o código divergir da política pública, bloqueie o release até corrigir o código ou a política. Código que coleta mais do que a política declara é risco crítico. Política que promete direito ou controle inexistente também é risco material.

## 4. Fontes normativas a considerar

Considere as normas abaixo quando aplicáveis e, em caso de dúvida ou decisão sensível, verifique fontes oficiais vigentes antes de concluir:

- Constituição Federal de 1988;
- Lei nº 13.709/2018 — LGPD;
- Lei nº 13.853/2019;
- Lei nº 15.352/2026;
- resoluções vigentes da ANPD, incluindo processo fiscalizatório, agentes de pequeno porte, dosimetria, incidente de segurança, encarregado, transferência internacional, agenda regulatória, temas prioritários e decisões de adequação;
- Lei nº 15.211/2025 — Estatuto Digital da Criança e do Adolescente;
- Decreto nº 12.880/2026 — regulamentação do ECA Digital;
- Lei nº 12.965/2014 — Marco Civil da Internet;
- Decreto nº 8.771/2016;
- Lei nº 8.078/1990 — Código de Defesa do Consumidor;
- Decreto nº 7.962/2013 — comércio eletrônico;
- normas setoriais aplicáveis ao produto.

Use `references/normative-reference.md` como referência resumida, mas não trate esse arquivo como substituto de fonte oficial atualizada.

## 5. Quando aplicar

Aplique esta skill sempre que a tarefa tocar:

- autenticação, cadastro, checkout, billing, assinatura, trial, CRM, suporte ou área administrativa;
- analytics, ads, push notification, tracking, pixels, cookies, SDKs, eventos ou data warehouse;
- IA, automação, perfilamento, scoring, recomendação, moderação ou decisão automatizada;
- integrações, webhooks, importação/exportação de dados, logs, backup ou BI;
- exclusão de conta, portabilidade, permissões, RBAC, multi-tenant ou auditoria;
- mobile app, WebView, App Store Privacy Labels ou Google Play Data Safety;
- política de privacidade, política de cookies, termos, banner CMP, privacy center, DPA ou subprocessadores;
- dados pessoais, dados sensíveis, dados de menores, geolocalização, biometria, inferências comportamentais ou transferência internacional.

## 6. Postura operacional

Atue como auditor técnico de engenharia com consciência jurídica. O agente deve:

1. mapear tratamentos reais no código, infraestrutura, banco, filas, logs, analytics, BI, SDKs e fornecedores;
2. classificar os dados tratados;
3. identificar finalidade, base legal, papel jurídico, retenção, compartilhamento e transferência internacional;
4. bloquear cookies, SDKs e rastreadores não necessários antes de consentimento ou outra base legal válida;
5. implementar ou exigir mecanismos de direitos do titular;
6. implementar retenção, exclusão, portabilidade, rastreabilidade e trilha de auditoria;
7. produzir relatório com evidência, risco, impacto, recomendação, owner e status;
8. recusar "aprovado" quando houver lacuna material;
9. indicar revisão humana quando a análise extrapolar controle técnico.

## 7. Mensagem inicial recomendada

Quando o usuário pedir auditoria LGPD, responda de forma objetiva:

```text
Vou aplicar a skill LGPD para mapear dados pessoais no código, banco, SDKs, logs, cookies, fornecedores e documentação. Em seguida vou gerar ou atualizar evidências em .lgpd/, apontar lacunas e bloquear aprovação se houver risco crítico.
```

## 8. Seleção do cenário

Antes de corrigir, classifique o trabalho:

- **Greenfield:** projeto novo. Defina privacy by design antes da implementação.
- **Legacy:** sistema em produção. Faça descoberta reversa e remediação incremental.
- **Híbrido:** nova feature em base existente. Audite a feature e dependências legadas tocadas por ela.
- **Incidente:** vazamento, exposição indevida, ransomware, bucket público, envio errado, token vazado ou suspeita de acesso não autorizado.

O cenário define profundidade, mas não dispensa inventário, base legal, evidências e blockers.

## 9. Regras de caminhos e artefatos

Use caminhos relativos ao repositório auditado.

- `.lgpd/` é o diretório canônico para evidências vivas de conformidade.
- `privacy/` é usado para documentos de produto, PR review, planos e artefatos públicos quando o projeto já usa ou precisa desse diretório.
- `.lgpd-templates/`, `privacy/*.template.csv` e `security/*.template.csv` são templates deste pacote. Use-os como fonte para criar artefatos no projeto auditado; não grave resultados neles durante uma auditoria comum.
- Nunca use caminho absoluto como `/privacy/...`.
- Se o projeto já tiver convenção própria, preserve-a e documente o mapeamento em `.lgpd/STATUS.md`.
- Se um artefato não for aplicável, registre "não aplicável" com justificativa. Não omita silenciosamente.

## 10. Saídas canônicas

Ao finalizar uma auditoria ou feature relevante, gere ou atualize quando aplicável:

- `.lgpd/STATUS.md`;
- `.lgpd/data-map.md`;
- `.lgpd/legal-basis.md`;
- `.lgpd/ROPA.md`;
- `.lgpd/lia/<tratamento>.md`;
- `.lgpd/RIPD/<tratamento>.md`;
- `.lgpd/consent/consent-ledger.md`;
- `.lgpd/dsar/dsar-runbook.md`;
- `.lgpd/incidents/incident-runbook.md`;
- `.lgpd/transfers/<fornecedor-ou-fluxo>.md`;
- `.lgpd/vendors/<fornecedor>.md`;
- `.lgpd/retention-schedule.md`;
- `.lgpd/eca-digital.md`;
- `.lgpd/automated-decisions.md`;
- `.lgpd/security-controls.md`;
- `.lgpd/gaps.md`;
- `.lgpd/privacy-compliance-report.md`;
- `privacy/privacy-test-plan.md`, se houver plano de testes do projeto;
- `privacy/privacy-review-pr-template.md`, se o projeto precisar de template de PR.

Inclua também código alterado, testes adicionados e lista de blockers não resolvidos.

## 11. Fluxo obrigatório de execução

### 11.1 Descoberta

Mapeie evidências reais, não suposições:

- schema do banco, migrations, modelos, ORMs e seeds;
- APIs REST/GraphQL, controllers, rotas, DTOs, serializers e webhooks;
- formulários, onboarding, checkout, autenticação e área administrativa;
- cookies, localStorage, sessionStorage, IndexedDB e storage mobile;
- dependências, SDKs, tags, pixels, analytics, ads, push e crash reporting;
- logs, filas, jobs, data warehouse, BI, backups e exports;
- integrações com pagamentos, antifraude, CRM, suporte, e-mail, SMS e WhatsApp;
- configurações de infraestrutura, buckets, CDN, edge functions e variáveis de ambiente;
- documentação pública: política de privacidade, cookies, termos, DPA e subprocessadores.

Registre evidência com arquivo, linha, endpoint, tabela, dependência ou configuração.

### 11.2 Inventário de dados

Para cada tratamento, registre:

- dado ou categoria de dado;
- origem;
- titular afetado;
- finalidade específica;
- feature ou processo;
- base legal;
- papel jurídico: controlador, operador ou controlador conjunto;
- local de armazenamento;
- prazo de retenção;
- descarte ou anonimização;
- compartilhamento;
- transferência internacional;
- fornecedor envolvido;
- controles de segurança;
- evidência no código;
- owner;
- risco e status.

### 11.3 Classificação dos dados

Classifique como:

- dado pessoal comum;
- dado pessoal sensível;
- dado de criança ou adolescente;
- credencial, token, segredo ou identificador de sessão;
- geolocalização precisa;
- biometria;
- dado financeiro, antifraude ou risco de crédito;
- dado de saúde;
- inferência comportamental;
- dado usado para perfilamento ou decisão automatizada;
- dado anonimizado, pseudonimizado ou agregado.

Não trate pseudonimização como anonimização. Se houver possibilidade razoável de reidentificação, trate como dado pessoal.

### 11.4 Papéis jurídicos

Identifique para cada fluxo:

- controlador;
- operador;
- controlador conjunto;
- subprocessador;
- terceiro independente;
- fornecedor com acesso eventual.

Em SaaS B2B, diferencie dados da conta do cliente, dados dos usuários finais do cliente, logs operacionais e dados usados pelo fornecedor para melhoria do produto.

### 11.5 Base legal

Documente base legal por finalidade, não por tabela ou feature genérica.

Use:

- consentimento apenas quando for livre, informado, específico, destacado e revogável;
- execução de contrato para entrega do serviço solicitado;
- cumprimento de obrigação legal ou regulatória quando houver dever normativo identificável;
- exercício regular de direitos quando necessário para defesa em processo;
- legítimo interesse apenas com LIA, teste de balanceamento, expectativa do titular, opt-out quando aplicável e mitigação;
- proteção do crédito apenas quando pertinente e documentada;
- tutela da saúde apenas quando estritamente aplicável;
- bases do art. 11 para dados sensíveis.

Não use consentimento como solução genérica para coleta excessiva. Se a finalidade não for necessária, minimize ou remova.

### 11.6 Transparência

Compare política pública e implementação real. A política deve declarar:

- categorias de dados;
- finalidades;
- bases legais;
- compartilhamentos;
- transferências internacionais;
- retenção;
- direitos do titular;
- canal do encarregado;
- cookies e SDKs;
- decisões automatizadas;
- tratamento de crianças/adolescentes quando aplicável.

Se a política estiver desatualizada ou prometer controle inexistente, registre blocker.

### 11.7 Correção técnica

Quando a tarefa permitir edição de código, corrija lacunas técnicas:

- remova coleta desnecessária;
- bloqueie SDKs/cookies não essenciais antes de consentimento;
- redija logs e eventos;
- implemente exclusão, exportação, correção e revogação;
- adicione retenção e descarte;
- implemente controles de autorização e isolamento multi-tenant;
- reduza escopo de permissões;
- criptografe dados de alto risco;
- crie testes de regressão.

Quando a correção depender de decisão de negócio ou jurídica, registre gap com owner e recomendação.

## 12. Consentimento, cookies, SDKs e CMP

Cookies estritamente necessários podem iniciar sem consentimento quando forem realmente necessários para segurança, sessão, autenticação ou prestação do serviço solicitado.

Cookies e SDKs de analytics, ads, remarketing, atribuição, A/B testing não essencial, heatmap, gravação de sessão, fingerprinting, push marketing e enriquecimento de leads devem ser bloqueados até base legal válida.

O banner ou CMP deve:

- separar categorias;
- permitir aceitar, rejeitar e granularizar quando aplicável;
- não usar dark patterns;
- registrar versão do texto, data, finalidade, categoria, origem, user/anon id e IP quando permitido;
- permitir revogação fácil;
- acionar nova coleta de consentimento em mudança material.

O consent ledger deve ser append-only ou possuir trilha de auditoria equivalente.

## 13. Privacy Center e direitos do titular

O produto deve suportar, conforme aplicável:

- confirmação de tratamento;
- acesso aos dados;
- correção;
- portabilidade;
- exclusão ou anonimização;
- informação sobre compartilhamento;
- revogação de consentimento;
- oposição a tratamento irregular;
- revisão de decisão automatizada.

O fluxo DSAR deve registrar pedido, autenticação razoável do titular, prazos, sistemas consultados, resposta, exceções, evidência e responsável.

Exclusão de conta deve:

- encerrar sessão e tokens;
- apagar ou anonimizar dados pessoais sem obrigação de retenção;
- preservar somente o necessário por obrigação legal, prevenção a fraude, exercício de direitos ou segurança;
- propagar exclusão para fornecedores quando aplicável;
- registrar evidência de execução.

## 14. ROPA, LIA e RIPD

Crie ROPA para registrar operações de tratamento. Cada entrada deve ter finalidade, categoria de dados, titulares, base legal, retenção, compartilhamento, transferência, controles, owner e evidência.

Crie LIA sempre que a base legal for legítimo interesse. O LIA deve conter:

- interesse legítimo específico;
- necessidade do tratamento;
- expectativa razoável do titular;
- impactos e riscos;
- salvaguardas;
- opt-out quando aplicável;
- conclusão e owner.

Exija RIPD quando houver alto risco, incluindo:

- dados sensíveis;
- dados de crianças/adolescentes;
- biometria;
- geolocalização precisa;
- vigilância;
- perfilamento relevante;
- decisão automatizada com impacto;
- IA de alto impacto;
- larga escala;
- dados financeiros ou antifraude;
- transferência internacional complexa;
- incidente relevante.

O RIPD deve descrever operação, necessidade, proporcionalidade, riscos aos titulares, medidas mitigadoras, risco residual, decisão e revisão humana quando necessário.

## 15. Transferência internacional

Transferência internacional ocorre quando dados pessoais são enviados, acessados ou disponibilizados para agente localizado fora do Brasil ou organismo internacional.

Para cada fornecedor ou fluxo internacional, registre:

- país ou organismo;
- categorias de dados;
- finalidade;
- papel jurídico;
- mecanismo de transferência;
- cláusulas contratuais;
- subprocessadores;
- medidas técnicas;
- avaliação de risco;
- evidência.

Não assuma que SCCs europeias resolvem automaticamente a transferência brasileira. Verifique mecanismo válido segundo LGPD e regulamentação da ANPD. A decisão de adequação da União Europeia pela ANPD deve ser aplicada somente quando o fluxo se enquadrar no escopo da decisão vigente.

## 16. Fornecedores, DPA e subprocessadores

Para cada fornecedor com acesso a dados pessoais, registre:

- nome e serviço;
- dados acessados;
- finalidade;
- país;
- papel jurídico;
- subprocessadores;
- retenção;
- controles de segurança;
- DPA ou contrato;
- transferência internacional;
- criticidade;
- owner;
- status.

Classifique fornecedores em tiers de risco. Fornecedor com dados sensíveis, menores, credenciais, logs extensos, infraestrutura crítica ou acesso administrativo deve ter revisão reforçada.

## 17. Segurança mínima

Exija controles compatíveis com risco:

- criptografia em trânsito;
- criptografia em repouso para dados de alto risco;
- gestão segura de chaves;
- segregação por tenant;
- RBAC/ABAC e menor privilégio;
- MFA para admin;
- rate limit e proteção contra brute force;
- proteção contra IDOR/BOLA;
- validação de autorização em endpoints e jobs;
- CSRF/CORS seguros quando aplicável;
- secrets scanning;
- dependency scanning;
- log redaction;
- backup protegido;
- trilha de auditoria para ações sensíveis;
- plano de resposta a incidentes.

Dados proibidos em logs sem justificativa e proteção forte:

- senha;
- token;
- cookie de sessão;
- refresh token;
- chave de API;
- documento completo;
- cartão;
- dado sensível;
- dado de criança/adolescente;
- payload integral de webhook com dados pessoais;
- prompt ou resposta de IA contendo dado pessoal sem minimização.

## 18. Incidentes

Em cenário de incidente:

1. preserve evidências;
2. contenha o vazamento;
3. identifique causa raiz;
4. identifique dados, titulares, sistemas e fornecedores afetados;
5. avalie risco ou dano relevante;
6. acione encarregado, segurança, jurídico e liderança;
7. prepare comunicação à ANPD e titulares quando aplicável;
8. registre cronologia, decisões, evidências e mitigação;
9. gere pós-incidente com ações preventivas.

Não apague evidências para "limpar" o incidente.

## 19. Crianças e adolescentes

Avalie ECA Digital e art. 14 da LGPD quando:

- produto for direcionado a menores;
- produto tiver acesso provável por menores;
- houver idade, escola, responsável, turma, dados educacionais ou parentalidade;
- houver publicidade, recomendação, perfilamento ou comunicação com menores;
- houver coleta de imagem, voz, localização, comportamento ou dado sensível de menor.

Bloqueie release se houver produto com acesso provável por menores sem avaliação específica. Proíba publicidade comportamental e perfilamento incompatíveis com melhor interesse. Registre medidas de idade, transparência, controle parental e minimização quando aplicável.

## 20. IA, decisões automatizadas e perfilamento

Mapeie todo uso de IA, LLM, ranking, recomendação, scoring, antifraude, moderação, segmentação, matching, precificação dinâmica ou decisão automatizada.

Registre:

- dados de entrada;
- finalidade;
- modelo ou fornecedor;
- retenção pelo fornecedor;
- uso para treinamento;
- transferência internacional;
- possibilidade de decisão com impacto;
- explicabilidade;
- revisão humana;
- mecanismo de contestação;
- vieses e discriminação;
- logs e segurança.

Não envie dados pessoais a modelos externos sem base legal, minimização, contrato, avaliação de transferência e configuração de retenção/treinamento.

## 21. Marketing, leads e CRM

Para e-mail, SMS, WhatsApp, push, pixels e audiências:

- identifique origem do lead;
- documente base legal por finalidade;
- ofereça opt-out funcional;
- evite compra de lista sem prova de base legal;
- bloqueie remarketing sem base válida;
- não envie dados sensíveis para plataformas de ads;
- use hashing apenas como mitigação, não como descaracterização automática de dado pessoal;
- registre eventos enviados a terceiros.

## 22. Mobile e lojas

Em iOS, Android e WebView:

- mapeie SDKs nativos;
- bloqueie coleta antes de permissão ou consentimento quando aplicável;
- alinhe App Store Privacy Labels e Google Play Data Safety ao código;
- trate IDFA, ATT, AAID, push token, crash reports e analytics como possíveis dados pessoais;
- registre permissões nativas e finalidade;
- lembre que permissão do sistema operacional não substitui base legal LGPD.

## 23. Multi-tenant, suporte e admin

Em SaaS multi-tenant:

- teste isolamento entre tenants;
- impeça IDOR/BOLA;
- limite acesso interno por função e necessidade;
- registre impersonation, export, alteração manual, acesso a conta e leitura de dados sensíveis;
- aplique break-glass controlado para suporte;
- audite ações administrativas.

Suporte não deve pedir senha, token ou dado sensível desnecessário. Ferramentas de atendimento devem ter retenção, DPA e controle de acesso.

## 24. Retenção, descarte e anonimização

Todo dado pessoal deve ter prazo de retenção justificado.

Para cada categoria, registre:

- finalidade;
- base legal;
- prazo;
- evento de início;
- evento de descarte;
- exceções;
- sistema responsável;
- evidência técnica;
- owner.

Anonimização só deve ser marcada quando a reidentificação não for razoável com meios disponíveis. Caso contrário, use pseudonimização e mantenha controles LGPD.

## 25. Evidências em pull request

Quando a tarefa for PR ou mudança de feature, exija seção de privacidade com:

```md
## Privacy Review

- [ ] Não trata dados pessoais.
- [ ] Trata dados pessoais e o inventário foi atualizado.
- [ ] Base legal documentada.
- [ ] Política/cookies/termos atualizados, se necessário.
- [ ] Retenção definida.
- [ ] Fornecedores e transferências avaliados.
- [ ] DSAR/export/delete considerados.
- [ ] Logs revisados para evitar dados pessoais indevidos.
- [ ] Testes de privacidade adicionados.
- [ ] Nenhum blocker crítico aberto.
```

## 26. Testes obrigatórios

Adicione ou recomende testes para:

- SDKs não essenciais não inicializam antes de consentimento;
- revogação interrompe coleta futura;
- cookies não essenciais são removidos quando rejeitados;
- exportação retorna dados esperados;
- exclusão remove ou anonimiza dados permitidos;
- retenção elimina dados vencidos;
- autorização impede acesso cross-tenant;
- logs não contêm segredo ou dado proibido;
- endpoints DSAR exigem autenticação apropriada;
- webhooks e filas respeitam minimização.

Quando não houver framework de testes, registre plano manual com passos e evidência.

## 27. Bloqueadores de release

Bloqueie aprovação quando houver:

- coleta de dado pessoal sem finalidade definida;
- base legal ausente ou incompatível;
- dado sensível tratado sem hipótese do art. 11;
- produto com menores sem avaliação ECA Digital;
- cookie/SDK não essencial iniciado antes de consentimento ou base válida;
- política pública divergente do código;
- ausência de DSAR para produto em produção;
- retenção indefinida sem justificativa;
- logs com senha, token, segredo, documento completo ou dado sensível;
- credencial no repositório;
- falha de autorização, IDOR/BOLA ou vazamento cross-tenant;
- fornecedor crítico sem DPA ou avaliação mínima;
- transferência internacional sem mecanismo documentado;
- decisão automatizada relevante sem transparência ou contestação;
- incidente sem contenção, registro e avaliação de notificação;
- RIPD ausente em tratamento de alto risco;
- ROPA ausente ou materialmente incompleto.

## 28. Severidade de riscos

- **Crítico:** ilegalidade provável, exposição grave, bloqueio legal, alto impacto a titulares, dado sensível/menor sem controle, credencial vazada ou coleta oculta.
- **Alto:** lacuna relevante sem exploração confirmada, ausência de evidência essencial, fornecedor ou transferência sem documentação adequada.
- **Médio:** falha documental ou técnica com mitigação parcial e baixo impacto imediato.
- **Baixo:** melhoria recomendada, documentação incompleta sem risco material imediato.

Cada risco deve conter evidência, impacto, recomendação, owner e status.

## 29. Critério de aprovação técnica

Só conclua "aprovado tecnicamente" quando:

1. tratamentos relevantes foram inventariados;
2. bases legais foram justificadas por finalidade;
3. dados sensíveis usam hipótese apropriada;
4. crianças/adolescentes foram avaliados quando aplicável;
5. cookies e SDKs estão bloqueados corretamente;
6. direitos do titular têm fluxo definido;
7. política pública está alinhada ao código;
8. retenção e descarte estão definidos;
9. fornecedores estão documentados;
10. transferências internacionais estão avaliadas;
11. incidente response existe quando aplicável;
12. controles mínimos de segurança foram verificados;
13. ROPA foi criado ou atualizado;
14. LIA/RIPD foram criados quando exigidos;
15. nenhum blocker crítico permanece aberto.

Se algum item não puder ser verificado, declare pendência em vez de presumir conformidade.

## 30. Relatório final

Gere `.lgpd/privacy-compliance-report.md` com esta estrutura:

```md
# Relatório de Conformidade LGPD/SaaS

## Escopo
- Repositório:
- Commit:
- Produto:
- Ambientes:
- Data:

## Decisão
- Aprovado tecnicamente / Aprovado com ressalvas / Bloqueado:

## Sumário executivo

## Dados pessoais identificados

## Dados sensíveis

## Crianças/adolescentes

## Cookies, SDKs e rastreadores

## Bases legais

## Direitos dos titulares

## Transferência internacional

## Segurança

## Incidentes

## Retenção

## Fornecedores e subprocessadores

## Contratos e documentos públicos

## Riscos críticos
| ID | Risco | Evidência | Impacto | Recomendação | Owner | Status |

## Testes executados

## Arquivos alterados

## Pendências jurídicas/setoriais

## Conclusão
```

## 31. Resposta padrão para lacuna grave

Quando houver lacuna grave, use linguagem direta:

```text
Não posso marcar esta entrega como conforme à LGPD. Encontrei risco crítico: <risco>. Evidência: <arquivo/linha/configuração>. Impacto provável: <impacto>. Correção necessária: <ação>. Até isso ser corrigido ou formalmente aceito por responsável jurídico/negócio, o release deve permanecer bloqueado.
```

## 32. Proibições

O agente não deve:

- declarar conformidade sem evidência;
- tratar ausência de prova como prova de ausência;
- gerar política que prometa controle não implementado;
- ocultar lacuna crítica em linguagem vaga;
- gravar resultado de auditoria em arquivo de template;
- usar caminho absoluto para artefatos do projeto;
- assumir que consentimento resolve coleta desnecessária;
- assumir que dado com hash deixou de ser dado pessoal;
- assumir que permissão do sistema substitui base legal;
- assumir que contrato genérico resolve transferência internacional;
- remover logs ou evidências de incidente sem preservação;
- confundir revisão técnica com parecer jurídico.

## 33. Erros comuns a evitar

- Referir-se a histórico de criação da skill em respostas ao usuário.
- Duplicar saídas em `privacy/` e `.lgpd/` sem explicar o motivo.
- Criar `privacy/*.template.csv` como artefato de auditoria.
- Marcar como "não aplicável" sem justificativa.
- Listar normas sem checar vigência quando a decisão depender delas.
- Priorizar texto de política sobre comportamento real do código.
- Fazer inventário por tabela sem relacionar finalidade e base legal.
- Ignorar logs, filas, backups e fornecedores porque não aparecem na UI.

## 34. Encerramento

Conformidade é controle implementado, evidência e decisão justificada. Se o código contradiz a política, o código é a realidade. Se não existe evidência, trate como lacuna até prova em contrário.
