# Decisões

Para cada decisão: o que foi escolhido, as alternativas consideradas e o custo assumido.

As decisões **P** são de produto e foram tomadas no sistema original, em produção. As decisões
**A** são de arquitetura da reconstrução. Nas decisões A, o status indica o que já está neste
repositório: **implementado** tem código e teste aqui; **fase 2** é a decisão tomada, ainda sem código.

# Decisões de produto

## P1. Levar o dado até o vendedor em vez de melhorar o painel

**Escolha:** o vendedor não vai até o farol. O farol chega até ele, já lido, dentro do CRM, com a
situação da conta, a próxima ação e a mensagem prontas.

**Alternativas**
- Painel melhor no ERP ou no BI, com treinamento e cobrança de uso. Ataca a adesão, mas continua
  pedindo que o vendedor abra, interprete e decida sozinho.
- Relatório semanal por e-mail para a gestão. Dá visibilidade à diretoria, mas não muda o que o
  vendedor faz no dia.

**Por quê:** o farol estava certo e ninguém o consultava. O problema não era falta de informação,
era a atenção que cada consulta cobrava. Herbert Simon descreveu isso em 1971: um sistema de
informação só reduz a carga de quem o usa se absorve mais informação do que produz.

**Custo assumido:** o produto passa a decidir o que o vendedor vê primeiro. Se a regra de disparo
estiver errada, ele deixa de ver contas que um painel mostraria.

## P2. Disparar no vermelho para antecipar e no preto para resgatar

**Escolha:** o briefing é gerado quando a conta entra no vermelho (61 a 90 dias sem compra) ou no
preto (91 a 120). Verde, amarelo e roxo não disparam nada.

**Por quê:** quem decide a compra é o professor, que monta o kit da turma a cada trimestre de
aulas. As faixas do farol acompanham esse ciclo: verde e amarelo cobrem o trimestre em andamento,
vermelho é a janela antes do próximo kit, e preto indica que o professor pulou um ciclo. O
vermelho é o momento de antecipar; o preto, de resgatar.

**Alternativas**
- Disparar no amarelo. Chega cedo demais: o kit do trimestre ainda está em uso, e o contato vira ruído.
- Disparar só no preto. Chega tarde: o professor já fechou o kit com outro fornecedor.

**Custo assumido:** quando o cadastro é da faculdade, vários professores dividem uma conta e uma
cor. Um professor ativo pode esconder outro que pulou o ciclo (ver A3).

## P3. A IA redige, o vendedor decide

**Escolha:** todo briefing nasce como rascunho. O vendedor revisa e envia em um clique. Nada sai
sem alguém ler.

**Alternativas:** envio automático por regra, ou envio automático só para contas de baixo valor.

**Custo assumido:** um passo a mais na rotina do vendedor, em troca de nunca mandar a um professor
um texto que ninguém leu. É também o que permite medir se o texto da IA serve como está: o que o
vendedor muda antes de enviar é o sinal de qualidade mais honesto que existe.

## P4. As regras do negócio viram regras do produto

**Escolha:** a IA só pode citar números que estão no ERP e não pode oferecer desconto, promoção,
brinde ou condição especial. As duas regras estão no prompt, na validação em tempo de execução e
na rubrica do eval.

**Por quê:** o vendedor não tinha autonomia para dar desconto. Se a IA prometesse, criaria um
compromisso que ninguém na conversa podia cumprir. A regra não foi criada para a IA: ela já existia
para as pessoas, e o produto a tratou como fronteira.

**Custo assumido:** mensagens menos agressivas comercialmente. A checagem de número inventado fica
no eval e não em tempo de execução, porque falso positivo mandaria briefings bons para o template (ver A6).

## P5. Validar em plataforma pronta antes de construir

**Escolha:** o primeiro MVP rodou sobre um CRM de mercado (Agendor), para ganhar tempo, com as
integrações construídas do zero em vez de compradas. Só depois de ver o vendedor usando, CRM,
funil e montagem de kit foram para uma aplicação própria (Bubble).

**Alternativas**
- Construir a aplicação própria desde o início. Mais controle, mas paga o custo de construir antes
  de saber se o vendedor usaria.
- Manter as ferramentas que já existiam e só integrar. Mais barato no início, mas mantém as duas
  licenças e o preenchimento manual.

**Resultado:** mais de 60% de redução de custo com ferramentas comerciais. A licença do CRM saiu, e
a montagem de kit validou substituir também a ferramenta de força de vendas, que era a mais cara.

**Custo assumido:** uma migração no meio do caminho, do MVP para a aplicação própria.

## P6. A regra do kit mora no produto, não na cabeça do vendedor

