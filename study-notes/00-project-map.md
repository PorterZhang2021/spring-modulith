# Spring Modulith Study Map

## Baseline

- Repository: `spring-projects/spring-modulith`
- Study branch: `study/2.1.0`
- Version: `2.1.0`
- Baseline commit: `c75f173e`
- Purpose: understand design decisions and reusable engineering principles, not read every file.

## What The Project Does

Spring Modulith helps Spring Boot applications organize domain-driven application modules and verify their boundaries. It also provides module-level testing, event integration, observability, and documentation generation.

## First Runtime Chain

```text
example.Application
  -> example.order.OrderManagement.complete()
  -> publish OrderCompleted
  -> example.inventory.InventoryManagement.on()
  -> module-local processing
```

## Recommended Study Order

1. `spring-modulith-examples/spring-modulith-example-full`
2. `spring-modulith-api`
3. `spring-modulith-core`
4. `spring-modulith-events`
5. `spring-modulith-test` and `spring-modulith-junit`
6. Optional adapters and infrastructure modules

## Reading Rule

For each topic, establish the user's design first, trace a small runtime chain, compare the two designs, and record only shared conclusions and unresolved questions.
