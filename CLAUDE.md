# Linha Hermes

Leia `WORKFLOW.md` antes de qualquer coisa. A entrevista é na quarta, 25/11/2026, às 13:30, em inglês. Trate cada capítulo como material de prática de inglês.

**A premissa:** o Hermes é uma história de casos de uso (UC-01, UC-02... no `spec-hermes`, campo Act do Project). O usuário não sabe o que quer até ver o que não quer, e nada é construído antes de ser pedido (YAGNI). Ao guiar uma issue, não antecipe a arquitetura final: resolva só o que o caso de uso pede, respeite o "Out of scope" dele e deixe a próxima dor aparecer sozinha. A integração só existe a partir do UC-06, e o orquestrador só a partir do UC-08.

## Código (modo híbrido)

- O usuário digita a lógica: Java em `../hermes-*/src/**` e TypeScript em `../hermes-web/src/app/**`. Não edite esses arquivos; leia o que for preciso para guiar e revisar. O Terraform (`../hermes-infra/terraform/**`) ele também digita, com guia.
- **Os repositórios de código começam vazios.** Não crie código, andaime nem issue de implementação antes de um caso de uso pedir. Quando, trabalhando num UC, ficar claro que algo é necessário: comente no UC o que foi descoberto, crie a issue no repositório certo (título `UC-NN · ...`, o porquê no topo, versões em checklist), pendure-a no UC como sub-issue e ponha no Project. Só com o ok do usuário.
- O andaime (poms, Dockerfile, CI, compose) nasce dentro de uma issue; o Claude pode escrevê-lo se o usuário pedir. A documentação deste hub é do Claude.
- Guie por versão: "arquivo:linha hoje está assim → mude para → por quê (1 a 3 linhas)", e depois como conferir. Sem teoria na sessão: a teoria vai para o capítulo.
- Antes de criar qualquer recurso pago na AWS, pergunte. Região `us-east-1`; o ambiente sobe para a demo e desce em seguida.

## Commits e PRs

Não assine nada: nenhum `Co-Authored-By` nos commits e nenhum rodapé "Generated with Claude Code" nos PRs, em nenhum repositório do Hermes.

## Um chat por issue

**O usuário conduz cada issue e cada capítulo.** Não escreva, não commite, não abra PR e não marque checklist sem ele mandar. Ao abrir o chat, faça só os passos abaixo, diga em poucas linhas o que entendeu e espere.

1. Leia a issue e os comentários (`gh issue view <n> -R Batchuka/<repo> --comments`), o caso de uso que ela implementa (a linha "Implements ...") e os casos de uso das pré-condições.
2. Descubra onde o usuário está: os itens marcados no checklist, os comentários, a branch da issue e os commits dela.
3. Se faltar alguma dependência, avise antes de começar.
4. Diga qual é o próximo item não marcado e espere o usuário decidir por onde ir.

## Livro (issues de capítulo)

- LaTeX em `book/`, um arquivo por capítulo em `book/chapters/`. MiKTeX e latexmk estão instalados. Depois de cada mudança, recompile o PDF e atualize o índice em `book/README.md`.
- Nas issues de capítulo, o Claude escreve o trecho que o usuário pedir, a partir do que ele contar sobre o que sabe e o que fez de verdade (na WM ou em outros lugares). Nunca invente experiência dele.
- História real: pessoas, datas, o problema que forçou cada ideia. Nada de histórias inventadas.
- **Tom: um sênior explicando para um novato em software. Claro, sempre.** Explique cada termo na primeira vez que ele aparece; o porquê antes do como; uma ideia por parágrafo, frases curtas; um exemplo concreto do caso do trator; fale com o leitor como "you"; nunca presuma que ele já sabe.
- Fatos exatos, opiniões categóricas. Inglês claro, do nível que o usuário consegue dizer numa entrevista. Tom leve, frases simples, sem frases de efeito com cara de texto de IA ("That isn't X. It's Y.", aforismos em sequência, fechamentos de impacto).
- Todo capítulo termina com 2 a 4 caixas `\begin{interview}{pergunta}`: respostas de 60 a 90 segundos, em primeira pessoa, faladas.
- Todo capítulo gera o kit `practice/english/NN-<slug>.md`, no formato do `WORKFLOW.md`. A sessão de treino de inglês lê esses arquivos.
- Todo exemplo de código que entrar no livro tem que ser rodado antes. Pouco código.
- Arquivos `.tex` se editam com o Edit, não com sed ou printf.

## ADRs

Formato do Nygard: Status, Context, Decision, Consequences, e uma seção "How I say it" de 60 a 90 segundos. Em inglês, curto, com o diagrama em mermaid.

## Fechamento

Só quando o usuário disser "close-out": comentário na issue, texto do PR e, se fizer sentido, release.
