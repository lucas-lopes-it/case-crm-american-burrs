# Sprint 001: review

> A regra de produção é o requisito. A reconstrução começa por ela.

## Objetivo

Tirar as regras do produto de dentro de uma aplicação low-code e colocá-las em código testado, com
dados fictícios, de modo que qualquer pessoa consiga rodar e verificar.

## Histórias entregues

### 1. Estrutura da reconstrução

- Projeto em TypeScript com Vitest, sem dependência de banco ou de chave de API para rodar os testes.
- Separação entre domínio (`src/domain`), infraestrutura (`src/infra`) e avaliação (`src/eval`).
- Aviso no topo do README: nenhum código, dado, credencial ou cliente do ambiente real.

### 2. Regra do farol

- `classificarFarol(dias)` com as cinco faixas, fiel ao SQL de produção.
- Testes de borda para cada limite de faixa, para nulo e para o dia 0.
- A borda do dia 0 (quem comprou hoje cai em roxo) foi mantida e documentada na decisão A5.

### 3. Validação do kit

- Validação por turma: mínimo de 8 unidades por aluno, ao menos uma broca diamantada e uma carbide,
  estoque para a turma inteira e custo por aluno dentro do teto.
- Dinheiro em centavos inteiros (decisão A8).

### 4. Geração do briefing

- Saída estruturada com schema de forma, e regras de texto validadas no domínio: limite de palavras,
  pergunta única no WhatsApp e ausência de desconto.
- Uma chamada mais até duas novas tentativas, com timeout por tentativa.
- Erros que não mudam ao repetir vão direto ao template.
- Template determinístico com os dados da conta, e evento registrado a cada fallback (decisão A6).

### 5. Eval do briefing

- 20 contas fictícias em `evals/fixtures/contas.json`.
- Rubrica automática com seis critérios.
- Dois clientes falsos: um que segue as regras e um com defeitos, para provar que a rubrica reprova.
- Histórico por execução, com versão e hash do prompt, e comparação entre as duas últimas execuções.

## Números

- 72 testes em 5 arquivos, todos passando.
- Eval em mock bom: 100% de aprovação. Em mock ruim: a rubrica reprova metade.
- 4 desvios do agente de código registrados em [LOG_DE_ERROS.md](../../LOG_DE_ERROS.md).

## O que ficou para depois

- Banco, orquestração, app e canais de envio (fase 2).
- Seções de arquitetura e de roteiro de demo do README, ainda marcadas como em construção ao fim da
  sprint.
