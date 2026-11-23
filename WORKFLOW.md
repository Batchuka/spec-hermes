# Como trabalho nesta linha

## Prazo

A entrevista técnica na John Deere é na quarta, 25/11/2026, às 13:30, toda em inglês. Até lá, o que mais vale é **explicar** a arquitetura em inglês. Código rodando é bônus, e AWS real é bônus do bônus.

## Papéis (modo híbrido)

- **Eu digito a lógica que vou explicar**: o código Java em `src/main` e `src/test` e os handlers Python em `lambdas/`.
- **O Claude escreve e commita o andaime**: `pom.xml`, Maven wrapper, `Dockerfile`, `docker-compose.yml`, scripts e templates de `infra/`, o `application.yml` inicial e a classe `*Application` vazia de cada módulo. Também escreve e commita a documentação deste hub.
- **O Claude guia.** Em cada versão ele responde assim: "arquivo:linha hoje está assim → mude para → por quê (1 a 3 linhas)", e diz como conferir. A teoria não fica na sessão: vai para o livro.

## Versões progressivas

Toda issue começa com uma **v0 ingênua**, escrita como um iniciante escreveria. Eu rodo, vejo quebrar, e cada versão seguinte corrige **uma** coisa que eu observei. As issues trazem as versões em checklist. A lista pode mudar no caminho.

## GitHub Flow

1. Uma branch por issue: `<tipo>/<n>-<resumo>`, por exemplo `feat/1-rx-polling`.
2. Um commit por versão.
3. Um comentário na issue por versão: o que quebrou, por quê e o que mudou. Em inglês, porque serve de treino.
4. PR em inglês, merge sem squash, para o histórico de versões ficar no `main`. A descrição do PR conta a história da issue em parágrafos curtos, que eu consiga ler em voz alta.

## Commits

[Conventional Commits](https://www.conventionalcommits.org/), em inglês. Branches, PRs, issues e código também em inglês.

```
feat(orchestrator): poll the RX queue with long polling

v1 of the RX consumer: short polling hit SQS in a tight loop and spent one
request per empty answer. WaitTimeSeconds=20 lets SQS hold the request until a
message arrives.

Refs #1
```

## HackerRank

De vez em quando entra um exercício "típico" ligado a um trecho do case (hash map para a idempotência, sliding window para o polling, heap para a similaridade...). Eu resolvo no HackerRank e versiono a solução em `practice/hackerrank/`, com uma nota dizendo a que parte do case ele se liga.

## Simbiose com o treino de inglês

O ADR, os capítulos e as descrições de PR servem de material para a sessão de prática de inglês. Por isso são escritos em frases curtas e diretas, com o vocabulário que um entrevistador usaria.

## Repositórios

Ficam lado a lado em `C:\Projetos\hermes\`:

| Pasta | O que é |
| --- | --- |
| `spec-hermes` | este hub: o livro, as decisões (`docs/adr/`), a prática e este fluxo |
| `hermes` | o código: monorepo Maven, Lambdas Python e infra |

## Rodar localmente

Tudo roda no LocalStack, que emula EventBridge, SQS, Lambda, SNS e S3 de graça. Os comandos estão no README do `hermes`.

## AWS de verdade

Nenhum recurso pago é criado sem o meu ok. Região `us-east-1`. Subir no ECS só para uma demo e derrubar logo depois.
