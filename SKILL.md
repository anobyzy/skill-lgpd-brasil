---
name: lgpd-saas-brasil-compliance-skill
description: "Use when auditing or implementing LGPD/privacy compliance for Brazilian SaaS, web apps, mobile apps, APIs, cookies, SDKs, analytics, ads, billing, support, logs, AI, DSAR, ROPA, RIPD/LIA, international transfers, incidents, vendors, privacy policies, consent, retention, security controls, or release blockers."
license: "All rights reserved"
metadata:
  version: "2.0.1"
  language: "pt-BR"
  author: "Anobyz"
  author_email: "arh.sabrina@gmail.com"
  last_reviewed: "2026-06-03"
  risk_posture: "conservadora"
  intended_agents: "Codex, Claude Code, Gemini CLI / Gemini Code Assist e outros agentes de engenharia com acesso ao repositório"
---

# Skill — Conformidade LGPD, Privacidade, Cookies, SDKs e Segurança para SaaS no Brasil

> **Atualização v2.0.1 — pacote consolidado e preparado para publicação**  
> Esta versão edita a skill original enviada em `skill_lgpd.zip` e incorpora integralmente os pontos levantados em `DOC LGPD.md`, além dos elementos úteis dos projetos `Privacy-Data-Protection-Skills` e `lgpd-skills`: orquestração por subskills, living artifacts em `.lgpd/`, ROPA, RIPD, LIA, DSAR, consent ledger, incident response, encarregado, DPA, transferências internacionais, vendor audit, audit log imutável, criptografia, anonimização, retenção, ECA Digital, decisões automatizadas e bloqueios de release.


## 0. Finalidade da skill

Esta skill instrui agentes de código a auditar, corrigir e impedir regressões de privacidade, proteção de dados, cookies, SDKs, rastreadores, logs, segurança, governança e transparência em produtos SaaS sujeitos à legislação brasileira, especialmente LGPD, normas da ANPD, Marco Civil da Internet, ECA Digital e regras consumeristas aplicáveis.

A skill deve ser usada sempre que o agente:

- implementar autenticação, cadastro, checkout, billing, assinatura, trial, CRM, suporte, analytics, ads, push notification, tracking, cookies, SDKs, eventos, logs, data warehouse, IA, automação, integrações, webhooks, importação/exportação de dados, exclusão de conta, permissões, área administrativa, RBAC, multi-tenant, mobile app, WebView, landing pages ou pixel de marketing;
- revisar política de privacidade, política de cookies, termos de uso, banner CMP, tela de consentimento, privacy center, App Store Privacy Labels, Google Play Data Safety, DPA, subprocessadores ou contratos com fornecedores;
- encontrar dados pessoais, dados pessoais sensíveis, dados de crianças/adolescentes, geolocalização, biometria, inferências comportamentais, perfilamento, decisões automatizadas ou transferência internacional;
- receber solicitação de “adequar LGPD”, “cookies”, “privacidade”, “compliance”, “proteção de dados”, “DPO”, “ANPD”, “privacy by design” ou “evitar processo”.

## 1. Mandato operacional do agente

O agente deve atuar como auditor técnico-jurídico de engenharia. O objetivo não é “gerar texto bonito”, mas produzir evidências verificáveis de conformidade.

O agente deve:

1. mapear tratamentos reais no código, infraestrutura, SDKs, banco de dados, filas, logs, analytics, BI e fornecedores;
2. classificar os dados tratados;
3. identificar finalidade, base legal, papel do agente de tratamento, retenção, compartilhamento e transferência internacional;
4. bloquear inicialização de cookies/SDKs/rastreadores não necessários antes de base legal válida;
5. implementar ou exigir mecanismos de direitos do titular;
6. implementar retenção, exclusão, portabilidade e rastreabilidade;
7. criar trilha de auditoria probatória;
8. produzir relatório de riscos com severidade, evidência, impacto, recomendação e status;
9. recusar marcar conformidade como “aprovada” quando houver lacuna material;
10. sinalizar quando o caso requer revisão jurídica humana.

## 2. Limite honesto

Nenhum agente deve prometer risco jurídico zero. Conformidade reduz risco, mas não elimina:

- ações individuais;
- ações coletivas;
- reclamações em Procon/SENACON;
- denúncias à ANPD;
- atuação do Ministério Público;
- autuações setoriais;
- questionamentos contratuais de clientes enterprise;
- disputas por falha de segurança;
- danos morais ou materiais em caso de incidente.

O agente deve usar a seguinte regra: **“aprovado tecnicamente” só significa que os controles verificáveis exigidos por esta skill foram implementados ou justificados; não significa parecer jurídico definitivo.**

## 3. Fontes normativas obrigatórias

O agente deve considerar, no mínimo, as seguintes normas e orientações quando aplicáveis ao SaaS brasileiro.

### 3.1 Núcleo de proteção de dados

1. Constituição Federal de 1988:
   - direito à intimidade, vida privada, honra e imagem;
   - proteção de dados pessoais como direito fundamental;
   - sigilo das comunicações e devido processo.
2. LGPD — Lei nº 13.709/2018:
   - arts. 1º a 4º: objeto, aplicação territorial e exceções;
   - art. 5º: conceitos;
   - art. 6º: princípios;
   - arts. 7º a 10: hipóteses legais para dados pessoais comuns, consentimento e legítimo interesse;
   - arts. 11 a 13: dados pessoais sensíveis;
   - art. 14: crianças e adolescentes;
   - arts. 15 e 16: término do tratamento e conservação;
   - arts. 17 a 22: direitos do titular;
   - arts. 23 a 30: poder público, quando aplicável;
   - arts. 31 e 32: responsabilização pública e RIPD público, quando aplicável;
   - arts. 33 a 36: transferência internacional;
   - art. 37: registro das operações de tratamento;
   - art. 38: RIPD;
   - arts. 39 e 40: operador e padrões de interoperabilidade/portabilidade;
   - art. 41: encarregado;
   - arts. 42 a 45: responsabilidade e ressarcimento de danos;
   - arts. 46 a 49: segurança e boas práticas;
   - art. 50: governança, boas práticas e privacy by design;
   - arts. 52 a 54: sanções administrativas;
   - arts. 55-A a 58-B: ANPD e CNPD.
3. Regulamentações da ANPD:
   - Resolução CD/ANPD nº 1/2021 — Processo de Fiscalização e Processo Administrativo Sancionador;
   - Resolução CD/ANPD nº 2/2022 — aplicação da LGPD para agentes de tratamento de pequeno porte, quando aplicável;
   - Resolução CD/ANPD nº 4/2023 — Dosimetria e Aplicação de Sanções Administrativas;
   - Resolução CD/ANPD nº 15/2024 — Comunicação de Incidente de Segurança;
   - Resolução CD/ANPD nº 18/2024 — atuação do encarregado pelo tratamento de dados pessoais;
   - Resolução CD/ANPD nº 19/2024 — Transferência Internacional de Dados e cláusulas-padrão contratuais;
   - Resolução CD/ANPD nº 32/2026 — reconhecimento da União Europeia como organismo internacional com grau adequado de proteção, para fins de transferência internacional, se aplicável;
   - futuras resoluções vigentes da ANPD publicadas após a data desta skill.
4. Orientações e guias da ANPD:
   - Guia Orientativo sobre Cookies e Proteção de Dados Pessoais;
   - Guia Orientativo sobre Segurança da Informação para Agentes de Tratamento de Pequeno Porte;
   - orientações da ANPD sobre RIPD;
   - guia/orientações sobre encarregado;
   - guia/orientações sobre legítimo interesse;
   - glossário e FAQs da ANPD;
   - notas técnicas e guias futuros sobre biometria, decisões automatizadas, IA, crianças/adolescentes, direitos dos titulares e RIPD.

### 3.2 Internet, logs, aplicações e provedores

1. Marco Civil da Internet — Lei nº 12.965/2014:
   - direitos dos usuários;
   - proteção da privacidade;
   - proteção de registros, dados pessoais e comunicações privadas;
   - guarda de registros de conexão e registros de acesso a aplicações;
   - deveres dos provedores de aplicação;
   - remoção de conteúdo em hipóteses legais;
   - requisição judicial de registros.
2. Decreto nº 8.771/2016:
   - regulamentação do Marco Civil;
   - padrões de segurança, sigilo e governança para registros e dados;
   - diretrizes de transparência e guarda de registros.

### 3.3 Crianças e adolescentes

1. Estatuto da Criança e do Adolescente — Lei nº 8.069/1990, quando houver menores.
2. ECA Digital — Lei nº 15.211/2025:
   - produtos e serviços digitais direcionados ou de acesso provável por crianças/adolescentes;
   - segurança por padrão;
   - prevenção e mitigação de riscos;
   - supervisão parental;
   - aferição de idade quando aplicável;
   - publicidade comercial e proteção contra rastreamento/perfilamento abusivo;
   - jogos eletrônicos, conteúdo, denúncias e deveres de remoção, quando aplicável.
3. Decreto nº 12.880/2026:
   - regulamentação do ECA Digital;
   - política nacional de proteção de crianças e adolescentes no ambiente digital;
   - parâmetros iniciais para produtos/serviços impróprios, inadequados ou proibidos;
   - mecanismos de supervisão e segurança por padrão.
4. Enunciado CD/ANPD nº 1/2023:
   - tratamento de dados de crianças/adolescentes pode usar hipóteses legais dos arts. 7º ou 11 da LGPD, desde que observado e prevalecente o melhor interesse no caso concreto.

### 3.4 Relações de consumo e contratação online

Aplicável quando o SaaS for B2C, marketplace, assinatura individual, app pago, trial, checkout online, venda recorrente, curso, infoproduto, assinatura digital, app mobile monetizado ou serviço contratado por pessoa física.

1. Código de Defesa do Consumidor — Lei nº 8.078/1990:
   - informação adequada e clara;
   - publicidade enganosa ou abusiva;
   - práticas abusivas;
   - cláusulas abusivas;
   - responsabilidade por falha na prestação do serviço;
   - segurança do serviço;
   - direito de arrependimento quando aplicável;
   - proteção contratual.
2. Decreto nº 7.962/2013 — contratação no comércio eletrônico:
   - identificação clara do fornecedor;
   - características essenciais do serviço;
   - preço, cobrança, assinatura e restrições;
   - atendimento facilitado;
   - confirmação de compra/cancelamento;
   - exercício do arrependimento quando cabível.
3. Decreto nº 11.034/2022 — SAC, quando houver obrigação/estrutura aplicável:
   - gratuidade e acessibilidade do atendimento;
   - rastreamento da demanda;
   - tratamento de reclamações, cancelamentos e informação ao consumidor.

### 3.5 Assinaturas, pagamentos e antifraude

Aplicável quando o SaaS processa pagamentos, tokens, cartão, Pix, chargeback, antifraude, score ou inadimplência.

1. LGPD para dados financeiros, antifraude, identificação, logs e perfilamento.
2. CDC para cobrança, oferta, cancelamento e transparência.
3. Normas de arranjos de pagamento, Banco Central e Pix quando a empresa atuar como participante, iniciador, instituição regulada ou integrar soluções financeiras reguladas.
4. PCI DSS como padrão técnico contratual/setorial quando houver cartão, mesmo não sendo lei brasileira geral.
5. Contratos de adquirentes, subadquirentes, gateways, PSPs e antifraude.

### 3.6 Setores regulados e gatilhos especiais

O agente deve parar e exigir validação setorial quando houver:

