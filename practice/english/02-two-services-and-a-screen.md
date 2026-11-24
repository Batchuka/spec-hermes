# Kit 02 · Two Services and a Screen

Source: [`book/chapters/02-two-services-and-a-screen.tex`](../../book/chapters/02-two-services-and-a-screen.tex) · UC-02 ([spec-hermes#17](https://github.com/Batchuka/spec-hermes/issues/17)), built in [hermes-credit#1](https://github.com/Batchuka/hermes-credit/issues/1), [hermes-credit#5](https://github.com/Batchuka/hermes-credit/issues/5), [hermes-infra#2](https://github.com/Batchuka/hermes-infra/issues/2), [hermes-web#1](https://github.com/Batchuka/hermes-web/issues/1) and [hermes-web#2](https://github.com/Batchuka/hermes-web/issues/2) · Decision: [ADR 0002](../../docs/adr/0002-database-per-service.md)

## 1. Pitch

After Sales got its tool, the Credit team asked for theirs: analysts scored proposals in personal spreadsheets, with no history of decisions. Credit is a different domain, so it got a second service, not a new package inside the first one. Each service owns its database. Proposals keeps MongoDB, because the documents have fields nobody knows in advance. Credit uses MySQL, because an analysis always has the same fields, and its schema is versioned with Flyway. Indexes matter too: in a hundred thousand rows, an index turns a search by farmer from a full table scan into an index lookup, and EXPLAIN shows it. Then each team got a screen, in one Angular app: components, one API class per back end with HttpClient, and signals to keep the list up to date.

## 2. Interview Q&A

**Q: Why does each service have its own database?**
Because the database is part of the service, not something shared. In my project, Hermes, the proposals service and the credit service each own their data, and no service reads another service's database. If Credit needs something from Sales, it has to call the API of Sales. The reason is independence: Sales can change the shape of a proposal, or even change its database, and nothing outside breaks, as long as the API stays the same. If Credit read the Mongo collection directly, that collection would become a hidden contract. Owning the data also let each service pick the right engine. Proposals has documents with fields nobody knows in advance, so it uses MongoDB. Credit has analyses with fixed fields, so it uses MySQL. The price is that I can't join data from two domains in one query, and some data is copied, like the farmer's name. I wrote that decision down in an ADR.

**Q: How do you decide where to put an index?**
I start from the queries, not from the table. An index makes a search fast, but every insert and update has to maintain it, so I only index columns that someone really searches by. Then I check with EXPLAIN. Take the credit table: with a hundred thousand analyses, a search by farmer without an index is a full table scan. MySQL reads every row, and it takes about forty milliseconds. With an index on the farmer column, it becomes an index lookup and takes a few hundredths of a millisecond. The primary key is already an index, so searching by id is fast from the start. In the real service there is no index on farmer yet, because nobody searches by farmer yet. When that request comes, the index comes with it. In MongoDB it is the same idea, and for fields nobody knows in advance there is the wildcard index.

**Q: How does an Angular app talk to a back end?**
Through a service class that uses HttpClient. In my project I have one class per back end: ProposalsApi talks to the proposals service and AnalysesApi talks to the credit service. The components never call HTTP themselves. They get the API class by dependency injection, call a method, and subscribe to the answer. The answer goes into a signal, and the screen updates by itself. Errors come back as a ProblemDetail, so the form can show the message of the server, for example that income is required to score. In development, the Angular dev server has a proxy: it sends /proposals to one service and /analyses to the other. The browser sees one address, so I don't need CORS. The screens are separate, Sales and Credit, with a navigation bar between them, because each team only works with its own service for now.

## 3. Follow-ups

1. Why not start with a monolith and split it later?
2. What are the first three normal forms, and when would you denormalize on purpose?
3. Why did you replace `ddl-auto: update` with Flyway, and what does `baseline-on-migrate` do?
4. In InnoDB, what is the difference between the primary key and a secondary index?
5. What is a signal in Angular, and why does the template call `proposals()` with parentheses?

## 4. Glossary

| Term | Meaning | Example |
| --- | --- | --- |
| domain | one area of the business, with its own people, words and rules | Credit is a different domain from Sales, so it got its own service. |
| microservice | a small application that serves one domain and owns its data | The credit microservice runs on its own port with its own MySQL. |
| monolith | one application where everything lives together | A monolith is the simplest way to start, but adding a domain later means opening it. |
| database per service | no service reads another service's database | Credit asks the API of Sales; it never opens the Mongo collection. |
| normalization | changing tables so each fact lives in one place | Normalization would move the farmer's city to a farmers table. |
| foreign key | a column that holds the primary key of a row in another table | `farmer_id` is a foreign key to `farmers`. |
| schema on write | the database checks the shape when you save | MySQL refused `MAYBE` in the decision column. |
| schema migration | one numbered change to the schema, kept with the code | `V1__create_analyses.sql` is the first migration of Credit. |
| index | a sorted structure that finds rows without reading the whole table | The index on farmer turned a table scan into an index lookup. |
| full table scan | reading every row to find the ones that match | Without an index, EXPLAIN showed a full table scan of 100,000 rows. |
| component | one piece of an Angular screen: template, class and style | The Sales page is made of a form, a list and a detail component. |
| signal | a box that holds a value and tells Angular when it changes | When `load()` sets the signal, the list on the screen redraws. |

## 5. Frames

- `We chose ___ over ___ because ___.` → *We chose MySQL over MongoDB for credit because an analysis always has the same fields.*
- `The price is ___, and we accept it because ___.` → *The price is two database engines to run, and we accept it because each service stores data in the shape it really has.*
- `___ shows ___, so ___.` → *EXPLAIN shows a full table scan of a hundred thousand rows, so the column needs an index.*
