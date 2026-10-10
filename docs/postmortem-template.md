# Postmortem (template *blameless*)

> O objetivo é aprender, não culpar. Descreva o que o sistema permitiu, não quem errou.

**Incidente:** `<título>`
**Data:** `AAAA-MM-DD`
**Severidade:** `SEV1..4`
**Duração (MTTR):** `HH:MM`
**Autor(es):** `@nomes`
**Status:** `Rascunho | Em revisão | Final`

## 1. Resumo

Uma ou duas frases sobre o que aconteceu e o impacto.

## 2. Impacto

- **Cliente/negócio:** quem foi afetado e como.
- **Métricas:** `X%` das requisições com erro, `Y` transações impactadas, P95 em `Zs`.
- **SLO/error budget:** quanto foi consumido.

## 3. Linha do tempo (horário local + fuso)

| Hora | Evento |
|------|--------|
| HH:MM | Deploy/falha/alerta |
| HH:MM | Detecção (qual alerta) |
| HH:MM | Incidente declarado (SEV, IC) |
| HH:MM | Mitigação aplicada |
| HH:MM | Serviço estabilizado |
| HH:MM | Resolução definitiva |

## 4. Causa raiz

Use os **5 porquês** para chegar à causa real (não pare no sintoma).

1. Por quê? →
2. Por quê? →
3. Por quê? →
4. Por quê? →
5. Por quê? →

## 5. O que funcionou bem

- (ex.: alerta disparou em 30s; rollback automatizado)

## 6. O que poderia ter sido melhor

- (ex.: detecção tardia; runbook desatualizado)

## 7. Ações (com dono e prazo)

| # | Ação | Tipo | Dono | Prazo |
|---|------|------|------|-------|
| 1 | Adicionar teste que cobre o caso | Prevenir | @ | AAAA-MM-DD |
| 2 | Ajustar alerta/timeout | Detectar | @ | AAAA-MM-DD |
| 3 | Atualizar runbook | Mitigar | @ | AAAA-MM-DD |

## 8. Lições aprendidas

O que mudaremos de forma sistêmica a partir de agora.