- saúde, prontuário, telemedicina, exames, dados médicos, wearable, fitness clínico;
- educação de menores;
- financeiro, crédito, seguros, investimentos, open finance, Pix regulado;
- telecomunicações;
- jurídico/advocacia;
- contabilidade/fiscal;
- recursos humanos, folha, benefícios, ponto eletrônico;
- biometria, reconhecimento facial, voz, íris, impressão digital;
- IA generativa com dados pessoais;
- monitoramento de trabalhadores;
- geolocalização contínua;
- dados públicos raspados em larga escala;
- enriquecimento de leads;
- scoring, predição, inferências sensíveis;
- publicidade política ou eleitoral;
- segurança pública, investigação ou defesa nacional.

Nestes casos, o agente deve aplicar esta skill e adicionar um item “pendente de revisão jurídica/regulatória setorial”.

## 4. Definições operacionais

### 4.1 Dado pessoal

Qualquer informação relacionada a pessoa natural identificada ou identificável. Exemplos:

- nome;
- e-mail;
- telefone;
- CPF;
- endereço;
- IP;
- identificador de dispositivo;
- advertising ID;
- cookies;
- session ID persistente;
- user ID;
- customer ID;
- eventos de uso;
- logs vinculáveis ao usuário;
- imagem;
- voz;
- geolocalização;
- histórico de compra;
- hábitos de consumo;
- perfil comportamental identificável.

Dados de pessoa jurídica não são dados pessoais, mas dados de representantes, funcionários e usuários vinculados a uma empresa são dados pessoais.

### 4.2 Dado pessoal sensível

Dado sobre origem racial ou étnica, convicção religiosa, opinião política, filiação sindical, organização religiosa/filosófica/política, saúde, vida sexual, dado genético ou biométrico vinculado a pessoa natural.

Trate também como alto risco dados inferidos que possam revelar características sensíveis, mesmo que não coletados diretamente.

### 4.3 Tratamento

Qualquer operação com dado pessoal: coleta, produção, recepção, classificação, uso, acesso, reprodução, transmissão, distribuição, processamento, arquivamento, armazenamento, eliminação, avaliação, controle, modificação, comunicação, transferência, difusão ou extração.

### 4.4 Controlador, operador e controlador conjunto

- Controlador: decide finalidade e meios essenciais do tratamento.
- Operador: trata dados em nome do controlador e conforme instruções.
- Controladores conjuntos: decidem conjuntamente finalidades/meios.
- Controlador independente: fornecedor usa dados para finalidade própria, fora de instruções do cliente.

Em SaaS B2B multi-tenant, a empresa SaaS pode ser operador para dados que clientes inserem na plataforma e controlador para dados de conta, cobrança, segurança, analytics próprio, suporte, marketing, vendas, telemetria e antifraude.

## 5. Princípios obrigatórios da LGPD convertidos em regra de engenharia

### 5.1 Finalidade

Todo dado precisa ter finalidade específica, explícita e documentada.

Proibido:

- coletar “para melhorar serviços” sem detalhar eventos e usos;
- usar dado coletado para suporte em marketing sem nova base legal compatível;
- reaproveitar logs para IA, analytics ou ads sem avaliação de compatibilidade.

### 5.2 Adequação

O tratamento deve ser compatível com a finalidade informada ao titular.

Regra: se o usuário médio não esperaria aquele uso, exigir nova avaliação, transparência reforçada e possivelmente novo consentimento.

### 5.3 Necessidade / minimização

Coletar apenas o mínimo necessário.

Proibido:

- CPF obrigatório sem finalidade real;
- nascimento completo quando só precisa de maioridade;
- localização precisa quando cidade/UF basta;
- logs com payload completo contendo dados pessoais sem necessidade;
- gravar tokens, senhas, documentos ou cartões em logs;
- manter dados de trial abandonado indefinidamente.

### 5.4 Livre acesso

O titular deve conseguir saber se há tratamento e acessar informações sobre seus dados.

### 5.5 Qualidade dos dados

Dados usados para conta, cobrança, segurança, score, acesso ou decisão devem poder ser corrigidos.

### 5.6 Transparência

Políticas, banners, telas de permissão, checkouts e privacy center devem explicar:

- quem é o controlador;
- quais dados são coletados;
- para quais finalidades;
- quais bases legais;
- com quem há compartilhamento;
- se há transferência internacional;
- direitos do titular;
- contato do encarregado/canal de privacidade;
- retenção;
- consequências da negativa de consentimento quando aplicável.

### 5.7 Segurança

Implementar medidas técnicas e administrativas proporcionais ao risco.

### 5.8 Prevenção

Evitar danos antes que ocorram: threat modeling, privacy review, testes, revisão de SDKs e bloqueio por design.

### 5.9 Não discriminação

Proibido tratamento com finalidade discriminatória ilícita ou abusiva.

Atenção especial a IA, scoring, antifraude, crédito, preços personalizados, segmentação de marketing, geolocalização e inferências.

### 5.10 Responsabilização e prestação de contas

A empresa deve provar conformidade. Sem evidência, considere não conforme.

Evidências mínimas:

- inventário de tratamento;
- matriz de bases legais;
- logs de consentimento;
- versões de políticas;
- contratos/DPA;
- lista de subprocessadores;
- teste de bloqueio prévio de SDKs;
- política de retenção;
- processo de atendimento ao titular;
- registro de incidentes;
- RIPD quando aplicável;
- registro de decisões de legítimo interesse;
- registros de revisão de segurança.

## 6. Fluxo obrigatório de execução pelo agente

### Etapa 1 — Descoberta

Antes de alterar código, o agente deve procurar:

- `package.json`, `pnpm-lock.yaml`, `yarn.lock`, `package-lock.json`;
- `requirements.txt`, `pyproject.toml`, `poetry.lock`, `Pipfile`;
- `Gemfile`, `composer.json`, `go.mod`, `Cargo.toml`;
- `Podfile`, `Package.swift`, `build.gradle`, `settings.gradle`;
- arquivos de infraestrutura: Dockerfile, compose, Terraform, Kubernetes, Helm;
- variáveis de ambiente;
- inicializadores de SDK;
- pixels e tags;
- scripts injetados no HTML;
- arquivos de analytics;
- middlewares de log;
- modelos de banco;
- schemas de eventos;
- endpoints de usuário;
- rotas de admin;
- processos de backup;
- jobs/cron;
- integrações externas;
- política de privacidade, cookies, termos, DPA, subprocessadores;
- documentação de App Store/Google Play, se mobile.

### Etapa 2 — Inventário de dados e tratamento

Criar ou atualizar `privacy/data-inventory.csv` com os campos:

```csv
id,produto,modulo,ambiente,dado,categoria_dado,sensivel,crianca_adolescente,origem,titular,finalidade,base_legal,necessario,coleta_obrigatoria,compartilhado_com,operador_ou_controlador,transferencia_internacional,pais_destino,mecanismo_transferencia,retencao,criterio_eliminacao,local_armazenamento,criptografia,acesso_interno,risco,ripd_necessario,evidencia_codigo,evidencia_documental,status,observacoes
```

### Etapa 3 — Inventário de cookies, SDKs e rastreadores

Criar ou atualizar `privacy/tracker-inventory.csv`:

```csv
id,nome,tipo,fornecedor,categoria,dominio_ou_sdk,dados_coletados,finalidade,base_legal,consentimento_necessario,carrega_antes_consentimento,retencao,expiracao,terceiro,compartilhamento,transferencia_internacional,pais,mecanismo,link_politica_fornecedor,local_no_codigo,como_bloquear,como_revogar,status
```

Categorias mínimas:

- estritamente necessário;
- segurança/fraude;
- preferências/funcionalidade;
- analytics/desempenho;
- marketing/publicidade;
- personalização/perfilamento;
- suporte/chat;
- A/B testing;
- mapas/geolocalização;
- mídia embedada;
- social login/social sharing.

### Etapa 4 — Classificação de papel jurídico

Criar `privacy/roles-map.md` com:

- empresa SaaS como controlador;
- empresa SaaS como operador;
- cliente como controlador;
- fornecedor como operador;
- fornecedor como controlador independente;
- fornecedor como suboperador;
- controladoria conjunta, se houver.

Não presumir que todo fornecedor é operador. SDKs de ads, social login, antifraude, analytics e app stores frequentemente têm finalidades próprias.

### Etapa 5 — Base legal

Criar `privacy/legal-basis-matrix.csv`:

```csv
tratamento,finalidade,dados,base_legal,justificativa,alternativa_menos_intrusiva,expectativa_do_titular,necessita_consentimento,exige_opt_out,exige_lia,exige_ripd,evidencia,status
```

Bases legais de dados pessoais comuns:

- consentimento;
- cumprimento de obrigação legal ou regulatória;
- execução de políticas públicas, quando aplicável;
- estudos por órgão de pesquisa, com anonimização quando possível;
- execução de contrato ou procedimentos preliminares relacionados a contrato;
- exercício regular de direitos;
- proteção da vida ou incolumidade física;
- tutela da saúde por profissionais/serviços de saúde/autoridade sanitária;
- legítimo interesse;
- proteção do crédito.

Bases legais de dados sensíveis:

- consentimento específico e destacado;
- obrigação legal ou regulatória;
- políticas públicas;
- estudos por órgão de pesquisa;
- exercício regular de direitos;
- proteção da vida ou incolumidade física;
- tutela da saúde;
- prevenção à fraude e segurança do titular em processos de identificação/autenticação, resguardados direitos e liberdades fundamentais.

Regra: se a base legal for “legítimo interesse”, criar `privacy/legitimate-interest-assessment.md` ou entrada equivalente com:

- interesse legítimo específico;
- necessidade do tratamento;
- expectativa razoável do titular;
- impacto sobre direitos e liberdades;
- salvaguardas;
- opt-out quando possível;
- balanceamento;
- conclusão.

### Etapa 6 — Transparência e documentos públicos

Verificar/implementar:

- Política de Privacidade;
- Política de Cookies/Rastreadores;
- Termos de Uso;
- DPA/Contrato de operador para clientes B2B;
- lista de subprocessadores;
- página de encarregado/canal de privacidade;
- privacy center no produto;
- telas de consentimento e preferências;
- App Store Privacy Labels;
- Google Play Data Safety;
- termos de checkout e assinatura;
- cancelamento e exclusão de conta;
- data processing addendum para clientes enterprise.

### Etapa 7 — Implementação técnica

Implementar controles de privacidade diretamente no código, não só em política textual.

### Etapa 8 — Testes automatizados

Criar testes para garantir que:

- cookies/SDKs não essenciais não carreguem antes do consentimento;
- rejeitar todos bloqueie analytics, ads e perfilamento;
- aceitar analytics não habilite marketing;
- revogar consentimento interrompa novas coletas;
- nova versão de política solicite novo consentimento quando houver mudança material;
- exportação de dados funcione;
- exclusão/anomização funcione;
- logs não contenham senha, token, cartão, documento, payload sensível;
- permissões mobile não disparem coleta para finalidade não informada;
- multi-tenant não vaze dados entre tenants;
- endpoints de direitos do titular possuam autenticação adequada.

### Etapa 9 — Relatório final

Gerar `privacy/privacy-compliance-report.md` com:

- escopo analisado;
- data/hora;
- commit/hash;
- arquivos alterados;
- riscos críticos;
- lacunas pendentes;
- controles implementados;
- evidências;
- testes executados;
- itens que exigem revisão jurídica;
- decisão: aprovado, aprovado com ressalvas ou bloqueado.

## 7. Regras de bloqueio de release

O agente deve marcar como **BLOCKER** e não aprovar release quando houver qualquer item abaixo.

### 7.1 Dados e finalidade

