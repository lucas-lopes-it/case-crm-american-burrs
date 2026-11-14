# Farol de Clientes + CRM de Kits

> **Reconstrução para portfólio.** O sistema original rodou em produção na American Burrs
> (indústria odontológica, vendas B2B para o meio acadêmico). Este repositório **não contém
> código, dados, credenciais nem informações de clientes** do ambiente real. Clientes, produtos,
> pedidos, telefones e e-mails são fictícios. O ERP (Sankhya sobre Oracle) é simulado.

## Situação

A American Burrs vende brocas odontológicas para o meio acadêmico. Quem decide a compra não é a
instituição, é o professor: a cada trimestre de aulas ele monta o kit que a turma vai usar. O
cadastro no ERP pode estar no nome da faculdade ou do próprio professor.

O ERP já tinha um farol de clientes que classificava cada conta pelos dias desde a última compra.
Ninguém consultava. O vendedor não gostava de preencher o CRM, e a empresa pagava duas
ferramentas para o comercial: Ploomes como CRM e Mercos como força de vendas. Quando um professor
deixava passar o trimestre sem pedido, ninguém percebia a tempo.

## Decisão

O problema não era falta de dado, era o dado estar longe de quem precisava dele. Em vez de pedir
ao vendedor que abrisse o ERP, levei o farol para onde ele já trabalhava.

As faixas do farol acompanham o ciclo trimestral de aulas, e foi isso que definiu onde a IA entra:

| Farol | Dias sem compra | Leitura no ciclo trimestral | O que o sistema faz |
|---|---|---|---|
| Verde | 1 a 30 | trimestre em andamento | nada |
| Amarelo | 31 a 60 | trimestre em andamento | nada |
| Vermelho | 61 a 90 | janela antes do próximo kit | briefing de **antecipação** |
| Preto | 91 a 120 | o professor pulou um ciclo | briefing de **resgate** |
| Roxo | sem compra ou acima de 120 | inativo ou lead | nada |

Quando a conta entra em Vermelho ou Preto, o Claude gera um briefing com a situação da conta, uma
próxima ação, uma mensagem de WhatsApp e um e-mail, todos a partir dos dados do ERP. O vendedor
revisa e envia em um clique.

Três regras do negócio viraram guardrails do produto, verificados em código e não só pedidos no
prompt:

- **Nenhum número inventado.** Todo valor, data e quantidade precisa existir nos dados do ERP.
- **Nenhuma promessa de desconto.** O vendedor não tem essa autonomia, então a IA também não tem.
- **Nada sai sem revisão humana.** Todo briefing nasce como rascunho.

Para validar rápido, comecei com um MVP no Agendor, uma plataforma pronta, escolhida para ganhar
tempo de mercado, e construí as integrações do zero em vez de usar as pagas. Com a hipótese
validada, levei CRM, funil e montagem de kit para o Bubble, integrando Agendor, Bubble, Sankhya e
n8n.

## Resultado

- **Mais de 60% de redução de custo** com ferramentas comerciais: o Ploomes saiu e a montagem de
  kit validou substituir também o Mercos, que era o item mais caro. Sobrou a licença do Bubble.
- Briefing em produção, gerado pela Claude API e enviado em um clique por WhatsApp e e-mail.

## Tese

IA em operação comercial funciona melhor quando é invisível: o vendedor não conversa com um
chatbot, ele recebe o trabalho pronto no lugar onde já está, e as regras que o negócio impõe a ele
valem também para o modelo.

## O que este repositório mostra

A reconstrução troca o Bubble por código, para que as regras fiquem testáveis e versionadas.

| Parte | Onde está | Status |
|---|---|---|
| Regra do farol, fiel ao SQL de produção | `src/domain/farol.ts` | implementado |
| Validação do kit por turma (mínimo de unidades, tipos de broca, estoque, teto de custo) | `src/domain/kit.ts` | implementado |
| Geração do briefing com retry, timeout e fallback determinístico | `src/domain/briefing/` | implementado |
| Adaptador da Claude API com saída estruturada | `src/infra/anthropic.ts` | implementado |
| Eval com rubrica automática e histórico por versão de prompt | `scripts/`, `evals/` | implementado |
| ERP simulado em Postgres, app Next.js, workflows n8n, mock do WhatsApp | | fase 2 |

O raciocínio por trás de cada escolha está em [docs/DECISOES.md](docs/DECISOES.md).

## Como rodar

Requer Node 22 ou superior. Nenhuma chave é necessária para os três primeiros comandos.

```bash
npm install
npm test                      # 72 testes: farol, kit, schema, fallback e rubrica
npm run eval -- --mock        # 20 contas, cliente que segue as regras: aprovação de 100%
npm run eval -- --mock=ruim   # mesmo eval com um cliente defeituoso: a rubrica reprova metade
```

Com `ANTHROPIC_API_KEY` no `.env`, `npm run eval` roda contra a Claude API real, e
`npm run eval:compare` compara as duas execuções mais recentes, critério a critério.

## Avaliação do briefing

As 20 contas fictícias ficam em `evals/fixtures/contas.json`. A rubrica
(`src/domain/briefing/rubrica.ts`) verifica:

- o formato da saída;
- se todos os números estão nos dados de entrada;
- se o briefing cita os dias sem compra e o último pedido;
- os limites de palavras do WhatsApp e do e-mail;
- se o WhatsApp termina com uma única pergunta;
- se não há promessa de desconto.

Cada execução grava `evals/runs/<data>_<prompt>_<modelo>.json` e `.md` e acrescenta uma linha em
`evals/historico.csv` com a versão e o hash do prompt, para comparar versões.

## Documentação

- [docs/DECISOES.md](docs/DECISOES.md): decisões de arquitetura, alternativas e custos assumidos
- [docs/LOG_DE_ERROS.md](docs/LOG_DE_ERROS.md): como supervisionei o agente de código, com cada
  desvio do plano, como foi detectado e a regra que passou a valer
