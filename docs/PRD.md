# PRD: Next best action para o vendedor acadêmico

> PRD reconstruído para portfólio a partir do produto que rodou em produção na American Burrs.
> Os números de resultado estão no [README](../README.md#resultado); as decisões, com alternativas e
> custo assumido, em [DECISOES.md](DECISOES.md).

## Contexto

A American Burrs vende brocas odontológicas para o meio acadêmico. Quem decide a compra é o
professor, que monta o kit da turma a cada trimestre de aulas. O cadastro no ERP pode estar no nome
da faculdade ou do professor.

O ERP já classificava cada conta por cor, conforme os dias desde a última compra. Ninguém consultava.
O vendedor não gostava de preencher o CRM, e a empresa pagava duas ferramentas comerciais (CRM e força
de vendas) para guardar um dado que chegava incompleto.

## Problema

O vendedor carrega sozinho a decisão de com quem falar e o que dizer. A informação para isso existe,
mas está num lugar que ele não abre, e transformá-la em ação custa uma atenção que ele não tem.
O resultado é recompra perdida sem que ninguém perceba a tempo.

## Usuários

| Usuário | Tarefa | Dor |
|---|---|---|
| Vendedor | Manter a carteira comprando a cada trimestre | Não sabe quem está esfriando e não tem tempo de preparar a abordagem |
| Professor (cliente) | Montar o kit da turma no prazo | Ser procurado tarde, depois de já ter fechado com outro fornecedor |
| Gestão comercial | Acompanhar carteira e custo da operação | Depende de relatório manual e paga ferramenta que o time não usa direito |

## Objetivos

1. O vendedor age no dia certo do ciclo do professor, sem abrir painel.
2. Acabar com o preenchimento manual de CRM e de kit.
3. Reduzir o custo com ferramentas comerciais.

## Fora do escopo

- Envio automático de mensagem. Todo texto passa pelo vendedor.
- Desconto, promoção ou condição comercial gerada pela IA.
- Score preditivo de churn. A regra de dias sem compra já era entendida e aceita pelo comercial.
- Telas dentro do ERP.

## Hipótese de maior risco

O vendedor vai agir se a conta chegar já lida, com a próxima ação e a mensagem prontas, no lugar onde
ele já trabalha. Se essa hipótese cair, nada do resto importa. Por isso ela foi testada primeiro, antes
de construir qualquer aplicação própria.

## Requisitos

### Farol e disparo
- R1. Calcular o farol por conta todo dia a partir do histórico de vendas, com as faixas do ERP:
  verde (1 a 30 dias), amarelo (31 a 60), vermelho (61 a 90), preto (91 a 120), roxo (sem compra ou mais de 120).
- R2. Exibir o farol dentro do CRM, na conta, sem o vendedor abrir o ERP.
- R3. Gerar o briefing quando a conta entra no vermelho (antecipar o próximo kit) ou no preto (resgatar quem pulou um ciclo).

### Briefing
- R4. Entregar quatro partes: situação da conta, próxima ação, mensagem de WhatsApp e e-mail.
- R5. Citar só números que existem no histórico da conta, incluindo dias sem compra e último pedido.
- R6. Não oferecer desconto, promoção, brinde ou condição especial.
- R7. WhatsApp com até 50 palavras e uma única pergunta no fim; e-mail com até 90 palavras.
- R8. Nascer como rascunho. O vendedor revisa e envia em um clique, por WhatsApp ou e-mail, e o envio vira atividade no CRM.
- R9. Se a IA falhar, entregar um briefing por template com os dados da conta, e registrar a falha (requisito da reconstrução).

### Kit
- R10. Montar o kit por turma com preço e estoque lidos do ERP.
- R11. Validar antes do cadastro: mínimo de 8 unidades por aluno, ao menos uma broca diamantada e uma carbide, estoque para a turma inteira e custo por aluno dentro do teto.
- R12. Acompanhar a oportunidade num funil de 5 etapas: contato ou visita, montagem do kit, validação do kit, em cadastro, kit cadastrado.

## Métricas de sucesso

| Métrica | Tipo |
|---|---|
| Contas no vermelho que recompram no trimestre seguinte | Principal |
| Tempo entre a conta entrar no vermelho e o primeiro contato | Entrada |
| Briefings enviados sem edição | Qualidade |
| Briefings que caíram no template | Saúde |
| Briefings com número inventado ou desconto (eval) | Guardrail |
| Custo com ferramentas comerciais | Negócio |

## Fases

| Fase | O que entrou | O que validou |
|---|---|---|
| Discovery | Lean Inception | O professor como decisor e o ciclo trimestral |
| MVP | Farol e briefing sobre um CRM de mercado, com integrações construídas do zero | Se o vendedor age sobre o briefing pronto |
| Produto próprio | CRM, funil e montagem de kit numa aplicação própria em low-code | Que dava para tirar a licença do CRM e substituir a de força de vendas |
| Reconstrução pública | Regras em código, testes e eval da IA, com dados fictícios | As regras do produto ficam testáveis e versionadas |

## Riscos

| Risco | Mitigação |
|---|---|
| A IA inventar número ou prometer desconto | Regra no prompt, validação em tempo de execução e rubrica no eval |
| Mensagem errada chegar a um professor | Revisão humana obrigatória |
| Conta da faculdade esconder um professor que pulou o ciclo | Registrado como custo da decisão; próximo passo é tratar o professor como contato decisor |
| WhatsApp para cliente inativo fora da janela de 24 horas da API | Na reconstrução, template aprovado para a primeira mensagem |
| A IA ficar indisponível | Na reconstrução, retry com limite e template com os dados da conta |

## Em aberto

- Diferenciar o tom do briefing entre antecipação (vermelho) e resgate (preto).
- Ordenar a fila do dia por valor dos últimos 12 meses.
