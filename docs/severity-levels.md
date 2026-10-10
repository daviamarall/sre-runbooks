# Níveis de Severidade

Como classificar incidentes e qual a expectativa de resposta.

| Severidade | Impacto | Exemplos | Resposta | Comunicação |
|------------|---------|----------|----------|-------------|
| **SEV1** | Serviço crítico indisponível / perda de dados | Produção fora do ar, fraude não bloqueada | Imediata (24/7) | Status page + liderança |
| **SEV2** | Função importante degradada | Latência altíssima, taxa de erro alta em um fluxo | Imediata | Canal do incidente |
| **SEV3** | Impacto limitado | Parte dos usuários afetada, trabalho contornável | Comercial / plantão | Registro em ticket |
| **SEV4** | Sem impacto real | Alerta ruidoso, melhoria | Backlog | — |

## Prazos de resposta (alvo)

| Severidade | Confirmação | Atualização | Postmortem |
|------------|-------------|-------------|------------|
| SEV1 | 5 min | a cada 15–30 min | obrigatório em 3 dias |
| SEV2 | 15 min | a cada 30–60 min | obrigatório |
| SEV3 | 1 dia útil | diária | opcional |
| SEV4 | — | — | — |

## Regra de ouro

**Na dúvida entre dois níveis, comece pelo mais alto.** É mais fácil rebaixar a severidade do que descobrir tarde que era grave.
