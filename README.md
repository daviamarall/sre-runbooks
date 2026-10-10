# sre-runbooks

[![CI](https://github.com/daviamarall/sre-runbooks/actions/workflows/ci.yml/badge.svg)](https://github.com/daviamarall/sre-runbooks/actions/workflows/ci.yml)
![Docs](https://img.shields.io/badge/docs-runbooks-informational)
![License](https://img.shields.io/badge/license-MIT-green)

Conjunto de **runbooks**, **playbooks** e **templates** para responder a incidentes de forma rápida, padronizada e sem pânico — a base operacional de um time de **SRE / sustentação**.

> Projeto de portfólio focado em **SRE / sustentação**. A ideia: documentação viva que reduz **MTTR** (tempo médio de recuperação) e transforma incidentes em aprendizado.

---

## 🎯 Por que runbooks importam

Durante um incidente, ninguém quer improvisar. Um bom runbook responde:

1. **O que está acontecendo?** (sintomas)
2. **Como confirmar?** (comandos/consultas)
3. **Como mitigar agora?** (ação imediata)
4. **Como resolver de vez?** (causa raiz)

Este repositório aplica esse formato em cada documento.

## 🧭 Fluxo de resposta

```
Detecção (alerta) ─▶ Triagem (severidade) ─▶ Mitigação ─▶ Comunicação ─▶ Resolução ─▶ Postmortem
```

## 📚 Conteúdo

### Fundamentos (`docs/`)
- [Resposta a incidentes](docs/incident-response.md) — papéis, comunicação, escalonamento
- [Níveis de severidade](docs/severity-levels.md) — SEV1 a SEV4 e prazos
- [Template de postmortem](docs/postmortem-template.md) — *blameless*
- [Checklist de plantão (on-call)](docs/oncall-checklist.md)

### Runbooks (`runbooks/`)
- [Alta taxa de erro (5xx)](runbooks/high-error-rate.md)
- [Latência alta](runbooks/high-latency.md)
- [Uso de CPU alto](runbooks/high-cpu-usage.md)
- [Pool de conexões do banco esgotado](runbooks/database-connection-pool-exhaustion.md)
- [Disco cheio](runbooks/disk-space-full.md)
- [Rollback de deploy](runbooks/deployment-rollback.md)

### Playbooks (`playbooks/`)
- [Failover de banco de dados](playbooks/database-failover.md)

## ✍️ Como usar

1. Ao receber um alerta, abra o runbook correspondente.
2. Siga os passos de **confirmação → mitigação → resolução**.
3. Registre a linha do tempo durante o incidente.
4. Ao final, escreva um **postmortem** (sem culpar pessoas).

## 🧩 Convenções

- Um runbook = um documento curto e acionável.
- Comandos sempre em blocos de código, prontos para copiar.
- Cada alerta aponta para o runbook relacionado.
- Datas e autores no topo de cada runbook.

## 🛠️ Estrutura

```
sre-runbooks/
├── docs/        # fundamentos, templates e políticas
├── runbooks/    # procedimentos por sintoma
├── playbooks/   # procedimentos multi-etapa / maiores
└── .github/workflows/ci.yml
```

## 📄 Licença

MIT — veja [LICENSE](LICENSE).