- coleta de dado pessoal sem finalidade documentada;
- dado obrigatório sem necessidade;
- CPF, documento, nascimento, telefone, endereço ou localização exigidos sem justificativa;
- payload de usuário completo em logs;
- dados sensíveis sem base legal específica;
- dados de crianças/adolescentes sem avaliação de melhor interesse;
- uso secundário incompatível sem nova avaliação.

### 7.2 Consentimento, cookies e SDKs

- pixel/SDK de marketing carregando antes do consentimento;
- analytics comportamental carregando antes da base legal definida;
- botão “rejeitar” ausente, oculto ou mais difícil que aceitar;
- categorias pré-marcadas;
- consentimento por silêncio, scroll ou continuidade de navegação;
- revogação mais difícil que concessão;
- política de cookies sem lista real de terceiros;
- SDK desconhecido sem proprietário/finalidade/base legal;
- ATT iOS ignorado;
- AAID/Android opt-out ignorado;
- WebView com cookies não inventariados.

### 7.3 Direitos do titular

- inexistência de canal para direitos LGPD;
- inexistência de fluxo de acesso, correção, eliminação, portabilidade, informação de compartilhamento ou revogação;
- exclusão de conta apenas “desativa” sem explicar retenção legal;
- resposta ao titular sem trilha de auditoria;
- identidade do solicitante verificada de forma excessiva ou fraca.

### 7.4 Segurança

- senhas em texto claro;
- tokens/API keys no front-end quando deveriam ser secretos;
- dados pessoais sensíveis em logs;
- bucket público com dados pessoais;
- banco sem controle de acesso mínimo;
- falta de segregação por tenant;
- ausência de criptografia em trânsito;
- ausência de backup seguro para dados críticos;
- ausência de plano de incidente;
- credenciais em repositório;
- endpoints administrativos sem MFA ou RBAC proporcional;
- CORS permissivo em API sensível;
- exportação de dados sem autenticação forte.

### 7.5 Contratos e terceiros

- fornecedor/SDK recebe dados pessoais sem classificação jurídica;
- transferência internacional sem mecanismo documentado;
- ausência de DPA quando fornecedor atua como operador;
- suboperadores não listados;
- fornecedor usa dados para finalidade própria sem transparência;
- ausência de mecanismo de exclusão/retorno de dados ao encerrar contrato.

### 7.6 Crianças e adolescentes

- produto direcionado ou de acesso provável por menores sem avaliação ECA Digital;
- publicidade direcionada/perfilamento comportamental de crianças/adolescentes;
- coleta excessiva de dados de menores;
- ausência de segurança por padrão;
- ausência de supervisão parental quando exigida;
- ausência de aferição de idade quando necessária;
- conteúdo impróprio sem barreiras adequadas.

### 7.7 Incidentes

- inexistência de processo para detectar, classificar, registrar e comunicar incidente;
- ausência de responsável interno por incidentes;
- ausência de registro de incidentes por pelo menos 5 anos;
- fornecedor crítico sem obrigação contratual de notificar incidentes rapidamente.

## 8. Arquitetura técnica obrigatória de privacidade

### 8.1 Privacy Center

Todo SaaS deve ter uma área de privacidade acessível. Requisitos mínimos:

- ver dados de conta;
- editar dados básicos;
- exportar dados fornecidos e observados quando aplicável;
- solicitar exclusão ou anonimização;
- gerenciar consentimentos;
- gerenciar cookies/SDKs;
- revogar marketing;
- ver histórico de consentimentos relevantes;
- obter canal de privacidade/encarregado;
- consultar política de privacidade vigente;
- consultar lista de subprocessadores quando B2B;
- informar limitações por obrigações legais/contratuais.

### 8.2 Modelo de consentimento

Tabela ou coleção sugerida: `privacy_consents`.

Campos mínimos:

```json
{
  "id": "uuid",
  "user_id": "nullable uuid",
  "anonymous_subject_id": "nullable string",
  "tenant_id": "nullable uuid",
  "device_id_hash": "nullable string",
  "session_id_hash": "nullable string",
  "policy_version": "string",
  "cookie_policy_version": "string",
  "terms_version": "nullable string",
  "category": "necessary|security|preferences|analytics|marketing|personalization|support|ab_testing|geolocation",
  "status": "granted|denied|revoked|not_requested",
  "legal_basis": "consent|contract|legal_obligation|legitimate_interest|credit_protection|regular_exercise_rights|vital_interest|health_protection|research|public_policy",
  "source": "web_banner|mobile_cmp|privacy_center|api|import|admin",
  "ui_locale": "pt-BR",
  "ip_hash": "nullable string",
  "user_agent_hash": "nullable string",
  "country": "nullable string",
  "timestamp": "ISO-8601",
  "expires_at": "nullable ISO-8601",
  "evidence_ref": "string",
  "created_at": "ISO-8601"
}
```

Proibições:

- não armazenar e-mail no log de consentimento se um ID pseudonimizado basta;
- não sobrescrever consentimentos antigos sem trilha;
- não usar “aceitou tudo” como campo único;
- não tratar revogação como exclusão do histórico probatório.

### 8.3 Gating de SDKs

Nenhum SDK não necessário deve inicializar no bootstrap global antes da avaliação da CMP.

Padrão recomendado:

```ts
type ConsentCategory =
  | 'necessary'
  | 'security'
  | 'preferences'
  | 'analytics'
  | 'marketing'
  | 'personalization'
  | 'support'
  | 'ab_testing'
  | 'geolocation';

interface TrackerDefinition {
  id: string;
  vendor: string;
  category: ConsentCategory;
  init: () => Promise<void> | void;
  shutdown?: () => Promise<void> | void;
  purgeLocalState?: () => Promise<void> | void;
}

async function bootTrackers(consents: Record<ConsentCategory, boolean>) {
  for (const tracker of TRACKERS) {
    if (tracker.category === 'necessary') {
      await tracker.init();
      continue;
    }
    if (consents[tracker.category] === true) {
      await tracker.init();
    }
  }
}

async function revokeTracker(tracker: TrackerDefinition) {
  await tracker.shutdown?.();
  await tracker.purgeLocalState?.();
}
```

Regra para agentes: localizar qualquer chamada `init`, `start`, `load`, `track`, `identify`, `page`, `fbq`, `gtag`, `dataLayer.push`, `analytics.identify`, `mixpanel.init`, `amplitude.init`, `firebase.analytics`, `Appsflyer`, `Adjust`, `Branch`, `OneSignal`, `Intercom`, `Hotjar`, `FullStory`, `Sentry`, `PostHog`, `Meta Pixel`, `TikTok Pixel`, `Google Ads`, `GA4`, `GTM`, `Clarity` e condicionar à categoria correta.

Observação: ferramentas de crash/security podem usar outra base legal quando configuradas com minimização. O agente deve documentar a decisão e bloquear captura de payload pessoal desnecessário.

### 8.4 Cookies e armazenamento local

Inventariar e controlar:

- cookies HTTP;
- LocalStorage;
- SessionStorage;
- IndexedDB;
- Cache API;
- Service Workers;
- WebView cookies;
- SharedPreferences Android;
- NSUserDefaults iOS;
- SQLite/Realm;
- Secure Enclave/Keychain/Keystore;
- device identifiers;
- advertising IDs;
- installation IDs.

Para cada item:

- nome;
- finalidade;
- categoria;
- duração;
- domínio;
- primeiro/terceiro;
- acesso por terceiros;
- base legal;
- como excluir/revogar.

### 8.5 Logs

Logs são tratamento de dados pessoais quando vinculáveis a usuário, IP, sessão, tenant, dispositivo ou evento.

Regras:

- mascarar e-mail, telefone, CPF, documentos, cartão e tokens;
- não registrar request/response completo por padrão;
- separar logs de segurança, auditoria, aplicação e negócio;
- definir retenção por tipo de log;
- restringir acesso;
- criptografar ou proteger armazenamento;
- impedir logs de dados sensíveis salvo necessidade excepcional;
- registrar acesso administrativo a dados pessoais;
- evitar exportação de logs para fornecedores sem DPA e mecanismo internacional.

### 8.6 Multi-tenant SaaS

Obrigatório:

- `tenant_id` em todas as tabelas/coleções multi-tenant;
- isolamento em queries;
- testes anti-cross-tenant;
- RBAC por tenant;
- logs de acesso administrativo;
- trilha de exportação;
- proteção contra IDOR/BOLA;
- segregação de chaves quando risco alto;
- política de retenção por tenant;
- processo de devolução/exclusão ao encerrar contrato.

Teste obrigatório: usuário do tenant A não pode acessar, listar, exportar, inferir ou buscar dados do tenant B por API, URL, ID incremental, busca global, logs, webhooks, notificações ou anexos.

### 8.7 Webhooks, integrações e APIs

Para cada integração:

- documentar dados enviados;
- assinar webhooks;
- limitar escopo;
- permitir revogação;
- registrar envio;
- aplicar retry sem duplicar dados excessivos;
- mascarar payloads em logs;
- usar TLS;
- validar destinatário;
- não enviar dados sensíveis a URLs não verificadas;
- fornecer botão para apagar integração e tokens;
- rotacionar segredos.

### 8.8 IA, LLMs e automações

Quando dados pessoais forem usados em IA:

- inventariar prompts, respostas, embeddings, fine-tuning, logs e caches;
- separar ambiente de treinamento e inferência;
- não enviar dados pessoais a provedores externos sem base legal, contrato e transferência internacional;
- não usar dados de clientes B2B para treinar modelos globais sem autorização contratual e base legal adequada;
- permitir opt-out quando cabível;
- minimizar e pseudonimizar;
- avaliar risco de vazamento por prompt injection;
- impedir inclusão de segredos, tokens ou dados sensíveis em prompts;
- registrar modelo/provedor/localização;
- avaliar decisão automatizada e perfilamento;
- criar RIPD se alto risco.

### 8.9 Dados para treinamento, analytics e produto

Proibido transformar “dados de operação do cliente” em dataset de produto sem:

- previsão contratual;
- base legal;
- transparência;
- minimização;
- anonimização robusta quando possível;
- avaliação de reidentificação;
- opção de oposição/opt-out quando aplicável;
- revisão de segurança.

## 9. Direitos do titular

### 9.1 Direitos a suportar

Implementar fluxo para:

- confirmação da existência de tratamento;
- acesso aos dados;
- correção de dados incompletos, inexatos ou desatualizados;
- anonimização, bloqueio ou eliminação de dados desnecessários, excessivos ou tratados em desconformidade;
- portabilidade, quando regulamentada/aplicável e respeitados segredos comercial/industrial;
- eliminação dos dados tratados com consentimento, salvo hipóteses legais de conservação;
- informação das entidades públicas e privadas com as quais houve compartilhamento;
- informação sobre possibilidade de não consentir e consequências da negativa;
- revogação do consentimento;
- oposição a tratamento irregular ou baseado em dispensa de consentimento;
- revisão/contestação de decisões automatizadas quando aplicável.

### 9.2 Workflow de solicitação

Criar tabela/coleção `privacy_requests`:

```json
{
  "id": "uuid",
  "request_type": "access|confirmation|correction|deletion|anonymization|blocking|portability|sharing_info|consent_revocation|opposition|automated_decision_review",
  "subject_id": "uuid|string",
  "tenant_id": "nullable uuid",
  "requester_identity_status": "unverified|verified|rejected|needs_more_info",
  "channel": "privacy_center|email|support|api|admin",
  "status": "received|triage|in_progress|waiting_user|fulfilled|partially_fulfilled|rejected|closed",
  "legal_hold": "boolean",
  "deadline_at": "ISO-8601",
  "response_summary": "string",
  "evidence_refs": ["string"],
  "created_at": "ISO-8601",
  "updated_at": "ISO-8601"
}
```

