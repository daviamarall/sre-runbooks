# Runbook — Uso de CPU alto

**Sintoma:** CPU do pod/nó acima de 80–90% de forma sustentada.

## 1. Confirmar

```bash
kubectl top pod -n <namespace> --sort-by=cpu
kubectl top node
```

- É um pod específico ou todos os nós?
- Correlacione com aumento de tráfego/erros.

## 2. Mitigar

- **Tráfego legítimo?** Escale: `kubectl scale deployment/<app> --replicas=<N>`.
- **Loop/CPU spin?** Reinicie o pod e investigue (via [rollback](deployment-rollback.md) se veio de deploy).
- **Limite do HPA atingido?** Aumente `maxReplicas`.

## 3. Resolver

- Perfil de CPU (profiling) para achar o hot path.
- Ajustar `resources.requests/limits` conforme uso real.
- Otimizar algoritmo/consulta.

## 4. Cuidado

- CPU alta **sem** aumento de tráfego costuma indicar bug ou loop — trate como suspeita de regressão.
