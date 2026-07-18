# Event-Driven Module Integration

## Learning Goal

Understand how the order and inventory modules cooperate without the order module directly calling the inventory module.

## Initial Design Model

The initial design considered was:

```text
order completes
  -> persist order state
  -> inventory polls the order table
  -> read product and quantity
  -> decrease inventory
  -> persist inventory result
```

This is a valid design, but it couples inventory to the order database schema and introduces polling delay, duplicate-processing, and failure-coordination concerns.

## Actual Example Chain

```text
OrderManagement.complete(order)
  -> create OrderCompleted(orderId)
  -> ApplicationEventPublisher.publishEvent(...)
  -> ApplicationModuleListener receives the event
  -> InventoryManagement reads orderId
  -> example only logs and sleeps to simulate work
```

## Code Evidence

- `spring-modulith-examples/spring-modulith-example-full/src/main/java/example/order/OrderManagement.java`
- `spring-modulith-examples/spring-modulith-example-full/src/main/java/example/order/OrderCompleted.java`
- `spring-modulith-examples/spring-modulith-example-full/src/main/java/example/inventory/InventoryManagement.java`
- `spring-modulith-events/spring-modulith-events-api/src/main/java/org/springframework/modulith/events/ApplicationModuleListener.java`

## What The Example Actually Implements

`OrderCompleted` contains only an `OrderIdentifier`. The inventory listener reads that identifier and writes log messages. The example does not query order data or decrease inventory. It demonstrates the integration mechanism, not a complete inventory business process.

## Shared Conclusions

- An event expresses a business fact: the order has completed.
- An event is not a request telling one specific module which method to call.
- The publisher knows the event contract, but does not need to know all consumers.
- Multiple modules can subscribe to the same event.
- This is push-based communication, but it avoids a direct dependency on the receiver's implementation.
- `ApplicationModuleListener` is more than a plain listener in this version: it combines asynchronous execution with a transactional event listener and a new transaction for the handling work.
- Event-driven integration is useful when reactions can be independent and eventual, but it is not automatically better than a direct call.

## Important Tradeoffs

| Design | Strength | Cost |
| --- | --- | --- |
| Database polling | Simple persistence-based coordination | Polling delay and database/schema coupling |
| Direct module call | Immediate result and simple control flow | Publisher knows the concrete receiver |
| Event publication | Fan-out and lower implementation coupling | Indirect flow, failure handling, retries, and duplicate delivery need explicit design |

## Open Questions

- How does Spring register `@EventListener` and `@ApplicationModuleListener` methods?
- What is the call chain from `ApplicationEventPublisher` to the listener method?
- When exactly does the transactional listener run relative to the publishing transaction?
- How does the Event Publication Registry prevent a publication from being lost?
- Should a real event carry only an order ID or also the inventory-relevant order lines?
- Why does `OrderManagement` contain an injected `OrderInternal` dependency that is not used in this example?
