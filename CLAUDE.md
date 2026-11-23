# Linha Hermes

Leia `WORKFLOW.md` antes de qualquer coisa. A entrevista é na quarta, 25/11/2026, às 13:30, em inglês. Trabalhe pela prioridade do Project (P0 → P1 → P2) e trate cada capítulo como material de prática de inglês.

## Código (modo híbrido)

- O usuário digita a lógica: Java em `../hermes-*/src/**` e TypeScript em `../hermes-web/src/app/**`. Não edite esses arquivos; leia o que for preciso para guiar e revisar. O Terraform (`../hermes-infra/terraform/**`) ele também digita, com guia.
- O Claude pode escrever e commitar o andaime: poms, Dockerfile, CI, `../hermes-infra/local/**`, `application.yml` e a classe `*Application` vazia. E toda a documentação deste hub.
- Guie por versão: "arquivo:linha hoje está assim → mude para → por quê (1 a 3 linhas)", e depois como conferir. Sem teoria na sessão: a teoria vai para o capítulo.
- Antes de criar qualquer recurso pago na AWS, pergunte. Região `us-east-1`; o ambiente sobe para a demo e desce em seguida.

## Um chat por issue

1. Leia a issue e os comentários (`gh issue view <n> -R Batchuka/<repo> --comments`) e as issues citadas em "Depends on".
2. Descubra onde o usuário está: os itens marcados no checklist, os comentários, a branch da issue e os commits dela.
3. Se faltar alguma dependência, avise antes de começar.
4. Continue pelo próximo item não marcado.

## Livro (issues de capítulo)

- LaTeX em `book/`, um arquivo por capítulo em `book/chapters/`. MiKTeX e latexmk estão instalados. Depois de cada mudança, recompile o PDF e atualize o índice em `book/README.md`.
- Nas issues de capítulo, o Claude escreve o rascunho a partir da conversa com o usuário: primeiro pergunte o que ele sabe e o que fez de verdade (na WM ou em outros lugares) e use isso. Nunca invente experiência dele.
- História real: pessoas, datas, o problema que forçou cada ideia. Nada de histórias inventadas.
- Fatos exatos, opiniões categóricas. Inglês claro, do nível que o usuário consegue dizer numa entrevista. Tom leve, frases simples, sem frases de efeito com cara de texto de IA ("That isn't X. It's Y.", aforismos em sequência, fechamentos de impacto).
- Todo capítulo termina com 2 a 4 caixas `\begin{interview}{pergunta}`: respostas de 60 a 90 segundos, em primeira pessoa, faladas.
- Todo capítulo gera o kit `practice/english/NN-<slug>.md`, no formato do `WORKFLOW.md`. A sessão de treino de inglês lê esses arquivos.
- Todo exemplo de código que entrar no livro tem que ser rodado antes. Pouco código.
- Arquivos `.tex` se editam com o Edit, não com sed ou printf.

## ADRs

Formato do Nygard: Status, Context, Decision, Consequences, e uma seção "How I say it" de 60 a 90 segundos. Em inglês, curto, com o diagrama em mermaid.

## Fechamento

Só quando o usuário disser "close-out": comentário na issue, texto do PR e, se fizer sentido, release.
