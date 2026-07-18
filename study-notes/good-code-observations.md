# Good Code Observations

These are reusable observations extracted from completed study topics. They are principles to verify against more examples, not universal rules.

## Express Facts As Stable Contracts

`OrderCompleted` gives a name and a small payload to a meaningful domain fact. A consumer depends on that contract instead of the publisher's internal implementation.

Evidence: `example.order.OrderCompleted`.

## Keep Consumers Responsible For Their Reaction

The order module publishes the fact. The inventory module owns what to do after receiving it. This keeps order completion from accumulating inventory, points, notification, and logistics code.

Evidence: `OrderManagement` publishes; `InventoryManagement` handles.

## Distinguish Mechanism From Business Behavior

The example deliberately simulates inventory work with logging and a delay. The event delivery mechanism can be understood independently from the unfinished inventory business rules.

## Verify Claims Against Code

A reasonable business expectation such as "inventory should decrease" is not evidence that the example implements it. The listener body must be checked before recording that behavior as implemented.

## Record Tradeoffs, Not Slogans

"Use events for decoupling" is incomplete. The same choice also creates indirect control flow and requires decisions about transaction boundaries, retries, duplicate delivery, and observability.