Regras:

- verificar identidade de forma proporcional;
- não exigir documento desnecessário;
- responder em linguagem clara;
- manter evidência da resposta;
- se negar, explicar fundamento;
- se houver retenção legal/contratual, explicar o que fica, por quê e por quanto tempo;
- se envolver cliente B2B controlador, rotear conforme contrato/DPA.

### 9.3 Exclusão de conta

Exclusão deve distinguir:

- exclusão imediata de dados não necessários;
- anonimização quando possível;
- retenção por obrigação legal/regulatória;
- retenção para exercício regular de direitos;
- retenção antifraude/segurança quando justificada;
- backups com expurgo por ciclo;
- logs com retenção definida;
- dados de faturamento/notas fiscais;
- dados que pertencem ao cliente controlador em ambiente B2B.

Não chamar de “excluído” se apenas desativou a conta. Use “desativado” ou “programado para exclusão/anonimização” quando for o caso.

## 10. Encarregado e governança

### 10.1 Encarregado/canal de privacidade

A empresa deve manter canal público para titulares e ANPD.

O agente deve verificar se existem:

- contato do encarregado ou canal de privacidade;
- página pública ou seção na política;
- procedimento interno de triagem;
- evidência de indicação formal;
- SLA interno;
- responsável substituto;
- registro de solicitações;
- integração com incidentes e RIPD.

Para agente de tratamento de pequeno porte, verificar regras especiais aplicáveis, mas não presumir dispensa ampla. Mesmo quando houver flexibilização, manter canal de atendimento e boas práticas.

### 10.2 Programa de governança

Criar ou exigir:

- política interna de privacidade;
- política de segurança;
- política de retenção;
- política de classificação de dados;
- processo de privacy review em pull requests;
- DPIA/RIPD para alto risco;
- treinamento mínimo;
- gestão de fornecedores;
- resposta a incidentes;
- revisão periódica;
- auditoria de acessos;
- gestão de vulnerabilidades;
- privacy by design em roadmap.

## 11. RIPD — Relatório de Impacto à Proteção de Dados

### 11.1 Quando exigir RIPD

Criar RIPD quando houver alto risco ou quando a ANPD puder exigir. Gatilhos:

- larga escala;
- dados sensíveis;
- crianças/adolescentes/idosos;
- tecnologias emergentes;
- IA/LLM com dados pessoais;
- biometria;
- geolocalização contínua ou precisa;
- vigilância/monitoramento;
- decisões automatizadas relevantes;
- scoring;
- antifraude intrusivo;
- publicidade comportamental;
- enriquecimento de perfis;
- scraping de dados pessoais;
- integração de múltiplas bases;
- dados financeiros relevantes;
- risco de discriminação;
- compartilhamento com muitos terceiros;
- transferência internacional de alto risco;
- tratamento baseado em legítimo interesse com impacto relevante.

### 11.2 Conteúdo mínimo do RIPD

Criar `privacy/ripd.md` com:

- descrição do tratamento;
- controlador;
- operador/suboperadores;
- tipos de dados;
- titulares afetados;
- finalidades;
- hipóteses legais;
- fluxo de dados;
- sistemas envolvidos;
- países envolvidos;
- necessidade e proporcionalidade;
- riscos a direitos e liberdades;
- probabilidade e impacto;
- medidas de mitigação;
- salvaguardas;
- plano de ação;
- decisão final;
- opiniões divergentes relevantes;
- revisão do encarregado;
- data e versão.

## 12. Transferência internacional

### 12.1 Identificação

Transferência internacional ocorre quando dados pessoais são enviados, acessados ou disponibilizados para agente localizado fora do Brasil ou organismo internacional, conforme LGPD e regulamento da ANPD.

Mapear:

- cloud provider;
- CDN;
- observabilidade;
- crash reporting;
- email;
- CRM;
- analytics;
- ads;
- suporte/chat;
- IA/LLM;
- data warehouse;
- antifraude;
- pagamento;
- subprocessadores;
- backups;
- equipe remota com acesso fora do Brasil.

### 12.2 Mecanismos aceitos

Documentar pelo menos um mecanismo válido:

- decisão de adequação da ANPD;
- cláusulas-padrão contratuais da ANPD;
- cláusulas-padrão equivalentes reconhecidas pela ANPD;
- cláusulas contratuais específicas aprovadas pela ANPD;
- normas corporativas globais aprovadas pela ANPD;
- hipóteses específicas da LGPD para transferência internacional, quando aplicáveis.

Não assumir que SCCs europeias resolvem automaticamente a transferência brasileira, salvo reconhecimento/equivalência pela ANPD ou base jurídica válida documentada.

### 12.3 Checklist por fornecedor internacional

Para cada fornecedor:

- nome legal;
- país;
- dados transferidos;
- finalidade;
- papel jurídico;
- suboperadores;
- regiões de armazenamento;
- acesso por suporte;
- mecanismo de transferência;
- DPA assinado;
- cláusulas da ANPD incorporadas quando aplicável;
- política de retenção;
- medidas de segurança;
- direito de auditoria ou relatório SOC/ISO;
- processo de exclusão;
- incident notification SLA;
- link público de subprocessadores.

## 13. Segurança da informação

### 13.1 Controles mínimos

Obrigatório:

- TLS em trânsito;
- hash forte de senha com Argon2id, bcrypt ou equivalente adequado;
- MFA para admins e contas privilegiadas;
- RBAC/ABAC;
- princípio do menor privilégio;
- segregação por tenant;
- proteção contra IDOR/BOLA;
- rate limiting;
- logs de auditoria;
- criptografia em repouso para dados sensíveis ou alto risco;
- gerenciamento seguro de segredos;
- rotação de chaves;
- backup criptografado;
- teste de restauração;
- WAF ou controles equivalentes quando exposto;
- SAST/DAST/dependency scanning;
- atualização de dependências;
- política de vulnerabilidades;
- revisão de permissões;
- proteção contra CSRF/XSS/SQLi/SSRF/RCE;
- revisão de CORS;
- proteção de webhooks;
- ambiente de staging sem dados reais ou com anonimização;
- data masking em suporte/admin;
- controle de exportações;
- monitoramento de anomalias;
- plano de resposta a incidentes.

### 13.2 Dados proibidos em logs

Nunca registrar:

- senha;
- token de sessão;
- refresh token;
- API key;
- chave Pix completa se não necessária;
- dados completos de cartão;
- CVV;
- documento completo sem necessidade;
- dado sensível;
- payload completo de mensagens privadas;
- secrets de webhook;
- headers `Authorization`;
- cookies de autenticação;
- códigos 2FA;
- links mágicos de login.

### 13.3 Incidentes

Criar `security/incident-response-privacy.md` com:

- definição de incidente;
- critérios de risco/dano relevante;
- triagem;
- contenção;
- preservação de evidências;
- comunicação interna;
- comunicação à ANPD quando aplicável;
- comunicação aos titulares quando aplicável;
- comunicação a clientes controladores B2B;
- comunicação a fornecedores;
- comunicação a seguradora/cyber insurance, se houver;
- registro por no mínimo 5 anos;
- revisão pós-incidente;
- plano de remediação.

Campos mínimos do registro:

```csv
incident_id,detected_at,reported_by,systems_affected,data_categories,subjects_estimated,sensitive_data,minors_data,financial_data,auth_data,large_scale,root_cause,risk_assessment,contained_at,notified_anpd,notified_subjects,notified_customers,decision_reason,evidence,closed_at,lessons_learned
```

## 14. Cookies, SDKs e CMP

### 14.1 Categorias recomendadas

1. Necessários:
   - login;
   - sessão;
   - segurança;
   - antifraude essencial;
   - load balancing;
   - consent state;
   - carrinho/checkout essencial.

2. Preferências:
   - idioma;
   - tema;
   - layout;
   - preferências salvas.

3. Analytics/desempenho:
   - uso do produto;
   - páginas visitadas;
   - eventos;
   - crash logs;
   - performance.

4. Funcionalidade/suporte:
   - chat;
   - central de ajuda;
   - gravação de sessão;
   - feedback widget.

5. Marketing/publicidade:
   - pixels;
   - retargeting;
   - anúncios personalizados;
   - lookalike;
   - cross-app tracking.

6. Personalização/perfilamento:
   - recomendação individual;
   - ranking;
   - segmentação comportamental;
   - preço/oferta personalizada.

### 14.2 UX obrigatória

- aceitar e rejeitar devem estar acessíveis no primeiro nível para cookies não necessários;
- configurar preferências deve estar visível;
- categorias não essenciais devem começar desativadas;
- linguagem clara;
- sem dark patterns;
- sem botão de rejeição escondido;
- sem “continuar navegando = aceitar”;
- revogação tão fácil quanto concessão;
- link permanente no rodapé/configurações/perfil;
- preservar escolha sem incomodar excessivamente;
- solicitar novo consentimento quando houver mudança material.

### 14.3 Prova de consentimento

Registrar:

- versão da política;
- versão do banner/texto;
- categorias aceitas/negadas;
- data/hora/fuso;
- origem da ação;
- pseudônimo do titular/dispositivo;
- evidência da interface exibida;
- locale;
- revogações;
- expiração/revalidação.

## 15. Mobile apps

### 15.1 iOS

- usar App Tracking Transparency quando houver tracking conforme regras Apple;
- `NSUserTrackingUsageDescription` claro;
- ATT negado sobrepõe consentimento interno para tracking cross-app;
- não fingerprintar usuário para contornar ATT;
- mapear IDFA, IDFV, Keychain, push token, crash IDs;
- alinhar App Privacy Details da App Store com inventário real.

### 15.2 Android

- respeitar Advertising ID e opt-out/reset;
- mapear AAID, App Set ID, Firebase Installation ID, push token;
- usar permissões de runtime com finalidade clara;
- não usar permissões como substitutas da base legal;
- alinhar Google Play Data Safety com inventário real.

### 15.3 Permissões nativas

Permissão do sistema operacional não substitui LGPD.

Exemplo: usuário permitir localização não autoriza automaticamente marketing geolocalizado. O tratamento ainda precisa de finalidade, base legal, minimização, transparência e revogação.

## 16. Crianças e adolescentes

### 16.1 Classificação inicial

O agente deve responder:

- produto é direcionado a crianças/adolescentes?
- produto é de acesso provável por crianças/adolescentes?
- há conteúdo, linguagem, estética, marketing, canal, influenciadores, escola, jogos, vídeos, chat ou comunidade que atraia menores?
- há coleta de idade?
- há publicidade?
- há perfilamento?
- há recomendação algorítmica?
- há chat, comunidade, upload, comentários ou contato entre usuários?
- há compras, moedas virtuais, loot boxes, assinaturas ou gamificação?

### 16.2 Regras

- aplicar melhor interesse;
- minimizar coleta;
- evitar publicidade direcionada;
- não usar rastreamento para perfilamento comportamental de crianças/adolescentes;
- implementar segurança por padrão;
- avaliar aferição de idade proporcional ao risco;
- implementar supervisão parental quando exigível;
- linguagem acessível;
- bloquear conteúdo/serviço impróprio conforme aplicável;
- criar canal de denúncia/report;
- criar RIPD quando alto risco;
- documentar base legal e salvaguardas.

### 16.3 Bloqueios específicos

Bloquear release se:

- app provável para menores usa Meta Pixel/TikTok Pixel/ads behavioral sem controle;
- coleta nascimento completo sem necessidade;
- usa localização precisa de menor sem justificativa forte;
- tem chat aberto entre usuários menores sem mitigação;
- recomenda conteúdo sensível sem controle;
- permite compra recorrente por menor sem salvaguarda;
- não tem mecanismos de denúncia quando há UGC/comunidade.

