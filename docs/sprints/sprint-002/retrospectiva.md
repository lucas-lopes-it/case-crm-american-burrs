# Sprint 002: retrospectiva

> O que não está na `main` não existe para quem visita.

## O que funcionou

### Separar decisão de produto de decisão de arquitetura

A primeira versão de DECISOES.md tinha dez decisões, todas técnicas. Quem lia saía sabendo como o
sistema foi montado e sem saber por que ele existia. Colocar P1 a P6 na frente mudou a leitura do
repositório inteiro.

### Status em cada decisão e em cada métrica

Marcar "implementado", "fase 2" e "a instrumentar" tirou a ambiguidade entre o que rodou em
produção, o que está neste código e o que é intenção.

### A história separada do README

O README responde rápido a quem está avaliando. O CASE.md conta a história para quem quer ler. Um
documento só não faria bem as duas coisas.

## O que poderia melhorar

### A versão pronta ficou cinco dias fora da `main`

O conteúdo estava completo em 13/11 e só entrou na `main` em 18/11. Nesse intervalo, a primeira
tela do repositório ainda mostrava seções em construção.

### Uma branch ficou para trás

A branch `docs/narrativa-original-x-reconstrucao`, de 22/10, tem um commit que não foi mesclado. A
reescrita de 13/11 cobriu o mesmo assunto por outro caminho, e a branch antiga continua aberta sem
decisão registrada sobre ela.

### Imagens pesadas

As quatro imagens somam cerca de 2,4 MB. Para um README, dá para reduzir sem perda visível.

## O que muda

- Pull request de documentação é mesclado no mesmo dia em que fica pronto.
- Branch que não vai ser mesclada é fechada com uma linha explicando o motivo.
- Toda sprint termina com o README conferido na `main`, do jeito que um visitante vê.
