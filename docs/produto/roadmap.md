# Roadmap

O roadmap é organizado por capacidade, não por data. Cada capacidade é algo que o produto passa a
saber fazer e que pode ser verificado no repositório.

A direção é a da [visão](../visao/visao.md): cada capacidade nova precisa reduzir o que o vendedor
lê antes de agir.

## O produto em produção

O sistema original rodou na American Burrs. Estas fases aconteceram lá e não têm código aqui.

| Fase | O que entrou | O que validou |
|---|---|---|
| Discovery | Lean Inception com as áreas | O professor como decisor e o ciclo trimestral |
| MVP | Farol e briefing sobre um CRM de mercado, com integrações construídas do zero | Que o vendedor age sobre o briefing pronto |
| Produto próprio | CRM, funil e montagem de kit numa aplicação própria em low-code | Mais de 60% de redução no custo com ferramentas comerciais |

## Capacidades da reconstrução

| Capacidade | Status | Sprint |
|---|---|---|
| Regra do farol fiel ao SQL de produção | Entregue | 001 |
| Validação do kit por turma | Entregue | 001 |
| Briefing com saída estruturada e validação de regras de texto | Entregue | 001 |
| Retry com limite, timeout por tentativa e fallback para template | Entregue | 001 |
| Eval com 20 contas, rubrica automática e histórico por versão de prompt | Entregue | 001 |
| Registro de desvios do agente de código | Entregue | 001 |
| Case na lente de produto (README, decisões P e A) | Entregue | 002 |
| História em primeira pessoa e PRD | Entregue | 002 |
| Demonstração navegável do funil | Entregue | 002 |
| Visão, manifesto, princípios e glossário | Entregue | 003 |
| Ritual de sprint (review, retrospectiva, aprendizado) | Entregue | 003 |
| Governança aberta e integração contínua | Entregue | 003 |
| Prompt v2 com tom distinto para antecipação e resgate | Próximo | 004 |
| Fila do dia ordenada por valor dos últimos 12 meses | Próximo | 005 |
| Registro da diferença entre rascunho e texto enviado | Próximo | 006 |
| ERP simulado em Postgres com view do farol | Depois | fase 2 |
| Teste de paridade entre a regra em SQL e em TypeScript | Depois | fase 2 |
| Orquestração no n8n | Depois | fase 2 |
| App de CRM e kits | Depois | fase 2 |
| Mock do WhatsApp com o contrato da Cloud API | Depois | fase 2 |
| Primeira mensagem de resgate como template aprovado | Depois | fase 2 |

## Foco atual

### Sprint 003: as camadas em volta do código

Entregue nesta sprint:

- visão, manifesto, princípios e glossário em `docs/visao/`;
- este roadmap por capacidade;
- review, retrospectiva e aprendizado das sprints 001 e 002 em `docs/sprints/`;
- licença, código de conduta, política de segurança e guia de contribuição;
- modelo de pull request, modelo de issue e integração contínua com typecheck, testes e eval em mock.

## Próximo

### Sprint 004: prompt v2

**Problema:** o prompt v1 usa o mesmo tom para a conta no vermelho e para a conta no preto.
Antecipar um kit e resgatar um professor que pulou o ciclo são conversas diferentes.

**Entrega:** um prompt v2 com instrução distinta por cor, comparado com o v1 no eval, critério a
critério.

**Como saber se funcionou:** o v2 mantém 100% nos guardrails e a diferença de tom aparece nas 20
contas sem aumentar a taxa de fallback.

### Sprint 005: fila do dia

**Problema:** quando várias contas disparam no mesmo dia, o vendedor não sabe por onde começar.

**Entrega:** ordenação por valor comprado nos últimos 12 meses, com teste.

### Sprint 006: medir a edição

**Problema:** a métrica "briefings enviados sem edição" ainda está como "a instrumentar".

**Entrega:** registro do texto enviado ao lado do rascunho e cálculo da diferença.

## Fora do roadmap, de propósito

- Envio automático de mensagem.
- Desconto ou condição comercial gerada pela IA.
- Score preditivo de churn no lugar da regra de dias sem compra.
- Telas dentro do ERP.

As razões estão no [README](../../README.md#o-que-ficou-fora-de-propósito).
