# Runbook — Rollback de deploy

**Quando usar:** incidente começou logo após um deploy (regra: "mudou algo? desconfie do que mudou").

## 1. Confirmar que veio do deploy

- Compare o horário do incidente com o horário do deploy.
- Verifique erro novo nos logs/APM desde a versão atual.

## 2. Rollback (Kubernetes)

```bash
# Ver histórico
kubectl rollout history deployment/<app> -n <namespace>

# Voltar para a revisão anterior
kubectl rollout undo deployment/<app> -n <namespace>

# Voltar para uma revisão específica
kubectl rollout undo deployment/<app> --to-revision=<N> -n <namespace>

# Acompanhar
kubectl rollout status deployment/<app> -n <namespace>
```

## 3. Rollback (imagem/CI)

- Re-deploy da tag/imagem anterior (ex.: `ghcr.io/...:<sha-anterior>`).
- Se houver feature flag, **desligue a flag** (mais rápido que rollback).

## 4. Depois do rollback

- Confirme que as métricas voltaram ao normal.
- **Congele** novos deploys até o postmortem.
- Registre a linha do tempo.

## 5. Prevenção

- Canary / blue-green deploy.
- Rollback automatizado por SLO (se taxa de erro subir, reverte sozinho).
- Migrações de banco compatíveis (expand/contract).
