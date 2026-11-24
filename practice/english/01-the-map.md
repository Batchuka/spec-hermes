# Kit 01 · The Map

Source: [`book/chapters/01-the-map.tex`](../../book/chapters/01-the-map.tex) · UC-01 ([spec-hermes#16](https://github.com/Batchuka/spec-hermes/issues/16)), built in [hermes-proposals#1](https://github.com/Batchuka/hermes-proposals/issues/1)

## 1. Pitch

I don't design the whole system on day one. Users only find out what they want after they use something, so I build what was asked and nothing more. That's YAGNI. In this project the first request came from Sales: proposals for tractor financing were lost in e-mails and spreadsheets. I wrote it as a use case, with what can go wrong and what is out of scope, and I record technical choices in ADRs. Then I built one small Spring Boot service with MongoDB, because every dealer sends different documents and they live inside the proposal. It has three REST endpoints, validation that returns a ProblemDetail, and tests on each layer, with a real MongoDB in Testcontainers.

## 2. Interview Q&A

**Q: How do you decide what to build first?**
I start from the pain of the people who asked. In this project the first request came from Sales: proposals arrived by e-mail and WhatsApp and lived in a spreadsheet, and documents got lost. So the first thing I built was a small service to register a proposal and its documents. Nothing else. I wrote the request as a use case, with the main steps, what can go wrong, and a section called "out of scope" for what nobody asked for. Login, credit analysis and integration with other systems were all out of scope. I follow YAGNI: you aren't gonna need it. Users only find out what they really want after they use the system, so anything I build before they ask is a guess. The way I keep that safe is small versions and tests. When the next request comes, I can change the code without fear.

**Q: Why did you choose MongoDB for this service?**
Because of the shape of the data. A financing proposal comes with documents, and every dealer sends different ones: an invoice, a proof of income, and sometimes a type we have never seen. In a relational database I would need a table per document type, or a generic key-value table that is hard to query. In MongoDB the documents live inside the proposal, in one document, and each one keeps its own fields. The proposal is always read as a whole, so embedding fits. I didn't use MongoDB for everything, though. The contracts service handles money and installments, and that needs transactions across tables, so it uses MySQL. I pick the database per service, based on the data that service owns.

**Q: How do you design and test a REST endpoint?**
I start from the resource and the use case. For proposals I have `POST /proposals` to create, `GET /proposals` to list and `GET /proposals/{id}` to read one. The status codes matter: 200 when it works, 404 when the id doesn't exist, and 400 when the input is wrong. For the 400, I validate the body with Bean Validation, and an exception handler returns a ProblemDetail, the standard format for errors, with the name of each field that failed. Then I test each layer on its own. A WebMvcTest checks the controller with the repository mocked, so I can prove an invalid proposal is rejected and nothing is saved. For the repository I don't mock; I use Testcontainers with a real MongoDB, because a mock can't tell me if the mapping really works.

## 3. Follow-ups

1. What is the difference between a use case and a user story?
2. What goes into an ADR, and when do you write a new one?
3. Why `Integer` and not `int` for a field in the request?
4. What happens to a decimal value inside a `Map<String, Object>` when you save it?
5. When would you not use MongoDB?

## 4. Glossary

| Term | Meaning | Example |
| --- | --- | --- |
| YAGNI | build only what was asked, when it is needed | Login was out of scope, so YAGNI said not to build it. |
| use case | the steps one person takes with the system, and what can go wrong | UC-01 has two extensions. |
| out of scope | what nobody asked for, written down | Credit analysis is out of scope for UC-01. |
| ADR | a short record of one technical decision and why | ADR 0001 decides one service per domain. |
| embedding | keeping related data inside the same document | The documents are embedded in the proposal. |
| endpoint | an address plus an HTTP method | `POST /proposals` is the endpoint that creates a proposal. |
| status code | the number that says how a request went | An unknown id returns a 404. |
| ProblemDetail | the standard JSON shape for an HTTP error | The 400 comes back as a ProblemDetail with the fields that failed. |
| record | a Java class that only holds data | The proposal is a record, so I don't need Lombok. |
| dependency injection | the framework creates an object and passes it in | The repository comes in through the constructor. |
| mock | a fake object that records how it was called | The repository is a mock in the controller test. |
| Testcontainers | a library that starts real services in Docker for tests | The repository test runs against a real MongoDB in Testcontainers. |

## 5. Frames

- `We chose ___ over ___ because ___.` → *We chose MongoDB over MySQL for proposals because every dealer sends documents with a different shape.*
- `Nobody asked for ___, so I ___.` → *Nobody asked for paging, so I left it out until the volume makes it necessary.*
- `I don't mock ___ because ___.` → *I don't mock the repository because a mock can't tell me if the mapping works.*
