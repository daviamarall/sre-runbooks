# Runbook — Alta taxa de erro (5xx)

**Sintoma:** aumento de respostas 5xx em um serviço.
**Alerta relacionado:** `HighErrorRate` (ver projeto `observability-lab`).

## 1. Confirmar

- Verifique a taxa de erro no dashboard (painel "Error ratio").
- Identifique o endpoint mais afetado:

```promql
topk(5, sum by (endpoint) (rate(http_requests_total{status=~"5.."}[5m])))
```

- Cheque os logs recentes da aplicação.

## 2. Mitigar (ação imediata)

- **Deploy recente?** Faça **rollback** → [deployment-rollback](deployment-rollback.md).
- **Dependência externa fora?** Ative *circuit breaker* / degrade funcionalidade.
- **Pico de tráfego?** Escale horizontalmente.
- **Recurso saturado?** Ver [high-cpu-usage](high-cpu-usage.md) ou [database-connection-pool-exhaustion](database-connection-pool-exhaustion.md).

```bash
kubectl rollout undo deployment/<app> -n <namespace>
```

## 3. Resolver

- Corrija a causa raiz (bug, timeout, contrato de API).
- Adicione teste de regressão cobrindo o cenário.
- Confirme estabilidade por 30 min.

## 4. Registrar

- Linha do tempo + postmortem ([template](../docs/postmortem-template.md)).
