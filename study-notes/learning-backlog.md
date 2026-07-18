# Learning Backlog

## Current Topic

- [ ] Trace Spring's native event dispatch from `ApplicationEventPublisher` to the listener method.

## Core Topics

- [ ] Understand `ApplicationEventMulticaster` and listener registration.
- [ ] Understand the exact transaction phase and thread behavior of `ApplicationModuleListener`.
- [ ] Trace `PersistentApplicationEventMulticaster` and the Event Publication Registry.
- [ ] Understand how `ApplicationModules.of(...).verify()` discovers modules and checks dependencies.
- [ ] Understand named interfaces and package visibility as module APIs.
- [ ] Read module integration tests as executable architecture rules.

## Later Topics

- [ ] Study documentation generation from the application module model.
- [ ] Study module-level test support.
- [ ] Compare one event adapter, such as JDBC or Kafka, with the core event contract.
- [ ] Use a small experiment to observe duplicate or failed event handling.

## Explicitly Deferred

- Kafka, JMS, AMQP, and database-specific adapters in detail.
- Benchmarks and build infrastructure.
- Exhaustive configuration and every project module.