## 17. Consumidor, SaaS B2C e checkout

Quando houver venda direta para pessoa física:

- informar nome empresarial, CNPJ/CPF quando aplicável, endereço físico/eletrônico e contato;
- explicar serviço, funcionalidades, limitações, preço, recorrência, reajuste, período de teste, cancelamento e reembolso;
- não usar trial com cobrança surpresa;
- informar renovação automática;
- permitir cancelamento facilitado;
- confirmar recebimento de cancelamento;
- manter histórico de contratação;
- evitar publicidade enganosa;
- explicar restrições de uso;
- não condicionar privacidade a consentimento desnecessário;
- política de privacidade e termos devem ser acessíveis antes da contratação;
- botões de compra devem indicar cobrança de forma inequívoca.

## 18. Contratos B2B, DPA e subprocessadores

### 18.1 DPA mínimo

Para SaaS B2B, criar DPA com:

- partes e papéis;
- objeto e duração;
- categorias de titulares;
- categorias de dados;
- finalidades;
- instruções documentadas do controlador;
- confidencialidade;
- segurança;
- suboperadores;
- transferência internacional;
- resposta a incidentes;
- assistência em direitos dos titulares;
- exclusão/devolução ao término;
- auditoria/evidências;
- registros;
- responsabilidade;
- canal de contato.

### 18.2 Lista de subprocessadores

Publicar ou disponibilizar lista com:

- nome;
- serviço;
- país;
- dados tratados;
- finalidade;
- mecanismo internacional;
- link de política/DPA;
- data de inclusão;
- mecanismo de notificação de mudanças.

## 19. Retenção e descarte

### 19.1 Política obrigatória

Criar `privacy/retention-schedule.csv`:

```csv
categoria_dado,sistema,finalidade,base_legal,retencao,criterio_inicio,criterio_fim,metodo_exclusao,anonimizacao,backup_expurgo,excecoes,owner,status
```

### 19.2 Diretrizes

- reter pelo menor prazo compatível;
- excluir ou anonimizar após fim da finalidade;
- documentar exceções legais/contratuais;
- definir ciclo de expurgo em backups;
- evitar retenção indefinida de leads;
- revisar logs de segurança e auditoria;
- preservar dados necessários para defesa em processos dentro de prazo jurídico aplicável;
- diferenciar conta ativa, conta cancelada, trial expirado, lead inativo, usuário excluído e cliente B2B encerrado.

## 20. Decisões automatizadas, IA, perfilamento e discriminação

### 20.1 Identificação

O agente deve marcar como perfilamento/decisão automatizada quando houver:

- segmentação comportamental;
- recomendação personalizada;
- rankeamento individual;
- score de fraude;
- score de crédito;
- bloqueio automático de conta;
- precificação personalizada;
- oferta personalizada;
- priorização de suporte;
- moderação automática;
- classificação de risco;
- predição de churn;
- enriquecimento de leads;
- inferência sensível.

### 20.2 Regras

- informar finalidade;
- mapear dados usados;
- avaliar viés/discriminação;
- permitir contestação quando houver efeito relevante;
- manter explicabilidade suficiente;
- criar logs de decisão;
- permitir revisão humana quando aplicável;
- criar RIPD quando alto risco;
- não usar dados sensíveis para discriminação ilícita;
- testar fairness quando aplicável.

## 21. Marketing, leads e comunicação

### 21.1 E-mail, WhatsApp, SMS, push

Regras:

- base legal documentada;
- opt-out fácil;
- não comprar listas sem comprovação de origem e base legal;
- não enviar marketing para contatos sem fundamento;
- separar comunicação transacional de marketing;
- registrar origem do lead;
- registrar consentimento quando usado;
- respeitar descadastro;
- não compartilhar lead com terceiros sem transparência e base legal.

### 21.2 Pixels e audiências

Bloquear:

- upload de lista de clientes para ads sem base legal e transparência;
- lookalike/remarketing sem avaliação;
- pixel em área logada com dados sensíveis;
- eventos de conversão contendo e-mail/telefone sem hashing e base legal;
- rastreamento de menores.

## 22. Suporte, atendimento e acesso interno

### 22.1 Suporte

- acesso a dados pessoais deve ser limitado ao necessário;
- implementar impersonation seguro com consentimento/justificativa/log;
- mascarar dados sensíveis;
- registrar acesso de atendentes/admins;
- impedir download em massa sem permissão;
- treinar equipe;
- limpar anexos de suporte conforme retenção.

### 22.2 Admin interno

Obrigatório:

- MFA;
- RBAC;
- logs imutáveis ou protegidos;
- justificativa para acesso sensível;
- alertas para exportação;
- segregação de funções;
- revisão periódica de permissões;
- remoção imediata de ex-funcionários;
- controle de acesso de fornecedores.

## 23. App Store, Google Play e lojas

O agente deve verificar consistência entre:

- código real;
- SDKs embarcados;
- política de privacidade;
- tela de consentimento;
- App Store Privacy Details;
- Google Play Data Safety;
- permissões solicitadas;
- ATT;
- descrição pública do app;
- termos de assinatura;
- retenção e exclusão.

Divergência entre formulário da loja e comportamento real é risco material.

## 24. Evidências obrigatórias por pull request

Para qualquer PR que toque dados pessoais, o agente deve anexar:

```md
## Privacy Review

- [ ] Este PR trata dados pessoais? Sim/Não
- [ ] Quais dados?
- [ ] Quais titulares?
- [ ] Finalidade:
- [ ] Base legal:
- [ ] Há dado sensível? Sim/Não
- [ ] Há criança/adolescente? Sim/Não
- [ ] Há transferência internacional? Sim/Não
- [ ] Há novo fornecedor/SDK? Sim/Não
- [ ] Há alteração de retenção? Sim/Não
- [ ] Há alteração em consentimento/cookies? Sim/Não
- [ ] Há impacto em direitos do titular? Sim/Não
- [ ] Precisa atualizar política/termos/DPA? Sim/Não
- [ ] Precisa RIPD/LIA? Sim/Não
- [ ] Testes de privacidade executados:
- [ ] Riscos e mitigação:
- [ ] Status: aprovado / aprovado com ressalvas / bloqueado
```

## 25. Testes técnicos obrigatórios

### 25.1 Cookies/SDKs

- novo visitante: nenhum cookie/SDK não necessário antes da escolha;
- rejeitar todos: nenhum analytics/ads/personalização;
- aceitar analytics: analytics carrega, ads não;
- aceitar marketing: ads carrega após consentimento;
- revogar: novas coletas cessam;
- limpar local state: IDs não necessários são removidos quando viável;
- alteração de política: nova escolha solicitada se mudança material.

### 25.2 Direitos

- exportação exige autenticação;
- exportação contém dados corretos;
- exclusão exclui/anonimiza dados esperados;
- retenção legal é explicada;
- pedido fica registrado;
- usuário de outro tenant não consegue solicitar/exportar dados alheios.

### 25.3 Segurança

- IDOR/BOLA;
- CORS;
- CSRF;
- rate limit;
- brute force;
- secrets scanning;
- dependency scanning;
- log redaction;
- backup access;
- admin RBAC;
- multi-tenant isolation.

## 26. Saídas obrigatórias do agente

Ao finalizar, o agente deve entregar:

1. `privacy/privacy-compliance-report.md`;
2. `privacy/data-inventory.csv`;
3. `privacy/tracker-inventory.csv`;
4. `privacy/legal-basis-matrix.csv`;
5. `privacy/retention-schedule.csv`;
6. `privacy/subprocessors.md`;
7. `privacy/risk-register.csv`;
8. `privacy/privacy-test-plan.md`;
9. `privacy/ripd.md`, se aplicável;
10. `privacy/legitimate-interest-assessment.md`, se aplicável;
11. código alterado;
12. testes adicionados;
13. lista de blockers não resolvidos.

## 27. Formato do relatório final

```md
# Relatório de Conformidade LGPD/SaaS

## 1. Escopo
- Repositório:
- Commit:
- Produto:
- Ambientes:
- Data:

## 2. Decisão
Status: APROVADO / APROVADO COM RESSALVAS / BLOQUEADO

## 3. Sumário executivo

## 4. Dados pessoais identificados

## 5. Dados sensíveis

## 6. Crianças/adolescentes

## 7. Cookies/SDKs/rastreadores

## 8. Bases legais

## 9. Direitos dos titulares

## 10. Transferência internacional

## 11. Segurança

## 12. Incidentes

## 13. Retenção

## 14. Fornecedores/subprocessadores

## 15. Contratos e documentos públicos

## 16. Riscos críticos

| ID | Risco | Severidade | Evidência | Impacto | Correção | Status |
|---|---|---:|---|---|---|---|

## 17. Testes executados

## 18. Arquivos alterados

## 19. Pendências jurídicas/setoriais

## 20. Conclusão
```

## 28. Severidade de riscos

### Crítico
Pode gerar sanção grave, vazamento, coleta ilegal em larga escala, tratamento de menor/sensível sem salvaguarda, transferência internacional ilegal, ausência de direitos do titular, marketing sem consentimento ou risco alto de dano.

### Alto
Pode gerar reclamações, autuação, litígio, descumprimento contratual ou incidente relevante.

### Médio
Falha documental, transparência insuficiente, retenção mal definida, lacuna de evidência ou controle parcial.

### Baixo
Melhoria recomendada, inconsistência menor ou documentação incompleta sem risco imediato relevante.

## 29. Matriz rápida de risco por funcionalidade

| Funcionalidade | Risco base | Controles obrigatórios |
|---|---:|---|
| Cadastro com e-mail/senha | Médio | política, segurança, hash, direitos, retenção |
| CPF obrigatório | Alto | finalidade forte, minimização, retenção, segurança |
| Analytics básico | Médio | inventário, base legal, opt-out/consentimento conforme caso |
| Pixel de marketing | Alto | consentimento, bloqueio prévio, revogação, política |
| Geolocalização precisa | Alto | consentimento/permissão, minimização, RIPD se alto risco |
| Biometria | Crítico | base sensível, RIPD, segurança reforçada |
| Dados de saúde | Crítico | base sensível, RIPD, segurança, setor regulado |
| Crianças/adolescentes | Crítico | melhor interesse, ECA Digital, idade, parental, sem ads comportamental |
| IA com dados pessoais | Alto/Crítico | inventário, contrato, transferência, minimização, RIPD |
| Exportação de dados | Alto | autenticação, autorização, logs, escopo correto |
| Admin impersonation | Alto | justificativa, logs, MFA, RBAC |
| Webhooks | Alto | assinatura, escopo, logs mascarados, revogação |
| Multi-tenant | Crítico | isolamento, testes BOLA/IDOR, tenant_id obrigatório |

## 30. Checklist final de conformidade

### Documentos

- [ ] Política de Privacidade atualizada
- [ ] Política de Cookies/SDKs atualizada
- [ ] Termos de Uso atualizados
- [ ] DPA B2B, se aplicável
- [ ] Lista de subprocessadores
- [ ] Inventário de tratamento
- [ ] Matriz de bases legais
- [ ] Tabela de retenção
- [ ] Registro de consentimentos
- [ ] RIPD, se aplicável
- [ ] LIA, se legítimo interesse relevante
- [ ] Plano de incidentes
- [ ] Política de segurança
- [ ] App Store/Google Play atualizados, se aplicável

### Produto

