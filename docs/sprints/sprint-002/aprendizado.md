# Sprint 002: aprendizado

## O repositório também é um produto, e a primeira tela é o README

### O que aconteceu

Ao fim da sprint 001 o repositório tinha regra testada, fallback e eval. A primeira tela dizia
"arquitetura: em construção". Quem abrisse o link lia o aviso e ia embora antes de chegar ao código.

A sprint 002 não mudou uma linha de comportamento. Mudou o que o visitante entende nos primeiros
trinta segundos.

### Por que isso importa para quem faz produto

Um case técnico costuma ser escrito na ordem em que foi construído: estrutura, regra, integração,
resultado. Quem avalia lê na ordem contrária: quer saber primeiro o que mudou no negócio, depois
para quem, depois por que essa solução e não outra, e só então como foi feito.

Três movimentos fizeram a diferença:

1. **Resultado antes de arquitetura.** O número medido em produção abre o README.
2. **Decisão com custo.** Cada escolha traz a alternativa descartada e o que se perdeu ao escolher.
3. **Status honesto.** O que foi medido, o que está implementado e o que falta instrumentar aparecem
   separados.

O terceiro é o que mais gera confiança. Um leitor que encontra "a instrumentar" ao lado de uma
métrica acredita mais nas que estão marcadas como medidas.

### Como aplicar

Para qualquer projeto que você queira mostrar:

1. Escreva o resultado em uma linha, com número e unidade.
2. Liste as pessoas que usam e o que cada uma precisa, sem nome de ferramenta.
3. Declare a hipótese de maior risco e como ela foi testada antes de construir.
4. Para cada decisão, escreva a alternativa que você descartou e o custo que aceitou.
5. Escreva o que ficou fora de propósito.
6. Marque cada métrica como medida, implementada ou a instrumentar.

### Exercício

Abra o README de um projeto seu e leia só os primeiros trinta segundos. Responda sem rolar a tela:
qual problema ele resolve, para quem, e qual foi o resultado? O que faltar na resposta é o que falta
no topo do documento.
