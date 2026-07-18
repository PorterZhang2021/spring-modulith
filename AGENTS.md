# Study Workspace Instructions

## Purpose

This branch is a guided study workspace for understanding Spring Modulith as an example of high-quality framework engineering. The goal is to understand runtime flow, design decisions, tradeoffs, and reusable principles. Do not attempt to read every file.

## Baseline And Git

- Study branch: `study/2.1.0`
- Study baseline: tag `2.1.0`, commit `c75f173e`
- `upstream`: `git@github.com:spring-projects/spring-modulith.git`
- `origin`: `git@github.com:PorterZhang2021/spring-modulith.git`
- Keep source conclusions tied to the baseline version unless the user explicitly chooses another version.
- Do not push, merge, rebase, or switch the study baseline without the user's request.
- Preserve unrelated user changes.

## Study Interaction Protocol

For each topic, follow this order:

1. State one bounded topic and the business or runtime scenario.
2. Ask the user to design a rough solution before showing the implementation.
3. Trace the actual code in small slices, explaining each slice and asking one focused question at a time.
4. Compare the user's design with the repository design.
5. Discuss benefits, costs, alternatives, and failure modes.
6. Record shared conclusions, code evidence, open questions, and the next topic.

Do not dump a class list or explain the whole repository at once. If the user is confused, reset the current slice and explain the smallest relevant code unit before continuing.

## Study Notes

- `study-notes/00-project-map.md`: stable project overview and reading route.
- `study-notes/topics/`: one note per completed topic.
- `study-notes/good-code-observations.md`: reusable engineering principles backed by evidence.
- `study-notes/learning-backlog.md`: pending topics and deliberately deferred areas.

Notes should capture shared conclusions rather than a raw chat transcript. Every conclusion about behavior should include source-file evidence. Distinguish clearly between:

- behavior implemented by the code;
- behavior expected in a real business system but absent from the example;
- questions that remain unverified.

After a topic is complete, update the relevant topic note, observations, and backlog in the same study milestone when appropriate.

## Current Progress

The first completed topic is event-driven module integration in `spring-modulith-example-full`. The current next topic is the native Spring event dispatch chain:

```text
ApplicationEventPublisher
  -> ApplicationContext
  -> ApplicationEventMulticaster
  -> registered listener adapter
  -> listener method
```

After that, trace what Spring Modulith adds through `ApplicationModuleListener`, including transaction phase, asynchronous execution, and publication durability.

## Source Reading Priorities

Use this order unless the user changes the goal:

1. `spring-modulith-examples/spring-modulith-example-full`
2. `spring-modulith-api`
3. `spring-modulith-core`
4. `spring-modulith-events`
5. `spring-modulith-test` and `spring-modulith-junit`
6. Optional transport and persistence adapters

## Change And Verification Rules

- Keep study material in `study-notes/` and avoid changing production source code unless an experiment is explicitly planned.
- Use focused source inspection and tests to verify claims.
- For documentation-only changes, verify file paths, Git status, and rendered Markdown structure; no full build is required unless the change affects code.
- Before edits, state what will change. After edits, inspect the diff and report the commit and remote state.
