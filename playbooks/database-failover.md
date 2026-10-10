# Playbook — Failover de banco de dados

**Quando usar:** banco primário indisponível ou degradado de forma grave.

> Playbook = procedimento multi-etapa, com mais de um runbook envolvido. Mais arriscado que um runbook simples: **envolva o Incident Commander**.

## 0. Antes de começar

- [ ] Confirmar que o primário está realmente indisponível (não é problema de rede do app).
- [ ] Nomear **Incident Commander** e abrir canal.
- [ ] Comunicar stakeholders (impacto esperado durante o failover).

## 1. Avaliar

- Réplica/secundário está **saudável** e **sincronizado**?
- Qual o **lag** de replicação? (failover com lag alto = perda de dados).

```sql
-- Exemplo PostgreSQL
SELECT client_addr, state, sent_lsn, replay_lsn FROM pg_stat_replication;
```

## 2. Promover o secundário

- Execute o procedimento do provedor (RDS/Aurora) ou do cluster (ex.: `pg_ctl promote`).
- Aguarde o novo primário aceitar conexões.

## 3. Redirecionar a aplicação

- Atualize endpoint/connection string (ou use o endpoint estável do provedor).
- Recycle as conexões da aplicação (rolling restart dos pods).
- Veja também: [pool de conexões](../runbooks/database-connection-pool-exhaustion.md).

## 4. Validar

- Escrita e leitura funcionando.
- Métricas de erro/latência voltando ao normal.
- Réplicas antigas reconfiguradas (evitar *split-brain*).

## 5. Encerrar

- Comunicar normalização.
- Postmortem obrigatório ([template](../docs/postmortem-template.md)).
- Revisar se o failover foi automático ou manual — automatizar se possível.

## ⚠️ Riscos

- **Split-brain:** dois primários aceitando escrita.
- **Perda de dados:** se o secundário tinha lag.
- Nunca force promoção sem confirmar o estado da replicação.
