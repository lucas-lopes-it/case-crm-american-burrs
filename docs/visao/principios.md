# Princípios

Estes princípios orientam as decisões de produto e de arquitetura. Na dúvida entre duas soluções,
eles desempatam. Cada um aponta para a decisão em [DECISOES.md](../DECISOES.md) que o originou.

## 1. Atenção antes de informação

Toda funcionalidade é julgada por quanto o vendedor deixa de ler para agir, não por quanto dado ela
mostra. Origem: P1.

## 2. O dado vai até a pessoa

O produto entrega no lugar onde o usuário já trabalha. Se ele precisa abrir outra tela para ver, a
funcionalidade ainda não está pronta. Origem: P1, A4.

## 3. O disparo segue o ciclo do cliente

O momento da ação vem do calendário de quem compra, não do calendário de quem vende. Cedo demais é
ruído, tarde demais é venda perdida. Origem: P2.

## 4. A IA redige, a pessoa decide

Nada chega a um cliente sem alguém ler. O que o vendedor muda antes de enviar é o melhor sinal de
qualidade do texto. Origem: P3, A7.

## 5. Regra do negócio é fronteira do produto

O que as pessoas não têm autonomia para fazer, a IA também não faz. A regra fica em três lugares: no
prompt, na validação em tempo de execução e na rubrica do eval. Origem: P4.

## 6. Validar antes de construir

A hipótese de maior risco é testada primeiro, com o menor custo possível. Construção própria só
depois de ver o usuário usando. Origem: P5.

## 7. A regra mora no produto, não na cabeça de alguém

Se uma regra depende de uma pessoa lembrar, ela vira validação automática com teste. Origem: P6.

## 8. A IA é uma dependência, não o centro

O produto tem um caminho determinístico para quando o modelo falha, demora ou recusa. Trocar de
modelo não muda as regras. Origem: A6.

## 9. Regra de produção não muda sem confirmação

A reconstrução é fiel ao comportamento original, inclusive nas bordas estranhas. Melhoria vira
proposta registrada, não correção silenciosa. Origem: A5 e o primeiro item do
[LOG_DE_ERROS.md](../LOG_DE_ERROS.md).

## 10. Toda decisão registra o custo assumido

Uma decisão sem alternativa descartada e sem custo declarado é só uma preferência. Origem: o
formato de [DECISOES.md](../DECISOES.md).

## 11. Medido, implementado e a instrumentar não se misturam

Cada métrica carrega o seu status. Resultado de produção, resultado de eval e intenção ficam em
linhas diferentes. Origem: a tabela de métricas do [README](../../README.md).
