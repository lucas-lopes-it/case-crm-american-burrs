# Política de Segurança

## O que este repositório contém

Uma reconstrução com dados fictícios. Não há código, dado, credencial ou informação de cliente do
ambiente de produção original. Clientes, produtos, pedidos, telefones e e-mails foram gerados para
a demonstração.

## Segredos

- A única chave usada é `ANTHROPIC_API_KEY`, lida de um arquivo `.env` local que não vai para o git.
- Os testes e o eval em modo mock rodam sem nenhuma chave.
- Nunca inclua chave, token, documento interno ou dado pessoal em issue, pull request ou fixture.

## Como relatar uma vulnerabilidade

Use o relato privado do GitHub: aba **Security**, opção **Report a vulnerability**. Não abra issue
pública para esse tipo de assunto.

Se você encontrar neste repositório algo que pareça dado real, relate pelo mesmo caminho. Esse é o
tipo de falha mais grave que este projeto pode ter.

## Versões

Só a `main` recebe correção.
