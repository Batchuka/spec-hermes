# Livro

O livro desta linha: por que as tecnologias do Hermes são como são. Escrito em inglês, para eu estruturar e relembrar o que sei, aprender mais e treinar o inglês da entrevista. Cada capítulo fecha com perguntas de entrevista respondidas em voz alta, e gera um kit em [`../practice/english/`](../practice/english/).

Compilar: `latexmk -pdf main.tex` nesta pasta (gera `main.pdf`).

## Padrão visual

Definido em [hermes.sty](hermes.sty), a mesma família de caixas dos livros do Hefesto, do Monjolo e do Pítia, com uma caixa a mais.

- Caixa âmbar, `\begin{history}{ano · lugar}`: uma história, com quem, quando e o que forçou a ideia.
- Caixa azul, `\begin{concept}{nome}`: um conceito-chave, com o que é, o que corrige e o que custa.
- Caixa verde-azulada, `\begin{question}{pergunta}`: a pergunta boba que ninguém faz em voz alta, e a resposta.
- Caixa roxa, `\begin{reflection}{pergunta}`: uma pausa numa constatação que soa absurda.
- Caixa cinza, `\begin{etymology}`: de onde vêm as palavras.
- Caixa rosa, `\begin{interview}{pergunta}`: uma pergunta de entrevista e uma resposta de 60 a 90 segundos, para dizer em voz alta. Fecha todo capítulo.
- Código em `\begin{code}` (Java por padrão; `\begin{code}[language=Python]` para outras linguagens) e a saída de um comando em `\begin{terminal}`.
- Diagramas em TikZ, com uma cor por papel: cinza para a fonte dos dados, azul para os serviços (`hf/reader`), verde para armazenamento (`hf/store`), roxo para filas, barramentos e protocolos (`hf/bus`, setas `hf/push`) e vermelho para um custo ou uma proibição (`hf/pain`).

## Índice

A ordem segue a história do sistema: os atos e os casos de uso (UC) do `spec-hermes`. Nada é construído antes de alguém pedir. Cada capítulo tem, num comentário no `.tex`, o ato, os casos de uso e o que está planejado.

0. [How to Read This Book](chapters/00-how-to-read.tex): o livro como um sênior ao lado de quem começa, o projeto passo a passo (o financiamento de um trator) e a origem dele na WM, por que o livro conta história (o exemplo da fila), as seis caixas, código, a legenda das cores e fatos e opiniões.
1. [The Map](chapters/01-the-map.tex): *Ato 1, UC-01 a UC-05, a escrever.* Cada setor pede a sua ferramenta; um serviço por domínio e uma tela; a premissa (Humphrey e YAGNI).
2. [Documents](chapters/02-documents.tex): *Ato 1, UC-01, a escrever.* Modelo relacional e de documentos, MongoDB, Atlas.
3. [Anatomy of a Service](chapters/03-anatomy-of-a-service.tex): *Ato 1, UC-02, a escrever.* Microsserviços, Spring Boot, REST, camadas, validação, Spring Data, Flyway, testes.
4. [Money in Code](chapters/04-money-in-code.tex): *Ato 1, UC-03 e UC-04, a escrever.* `BigDecimal`, Price e SAC, transações ACID, pagar duas vezes.
5. [The Screen](chapters/05-the-screen.tex): *Ato 1, UC-05, a escrever.* Angular, uma tela para vários serviços.
6. [Queues](chapters/06-queues.tex): *Ato 2, UC-06 e UC-07, a escrever.* A primeira integração, ingênua; filas, SQS, SNS, idempotência; a coreografia que nasce sozinha.
7. [One Master](chapters/07-one-master.tex): *Ato 3, UC-08 a UC-11, a escrever.* O orquestrador nasce observador e vira mestre; TX e RX; roteiros; sagas.
8. [When Volume Arrives](chapters/08-when-volume-arrives.tex): *Ato 4, UC-12, a escrever.* Long polling, backoff, visibility timeout, DLQ; SQS, SNS e Kafka.
9. [Who Are You](chapters/09-who-are-you.tex): *Ato 5, UC-13, a escrever.* OAuth 2.0, OIDC, JWT, PKCE, Keycloak.
10. [Containers](chapters/10-containers.tex): *Ato 6, UC-14, a escrever.* Docker, imagens, a JVM no container.
11. [Infrastructure as Code](chapters/11-infrastructure-as-code.tex): *Ato 6, UC-14, a escrever.* Terraform, VPC, Fargate, ALB, RDS, CloudFront, custo.
12. [Pipelines](chapters/12-pipelines.tex): *Ato 6, UC-15, a escrever.* GitHub Actions, OIDC para a AWS.
