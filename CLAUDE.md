# Linha Hermes

Leia `WORKFLOW.md` antes de qualquer coisa. O prazo é a entrevista de quarta, 25/11/2026, às 13:30: priorize o que ajuda o usuário a **explicar** a arquitetura em inglês.

- Modo híbrido. O usuário digita a lógica: Java em `../hermes/**/src/**` e Python em `../hermes/lambdas/**`. Não edite esses arquivos; leia o que for preciso para guiar e revisar. O Claude pode escrever e commitar o andaime do `../hermes` (poms, wrapper, Dockerfile, compose, `infra/`, `application.yml` inicial, a classe `*Application` vazia) e a documentação deste hub.
- Guie por versão: "arquivo:linha hoje está assim → mude para → por quê (1 a 3 linhas)", e depois como conferir. Sem teoria na sessão.
- Todo conceito novo vem com a genealogia: quando surgiu, que problema o forçou a existir, o que ele corrige da solução anterior.
- Antes de criar qualquer recurso pago na AWS, pergunte.
- Tudo o que é público (issues, PRs, commits, ADRs, livro) é em inglês. `WORKFLOW.md` e este arquivo ficam em português.

## Um chat por issue

Ao começar o chat de uma issue:

1. Leia a issue e os comentários (`gh issue view <n> -R Batchuka/<repo> --comments`) e as issues citadas em "Depends on".
2. Descubra em que versão o usuário está: os itens marcados no checklist, os comentários de versão, a branch da issue e os commits dela (`git -C ../hermes log --oneline`).
3. Se faltar alguma dependência, avise antes de começar.
4. Comece a guiar pela próxima versão não marcada.

## Livro

- LaTeX em `book/`. MiKTeX e latexmk estão instalados. Depois de cada mudança, recompile o PDF e atualize o índice em `book/README.md`.
- O livro é do usuário. Só escreva nele com pedido explícito.
- História real: pessoas, datas, o problema que forçou cada ideia. Nada de histórias inventadas.
- Nunca o código literal do projeto. O livro é uma conversa paralela sobre por que as tecnologias são como são.
- Fatos exatos, opiniões categóricas. Tom leve, frases simples, sem frases de efeito com cara de texto de IA ("That isn't X. It's Y.", aforismos em sequência, fechamentos de impacto).
- Inglês claro, do nível que o usuário consegue ler em voz alta numa entrevista.
- Todo exemplo de código que entrar no livro tem que ser rodado antes.
- Arquivos `.tex` se editam com o Edit, não com sed ou printf.

## ADRs

Formato do Nygard: Status, Context, Decision, Consequences. Em inglês, curto, com o diagrama em mermaid. Cada ADR deve servir de roteiro para uma resposta falada de 60 a 90 segundos.

## Fechamento

Só quando o usuário disser "close-out": comentário na issue, texto do PR e, se fizer sentido, release.
