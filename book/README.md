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

A ordem segue a prioridade da entrevista (P0 primeiro). Cada capítulo tem, num comentário no `.tex`, o que está planejado para ele.

0. [How to Read This Book](chapters/00-how-to-read.tex): o aviso de que o livro é denso, o projeto (o financiamento de um trator) e a origem dele na WM, a genealogia, as seis caixas, código e a legenda das cores.
1. [The Map](chapters/01-the-map.tex): *P0, a escrever.* O processo de ponta a ponta, os quatro serviços, o mestre e os dois barramentos.
2. [Queues](chapters/02-queues.tex): *P0, a escrever.* SQS, at-least-once, long polling, visibility timeout, idempotência, DLQ, backoff; SQS, SNS e Kafka.
3. [One Master](chapters/03-one-master.tex): *P0, a escrever.* O modelo do fieldbus, EventBridge, orquestração e coreografia, sagas e compensação.
4. [Anatomy of a Service](chapters/04-anatomy-of-a-service.tex): *P0, a escrever.* Microsserviços, Spring Boot, REST, camadas, validação, Spring Data, Flyway, testes.
5. [Money in Code](chapters/05-money-in-code.tex): *P0, a escrever.* `BigDecimal`, Price e SAC, transações ACID, isolamento, SQL.
6. [Documents](chapters/06-documents.tex): *P1, a escrever.* Modelo relacional e de documentos, MongoDB, Atlas.
7. [Who Are You](chapters/07-who-are-you.tex): *P1, a escrever.* OAuth 2.0, OIDC, JWT, PKCE, Keycloak, resource server.
8. [The Screen](chapters/08-the-screen.tex): *P1, a escrever.* Angular, signals, HttpClient, login OIDC no navegador.
9. [Containers](chapters/09-containers.tex): *P1, a escrever.* Docker, imagens, a JVM no container, ECR.
10. [Infrastructure as Code](chapters/10-infrastructure-as-code.tex): *P1, a escrever.* Terraform, VPC, ECS Fargate, ALB, RDS, CloudFront, custo.
11. [Pipelines](chapters/11-pipelines.tex): *P2, a escrever.* GitHub Actions, OIDC para a AWS, deploy.
