# Runbook — Latência alta

**Sintoma:** P95/P99 de latência acima do SLO.
**Alerta relacionado:** `HighLatencyP95`.

## 1. Confirmar

```promql
histogram_quantile(0.95, sum(rate(http_request_duration_seconds_bucket[5m])) by (le))
```

- Compare com a linha de base normal.
- Verifique se é sistêmico ou de um endpoint específico.

## 2. Mitigar

- **CPU/memória saturados?** Escale réplicas (HPA/manual).
- **Banco lento?** Veja [connection pool](database-connection-pool-exhaustion.md).
- **Consumo de downstream lento?** Aumente timeout/circuit breaker.
- **Cache frio após deploy?** Aguarde aquecimento ou faça pré-aquecimento.

```bash
kubectl scale deployment/<app> --replicas=<N> -n <namespace>
```

## 3. Resolver

- Otimize queries (índices, N+1), adicione cache.
- Revise timeouts e limites de concorrência.

## 4. Registrar

- Linha do tempo; compare o "antes/depois" no dashboard.
