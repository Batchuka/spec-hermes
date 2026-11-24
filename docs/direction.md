# Direction

These are hypotheses, not requests. Nobody asked for any of this yet.

I know where an architecture like this can end, because I built one at WM Trading: one master orchestrator, a TX bus and an RX bus on EventBridge, and SQS queues in front of each service. But users only know what they want after they see what they don't want. So the use cases are written one at a time. The next one is written only when the previous one is closed, from what it showed. Each line below is the pain that would usually push the system one step further. If the real story takes another path, this page changes, not the story.

| Act | A pain that could appear | Where it would push the system |
| --- | --- | --- |
| 1 · Each team asks for its own tool | Each team still works in spreadsheets and paper. | Independent services, each with its own data and its own screen. |
| 2 · Stop retyping | "Why do I have to type this proposal again?" | The first integration, done the naive way, and then queues. Services start reacting to each other without anyone deciding it. |
| 3 · One master | "Where is this proposal right now?" Nobody can answer. | An orchestrator that first only watches, then becomes the master: TX and RX, routes, compensation. |
| 4 · Volume arrives | Many proposals a day, and some get lost or processed twice. | Long polling, backoff, visibility timeout, dead-letter queues, idempotency. |
| 5 · People from outside | Dealers and farmers want to use the system. | Login and roles with Keycloak. |
| 6 · Show it and ship it | It has to run somewhere other than a laptop. | Containers, Terraform on AWS, a pipeline. |

## Written so far

- UC-01 · Sales registers a financing proposal (spec-hermes#16)
- UC-02 · Sales submits a proposal and Credit analyzes it (spec-hermes#17)
