# Runbook — Pool de conexões do banco esgotado

**Sintoma:** erros de "connection pool exhausted", timeouts ao adquirir conexão.

## 1. Confirmar

- Logs da aplicação com `pool exhausted` / `timeout acquiring connection`.
- Métricas do banco: conexões ativas vs. limite (`max_connections`).
- Veja o painel de conexões ativas do pool.

## 2. Mitigar (rápido)

- Reinicie a aplicação para liberar conexões presas (paliativo).
- Reduza a carga temporariamente (feature flag / rate limit).

## 3. Investigar

- **Vazamento de conexão:** há `DbContext`/`Session` não liberado? (uso de `using`/scope).
- **Query lenta segurando conexão:** veja sessões ativas lentas.

```sql
-- Oracle: sessões ativas por usuário
SELECT username, status, COUNT(*) FROM v$session GROUP BY username, status;
```

```sql
-- PostgreSQL
SELECT state, COUNT(*) FROM pg_stat_activity GROUP BY state;
```

## 4. Resolver

- Corrigi vazamentos; garanta `using`/injeção com escopo correto.
- Ajuste o tamanho do pool em relação ao `max_connections` **e** ao nº de réplicas.
- Adicione timeout de query e circuit breaker.

## 5. Prevenção

- Alerta em `%` de uso do pool (ex.: > 80%).
- Teste de carga cobrindo o pico.
