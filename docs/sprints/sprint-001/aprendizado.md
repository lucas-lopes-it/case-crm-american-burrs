# Sprint 001: aprendizado

## Fidelidade vem antes de melhoria

### O que aconteceu

A regra do farol em produção classifica como verde quem está entre 1 e 30 dias sem compra. Quem
comprou hoje tem 0 dias e, pela regra, cai em roxo, a mesma cor de um cliente inativo. Parece um
erro. O agente de código tratou como erro e corrigiu.

Eu reverti.

### Por que isso importa para quem faz produto

Uma regra em produção é um acordo que a operação já absorveu. Alguém pode depender do comportamento
estranho sem saber. Quando a reconstrução corrige por conta própria, ela deixa de descrever o
produto que existiu e passa a descrever o produto que alguém achou que deveria existir.

O mesmo vale para a IA. A regra de não oferecer desconto não foi criada para o modelo. Ela já
valia para o vendedor. O trabalho de produto foi reconhecer a regra e colocá-la em três lugares: no
prompt, na validação e na rubrica.

### Como aplicar

Antes de mudar uma regra herdada:

1. Escreva um teste que descreva o comportamento atual, inclusive a parte estranha.
2. Registre a mudança como proposta, com o efeito prático e quem precisa concordar.
3. Só altere depois da confirmação de quem responde pela regra.

Antes de confiar numa avaliação automática:

1. Rode a avaliação contra uma saída que você sabe que está errada.
2. Confira se cada critério reprova o defeito que deveria reprovar.
3. Só então leia o resultado da saída real.

### Exercício

Rode os dois comandos e compare os relatórios gerados em `evals/runs/`:

```bash
npm run eval -- --mock
npm run eval -- --mock=ruim
```

Depois responda: qual critério da rubrica você removeria sem perder proteção, e qual defeito do
cliente ruim nenhum critério pega?
