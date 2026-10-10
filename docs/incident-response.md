# Resposta a Incidentes

Guia rápido de quem faz o quê e como comunicar durante um incidente.

## Princípios

- **Ninguém é culpado.** Foco em sistemas e processos, não em pessoas.
- **Mitigar antes de explicar.** Primeiro reduzir impacto, depois investigar causa raiz.
- **Comunicação constante.** Melhor uma atualização curta a cada 20–30 min do que silêncio.

## Papéis

| Papel | Responsabilidade |
|-------|------------------|
| **Incident Commander (IC)** | Coordena o incidente, decide prioridades, não "mete a mão" no sistema |
| **Comunicação (Scribe/Comms)** | Atualiza stakeholders e mantém a linha do tempo |
| **Responders (engenharia)** | Investigam e executam mitigação |
| **On-call** | Primeiro a responder ao alerta; aciona o IC se necessário |

> Em times pequenos, uma pessoa pode acumular papéis — mas nunca deixe um incidente SEV1/SEV2 sem um **Incident Commander** nomeado.

## Escalonamento

1. Alerta dispara → **on-call** confirma em até 5 min.
2. SEV1/SEV2 → **aciona Incident Commander** e abre canal (`#inc-<data>-<tema>`).
3. Sem progresso em 30 min → **escalona** para especialista/líder (segundo nível).
4. Impacto ao cliente → **aciona comunicação** (status page, suporte).

## Ciclo de vida

| Fase | Objetivo | Saída |
|------|----------|-------|
| **Detecção** | Reconhecer que algo está errado | Alerta confirmado |
| **Triagem** | Definir severidade e papéis | SEV definido, IC nomeado |
| **Mitigação** | Reduzir impacto | Serviço estabilizado |
| **Resolução** | Corrigir causa raiz | Fix aplicado |
| **Pós-incidente** | Aprender | Postmortem + ações |

## Comunicação

- Canal dedicado do incidente (Slack/Teams).
- Atualizações em cadência fixa (ex.: a cada 20 min) com o formato:
  - **Impacto**, **O que sabemos**, **O que estamos fazendo**, **Próxima atualização**.
- Ao encerrar: mensagem de "all-clear" + link do postmortem.

## Veja também
- [Níveis de severidade](severity-levels.md)
- [Template de postmortem](postmortem-template.md)
- [Checklist de on-call](oncall-checklist.md)
