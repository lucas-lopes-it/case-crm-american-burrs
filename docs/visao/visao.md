# Visão

## Missão

Devolver atenção ao vendedor. O produto lê a carteira por ele e entrega, no dia certo do ciclo do
cliente, a conta já interpretada, a próxima ação e a mensagem pronta para revisar.

## O problema

A maior parte das ferramentas comerciais entrega mais informação a quem já não tem tempo de ler a
que existe. Na American Burrs o ERP classificava cada cliente por cor, conforme os dias desde a
última compra. O farol estava certo e ninguém o consultava.

As respostas habituais para isso não resolvem:

- painel melhor: continua pedindo que o vendedor abra, interprete e decida sozinho;
- treinamento e cobrança de uso: trata como adesão um problema que é de atenção;
- relatório para a gestão: dá visibilidade à diretoria e não muda o dia do vendedor;
- chatbot de vendas: exige que o vendedor vá até a IA e saiba o que perguntar.

## A visão

Operação comercial em que o sistema absorve mais informação do que produz. O vendedor não consulta
painel, não preenche CRM e não monta kit na planilha. Ele recebe o trabalho lido e decide.

Para isso o produto precisa:

- entender o ciclo de compra do cliente, não só o histórico de pedidos;
- chegar ao vendedor no lugar onde ele já trabalha;
- tratar as regras do negócio como fronteira do que a IA pode escrever;
- manter uma pessoa entre a IA e o cliente;
- continuar funcionando quando a IA falha.

## O que este repositório é

A reconstrução pública da lógica desse produto, com dados fictícios. As regras que em produção
moravam numa aplicação low-code aqui são código testado, e o texto da IA é avaliado por uma rubrica
automática a cada versão de prompt.

Ele serve a dois leitores:

- quem avalia o meu trabalho de produto e quer ver problema, decisão, custo assumido e resultado;
- quem constrói IA para operação e quer um exemplo pequeno de regra de negócio, fallback e eval.

## O que este repositório não é

- Não é o sistema de produção. Não há código, dado, credencial ou cliente real aqui.
- Não é um CRM pronto para instalar. A fase 2 (banco, orquestração, app e canais) está decidida e
  ainda não tem código.
- Não é um framework. É um case com as regras expostas.

## Para onde vai

O caminho está em [roadmap.md](../produto/roadmap.md). A direção é sempre a mesma: cada capacidade
nova precisa reduzir o que o vendedor lê antes de agir, e precisa chegar com uma forma de medir se
reduziu.
