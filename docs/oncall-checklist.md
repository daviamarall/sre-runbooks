# Checklist de On-call

Use antes, durante e depois do plantão.

## Antes do plantão

- [ ] Acesso ao cluster/ferramentas garantido (VPN, Kubectl, dashboards).
- [ ] Alertas testados (recebo uma notificação de teste?).
- [ ] Runbooks revisados e com links válidos.
- [ ] Contatos de escalonamento atualizados.
- [ ] Janela de manutenção/deploys conhecida.

## Ao receber um alerta

- [ ] **Confirmar** o impacto (é real? é ruído?).
- [ ] Definir **severidade** ([severity-levels](../docs/severity-levels.md)).
- [ ] SEV1/SEV2: nomear **Incident Commander** e abrir canal.
- [ ] Abrir o **runbook** correspondente ao sintoma.
- [ ] Iniciar a **linha do tempo** (registre tudo com horário).

## Durante

- [ ] Mitigar primeiro (rollback, escala, restart), investigar depois.
- [ ] Comunicar em cadência fixa.
- [ ] Evitar mudanças não relacionadas ao incidente.
- [ ] Registrar hipóteses testadas.

## Depois

- [ ] Confirmar estabilidade por um período (ex.: 30 min sem alertas).
- [ ] Enviar mensagem de encerramento + link do postmortem.
- [ ] Agendar o postmortem (SEV1/SEV2 em até 3 dias).
- [ ] Atualizar/criar o runbook se houve lacuna.