- [ ] Privacy Center
- [ ] Canal de direitos do titular
- [ ] Exportação de dados
- [ ] Exclusão/anonimização
- [ ] Revogação de consentimento
- [ ] Gerenciamento de cookies
- [ ] Consentimento granular
- [ ] Bloqueio prévio de SDKs
- [ ] Link permanente de privacidade
- [ ] Logs mascarados
- [ ] Retenção automatizada
- [ ] Multi-tenant isolado
- [ ] Admin protegido

### Jurídico-operacional

- [ ] Encarregado/canal publicado
- [ ] Contratos com operadores
- [ ] Transferência internacional documentada
- [ ] Processo de incidente
- [ ] Processo de atendimento a titulares
- [ ] Processo de revisão de fornecedores
- [ ] Processo de privacy review em PRs
- [ ] Treinamento mínimo interno

## 31. Instruções especiais para Codex

Quando usado no Codex:

1. Analise o repositório antes de editar.
2. Procure inicialização de SDKs/rastreadores.
3. Crie ou atualize arquivos em `/privacy`.
4. Faça patches pequenos e testáveis.
5. Adicione testes automatizados sempre que possível.
6. Não remova coleta sem entender impacto funcional; gateie por base legal/consentimento.
7. Não invente política; gere rascunho e marque campos que exigem validação da empresa.
8. Se houver blocker, pare e liste exatamente o que impede aprovação.

## 32. Instruções especiais para Claude Code

Quando usado no Claude Code:

1. Use busca semântica e grep para localizar tratamento de dados.
2. Crie plano antes de alterar arquivos.
3. Execute testes e linters disponíveis.
4. Gere evidências em Markdown.
5. Mantenha um `privacy/risk-register.csv` atualizado.
6. Ao encontrar incerteza jurídica, marque `LEGAL_REVIEW_REQUIRED`.
7. Não declare “LGPD compliant” sem evidência.
8. Priorize blockers críticos antes de melhorias cosméticas.

## 33. Instruções especiais para Gemini

Quando usado no Gemini Code Assist/CLI:

1. Analise código, configs e documentação.
2. Classifique dados e fluxos.
3. Sugira mudanças com diffs.
4. Evite respostas genéricas: sempre cite arquivo, linha, função ou endpoint.
5. Gere checklists em `/privacy`.
6. Identifique inconsistência entre código e política.
7. Marque riscos de terceiros, IA e mobile.
8. Não aprove release se houver SDK não inventariado.

## 34. Resposta padrão quando houver lacuna grave

Use este formato:

```md
Status: BLOQUEADO

Motivo: [descrição objetiva]

Evidência:
- Arquivo/linha:
- Fluxo afetado:
- Dado pessoal envolvido:
- Titulares afetados:
- Base legal ausente ou inadequada:

Risco:
- LGPD/ANPD:
- Contratual:
- Segurança:
- Consumidor:

Correção mínima:
1.
2.
3.

Arquivos a alterar:
-

Teste de aceitação:
-

Revisão jurídica necessária: Sim/Não
```

## 35. Proibições absolutas para o agente

O agente nunca deve:

- inventar base legal;
- presumir consentimento;
- esconder rejeição;
- carregar marketing antes de consentimento;
- usar dados de clientes B2B para treinar IA sem autorização e base legal;
- manter dados indefinidamente por conveniência;
- registrar secrets/dados sensíveis em logs;
- afirmar conformidade sem evidência;
- ignorar crianças/adolescentes;
- ignorar transferência internacional;
- tratar política de privacidade como substituto de controle técnico;
- copiar política genérica sem alinhar ao código real;
- classificar todo SDK como “necessário”;
- considerar dado anonimizado sem teste de reidentificação;
- usar “legítimo interesse” como base universal;
- negar direitos do titular sem fundamentação;
- apagar evidência de consentimento necessária para prova;
- expor dados de um tenant a outro;
- deixar admin sem MFA/RBAC;
- usar fornecedor sem DPA quando ele atuar como operador.

## 36. Critério de aprovação

A saída só pode ser “APROVADO” quando:

- todos os tratamentos têm finalidade e base legal;
- dados sensíveis/menores foram avaliados;
- cookies/SDKs não necessários estão bloqueados antes de base legal/consentimento;
- privacy center ou canal equivalente existe;
- direitos dos titulares têm fluxo;
- retenção está definida;
- transferência internacional está documentada;
- fornecedores estão classificados;
- segurança mínima foi verificada;
- incidentes têm processo;
- evidências foram geradas;
- testes críticos passaram;
- pendências jurídicas não bloqueantes estão explicitadas.

Caso contrário, usar “APROVADO COM RESSALVAS” ou “BLOQUEADO”.

## 37. Referências legais e técnicas para revisão humana

Fontes mínimas a consultar periodicamente:

- Portal da ANPD — regulamentações vigentes;
- LGPD — Lei nº 13.709/2018;
- Guia Orientativo da ANPD sobre Cookies e Proteção de Dados Pessoais;
- Guia Orientativo da ANPD sobre Segurança da Informação para agentes de tratamento de pequeno porte;
- Página da ANPD sobre Comunicação de Incidente de Segurança;
- Página da ANPD sobre Transferência Internacional de Dados;
- Página da ANPD sobre RIPD;
- Resoluções ANPD vigentes;
- Marco Civil da Internet — Lei nº 12.965/2014;
- Decreto nº 8.771/2016;
- ECA — Lei nº 8.069/1990;
- ECA Digital — Lei nº 15.211/2025;
- Decreto nº 12.880/2026;
- Código de Defesa do Consumidor — Lei nº 8.078/1990;
- Decreto nº 7.962/2013;
- Decreto nº 11.034/2022, quando SAC aplicável;
- regras Apple App Store e Google Play vigentes;
- normas setoriais aplicáveis ao produto.

## 38. Anexo — Modelo de `privacy/subprocessors.md`

```md
# Subprocessadores

Última atualização: AAAA-MM-DD

| Fornecedor | Serviço | Papel | País | Dados tratados | Finalidade | Transferência internacional | Mecanismo | Link | Status |
|---|---|---|---|---|---|---|---|---|---|

## Notificação de alterações

Clientes serão notificados sobre novos subprocessadores por [canal] com antecedência de [prazo], quando contratualmente aplicável.
```

## 39. Anexo — Modelo de `privacy/risk-register.csv`

```csv
id,data,area,risco,severidade,probabilidade,impacto,dados_afetados,titulares_afetados,evidencia,lei_norma_relacionada,mitigacao,owner,prazo,status
```

## 40. Anexo — Modelo de `privacy/privacy-test-plan.md`

```md
# Plano de Testes de Privacidade

## Cookies e SDKs
- [ ] Sem consentimento: verificar network calls
- [ ] Rejeitar todos: verificar bloqueio
- [ ] Aceitar por categoria: verificar granularidade
- [ ] Revogar: verificar interrupção

## Direitos
- [ ] Acesso
- [ ] Exportação
- [ ] Correção
- [ ] Exclusão/anonimização
- [ ] Revogação
- [ ] Informação de compartilhamento

## Segurança
- [ ] Logs mascarados
- [ ] Admin MFA/RBAC
- [ ] Multi-tenant isolation
- [ ] Secrets scanning
- [ ] CORS
- [ ] Rate limiting
- [ ] Webhook signature

## Mobile
- [ ] ATT iOS
- [ ] AAID Android
- [ ] Permissões nativas
- [ ] App Store/Google Play consistency
```

## 41. Anexo — Modelo de política de decisão

```md
# Decisão de Privacidade

Tratamento:
Finalidade:
Dados:
Titulares:
Base legal:
Alternativas avaliadas:
Necessidade:
Riscos:
Salvaguardas:
Retenção:
Transferência internacional:
Fornecedores:
Conclusão:
Aprovador técnico:
Revisão jurídica:
Data:
```

## 42. Nota final para o agente

Conformidade não é um texto. É um conjunto de controles implementados, evidências e decisões justificadas. Se o código contradiz a política, o código é a realidade. Se não existe evidência, trate como não conforme até prova em contrário.

---

# 43. Consolidação v2.0 — junção da skill original + DOC LGPD.md + Privacy‑Data‑Protection‑Skills + lgpd‑skills

Esta seção torna explícito o que foi incorporado da análise dos repositórios externos e do documento `DOC LGPD.md`. Ela não substitui as seções anteriores; ela reforça, organiza e acrescenta regras operacionais que o agente deve aplicar em qualquer auditoria, feature ou pull request que toque dados pessoais.

## 43.1 Regra de precedência operacional

Quando houver conflito entre instruções internas desta skill, aplique a regra mais conservadora para o titular de dados e mais segura para o controlador. A ordem de prevalência é:

1. Lei vigente e regulamentação oficial brasileira.
2. LGPD e resoluções da ANPD.
3. ECA Digital, quando houver criança, adolescente ou produto de acesso provável por menores.
4. Marco Civil da Internet, CDC, Constituição Federal e normas setoriais.
5. Contratos B2B, DPA e termos enterprise.
6. Política de privacidade pública.
7. Implementação técnica.

Se a implementação técnica divergir da política pública, o agente deve bloquear o release e exigir correção de uma das duas pontas. Política que promete menos que o código coleta é risco jurídico. Código que coleta mais do que a política declara é risco crítico.

## 43.2 Orquestrador de auditoria LGPD

O agente deve operar como maestro. Antes de implementar correções, classifique o cenário:

- **A — Greenfield:** projeto novo; aplicar privacy by design desde a arquitetura.
- **B — Legacy:** sistema em produção; fazer descoberta reversa e retrofit.
- **C — Híbrido:** base antiga com novas features; auditar a feature e o legado que ela toca.
- **D — Incidente:** vazamento, exposição indevida, ransomware, bucket público, envio errado, token vazado ou suspeita de acesso não autorizado.

O agente deve executar o pipeline correspondente:

### Pipeline A — Greenfield

1. Criar `.lgpd/STATUS.md`.
2. Mapear dados por feature.
3. Definir base legal antes do código.
4. Definir retenção e descarte.
5. Definir consentimento, se aplicável.
6. Projetar DSAR.
7. Projetar logs auditáveis.
8. Projetar segurança e criptografia.
9. Criar política de privacidade inicial.
10. Criar ROPA.
11. Criar RIPD se houver alto risco.
12. Avaliar ECA Digital.
13. Avaliar fornecedores e transferências.
14. Bloquear release até fechar riscos críticos.

### Pipeline B — Legacy

1. Fazer discovery reverso do banco, APIs, logs, SDKs, cookies e fornecedores.
2. Criar inventário real, não presumido.
3. Identificar dados sem finalidade, sem base legal ou com retenção indefinida.
4. Classificar riscos por severidade.
5. Corrigir coleta excessiva.
6. Implementar direitos do titular.
7. Criar ou corrigir política pública.
8. Criar ROPA.
9. Criar RIPD para alto risco.
10. Corrigir contratos, DPAs e transferências.
11. Criar plano de remediação com responsáveis.

### Pipeline C — Híbrido

1. Auditar a nova feature.
2. Auditar dependências legadas tocadas pela feature.
3. Verificar se a nova feature muda finalidade, base legal, política, retenção, fornecedores ou transferência internacional.
4. Gerar diff LGPD no pull request.
5. Bloquear merge se houver risco crítico.

### Pipeline D — Incidente

1. Abrir registro em `.lgpd/incidents/`.
2. Preservar evidências.
3. Conter o incidente.
4. Identificar dados e titulares afetados.
5. Aplicar critério de notificação da Resolução CD/ANPD nº 15/2024.
6. Acionar encarregado e jurídico.
7. Preparar comunicação à ANPD e titulares quando aplicável.
8. Criar pós-incidente, causa raiz e plano de remediação.

## 43.3 Subskills obrigatórias codificadas dentro desta skill

