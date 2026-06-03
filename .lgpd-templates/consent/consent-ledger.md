# Consent Ledger

Campos mínimos:

- subject_id
- device_id
- purpose
- category
- policy_version
- banner_version
- status
- timestamp
- source
- user_agent
- ip_or_region
- presented_text_hash
- action_hash

Regras:

- Append-only.
- Não sobrescrever eventos.
- Revogação preservada.
- SDKs observam estado atual.
