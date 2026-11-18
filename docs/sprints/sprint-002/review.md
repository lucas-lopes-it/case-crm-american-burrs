# Sprint 002: review

> O código mostrava como o produto funciona. Faltava mostrar por que ele existe.

## Objetivo

Reescrever a documentação na lente de produto: resultado primeiro, depois usuário, problema,
hipótese, decisões, o que ficou fora e como se mede.

## Histórias entregues

### 1. README em formato de case

- Abertura pelo resultado: mais de 60% de redução no custo com ferramentas comerciais.
- Quadro de usuários (vendedor, professor, gestão comercial) com o que cada um precisa do produto.
- Hipótese de maior risco e como foi validada antes de construir.
- Tabela de evolução do produto: discovery, MVP, produto próprio e reconstrução.
- Seção "o que ficou fora, de propósito".
- Métricas com status: medido em produção, implementado, medido no eval ou a instrumentar.

### 2. Decisões de produto antes das de arquitetura

- Seis decisões de produto (P1 a P6), tomadas no sistema original.
- As dez decisões de arquitetura renumeradas como A1 a A10, cada uma com status: implementado ou
  fase 2.
- Referências no código atualizadas para a nova numeração.

### 3. A história em primeira pessoa

- [CASE.md](../../CASE.md): o farol que ninguém olhava, com a leitura de Herbert Simon sobre
  atenção como eixo do argumento.

### 4. PRD

- [PRD.md](../../PRD.md): problema, usuários, objetivos, fora do escopo, doze requisitos, métricas,
  fases, riscos e questões em aberto.

### 5. Demonstração navegável

- `docs/demo/funil.html`: arquitetura, funil de 5 etapas, validação de kit e farol com briefing, em
  um arquivo único com dados fictícios.
- Quatro imagens do produto no README.

## Números

- 5 documentos novos ou reescritos e 1 demonstração navegável.
- 72 testes continuam passando. A única mudança de código foi a numeração das decisões nos
  comentários.
- Pull request 1 mesclado na `main` em 18/11/2026.

## O que ficou para depois

- Visão, princípios e glossário como documentos próprios.
- Registro das sprints.
- Licença, guia de contribuição e integração contínua.
