# Como trabalho nesta linha

## A premissa

O usuário não sabe o que quer. Ele só descobre quando vê o que não quer. Ninguém pede "integre todos os sistemas": cada setor pede a ferramenta que resolve a dor do seu dia, e a integração aparece quando alguém pergunta "por que isso não entra lá sozinho?". Watts Humphrey chamou isso de princípio da incerteza dos requisitos; Ron Jeffries resumiu o outro lado no YAGNI ("You aren't gonna need it"): não se constrói nada que não foi pedido. Quando a mudança chega, ela é feita da forma mais eficiente, com boas práticas.

Por isso o Hermes é uma **história de casos de uso**. A arquitetura final (mestre único, barramentos TX e RX) não é desenhada no começo: ela surge de demandas que vão ficando mais exigentes.

## A ordem

O [Project](https://github.com/users/Batchuka/projects/13) tem o campo **Act**, e a ordem é a dos casos de uso (UC-01, UC-02...):

1. **Cada setor pede a sua ferramenta** (UC-01 a UC-05): serviços independentes e uma tela.
2. **"Por que eu tenho que redigitar?"** (UC-06, UC-07): a primeira integração, ingênua; a coreografia nasce sozinha.
3. **Um mestre** (UC-08 a UC-11): o orquestrador nasce observador e vira mestre.
4. **O volume chega** (UC-12): 5.000 propostas por dia.
5. **Gente de fora** (UC-13): login e papéis.
6. **Mostrar e entregar** (UC-14 a UC-16): AWS, pipeline, extras.

A entrevista técnica na John Deere é na quarta, 25/11/2026, às 13:30, em inglês. Vou na ordem e no meu ritmo; o que estiver pronto até lá, ótimo.

## Três tipos de issue

### Caso de uso (no `spec-hermes`)

A demanda de um setor, no formato de Alistair Cockburn (*Writing Effective Use Cases*, 2000), simplificado: quem pediu e por quê agora, ator, objetivo, pré-condições, cenário principal, extensões e **fora do escopo** (o que ninguém pediu: o YAGNI escrito). As issues de implementação ficam penduradas nele como sub-issues, uma por repositório afetado.

### Implementação (nos repositórios `hermes-*`)

O título começa pelo caso de uso (`UC-06 · ...`). As versões v0 → vN estão em checklist (veja "Código", abaixo).

### Capítulo (no `spec-hermes`)

Cada capítulo explica os casos de uso de um ato.

Os capítulos andam **em ordem, um por vez, no meu ritmo**, sem chats em paralelo. Um chat **Opus** por capítulo, aberto nesta pasta quando eu chegar nele. Os chats das issues de código são **Sonnet**, e eu os crio conforme avanço. **Eu conduzo cada passo.** O Claude não escreve, não commita e não abre PR sem eu mandar. Ao abrir o chat, ele só lê a issue, diz em poucas linhas o que entendeu e espera. Depois, na ordem que eu decidir:

1. Eu conto o que sei e o que fiz de verdade na WM sobre o assunto. A minha experiência entra no capítulo.
2. O Claude escreve o trecho que eu pedir, em inglês, com a genealogia de cada conceito (quem, quando, que problema forçou a ideia) e o código mínimo, rodado.
3. O capítulo fecha com 2 a 4 caixas **In the interview**: uma pergunta de entrevista e uma resposta de 60 a 90 segundos, para dizer em voz alta.
4. Sai o **kit de inglês** em `practice/english/NN-<slug>.md` (formato abaixo).
5. Eu reviso, leio em voz alta e corrijo o que não soa como eu.

## Código

Modo híbrido:

- **Eu digito a lógica que vou explicar**: Java em `src/` e TypeScript do Angular em `src/app/`. Para o Terraform, eu digito com guia.
- **O Claude escreve e commita o andaime**: `pom.xml`, `Dockerfile`, CI, `docker-compose`, scripts do LocalStack, realm do Keycloak, `application.yml`, a classe `*Application` vazia. E toda a documentação deste hub.
- **O Claude guia por versão**: "arquivo:linha hoje está assim → mude para → por quê (1 a 3 linhas)", e como conferir.
- Toda issue começa numa **v0 ingênua**. Eu rodo, vejo quebrar, e cada versão seguinte corrige **uma** coisa que eu observei.

## O kit de inglês

Um arquivo por capítulo, em `practice/english/`, que a sessão de treino de inglês usa para gerar prática. Sempre com estas seções:

1. **Pitch**: o capítulo em 60 segundos, em primeira pessoa.
2. **Interview Q&A**: as mesmas perguntas das caixas do capítulo, com as respostas.
3. **Follow-ups**: 5 perguntas que um entrevistador faria em seguida, sem resposta.
4. **Glossary**: 8 a 12 termos, com uma linha de significado e uma frase de exemplo.
5. **Frames**: 3 construções reutilizáveis (`We chose ___ over ___ because ___.`).

## GitHub Flow

1. Uma branch por issue: `<tipo>/<n>-<resumo>`, por exemplo `feat/1-rx-polling` ou `docs/4-chapter-queues`.
2. Um commit por versão (código) ou por seção (capítulo).
3. Um comentário na issue por versão: o que quebrou, por quê e o que mudou. Em inglês, porque serve de treino.
4. PR em inglês, merge sem squash. A descrição do PR conta a história em parágrafos curtos, que eu consiga ler em voz alta.

## Commits

[Conventional Commits](https://www.conventionalcommits.org/), em inglês, com `Refs #N`.

```
feat(orchestrator): poll the RX queue with long polling

v1 of the RX consumer: short polling hit SQS in a tight loop and spent one
request per empty answer. WaitTimeSeconds=20 lets SQS hold the request until a
message arrives.

Refs #1
```

## HackerRank

De vez em quando entra um exercício "típico" ligado a um trecho do código. Eu resolvo no HackerRank e versiono a solução em `practice/hackerrank/`, com uma nota dizendo a que parte do case ele se liga.

## Pastas

Tudo lado a lado em `C:\Projetos\hermes\`: `spec-hermes`, `hermes-orchestrator`, `hermes-proposals`, `hermes-credit`, `hermes-contracts`, `hermes-web` e `hermes-infra`. O workspace `hermes.code-workspace` abre todas.

## Rodar localmente

```powershell
cd C:\Projetos\hermes\hermes-infra\local; docker compose up -d
```

Depois, `./mvnw spring-boot:run` em cada app. Os detalhes estão no README do `hermes-infra`.

## AWS

Tenho US$ 200 de crédito, válidos por 6 meses, e quero que rendam várias demos. O ambiente sobe com `terraform apply` para a demo e desce com `terraform destroy` logo depois, por cerca de US$ 0,20 por hora ligado. Nenhum recurso pago é criado sem o meu ok. Região `us-east-1`.
