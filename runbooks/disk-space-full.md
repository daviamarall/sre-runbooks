# Runbook — Disco cheio

**Sintoma:** uso de disco > 90% em nó/pod; falhas de escrita.

## 1. Confirmar

```bash
df -h
du -sh /var/log/* | sort -h | tail
kubectl describe node <node> | grep -A3 "Allocated resources"
```

## 2. Mitigar (rápido)

- Rotacione/comprima logs antigos.
- Limpe imagens/containers órfãos (Docker) ou evicted pods.

```bash
docker system prune -af
kubectl delete pods --field-selector=status.phase=Failed -A
```

- Se for volume, aumente o PVC (se o storage class permitir).

## 3. Resolver

- Configure **log rotation** e retenção.
- Separe volumes de dados e de logs.
- Alerta proativo em 80% de uso.

## 4. Cuidado

- Nunca apague arquivos de dados sem confirmar o dono/backup.
- Verifique se o disco cheio é a **causa** ou **sintoma** (ex.: log flood de outro problema).
