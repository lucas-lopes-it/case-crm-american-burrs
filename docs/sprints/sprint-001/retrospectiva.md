# Sprint 001: retrospectiva

> Mudança em relação ao plano aprovado é perguntada antes, não comunicada depois.

## O que funcionou

### Plano aprovado antes do código

Escrevi e aprovei o plano antes de o agente tocar em qualquer arquivo. Foi o que tornou os desvios
visíveis: cada um deles apareceu como diferença entre o plano e o que foi feito.

### Testar a rubrica antes de confiar nela

O cliente falso com defeitos existe para responder a uma pergunta simples: a rubrica reprova quando
deveria? Sem ele, 100% de aprovação não quer dizer nada.

### Borda documentada em teste

A regra original manda para o roxo quem comprou hoje. Em vez de corrigir, mantive o comportamento,
escrevi um teste que o descreve e registrei a correção como proposta para discutir com o negócio.

## O que poderia melhorar

### Os quatro desvios tinham a mesma forma

O agente mudou a regra do dia 0, aceitou termos de instalação, trocou o modelo padrão e ativou um
recurso beta. Em todos os casos a decisão foi tomada e depois comunicada. O problema não foi a
qualidade de cada escolha. Foi a ordem.

### Edição de arquivo fora da ferramenta de edição

Um arquivo teve os acentos corrompidos por leitura e gravação no PowerShell. O diff pegou antes do
commit, mas o caminho estava errado desde o início.

### O README ficou para trás

A sprint fechou com seções marcadas como em construção. O código estava pronto e a primeira tela do
repositório dizia o contrário.

## O que mudou

- Regra de produção não muda sem confirmação explícita.
- Aceite de termo, licença ou contrato exige pergunta antes.
- Arquivo do projeto só é alterado pelas ferramentas de edição.
- Desvio do plano é perguntado antes.

As quatro regras estão em [LOG_DE_ERROS.md](../../LOG_DE_ERROS.md), cada uma ao lado do erro que a
originou.
