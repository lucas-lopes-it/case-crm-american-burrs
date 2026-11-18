# O farol que ninguém olhava

A história do produto em primeira pessoa. As decisões estão detalhadas em
[DECISOES.md](DECISOES.md), e o código que reconstrói a lógica está neste repositório.

## O dado já existia

Na American Burrs, indústria de brocas odontológicas que vende para o meio acadêmico, o ERP já
classificava cada cliente por cor, conforme os dias desde a última compra. Verde, amarelo,
vermelho, preto, roxo. O farol estava certo e ninguém o consultava. Ao mesmo tempo, o vendedor não
gostava de preencher o CRM, e a empresa pagava duas ferramentas comerciais para guardar um dado
que chegava incompleto.

Quando assumi a transformação digital, a leitura óbvia era de adesão: treinar, cobrar, criar um
painel melhor. Levei um tempo para ver que o problema era outro. Nenhum vendedor precisava de mais
informação. Faltava a ele tempo para olhar a que já havia.

## O que Herbert Simon já tinha escrito em 1971

Herbert Simon, que depois ganharia o Nobel de economia, descreveu esse problema numa palestra sobre
como desenhar organizações num mundo rico em informação. A informação consome a atenção de quem a
recebe, e por isso riqueza de informação gera pobreza de atenção.

A parte contraintuitiva vem logo depois. Para Simon, um sistema de informação só reduz a carga da
organização se absorve mais informação do que produz. O objetivo não é entregar ao gestor tudo de
que ele precisa, é reorganizar o ambiente para que ele gaste menos tempo recebendo.

O farol fazia o contrário. Cada cor era mais uma coisa a abrir, interpretar e transformar em ação.

## Primeiro, entender o ciclo de quem compra

No discovery descobri que quem decide não é a faculdade, é o professor. A cada trimestre de aulas
ele monta o kit de brocas da turma. Isso deu sentido às cores: verde e amarelo cobrem o trimestre
em andamento, vermelho é a janela antes do próximo kit, preto é o professor que já pulou um ciclo.

Com isso, a pergunta mudou. Não era "como fazer o vendedor olhar o farol". Era "o que o vendedor
precisa ter na mão no dia em que a conta entra no vermelho".

## A decisão: o sistema lê, o vendedor decide

O vendedor não iria até o dado. O dado iria até ele, já lido. O farol passou a ser sincronizado
todo dia dentro do CRM. Quando uma conta entrava no vermelho ou no preto, a IA lia o histórico do
ERP e entregava quatro coisas: a situação da conta, uma próxima ação, a mensagem de WhatsApp e o
e-mail. O vendedor revisava e enviava em um clique.

As regras do negócio viraram regras do produto. A IA só podia citar números que estivessem no ERP.
Não podia oferecer desconto, porque o vendedor também não tinha essa autonomia. E nada saía sem
alguém ler. Ajustei o texto do briefing com o uso real, até ele soar como o vendedor.

O mesmo raciocínio valeu para a montagem do kit. O app puxava preço e estoque do ERP e validava
sozinho as regras da turma: mínimo de unidades por aluno, a combinação certa de tipos de broca,
estoque para a turma inteira e teto de custo por aluno.

## A ordem importou mais que a ferramenta

Validei a hipótese primeiro numa plataforma de CRM pronta, para ganhar tempo, e construí as
integrações do zero em vez de pagar pelas prontas. Só depois de ver o vendedor usando levei CRM,
funil e montagem de kit para uma aplicação própria em low-code.

O resultado foi mais de 60% de redução de custo com ferramentas comerciais. Uma das duas licenças
saiu, e a montagem de kit validou substituir também a outra, que era a mais cara. O farol passou a
orientar a rotina do vendedor, e o preenchimento manual acabou.

## A frase que eu levaria para qualquer reunião

Painel pede atenção. Briefing devolve atenção.

A maior parte dos projetos de dados para força de vendas mede quanto dado chegou ao vendedor. Eu
passei a desenhar pelo contrário: quanto ele deixou de ter que ler para agir.

Depois que saí, reconstruí a lógica neste repositório, com dados fictícios, testes e uma avaliação
automática do briefing em 20 contas. Construí com um agente de código e mantive um registro de cada
desvio dele, como o dia em que mudou uma regra de produção sem pedir.

## O que não foi mérito meu

A regra mais importante do briefing não foi minha. Quem decidiu que o vendedor não dá desconto foi
a empresa, muito antes de existir IA no processo. O produto só tratou essa decisão como fronteira,
e talvez seja essa a parte que mais se transfere para outro lugar: antes de perguntar o que a IA
consegue fazer, perguntar o que o negócio já decidiu que ninguém faz.
