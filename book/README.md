# Livro

O livro desta linha: por que as tecnologias do Hermes são como são. Escrito em inglês, para eu estruturar e relembrar o que sei, aprender mais e treinar o inglês da entrevista.

Compilar: `latexmk -pdf main.tex` nesta pasta (gera `main.pdf`).

## Padrão visual

Definido em [hermes.sty](hermes.sty), a mesma família de caixas dos livros do Hefesto, do Monjolo e do Pítia.

- Caixa âmbar, `\begin{history}{ano · lugar}`: uma história, com quem, quando e o que forçou a ideia.
- Caixa azul, `\begin{concept}{nome}`: um conceito-chave, com o que é, o que corrige e o que custa.
- Caixa verde-azulada, `\begin{question}{pergunta}`: a pergunta boba que ninguém faz em voz alta, e a resposta.
- Caixa roxa, `\begin{reflection}{pergunta}`: uma pausa numa constatação que soa absurda.
- Caixa cinza, `\begin{etymology}`: de onde vêm as palavras.
- Código em `\begin{code}` (Java por padrão; `\begin{code}[language=Python]` para Python) e a saída de um comando em `\begin{terminal}`.
- Diagramas em TikZ, com uma cor por papel: cinza para a fonte dos dados, azul para os serviços (`hf/reader`), verde para armazenamento (`hf/store`), roxo para filas, barramentos e protocolos (`hf/bus`, setas `hf/push`) e vermelho para um custo ou uma proibição (`hf/pain`).

## Índice

O esqueleto segue a ordem em que o projeto chega a cada assunto. Cada capítulo tem, num comentário no `.tex`, o que está planejado para ele.

0. [How to Read This Book](chapters/00-how-to-read.tex): o aviso de que o livro é denso, o projeto que atravessa o livro (o processo de importação), a genealogia (Profibus, sagas, AOP), as cinco caixas, código e a legenda das cores.
1. [From the Inbox to a System](chapters/01-from-the-inbox.tex): *a escrever.* Invoices por e-mail, document understanding, OCR, expressões regulares.
2. [Queues](chapters/02-queues.tex): *a escrever.* SQS, at-least-once, long polling, visibility timeout, idempotência, DLQ, backoff.
3. [The Fieldbus Model](chapters/03-the-fieldbus-model.tex): *a escrever.* Barramento compartilhado, mestre e escravos, TX e RX, EventBridge.
4. [One Master](chapters/04-one-master.tex): *a escrever.* Orquestração e coreografia, sagas, roteiros, "why not Step Functions".
5. [The Code Around the Code](chapters/05-code-around-the-code.tex): *a escrever.* Spring, eventos da aplicação, AOP.
6. [Classifying by Similarity](chapters/06-classifying-by-similarity.tex): *a escrever.* Sistema Harmonizado e NCM, embeddings, FAISS, Bedrock.
7. [Functions Without Servers](chapters/07-functions-without-servers.tex): *a escrever.* Lambda, ETL numa função, SAM, LocalStack.