A skill consolidada incorpora as seguintes capacidades como módulos internos. Mesmo que o agente não suporte subskills formais, ele deve executar cada módulo como etapa lógica.

| Módulo | Saída |
|---|---|
| `lgpd-audit` | auditoria geral |
| `lgpd-legal-basis` | bases legais |
| `lgpd-data-mapping` | mapa de dados |
| `lgpd-ropa` | ROPA |
| `lgpd-ripd` | RIPD |
| `lgpd-consent-schema` | consent ledger |
| `lgpd-dsar` | direitos do titular |
| `lgpd-privacy-policy` | política |
| `lgpd-incident-response` | runbook |
| `lgpd-dpo-encarregado` | encarregado |
| `lgpd-dpa` | DPA |
| `lgpd-international-transfer` | transferências |
| `lgpd-vendor-audit` | fornecedores |
| `lgpd-audit-logging` | logs imutáveis |
| `lgpd-encryption-keys` | chaves |
| `lgpd-anonymization` | anonimização |
| `lgpd-retention-erasure` | retenção |
| `lgpd-eca-digital-minors` | menores |
| `lgpd-legacy-retrofit` | legado |

## 43.4 Living artifacts obrigatórios

Todo projeto auditado deve manter artefatos versionáveis. A pasta padrão é `.lgpd/`. Se o repositório já usa `/privacy`, mantenha compatibilidade criando espelho ou links.

Estrutura mínima:

```text
.lgpd/
├── STATUS.md
├── data-map.md
├── legal-basis.md
├── ROPA.md
├── lia/
│   └── lia-{atividade}.md
├── RIPD/
│   └── ripd-{atividade}.md
├── consent/
│   ├── consent-ledger.md
│   └── consent-schema.md
├── dsar/
│   ├── dsar-runbook.md
│   └── dsar-log.md
├── incidents/
│   ├── incident-runbook.md
│   └── log.md
├── policies/
│   ├── privacy-policy-v1.md
│   └── cookie-policy-v1.md
├── vendors/
│   └── vendor-{nome}.md
├── transfers/
│   └── transfer-{vendor}.md
├── security/
│   ├── encryption.md
│   ├── access-control.md
│   └── audit-logging.md
├── eca-digital.md
├── automated-decisions.md
├── retention-schedule.md
├── subprocessors.md
├── app-store-google-play.md
└── gaps.md
```

Nenhum relatório final pode afirmar conformidade se os artefatos aplicáveis não existirem, estiverem vazios ou não refletirem o código real.

## 43.5 Data mapping reforçado

O agente deve fazer mapeamento de dados em duas camadas.

### Camada técnica

Inspecione:

- esquemas de banco;
- migrations;
- models ORM;
- DTOs;
- validators;
- endpoints REST;
- resolvers GraphQL;
- filas;
- workers;
- webhooks;
- logs;
- analytics;
- pixels;
- SDKs;
- buckets;
- planilhas;
- exports CSV;
- ferramentas de suporte;
- CRM;
- billing;
- antifraude;
- data warehouse;
- BI;
- backups;
- mobile permissions;
- WebView;
- push notification;
- feature flags.

### Camada jurídico-operacional

Para cada atividade, documente:

- finalidade;
- base legal;
- categoria de dado;
- categoria de titular;
- origem do dado;
- controlador;
- operador;
- suboperadores;
- transferência internacional;
- retenção;
- descarte;
- segurança;
- alto risco;
- necessidade de LIA;
- necessidade de RIPD;
- evidências no código.

## 43.6 Anotações LGPD no schema

Quando o projeto usar ORM, o agente deve sugerir anotações nos modelos.

Exemplo Prisma:

```prisma
/// @lgpd:activity=a001-account-management
/// @lgpd:purpose="autenticação, gestão de conta e prestação do serviço"
/// @lgpd:legal_basis="art_7_v"
/// @lgpd:retention="account_active_plus_5y"
/// @lgpd:sensitive=false
model User {
  id        String   @id
  email     String   @unique /// @lgpd:pii=high @lgpd:mask=partial
  cpf       String?  /// @lgpd:pii=high @lgpd:encrypt=true
  createdAt DateTime @default(now())
}
```

Se o agente encontrar campos pessoais sem anotação LGPD em modelo crítico, deve abrir gap.

## 43.7 Matriz de base legal reforçada

O agente deve aplicar a árvore de decisão:

1. O dado é pessoal?
2. O dado é sensível?
3. O titular é criança ou adolescente?
4. A finalidade é essencial ao serviço?
5. Há obrigação legal?
6. Há contrato ou etapa pré-contratual?
7. Há consentimento livre, informado e inequívoco?
8. Há legítimo interesse documentado em LIA?
9. Há transferência internacional?
10. Há risco alto que exige RIPD?

### Dados comuns — Art. 7º

Use apenas uma das 10 hipóteses legais previstas na LGPD:

1. consentimento;
2. obrigação legal ou regulatória;
3. administração pública;
4. estudos por órgão de pesquisa;
5. execução de contrato ou procedimento pré-contratual;
6. exercício regular de direitos;
7. proteção da vida;
8. tutela da saúde;
9. legítimo interesse;
10. proteção do crédito.

### Dados sensíveis — Art. 11

Use apenas uma das hipóteses específicas:

1. consentimento específico e destacado;
2. obrigação legal;
3. política pública;
4. pesquisa com anonimização quando possível;
5. exercício regular de direitos;
6. proteção da vida;
7. tutela da saúde;
8. prevenção à fraude e segurança do titular.

### Regras críticas

- Legítimo interesse não vale para dado sensível.
- Execução de contrato não vale para dado sensível.
- Consentimento genérico é inválido.
- Consentimento condicionado a finalidade não essencial é risco crítico.
- Marketing comportamental exige consentimento ou LIA muito robusto quando for dado comum e cenário excepcional.
- Perfilamento publicitário de menores deve ser bloqueado.

## 43.8 LIA obrigatório para legítimo interesse

Quando usar Art. 7º, IX, crie `.lgpd/lia/lia-{atividade}.md`.

Conteúdo mínimo:

1. **Finalidade legítima:** interesse real, lícito e específico.
2. **Necessidade:** por que a finalidade não pode ser atingida com menos dados.
3. **Expectativa do titular:** se o titular razoavelmente espera esse uso.
4. **Balanço:** impacto nos direitos do titular.
5. **Salvaguardas:** opt-out, minimização, pseudonimização, limitação de acesso.
6. **Risco residual:** baixo, médio, alto ou crítico.
7. **Decisão:** aprovado, aprovado com mitigação ou reprovado.

Se o LIA for reprovado, o tratamento deve ser removido ou migrado para outra base legal válida.

## 43.9 ROPA reforçado

O ROPA não pode ser uma lista genérica. Ele deve refletir o sistema real e ser atualizado a cada mudança relevante.

Para cada operação, registre:

- nome da atividade;
- finalidade;
- base legal;
- controlador;
- operador;
- categorias de titulares;
- categorias de dados;
- dados sensíveis;
- menores;
- sistemas;
- fornecedores;
- país de armazenamento;
- transferências;
- retenção;
- descarte;
- segurança;
- direitos afetados;
- LIA;
- RIPD;
- owner;
- data da revisão;
- evidência no código.

O agente deve gerar `.lgpd/ROPA.md` e também versão CSV em `/privacy/ropa.template.csv` quando possível.

## 43.10 RIPD reforçado

O agente deve exigir RIPD quando houver alto risco. Alto risco inclui:

- dados sensíveis;
- dados de menores;
- idosos em contexto vulnerável;
- larga escala;
- geolocalização precisa;
- biometria;
- reconhecimento facial;
- monitoramento sistemático;
- antifraude invasivo;
- score;
- decisão automatizada;
- IA generativa com dados pessoais;
- data broker;
- publicidade comportamental;
- inferência sensível;
- transferência internacional complexa;
- combinação de múltiplas bases de dados.

Conteúdo mínimo do RIPD:

1. descrição do tratamento;
2. finalidade;
3. necessidade;
4. proporcionalidade;
5. base legal;
6. dados e titulares;
7. fluxo de dados;
8. fornecedores;
9. transferência internacional;
10. retenção;
11. riscos;
12. probabilidade;
13. impacto;
14. mitigação;
15. risco residual;
16. decisão de continuidade;
17. plano de revisão;
18. aprovação do encarregado;
19. aprovação jurídica quando aplicável.

## 43.11 Consent ledger append-only

Quando a base legal for consentimento, a prova deve ser auditável. O agente deve criar ou exigir um ledger com registros append-only.

Campos mínimos:

- ID do titular ou pseudônimo;
- ID de dispositivo, quando aplicável;
- finalidade;
- categoria;
- versão da política;
- versão do banner;
- status;
- timestamp;
- IP ou região, quando necessário;
- user-agent;
- canal de coleta;
- origem da ação;
- hash do termo apresentado;
- prova de opt-in;
- prova de revogação.

Regras:

- Não sobrescrever consentimento antigo.
- Registrar nova versão a cada mudança.
- Revogação deve ser preservada.
- SDKs não essenciais devem observar o estado mais recente.
- O consentimento deve ser tão fácil de revogar quanto de conceder.

## 43.12 DSAR operacional

O agente deve criar fluxo para direitos do titular.

Endpoints ou fluxos mínimos:

- confirmação de tratamento;
- acesso aos dados;
- correção;
- eliminação;
- anonimização ou bloqueio;
- portabilidade;
- informação de compartilhamento;
- revogação de consentimento;
- oposição ao tratamento;
- revisão de decisão automatizada.

Regras:

- Resposta completa em até 15 dias, salvo regra específica aplicável.
- Validar identidade antes de entregar dados.
- Não expor dados de outro titular.
- Para menores, envolver responsável legal.
- Registrar solicitação e resposta em `.lgpd/dsar/dsar-log.md`.

## 43.13 Política de privacidade como reflexo do código

A política deve ser gerada a partir do inventário. Ela deve informar:

- controlador;
- contato;
- encarregado;
- dados coletados;
- finalidades;
- bases legais;
- cookies e SDKs;
- fornecedores;
- transferências internacionais;
- retenção;
- direitos do titular;
- canal DSAR;
- segurança;
- menores;
- decisões automatizadas;
- alterações futuras.

Se o código coleta dado não descrito na política, o agente deve bloquear release. Se a política descreve compartilhamento inexistente, o agente deve abrir gap de transparência e atualização.

## 43.14 Encarregado — Resolução CD/ANPD nº 18/2024

O agente deve exigir arquivo `.lgpd/encarregado.md` com:

- identidade ou canal do encarregado;
- forma de contato pública;
- atribuições;
- substituto;
- data de designação;
- política de conflito de interesse;
- procedimento de resposta ao titular;
- procedimento de comunicação com a ANPD;
- evidência de treinamento.

Se o controlador dispensar encarregado por regra de pequeno porte, a justificativa deve ser documentada. Mesmo quando dispensado, o canal de privacidade deve existir.

## 43.15 Incidentes — Resolução CD/ANPD nº 15/2024

O agente deve manter runbook de incidente com dois modos.

### Modo preparatório

- criar runbook;
- criar matriz de severidade;
- definir equipe de resposta;
- definir contatos de emergência;
- definir modelos de comunicação;
- definir canal com fornecedores;
- testar tabletop;
- registrar lições aprendidas.

### Modo emergencial

Ao detectar incidente:

1. registrar data e hora do conhecimento;
2. preservar evidências;
3. conter vazamento;
4. classificar dados;
5. estimar titulares;
6. identificar crianças, adolescentes, idosos ou dados sensíveis;
7. avaliar risco ou dano relevante;
8. decidir se notifica ANPD e titulares;
9. documentar decisão;
10. comunicar em até 3 dias úteis quando aplicável;
11. complementar em até 20 dias úteis quando necessário;
12. manter registro por 5 anos.