**Escolha:** o app de kits lê preço e estoque do ERP e valida sozinho a composição: mínimo de 8
unidades por aluno, ao menos uma broca diamantada e uma carbide, estoque para a turma inteira e
custo por aluno dentro do teto.

**Por quê:** a montagem de kit não tinha regra. Com a regra no produto, o vendedor monta o kit com
o professor e já sabe, na hora, se ele pode ser cadastrado.

**Custo assumido:** regra de negócio em mais um sistema, que precisa acompanhar quando o comercial
mudar o mínimo ou o teto.

# Decisões de arquitetura (reconstrução)

## A1. n8n como orquestrador, regra de negócio em código próprio

**Status:** fase 2.

**Escolha:** o n8n cuida de agendamento, webhooks e roteamento, e só faz chamadas HTTP ao app.
Farol, validação de kit, chamada ao Claude, validação com zod e fallback ficam em TypeScript,
cobertos por testes.

**Alternativas**
- Tudo no n8n, com nós de Code e HTTP. É mais rápido de montar, mas é difícil testar e versionar.
- Tudo em código, com cron e fila próprios. Dá controle total, mas a operação perde visibilidade
  das execuções e o reprocessamento manual fica mais trabalhoso.
- n8n lendo o Postgres direto. Fica mais perto de um n8n ligado ao Oracle, mas exige credencial
  importada e espalha lógica para fora dos testes.

**Custo assumido:** quando algo quebra, há dois lugares para olhar. Workflows em JSON são ruins
de revisar em diff.

## A2. View materializada com refresh diário, não consulta em tempo real

**Status:** fase 2.

**Escolha:** `vw_farol_rfm` é uma view materializada, atualizada uma vez por dia pelo n8n com
`REFRESH MATERIALIZED VIEW CONCURRENTLY`. A coluna `dt_referencia` mostra a data do cálculo.

**Alternativas**
- View comum, consultada ao vivo. O dado está sempre atual, mas cada abertura do farol custa
  agregação sobre todo o histórico de pedidos, e no ERP real isso concorre com o faturamento.
- Tabela atualizada por trigger a cada pedido. É incremental, mas acopla escrita no ERP e não
  resolve sozinha a passagem do tempo: os dias aumentam sem que nenhum pedido aconteça.

**Custo assumido:** os dias ficam defasados até o próximo refresh. Se um refresh falhar, o dado
fica velho sem aviso, e por isso `dt_referencia` aparece na tela.

## A3. CODPARC como chave de integração

**Status:** fase 2.

**Escolha:** o código do parceiro no ERP (`CODPARC`) é a chave da conta no CRM.

**Alternativas**
- CNPJ. É estável fora do ERP, mas há parceiros sem CNPJ (pessoa física, lead) e filiais com
  CNPJs distintos.
- ID próprio do CRM com tabela de-para. Desacopla os sistemas, mas é mais uma tabela para manter
  consistente.

**Contexto do negócio:** quem decide a compra é o professor, que monta o kit a cada trimestre de
aulas, e o cadastro no ERP pode estar no nome da faculdade ou do próprio professor. A conta do CRM
segue o cadastro que existe, sem forçar um modelo único.

**Custo assumido:** o CRM fica acoplado ao ERP. Um parceiro duplicado no Sankhya vira duas contas
no CRM. Quando o cadastro é da faculdade, vários professores dividem a mesma conta e o mesmo farol,
e um professor ativo pode esconder outro que pulou o ciclo.

## A4. Front separado do ERP

**Status:** fase 2.

**Escolha:** o CRM e o app de kits são um app Next.js próprio. O ERP fica no schema `erp`,
acessado com um role somente de leitura. O CRM fica no schema `crm`.

**Alternativas**
- Telas dentro do próprio ERP (Construtor de Telas do Sankhya). O dado fica num lugar só, mas a
  experiência do vendedor fica limitada pelo ERP, que era justamente o problema.
- Banco separado para o CRM. O isolamento é maior, mas a demo fica mais pesada.

**Custo assumido:** o mesmo dado existe em dois modelos, e a sincronização pode ficar defasada.

## A5. Regra do farol duplicada em SQL e TypeScript

**Status:** implementado em TypeScript; lado SQL e teste de paridade na fase 2.

**Escolha:** `erp.fn_farol(dias)` alimenta a view, e `classificarFarol(dias)` é usada no app.
Na fase 2, um teste de integração compara as duas para 0 a 200 dias e para nulo.

**Regra fiel ao SQL de produção:**

