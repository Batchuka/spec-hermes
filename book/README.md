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
- Card verde, `\begin{usecase}{UC-01}{título}{link da issue}`: um caso de uso como o negócio pediu, com o link para a issue. No texto, toda citação a um caso de uso usa `\uc{UC-01}` ou `\uc{UC-01 3a}` (o caso e o passo), no mesmo verde.
- Linha cinza `\incode{repo}{commit}{o que mudou}`, logo depois de um código ou diagrama: o commit onde aquela estrutura apareceu, com link para o GitHub.
- Código em `\begin{code}` (Java por padrão; `\begin{code}[language=Python]` para outras linguagens) e a saída de um comando em `\begin{terminal}`.
- Diagramas em TikZ, com uma cor por papel: cinza para a fonte dos dados, azul para os serviços (`hf/reader`), verde para armazenamento (`hf/store`), roxo para filas, barramentos e protocolos (`hf/bus`, setas `hf/push`) e vermelho para um custo ou uma proibição (`hf/pain`).
- Tabelas de banco desenhadas com as linhas: `hf/table` com o nome em `hf/tablename`, `\hfpk{id}` sublinha a chave primária, `\hfbad{valor}` marca em vermelho um fato no lugar errado e `hf/fk` é a seta da chave estrangeira.
- Um caminho passo a passo num diagrama: círculos azuis numerados com `hf/step` (`\node[hf/step, left=2mm of x] {1};`), e logo abaixo do desenho uma lista numerada com os mesmos passos.
- Seção **Going further** no fim do capítulo, antes de *In the interview*: o texto principal só cita um conceito em uma ou duas frases e aponta para ela (`Section~\ref{sec:...-further}`). Lá cada conceito ganha uma subseção, com desenhos, para o raciocínio principal não parar no meio.

## Índice

A ordem segue a história do sistema: os casos de uso (UC) do `spec-hermes`, escritos um por vez. Nada é construído antes de alguém pedir, e nenhum capítulo é planejado antes de a história chegar nele: um capítulo novo nasce quando um caso de uso mostra o que precisa ser explicado (o rumo provável está em `docs/direction.md`). Cada capítulo tem, num comentário no `.tex`, o ato, os casos de uso e o que está planejado.

0. [How to Read This Book](chapters/00-how-to-read.tex): o livro como um sênior ao lado de quem começa, o projeto passo a passo (o financiamento de um trator) e a origem dele na WM, por que o livro conta história (o exemplo da fila), as seis caixas, código, a legenda das cores e fatos e opiniões.
1. [The Map](chapters/01-the-map.tex): *Ato 1, UC-01, escrito.* YAGNI (Humphrey, Jeffries); caso de uso (Jacobson, Cockburn) e ADR (Nygard); o UC-01 de Vendas; bootstrap no Initializr (Boot 4, Java 21, Maven); por que MongoDB e embedding; os arquivos e REST (record, controller, POST/GET, 200/400/404, ProblemDetail); o que quebrou (`int` e Jackson 3, `@Valid` no elemento, `BigDecimal` num `Map`); testes por camada (`@WebMvcTest`, `@DataMongoTest` com Testcontainers). Going further: o Maven Wrapper (`mvnw`, a versão fixa do Maven, a permissão de execução no Git e o `.gitattributes`).
2. [Two Services and a Screen](chapters/02-two-services-and-a-screen.tex): *Ato 1, UC-02, escrito (sem a experiência do autor na WM; marcadores `TODO(user)` no `.tex`).* O microsserviço (o card do UC-02, monólito e domínio, Lewis e Fowler, MonolithFirst, a porta 8081, um banco por serviço e o ADR 0002); o MySQL e os índices (Codd, a tabela do Credit pelo `V1` e desenhada com linhas, normalização, chave estrangeira e join, a proposta em tabelas, schema on write e on read, migrations com Flyway (baseline e `ddl-auto: validate`), `EXPLAIN ANALYZE` antes e depois do índice, B-tree, wildcard index no Mongo); o Angular (AngularJS e Angular, SPA, componentes com input e output, signals (o ciclo desenhado do Register até a lista), o service com `HttpClient` e `inject`, o proxy de desenvolvimento e CORS, a barra de navegação). Going further: as formas normais desenhadas; InnoDB, a tabela como B+tree (clustered index e índice secundário). Três caixas de entrevista. Ficou de fora: embutir ou referenciar, `MongoTemplate`, Atlas e DocumentDB.
3. [Anatomy of a Service](chapters/03-anatomy-of-a-service.tex): *Ato 1, UC-02, a escrever.* A história do Spring, REST básico, ProblemDetail, validação e Testcontainers já estão no Cap. 1. Microsserviços, um banco por serviço, o modelo relacional e o Flyway foram adiantados para o Cap. 2. Aqui: injeção de dependência a fundo, a camada de serviço, PUT e PATCH, o JPA em si, teste unitário e `@DataJpaTest`.
