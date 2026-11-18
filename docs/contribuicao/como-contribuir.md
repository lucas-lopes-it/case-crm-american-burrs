# Como contribuir

Contribuições de pessoas de produto, de operação comercial e de tecnologia são bem-vindas. Você não
precisa escrever código. Um caso de borda que a regra não cobre, uma conta fictícia nova para o
eval ou uma correção na documentação também melhoram o projeto.

## Preparação

1. Crie um fork e uma branch pequena.
2. Instale Node 22 ou superior.
3. Rode `npm install`.
4. Rode `npm test` e `npm run typecheck` antes e depois da mudança.
5. Se mexer no briefing, rode `npm run eval -- --mock` e `npm run eval -- --mock=ruim`.

Nenhuma chave de API é necessária para esses comandos.

## Boas contribuições

- Explicam qual problema do vendedor, do professor ou da gestão está sendo resolvido.
- São pequenas e vêm com teste.
- Mantêm a regra de negócio em `src/domain`, sem dependência de infraestrutura.
- Respeitam os [princípios](../visao/principios.md), em especial o 9: regra de produção não muda
  sem confirmação. Proposta de mudança de regra entra como issue antes de virar código.
- Registram decisão relevante em [DECISOES.md](../DECISOES.md), com alternativa e custo assumido.
- Usam só dados fictícios.

## Pull request

Descreva o problema, a solução, como testar e o que muda para o vendedor. Ao participar, você
concorda com o [Código de Conduta](../../CODE_OF_CONDUCT.md).