| DIASULTIMACOMPRA | Farol |
|---|---|
| `> 0 and <= 30` | Verde |
| 31 a 60 | Amarelo |
| 61 a 90 | Vermelho |
| 91 a 120 | Preto |
| demais, incluindo `NULL` (sem compra) e `0` | Roxo |

**Limitação conhecida (borda do dia 0):** uma conta que comprou hoje tem DIASULTIMACOMPRA = 0 e,
pela regra original, cai em **Roxo**, a mesma cor de um inativo ou lead. A reconstrução mantém
esse comportamento de propósito, para ser fiel ao original. Um teste de borda documenta o caso.
Na prática, o efeito aparece no máximo por um dia: no refresh seguinte a conta tem 1 dia e passa
a Verde.

**Sugestão (não aplicada):** trocar a primeira faixa para `>= 0 and <= 30` e deixar o Roxo só para
`NULL` e para mais de 120 dias. A mudança teria que ser feita no SQL e no TypeScript ao mesmo
tempo, com o teste de paridade atualizado. Fica registrada como proposta para discutir com o
negócio, não como mudança da regra.

**Leitura no ciclo trimestral:** as faixas acompanham o trimestre de aulas. Verde e Amarelo cobrem
o trimestre em andamento, Vermelho é a janela antes do próximo kit e Preto indica que o professor
pulou um ciclo. Por isso o briefing dispara nas duas cores: no Vermelho para antecipar o kit, no
Preto para resgatar a conta.

**Custo assumido:** duas implementações a manter. O teste de paridade cobre o risco de divergência.

## A6. Retry e fallback do briefing

**Status:** implementado.

**Escolha:** o SDK roda com `maxRetries: 0`, e o controle de tentativas é nosso: 1 chamada mais
até 2 novas tentativas, com timeout por tentativa. Se todas falharem (erro de API, timeout ou
saída fora do schema), entra um template com os dados do ERP, com `origem = 'template'`, e o
evento é registrado.

A validação em runtime cobre schema, limites de palavras, pergunta única e ausência de desconto.
A checagem de "nenhum número inventado" fica só no eval.

Detalhes da implementação (`src/domain/briefing/gerar.ts`, `src/infra/anthropic.ts`):
- Erros que não mudam ao repetir (400, 401, 403, 404 e recusa do modelo) vão direto ao fallback,
  sem gastar as 2 novas tentativas. A regra é "no máximo 2", e repetir uma chave inválida só
  adiciona latência.
- O timeout é por tentativa e aborta a requisição HTTP (`AbortSignal`), para não deixar uma
  chamada órfã consumindo tokens.
- O modelo vem de `CLAUDE_MODEL`, com padrão `claude-sonnet-5-5`. A saída usa structured output com
  o schema de forma (zod). As regras de texto (palavras, pergunta, desconto) são validadas no
  domínio, porque refinements não viram JSON Schema.
- Nenhum recurso beta da API é usado. Uma recusa do modelo por política vai direto ao template.

**Custo assumido:** se a checagem de número inventado rodasse em runtime, falsos positivos
mandariam briefings bons para o fallback. Por isso ela fica no eval, e o vendedor revisa tudo.

## A7. Revisão humana obrigatória

**Status:** o briefing é gerado como texto para revisão, sem envio automático; o fluxo de aprovação e envio fica na fase 2.

**Escolha:** todo briefing nasce como `rascunho`. Nada é enviado sem aprovação do vendedor.

**Custo assumido:** um passo a mais para o vendedor, em troca de nunca mandar a um cliente um
texto que ninguém leu.

## A8. Dinheiro em centavos inteiros

**Status:** implementado.

**Escolha:** o TypeScript usa centavos inteiros e o SQL usa `numeric(14,2)`.

**Custo assumido:** é preciso converter na borda, mas evita erro de ponto flutuante no custo
por aluno.

## A9. SQL puro com `pg`, sem ORM

**Status:** fase 2.

**Escolha:** queries SQL explícitas.

**Alternativas:** Prisma ou Drizzle, que trazem tipagem automática e migrações.

**Custo assumido:** tipagem manual das linhas. O ganho é o SQL ficar visível, como no dia a dia
com Sankhya e Oracle.

## A10. Mock do WhatsApp com o contrato da Cloud API

**Status:** fase 2.

**Escolha:** o mock aceita `POST /v21.0/{phone-number-id}/messages`, exige `Authorization: Bearer`,
valida o payload e responde no formato oficial, inclusive os erros.

**Limitação conhecida:** na API real, uma mensagem livre só pode ser enviada dentro da janela de
24 h após a última mensagem do cliente. Para resgatar um cliente inativo seria preciso um template
aprovado. O mock só registra um aviso, e o tema fica registrado aqui como ponto de atenção.
