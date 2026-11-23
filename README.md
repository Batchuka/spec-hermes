# spec-hermes

> Hermes, the Greek god of trade and messengers, crossed every border carrying messages.

**Hermes** is a demo of an equipment financing process: a farmer asks for credit to buy a tractor, the proposal and its documents are read, the credit is analyzed, and if the answer is yes a contract is issued and the money goes to the dealer.

Its architecture is the one I designed at WM Trading, a foreign trade company, in 2023–2024 (sections 1.2 and 1.3 of my [portfolio](https://batchuka.github.io/)): domain microservices that do not know each other, a **single master** that drives every process, a **TX bus** for commands and an **RX bus** for answers. The original ran import processes; this one runs financing, small enough to read in an afternoon and cheap enough to run on AWS for an hour.

This hub holds the book, the decisions and the workflow.

## Repositories

| Repository | Role | Stack |
| --- | --- | --- |
| [`hermes-orchestrator`](https://github.com/Batchuka/hermes-orchestrator) | the master: runs the route of each proposal | Spring Boot, MySQL, EventBridge, SQS |
| [`hermes-proposals`](https://github.com/Batchuka/hermes-proposals) | proposals and their documents | Spring Boot, MongoDB |
| [`hermes-credit`](https://github.com/Batchuka/hermes-credit) | credit analysis: score, limit, suggested decision | Spring Boot, MySQL |
| [`hermes-contracts`](https://github.com/Batchuka/hermes-contracts) | contract, installments (Price or SAC), disbursement | Spring Boot, MySQL |
| [`hermes-web`](https://github.com/Batchuka/hermes-web) | the screen | Angular, Keycloak login |
| [`hermes-infra`](https://github.com/Batchuka/hermes-infra) | local stack and the AWS environment | Docker Compose, LocalStack, Keycloak, Terraform |
| [`spec-hermes`](https://github.com/Batchuka/spec-hermes) | this hub: book, ADRs, practice, workflow | LaTeX, Markdown |

Issues live in each repository and on the [Hermes project](https://github.com/users/Batchuka/projects/13). How I work is in [`WORKFLOW.md`](WORKFLOW.md).

## Architecture

Decisions are in [`docs/adr/`](docs/adr/). The overall architecture is [ADR 0001](docs/adr/0001-architecture.md).

```mermaid
flowchart LR
    user(["user"])
    cf["CloudFront<br/>HTTPS"]
    web["Angular<br/>S3"]
    alb["ALB"]
    kc["Keycloak"]
    orch["orchestrator<br/>the master"]
    prop["proposals"]
    cred["credit"]
    con["contracts"]
    tx{{"EventBridge TX"}}
    rx{{"EventBridge RX"}}
    cq[["SQS: one command<br/>queue per service"]]
    rxq[["SQS hermes-rx"]]
    mysql[("RDS MySQL<br/>one database per service")]
    mongo[("MongoDB Atlas M0")]

    user --> cf --> web
    cf -->|"/api, /auth"| alb --> orch & prop & cred & con & kc
    orch -->|command| tx --> cq --> prop & cred & con
    prop & cred & con -->|event| rx --> rxq --> orch
    orch & cred & con & kc --> mysql
    prop --> mongo
```

## Book and practice

- [`book/`](book/): why the technologies in this project are the way they are. Every chapter ends with interview questions answered out loud.
- [`practice/english/`](practice/english/): one English practice kit per chapter.
- [`practice/hackerrank/`](practice/hackerrank/): typical coding exercises, each tied to a part of the code.
