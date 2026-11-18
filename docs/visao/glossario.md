# Glossário

Os termos do domínio, na forma em que aparecem no código e na documentação.

## Negócio

**Meio acadêmico.** Faculdades e cursos de odontologia. É o mercado atendido pela operação
comercial deste case.

**Professor.** Quem decide a compra. Monta o kit de brocas da turma a cada trimestre de aulas.

**Ciclo trimestral.** O intervalo entre um kit e o próximo. É o que dá sentido às faixas do farol.

**Kit.** O conjunto de brocas que cada aluno de uma turma recebe. Tem regras de composição: mínimo
de unidades por aluno, ao menos uma broca diamantada e uma carbide, estoque para a turma inteira e
teto de custo por aluno.

**Conta.** O cliente no CRM. Pode estar cadastrada no nome da faculdade ou do próprio professor.

**CODPARC.** O código do parceiro no ERP. É a chave que liga a conta do CRM ao cadastro do ERP.

## Farol

**Farol.** A classificação de cada conta por cor, conforme os dias desde a última compra.

| Cor | Dias sem compra | Leitura |
|---|---|---|
| Verde | 1 a 30 | Trimestre em andamento |
| Amarelo | 31 a 60 | Trimestre em andamento |
| Vermelho | 61 a 90 | Janela antes do próximo kit |
| Preto | 91 a 120 | O professor pulou um ciclo |
| Roxo | sem compra, 0 ou mais de 120 | Inativo ou lead |

**Antecipação.** O contato feito quando a conta entra no vermelho, antes de o professor fechar o
próximo kit.

**Resgate.** O contato feito quando a conta entra no preto, depois de um ciclo pulado.

**Borda do dia 0.** Quem comprou hoje tem zero dias sem compra e cai em roxo pela regra original.
A reconstrução mantém o comportamento e documenta o caso em teste.

## Briefing

**Briefing.** O que a IA entrega ao vendedor quando a conta dispara: situação da conta, próxima
ação, mensagem de WhatsApp e e-mail.

**Rascunho.** O estado em que todo briefing nasce. Só vira mensagem enviada depois da revisão do
vendedor.

**Template.** O briefing determinístico, montado só com os dados da conta, que entra quando a IA
falha.

**Fallback.** A passagem da IA para o template, depois de esgotadas as tentativas ou diante de um
erro que não muda ao repetir.

**Guardrail.** Regra que o texto não pode violar: só números que existem na entrada e nenhuma
promessa de desconto, promoção, brinde ou condição especial.

## Avaliação

**Eval.** A execução do briefing sobre 20 contas fictícias, com nota automática por critério.

**Rubrica.** O conjunto de critérios do eval: formato, números presentes na entrada, citação de
dias sem compra e último pedido, limites de palavras, pergunta única no WhatsApp e ausência de
desconto.

**Mock bom e mock ruim.** Dois clientes falsos da IA. O primeiro segue todas as regras e deve passar
em tudo. O segundo tem defeitos de propósito, para provar que a rubrica reprova.

**Histórico.** O registro de cada execução do eval, com versão e hash do prompt, para comparar
versões.

## Reconstrução

**Reconstrução.** Este repositório: a lógica do produto refeita em código, com dados fictícios.

**Fase 2.** O que está decidido e ainda não tem código aqui: ERP simulado em Postgres, orquestração
no n8n, app de CRM e kits, mock do WhatsApp.

**Decisão P e decisão A.** P é decisão de produto, tomada no sistema original. A é decisão de
arquitetura da reconstrução.