### Conteúdo mínimo para ANPD

Inclua:

1. natureza dos dados;
2. categorias dos dados;
3. número de titulares;
4. número de menores e idosos;
5. medidas técnicas antes e depois;
6. riscos;
7. impactos;
8. motivos de demora;
9. mitigação;
10. data do incidente;
11. data do conhecimento;
12. dados do encarregado;
13. identificação do controlador;
14. identificação do operador;
15. causa provável;
16. total de titulares tratados na atividade afetada.

### Conteúdo mínimo para titulares

Inclua:

- natureza dos dados;
- medidas de segurança;
- riscos;
- medidas de mitigação;
- data de conhecimento;
- contato do encarregado;
- orientações práticas.

## 43.16 Transferência internacional — Arts. 33 a 36 e Resolução CD/ANPD nº 19/2024

Para qualquer fornecedor, cloud, CDN, observabilidade, analytics, suporte, pagamento, CRM ou IA fora do Brasil, o agente deve criar avaliação em `.lgpd/transfers/`.

Hipóteses do Art. 33:

1. país ou organismo internacional com grau adequado;
2. cláusulas contratuais específicas;
3. cláusulas-padrão contratuais;
4. normas corporativas globais;
5. selos, certificados ou códigos de conduta;
6. cooperação jurídica internacional;
7. proteção da vida;
8. autorização da ANPD;
9. política pública;
10. consentimento específico e destacado;
11. obrigação legal;
12. contrato ou procedimento pré-contratual;
13. exercício regular de direitos.

Regras:

- Cláusulas-padrão brasileiras devem ser adotadas integralmente.
- O prazo de adaptação contratual da Resolução 19/2024 já expirou.
- A União Europeia foi reconhecida pela ANPD como organismo internacional com grau adequado por Resolução CD/ANPD nº 32/2026.
- Mesmo com adequação, documente a transferência e mantenha contrato.
- Transferência para EUA ou outros países sem adequação exige mecanismo apropriado.
- Consentimento específico para transferência é exceção, não solução padrão.

## 43.17 DPA e operadores

Todo fornecedor que trate dados pessoais em nome do controlador deve ter DPA ou cláusula contratual equivalente.

O DPA deve tratar de:

1. objeto;
2. duração;
3. finalidade;
4. instruções documentadas;
5. confidencialidade;
6. segurança;
7. suboperadores;
8. transferência internacional;
9. assistência em DSAR;
10. incidentes;
11. auditoria;
12. eliminação ou devolução;
13. responsabilidade;
14. cooperação com a ANPD.

Sem DPA para operador relevante, o release deve ser bloqueado quando houver novo compartilhamento.

## 43.18 Vendor audit e tiering

Classifique fornecedores por risco.

| Nível | Critério |
|---|---|
| Crítico | dados sensíveis |
| Alto | grande volume |
| Médio | dados comuns |
| Baixo | sem PII |

Para fornecedores críticos ou altos, exigir:

- DPA;
- segurança documentada;
- suboperadores;
- localização de dados;
- transferência internacional;
- prazo de retenção;
- SLA de incidente;
- evidências de segurança;
- revisão anual.

## 43.19 Audit logging imutável

O agente deve criar trilha de auditoria para operações sobre dados pessoais.

Eventos mínimos:

- leitura administrativa;
- exportação;
- alteração;
- exclusão;
- restauração;
- download;
- acesso via suporte;
- uso de impersonation;
- mudança de permissão;
- revogação de consentimento;
- DSAR;
- incidentes.

Requisitos:

- timestamp confiável;
- actor;
- ação;
- recurso;
- resultado;
- IP;
- motivo;
- tenant;
- hash encadeado;
- armazenamento imutável;
- retenção mínima de 5 anos para incidentes e evidências relevantes.

## 43.20 Criptografia e gestão de chaves

Regras mínimas:

- TLS em todo tráfego externo;
- criptografia em repouso para bancos e backups;
- KMS ou vault para chaves;
- rotação de chaves;
- segregação de chaves por ambiente;
- Argon2id ou bcrypt para senhas;
- nunca armazenar senha reversível;
- mascarar CPF, telefone e e-mail em logs;
- tokenizar dados de alto risco;
- aplicar crypto-shredding quando viável;
- restringir acesso a secrets.

## 43.21 Anonimização e pseudonimização

O agente deve preferir anonimização sempre que o objetivo for analytics, BI, estatística, treinamento de IA ou produto agregado.

Técnicas possíveis:

- agregação;
- truncamento;
- masking;
- generalização;
- supressão;
- tokenização;
- k-anonymity;
- l-diversity;
- t-closeness;
- differential privacy;
- separação de identificadores;
- vault de tokens.

Se houver risco razoável de reidentificação, trate como dado pessoal. Não rotule como “anonimizado” aquilo que é apenas pseudonimizado.

## 43.22 Retenção e eliminação

O agente deve proibir retenção indefinida. Cada dado deve ter prazo e critério.

Regras:

- dados de conta: manter enquanto conta ativa e prazo jurídico necessário;
- logs de segurança: manter conforme finalidade e obrigação aplicável;
- logs de incidente: mínimo de 5 anos;
- consent logs: manter enquanto necessário para prova;
- analytics bruto: reduzir, agregar ou anonimizar;
- dados de marketing: apagar após opt-out ou inatividade;
- dados de pagamento: respeitar obrigações fiscais e antifraude;
- dados de menores: minimizar e revisar com maior frequência;
- backups: definir ciclo de expurgo ou crypto-shredding.

## 43.23 ECA Digital — Lei nº 15.211/2025

Aplique quando o serviço for direcionado ou de acesso provável por crianças e adolescentes no Brasil.

Sinais de acesso provável:

- jogos;
- rede social;
- chat;
- comunidade;
- educação;
- vídeos;
- música;
- influenciadores;
- avatares;
- gamificação;
- linguagem infantil;
- design atrativo a menores;
- uso em escolas;
- preço ou oferta familiar.

Obrigações técnicas:

1. avaliar aplicabilidade;
2. aplicar melhor interesse;
3. usar privacy by default;
4. adotar verificação de idade confiável quando exigida;
5. não depender só de autodeclaração quando a lei exigir mecanismo confiável;
6. vincular contas de menores ao responsável quando aplicável;
7. fornecer supervisão parental;
8. proibir perfilamento publicitário de menores;
9. bloquear pixels de ads para menores;
10. bloquear loot boxes em jogos de acesso provável por menores;
11. mitigar chat com desconhecidos;
12. remover conteúdo ilícito contra menores;
13. avaliar relatório de transparência semestral se ultrapassar o threshold legal;
14. documentar tudo em `.lgpd/eca-digital.md`.

Se houver menores e publicidade comportamental, classifique como risco crítico.

## 43.24 Decisões automatizadas, IA e perfilamento

Para qualquer IA, modelo, score, regra automatizada ou recomendação que afete o titular:

- mapear dados de entrada;
- mapear finalidade;
- definir base legal;
- verificar dados sensíveis inferidos;
- verificar menores;
- avaliar discriminação;
- criar explicabilidade mínima;
- permitir contestação quando aplicável;
- registrar versão do modelo;
- registrar métricas de viés;
- criar RIPD quando houver alto risco;
- impedir treinamento com dados pessoais sem base legal;
- proibir envio de PII para LLM externo sem DPA e transferência adequada.

## 43.25 Mobile, ATT, AAID e lojas

Para apps iOS e Android:

- ATT não substitui LGPD;
- permissão de sistema não substitui base legal;
- IDFA/AAID devem respeitar opt-out;
- push token é dado pessoal quando vinculável;
- geolocalização precisa exige minimização;
- WebView deve respeitar CMP;
- App Store Privacy Details deve bater com inventário;
- Google Play Data Safety deve bater com inventário;
- SDKs não essenciais só podem inicializar após base legal válida;
- revogação deve desligar coleta futura.

## 43.26 Marketing, leads e CRM

Regras:

- lead magnet precisa informar finalidade;
- newsletter precisa opt-out;
- enriquecimento de lead exige base legal;
- scraping de contatos é alto risco;
- compra de listas é risco alto ou crítico;
- pixel de remarketing exige consentimento;
- lookalike audience exige avaliação específica;
- WhatsApp marketing exige base legal e opt-out;
- dados de menores não podem entrar em ads comportamental.

## 43.27 Multi-tenant SaaS

Para SaaS B2B multi-tenant:

- isolar tenants no banco e storage;
- impedir acesso cruzado;
- registrar tenant em logs;
- controlar impersonation;
- limitar suporte humano;
- criar DPA;
- listar subprocessadores;
- permitir exportação por cliente;
- permitir exclusão por contrato;
- registrar regiões de dados;
- separar papéis controlador/operador.

## 43.28 Bloqueadores objetivos de release

Bloquear merge ou deploy se existir:

- dado pessoal sem finalidade;
- dado pessoal sem base legal;
- dado sensível sem hipótese do Art. 11;
- coleta de menor sem avaliação;
- ads comportamental para menor;
- cookie/SDK não essencial antes de consentimento;
- transferência internacional sem mecanismo;
- operador sem DPA;
- retenção indefinida;
- DSAR inexistente;
- política desatualizada;
- incidente sem registro;
- logs com CPF, senha, token ou dado sensível;
- credencial em repositório;
- ausência de criptografia para dado alto risco;
- decisão automatizada sem transparência;
- RIPD ausente em alto risco;
- ROPA ausente ou incompleto.

## 43.29 Critério de aprovação v2.0

O agente só pode concluir “aprovado tecnicamente” quando:

1. todos os tratamentos estão inventariados;
2. todas as bases legais estão justificadas;
3. dados sensíveis estão tratados com Art. 11;
4. menores foram avaliados;
5. cookies e SDKs estão bloqueados corretamente;
6. DSAR existe;
7. política está alinhada ao código;
8. retenção está definida;
9. fornecedores estão documentados;
10. transferências estão regulares;
11. incident response existe;
12. segurança mínima está implementada;
13. ROPA está criado;
14. RIPD/LIA estão criados quando exigidos;
15. nenhum blocker crítico permanece aberto.

## 43.30 Comando-padrão para agentes

Quando o usuário pedir auditoria, o agente deve iniciar com:

```text
Vou aplicar a skill LGPD v2.0. Primeiro vou mapear dados pessoais no código, banco, SDKs, logs, cookies, fornecedores e documentação. Em seguida vou gerar ou atualizar os artefatos em .lgpd/ e apontar blockers de release. Não vou marcar conformidade se houver lacuna crítica.
```

## 43.31 Saídas obrigatórias adicionais

Além das saídas já definidas na skill original, gerar quando aplicável:

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
- `.lgpd/gaps.md`;
- `/privacy/privacy-review-pr-template.md`;
- `/privacy/privacy-test-plan.md`.

## 43.32 Nota de completude

Esta skill agora cobre a camada técnica e documental da LGPD para SaaS brasileiro em nível amplo. Ainda assim, o agente deve declarar dependência de análise jurídica humana nos casos de:

- saúde;
- financeiro;
- crédito;
- seguros;
- educação infantil;
- biometria;
- reconhecimento facial;
- vigilância;
- dados trabalhistas;
- investigação interna;
- criança/adolescente;
- IA de alto impacto;
- incidentes relevantes;
- transferência internacional complexa;
- litígio;
- contratos enterprise com penalidades altas.

Nenhuma automação elimina risco jurídico. Ela reduz risco por meio de evidência, minimização, governança, rastreabilidade e correção técnica.
