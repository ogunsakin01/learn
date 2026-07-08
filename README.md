# The Senior PHP Engineer Build Plan

A guide to building one project that forces you to learn the core engineering depth a senior PHP engineer is tested on:

1. PHP and Laravel depth: architecture, SOLID, tactical Domain-Driven Design, DTOs, validation, dependency injection, design patterns.
2. SQL depth on PostgreSQL (the database you will build on) plus Eloquent: schema design, MVCC and isolation, locking, indexing, query performance, and the PostgreSQL-versus-MySQL comparisons interviewers love to probe.
3. Testing depth, the part most candidates are weak on, so it is where you stand out.
4. System design depth, the separate breadth-and-articulation muscle.

The project is a shared-bill payment app: several people pay into one pooled balance until a target amount is covered. Money plus concurrency is the densest training ground there is, because it forces idempotency, locking, isolation, transactional integrity, and a real aggregate boundary all at once. Keep the product boring and small. The hard parts are the only point.

### Why PostgreSQL

You build this on PostgreSQL, not the Laravel default. It keeps coming up in interviews, its concurrency model is the canonical teaching ground for the hardest topics here, and being able to compare it to MySQL out loud is itself a senior signal. Laravel speaks to Postgres through the same schema builder and Eloquent, so the switch costs you almost nothing and teaches you a lot. Throughout the plan you will learn the Postgres way and the MySQL contrast side by side.

---

## The one rule that makes this work

AI writes nothing for you. Not code, not the schema, not the migrations, not the design, not the fix. You design and write every part yourself.

AI gets exactly two jobs, and neither produces anything you keep:

1. Teach you a concept before you build it.
2. Review and interview you after you build it, pointing at what is wrong and where to learn the fix, never writing the fix.

If you catch yourself pasting code something else wrote, delete it and write it yourself. The understanding lives in the struggle. Let anything do the struggling for you and you are back where you started: a project full of things you cannot explain. Running framework commands that scaffold empty stubs is fine, because that is not a decision. The contents of every file are yours.

---

## Working with Claude Code: the daily loop

Use Claude Code as a tutor and a hostile interviewer, never as an engineer. The loop for every piece of work:

1. Concept first. Run Prompt 1 to learn the idea and the tradeoffs before you build.
2. Build it yourself. No AI.
3. Review. Run Prompt 2 so it points at what is weak without fixing it.
4. Research and fix yourself, using the search terms it gave you.
5. Grill. Run Prompt 3 so it interviews you on your decisions.
6. Go deeper. Run Prompt 4 for a reading path.

Commit to git after every feature, before you run Prompt 2. A small, focused diff is what makes the review sharp, and the habit of clean commits is itself a senior signal.

The prompts are written so Claude Code does not edit your files or hand you solutions, and so SOLID, DDD, and PostgreSQL are checked everywhere. Copy them, fill the brackets.

### When in the day to run each prompt

There is a rhythm. Prompt 1 opens new work, Prompts 2, 3, and 4 close it.

- Prompt 1 (learn the concept): at the START of a day, before you write anything new. Never run it after you have already built the thing, that defeats the point.
- Prompt 2 (review): at the END of a day on which you wrote code, after you have committed. Then spend the next morning fixing what it flagged, by yourself.
- Prompt 3 (grill): at the END of the last day of a feature, once it works and you have already acted on the review. This is your mock interview for that feature.
- Prompt 4 (go deeper): at the END of a topic, when you want mastery beyond passing. Good for a lighter day or a weekend.

Each week below has a "Prompt rhythm" line telling you exactly which prompt to run on which day, and whether at the start or the end.

### Prompt 1: Concept first (learn before building)

```
I am learning [TOPIC] by building it myself in a Laravel project on PostgreSQL. Do not
write any code, do not design my solution, and do not edit any files. Explain the
concept from first principles, the two or three standard approaches with the tradeoffs
between them, and the specific failure each approach prevents or causes. Where it is
relevant, explain how PostgreSQL handles it and how that differs from MySQL, and how it
relates to SOLID principles and to tactical DDD (aggregates, value objects,
repositories, domain services, domain events). Then list the exact things I should be
able to explain out loud once I have built it. Stop there. I will build it and come back.
```

### Prompt 2: Code review (point, do not fix)

```
Review the code I just wrote at [PATHS, or "in the latest git diff"]. Act as a senior
engineer doing a strict review. Hard rules: do not write corrected code, do not show me
the fix, do not edit any files.

Check specifically for:
- SOLID violations (name the principle and where it breaks).
- DDD problems: domain logic leaking into controllers or models, anemic domain objects,
  missing or wrong aggregate boundaries, persistence concerns bleeding into the domain,
  repositories that are just pass-throughs.
- PostgreSQL-specific issues: wrong isolation level for the operation, wrong lock type,
  wrong or missing index type, queries that will not scale, misuse of transactions.
- Laravel craft: fat controllers, validation in the wrong layer, missing DTOs at
  boundaries, N+1 queries, Eloquent used where the query builder fits better.

For each issue: name it, explain why it matters at a senior level, rate it (blocker /
important / minor), and give me the search terms or the exact resource to learn the
correct approach myself. End with the top three things to fix first, in order. I will
research and fix them on my own.
```

### Prompt 3: Grill me (interview on decisions and tradeoffs)

```
I just built [FEATURE]. Interview me like a skeptical senior interviewer who doubts my
choices. Pick the real design decisions in my code and challenge them one at a time:
why this over the alternative, what breaks under load or concurrency, what the tradeoff
is. Push on my SOLID and DDD decisions (aggregate boundaries, where I put domain logic,
why a value object here, why a repository there) and on my PostgreSQL choices (isolation
level, lock type, index type, and how MySQL would differ). Ask one question, wait for my
answer, then push harder or correct me before the next. Do not accept vague answers,
force me to be specific. Do not write or fix any code. At the end, tell me which of my
answers were weak and exactly what to study.
```

### Prompt 4: Where to learn more (reading path)

```
I just finished building [TOPIC]. Give me a structured reading path from fundamentals to
advanced, naming the canonical books, official docs, and articles, and include the
PostgreSQL, SOLID, and DDD angles where relevant. Then give me five questions a senior
engineer must be able to answer about this topic, and tell me where each answer is found
without answering them for me. Do not write code.
```

A note on the schedule: "8 weeks" counts sessions, not calendar weeks. Every day here means designing and writing the thing yourself with no AI, on top of real reading (DDIA chapter 7, SQL Antipatterns, the Vernon books). At a sustainable part-time pace that is months, not weeks, and that is fine. Treat each day as a session, not a calendar rule. Miss a day, just continue. The number that matters is not how fast you finish, it is whether you can defend every line at the end.

---

## Craft reference: read once, apply throughout

### SOLID, mapped to this project

Do not recite SOLID. Point at it in your own code:

- Single responsibility: the controller only coordinates, the Form Request only validates input shape, the service holds one use case, the value object holds one concept. If a class has two reasons to change, split it.
- Open/closed: adding Paystack next to Stripe without touching a single caller. New behaviour by adding a class, not editing existing ones.
- Liskov substitution: any PaymentGateway implementation, real or fake, is swappable without the caller knowing or breaking.
- Interface segregation: the gateway interface stays minimal. No client is forced to depend on methods it does not use. No fat "do everything" interfaces.
- Dependency inversion: your code depends on the gateway interface and the repository interface, never on the concrete Stripe class or Eloquent directly. The container wires the concretes in.

The review and grill prompts already check these. Make yourself able to point at a real line for each letter.

### Tactical DDD, mapped to this project

Full strategic DDD (multiple bounded contexts, context maps) is overkill for a solo project, and saying so in an interview is itself a sign of maturity. What applies here is tactical DDD, and it maps cleanly:

- Ubiquitous language: name everything in domain terms and use those same words in code, tests, and DESIGN.md. A "Bill", a "contribution", a "settlement". Not "record" and "row".
- Aggregate root: the Bill (the pooled balance) is your aggregate root and your consistency boundary. It owns the invariant that contributions cannot exceed the target and that a settled bill takes no more money. This is not decoration: it is exactly what the concurrency weeks protect with locking.
- Value objects: Money (amount in minor units plus currency), and an idempotency key, immutable and compared by value, not identity.
- Domain events: the Bill raises PaymentReceived and BillSettled. Listeners react. This is the events week, given a domain meaning.
- Repositories: the domain talks to a BillRepository interface, not to Eloquent. Persistence lives behind the interface. This is dependency inversion and DDD meeting in the same place.
- Domain services: logic that does not belong to a single entity lives in a domain service, not smeared across controllers.

The honest tension: Laravel's Eloquent is the Active Record pattern, where the model knows how to persist itself. Classic DDD prefers persistence-ignorant domain objects (the Data Mapper pattern, which Doctrine uses). A senior must be able to discuss this. For this project, stay pragmatic: keep Eloquent, but put domain logic in the aggregate and domain services, hide persistence behind repository interfaces, and keep models from becoming dumping grounds. Know why a purist would split the domain model from the persistence model, and what that costs.

### Validation: where it goes

- Input shape (required, types, ranges, formats) belongs in a Form Request, one per endpoint. Not in the controller. Authorization can live there too.
- Domain rules that need database state or business logic ("this bill is already settled") belong in the domain, enforced by the aggregate or a domain service, not in the Form Request. The Form Request guards the shape, the aggregate guards the invariant. Knowing this split is a common interview probe.

### DTOs: where they earn their place

A DTO is a typed object you pass across a boundary instead of an array. Three boundaries here: validated request into the service (a PaymentData DTO), service into gateway (a typed charge input), and gateway back into service (a normalized ChargeResult, so Stripe and Paystack return the same shape). The normalized result is what makes the two-provider design clean. Build your first DTOs as plain readonly PHP classes so you learn the concept, then look at spatie/laravel-data to see it at scale.

### Eloquent vs Query Builder vs raw SQL

Eloquent for domain logic and relationships, the query builder for complex aggregations and performance-critical reads where you do not need full models, raw SQL only when neither fits and always parameterized. The senior point is knowing the cost: Eloquent hydrates objects and can hide N+1s, the query builder is leaner. Pick deliberately. With repositories in place, this choice lives inside the repository and the domain never sees it.

### Cross-cutting concerns you must not skip

These do not get their own week because they belong everywhere. A payments app that ignores them is not a senior project. Apply each where noted.

- Security (apply in weeks 2 and 7). A money endpoint is a target. Never pass raw request input into Eloquent create or update, guard mass assignment with explicit assignment or DTOs, this is the most common Laravel hole. Keep queries parameterized. Keep Stripe and Paystack keys in the environment, never in git. Verify webhook signatures (Stripe's signature, Paystack's x-paystack-signature HMAC SHA512) before trusting any payload, an unverified webhook lets anyone mark a bill paid. Rate-limit the payment endpoint with throttle middleware. Never log card data or secrets, and know why pushing card handling to the provider keeps you out of PCI scope. Be able to walk the OWASP Top 10 at a high level.
- The dual-write problem (name it in weeks 2 and 7). You cannot atomically commit a database transaction and call an external payment API in the same breath. If one succeeds and the other fails, your state diverges. This is the deep reason idempotency and ordering matter: commit local state first, make the foreign call retry-safe with an idempotency key, and reconcile through webhooks. The pattern that generalizes it is the transactional outbox. You need not build the full outbox, but be able to explain the problem and the shape of the fix. Brandur's article is exactly this.
- Safe schema changes (apply in week 5). A migration that is fine on an empty table can lock a production one. On Postgres, CREATE INDEX CONCURRENTLY builds an index without taking a write lock, and additive migrations (add a nullable column, backfill, then enforce) are how you ship without downtime. Be able to explain why a naive migration is dangerous and how you would do it safely.
- Observability and the audit log (apply in weeks 7 and 8). Seniors are expected to talk about running the thing. Add structured logging around payments, know where an error tracker like Sentry fits, and build an append-only audit log of every state change on a bill, which a payments domain needs for reconciliation and disputes. Be able to discuss logs versus metrics versus traces.
- API design (apply in week 2). Correct status codes, which HTTP methods are idempotent by definition, a consistent error response shape, and a versioning strategy. Small things, but a sloppy API reads as junior.
- PHP language and standards (throughout). The project is framework-heavy, but interviews probe pure PHP. Follow PSR-12 formatting and PSR-4 autoloading, understand Composer, and be ready for language questions outside Laravel: generators, traits, late static binding, readonly and enums, and the type system.

---

## The 8-week build plan

Each week states a goal, daily sessions, the threads to apply (SOLID, DDD, Postgres), what to read, and how you know you are done. Run Prompt 1 before building, Prompt 2 after, Prompt 3 to be interviewed, Prompt 4 to go deeper. Weeks 1 to 8 are the core. Weeks 9 to 13, further down, are the optional rounding-out for a complete senior profile.

### Week 1: Design the schema yourself on PostgreSQL

Goal: a data model you designed and can defend, on Postgres, with the domain language set.

- Day 1: Install Laravel, PostgreSQL, and Pest. Point Laravel at the pgsql driver. Read normalization basics until you know why you normalize and when you would not.
- Day 2: Money handling. Research why floats are wrong for currency, and decide between integer minor units and Postgres numeric. Design a Money value object on paper. This is your first DDD value object.
- Day 3: Establish the ubiquitous language. Name the entities (Bill, contribution, settlement) and sketch relationships only, no columns. Identify which entity is the aggregate root.
- Day 4: Turn the sketch into columns and Postgres types: prefer GENERATED ALWAYS AS IDENTITY over SERIAL, consider native enums versus PHP backed enums for status, UUIDs where they fit, and a version column for optimistic locking later. Decide foreign keys, unique constraints, and not-null rules, and push integrity into the database.
- Day 5: Write the migrations by hand and run them.
- Day 6: Write a paragraph defending every table, column, constraint, and type choice.
- Day 7: Run Prompt 3 on your schema and aggregate boundary.

Prompt rhythm: Day 1 start, Prompt 1 on data modeling and schema design. Day 5 end, Prompt 2 on your migrations, then fix on Day 6. Day 7, Prompt 3 to grill the schema, then Prompt 4 if you want to go deeper on indexing.

Threads: DDD (ubiquitous language, aggregate root, first value object), Postgres types. Reading: SQL Antipatterns (Karwin), normalization, Use The Index Luke (start), PostgreSQL docs on data types, Domain-Driven Design Distilled (Vernon) for the vocabulary.

Done when: migrations exist, the aggregate root is named, and you can defend every column and type out loud.

### Week 2: Validation and the idempotent endpoint

Goal: a validated, idempotent payment endpoint with the domain layer started.

- Day 1: Learn Form Requests. Validate input shape there.
- Day 2: Draw the line between input validation (Form Request) and domain invariants (the Bill aggregate). Decide what lives where.
- Day 3: Run Prompt 1 on idempotency. Understand the retry problem and the unique-constraint approach versus the broken check-then-insert.
- Day 4: Build the idempotent endpoint: store the key before processing, return the stored result on a repeat.
- Day 5: Add your first DTO, PaymentData, from the validated request into a service. Keep the charge logic in a domain service, not the controller.
- Day 6: Run Prompt 2. Research and fix yourself.
- Day 7: Run Prompt 3 on idempotency and on where you put the logic.

Prompt rhythm: Day 1 start, Prompt 1 on validation layering. Day 3 start, Prompt 1 on idempotency. Day 6 end, Prompt 2 on the endpoint. Day 7 end, Prompt 3 to grill idempotency, then Prompt 4 to go deeper.

Threads: SOLID (SRP across controller, request, service), DDD (value objects, domain service), DTOs. Also apply the security and API design items from the cross-cutting section (mass assignment, rate limiting, secrets, status codes). Reading: Laravel validation and Form Requests, Stripe idempotency docs, Brandur Leach's idempotency article, PHP readonly classes.

You must be able to answer: what idempotent means, why you store the key before processing, why check-then-insert breaks under concurrency, and which validation belongs in the request versus the aggregate.

Done when: the same request twice produces one charge, and the logic sits in the right layer.

### Week 3: Concurrency part one, MVCC, isolation, pessimistic locking (the centerpiece)

Goal: understand isolation deeply on Postgres and ship pessimistic locking. The most important fortnight.

- Day 1: Read Designing Data-Intensive Applications chapter 7, first half. Run Prompt 1 on lost updates and on PostgreSQL MVCC.
- Day 2: Write a failing test that fires two concurrent contributions into one Bill and watch the balance come out wrong. Do not fix it. Seeing the race fail is the lesson.
- Day 3: Learn Postgres isolation levels and how they differ from MySQL. Postgres defaults to READ COMMITTED, its REPEATABLE READ is snapshot isolation, and its SERIALIZABLE uses Serializable Snapshot Isolation to catch write skew. MySQL InnoDB defaults to REPEATABLE READ and uses next-key locks. Know this contrast cold.
- Day 4: Implement pessimistic locking with SELECT FOR UPDATE inside a transaction. Learn that Postgres readers do not block writers because of MVCC, and what FOR UPDATE actually locks. Hold onto the one sentence that ties the week together: the same MVCC that lets readers not block writers is exactly why the naive check-then-update loses the update under READ COMMITTED, because each transaction reads its own snapshot and neither sees the other's write until too late. That single line is a great interview answer. Make the test pass.
- Day 5: Read about deadlocks and add retry handling. Note that the lock protects the aggregate invariant, which is the DDD reason the boundary matters.
- Day 6: Run Prompt 2, fix yourself.
- Day 7: Run Prompt 3 on isolation, MVCC, and locking.

Prompt rhythm: Day 1 start, Prompt 1 on lost updates, MVCC, and isolation. Day 6 end, Prompt 2 on your locking, then fix. Day 7 end, Prompt 3 to grill isolation and locking, then Prompt 4 (this is the topic most worth the extra depth).

Threads: DDD (aggregate as consistency boundary), Postgres (MVCC, isolation, lock modes). Reading: DDIA chapter 7, PostgreSQL docs on concurrency control and transaction isolation, MySQL docs on InnoDB locking for the contrast, Fowler's offline lock patterns.

You must be able to answer: what anomaly each isolation level prevents, how Postgres SERIALIZABLE differs from REPEATABLE READ, how Postgres and MySQL defaults and locking differ, and what FOR UPDATE locks.

Done when: the race test fails without the lock and passes with it, and you can compare the two databases on isolation out loud.

### Week 4: Concurrency part two, optimistic locking and the first real tests

Goal: ship optimistic locking and prove both strategies.

- Day 1: Run Prompt 1 on optimistic locking. Understand the version-column approach as a guard on the aggregate.
- Day 2: Implement optimistic locking with the version column from week 1.
- Day 3: Write a test that forces the conflict and asserts the second writer is rejected.
- Day 4: Compare both strategies and write notes on when each is right by contention level. Mention Postgres advisory locks as a third tool and when you would reach for them.
- Day 5: Learn Pest. Refactor tests to be clean, with factories and a fresh database per test.
- Day 6: Run Prompt 2 on your tests.
- Day 7: Run Prompt 3 on pessimistic versus optimistic.

Prompt rhythm: Day 1 start, Prompt 1 on optimistic locking. Day 6 end, Prompt 2 on your tests. Day 7 end, Prompt 3 to grill the pessimistic-versus-optimistic tradeoff, then Prompt 4.

Threads: DDD (protecting the invariant), Postgres (advisory locks), testing. Reading: as week 3 plus Pest docs and the Postgres docs on advisory locks.

You must be able to answer: pessimistic versus optimistic and when each, what advisory locks are for, and at what contention optimistic becomes the wrong choice.

Done when: both strategies are built and tested and you can argue the tradeoff.

### Week 5: Queries, Eloquent vs query builder, pagination, indexing on PostgreSQL

Goal: a fast, correct feed and real Postgres query knowledge, with the repository pattern introduced.

- Day 1: Learn Eloquent versus query builder versus raw, and decide where each fits. Introduce a BillRepository interface so the domain stops touching Eloquent directly. This is dependency inversion and DDD in one move.
- Day 2: Build the contribution feed. Deliberately create an N+1, prove it with query logging.
- Day 3: Fix the N+1 with eager loading and understand why it happened.
- Day 4: Learn keyset pagination, replace offset with a cursor on an indexed column. Look at Postgres window functions and CTEs for any reporting view.
- Day 5: Postgres indexing. Learn B-tree versus partial, expression, and covering (INCLUDE) indexes, and where GIN and JSONB would apply. Read EXPLAIN ANALYZE before and after, and learn the leftmost-prefix rule.
- Day 6: Run Prompt 2 on queries, indexes, and the repository.
- Day 7: Run Prompt 3 on offset versus keyset, N+1, EXPLAIN ANALYZE, index types, and Eloquent versus query builder.

Prompt rhythm: Day 1 start, Prompt 1 on Eloquent versus query builder, repositories, and indexing. Day 6 end, Prompt 2 on queries, indexes, and the repository. Day 7 end, Prompt 3 to grill, then Prompt 4 on Postgres indexing depth.

Threads: SOLID (DIP via repository), DDD (repository), Postgres (index types, EXPLAIN ANALYZE, window functions). Also apply safe schema changes (CREATE INDEX CONCURRENTLY, additive migrations) from the cross-cutting section. Reading: Use The Index Luke, PostgreSQL docs on indexes and on EXPLAIN, Laravel pagination and eager loading.

You must be able to answer: why offset pagination is slow and unstable, what N+1 is and how you spot it, how to read EXPLAIN ANALYZE, when you would use a partial or covering or GIN index, and why the repository sits between domain and Eloquent.

Done when: the feed uses keyset pagination, the N+1 is fixed and explained, every index is justified by EXPLAIN ANALYZE, and the domain talks to a repository.

### Week 6: Architecture, the two-provider gateway, SOLID and DDD in full

Goal: defensible architecture serving Stripe and Paystack, with the tactical DDD layer complete.

- Day 1: Learn the service container and dependency injection. Run Prompt 1 on dependency inversion and the Active Record versus Data Mapper tension.
- Day 2: Define the gateway interface. Write the fake implementation first.
- Day 3: Write the Stripe implementation, mapping its response into your normalized ChargeResult DTO.
- Day 4: Write the Paystack implementation against the same interface and DTO. Notice you changed no callers, that is open/closed live.
- Day 5: Pull everything into shape: thin controllers, domain services for use cases, the aggregate enforcing invariants, repositories for persistence, DTOs at the boundaries. Walk through each SOLID letter and point at a real line. Then, with the full tactical layer in front of you, articulate where it is overkill and say so out loud. A shared-bill app has essentially one aggregate. Wheeling in repositories, domain services, domain events, and value objects on ground this thin risks learning to *perform* DDD ceremony rather than feel where it earns its place, and a good interviewer smells cargo-culting instantly. You built the full layer here because the point is to learn the moves, not because an app this size demands them. The senior signal is being able to say exactly that: "I applied the whole pattern to learn it, but for a service this small a single service class over the model would ship the same behaviour with less machinery, and here is the size and team at which the machinery starts paying for itself." Knowing when *not* to reach for DDD is as much a senior signal as knowing the patterns.
- Day 6: Run Prompt 2 on the architecture.
- Day 7: Run Prompt 3 on DI, open/closed, Liskov, the strategy pattern, aggregate design, and Active Record versus Data Mapper.

Prompt rhythm: Day 1 start, Prompt 1 on dependency injection and Active Record versus Data Mapper. Day 6 end, Prompt 2 on the architecture. Day 7 end, Prompt 3 to grill SOLID and the DDD boundaries, then Prompt 4.

Threads: SOLID (all five), DDD (aggregate, domain services, repositories, the persistence tension), DTOs, strategy pattern. Reading: Laravel container, providers, and contracts, Refactoring Guru on strategy, Fowler on dependency injection, Vaughn Vernon's Implementing Domain-Driven Design, Matthias Noback's writing on DDD in PHP, spatie/laravel-data to compare.

You must be able to answer: what DI is and why the container, how you add a provider without touching callers, a real example of each SOLID principle from your code, why the Bill is the aggregate, the tradeoff between Active Record and Data Mapper for DDD, and where the tactical DDD layer is overkill for an app this size.

Done when: adding Paystack touched no caller, the domain layer is clean, and you can both point at every SOLID letter and argue where the DDD machinery earns its place versus where it does not.

### Week 7: Async, queues, domain events, idempotent webhooks

Goal: async processing and reliable webhooks, with events given domain meaning.

- Day 1: Learn queues and jobs. Move notifications into a queued job. Note that Laravel's database queue uses SELECT FOR UPDATE SKIP LOCKED on Postgres, and understand why SKIP LOCKED is the right tool for a job queue.
- Day 2: Handle failed jobs and retries.
- Day 3: Learn events and listeners. Have the Bill aggregate raise PaymentReceived and BillSettled as domain events, with listeners reacting. This is DDD domain events, not just Laravel events.
- Day 4: Build the Stripe webhook handler, idempotent on the event ID, signature verified.
- Day 5: Build the Paystack webhook handler with the same idempotency idea, mapping into the same domain language.
- Day 6: Add feature tests for jobs, events, and webhook dedupe. Run Prompt 2.
- Day 7: Run Prompt 3 on sync versus async, SKIP LOCKED, duplicate webhooks, and domain events.

Prompt rhythm: Day 1 start, Prompt 1 on queues, events, and domain events. Day 6 end, Prompt 2 on jobs and webhooks. Day 7 end, Prompt 3 to grill async and webhook handling, then Prompt 4.

Threads: DDD (domain events), Postgres (SKIP LOCKED), reliability. Also apply webhook signature verification and the append-only audit log from the cross-cutting section. Reading: Laravel queues and events, PostgreSQL docs on SKIP LOCKED, Stripe and Paystack webhook docs.

You must be able to answer: why you queue instead of sending inline, what SKIP LOCKED does and why a job queue needs it, what happens on a duplicate webhook, and the difference between a Laravel event and a domain event.

Done when: a webhook delivered twice does nothing the second time, the aggregate raises real domain events, and you can explain SKIP LOCKED.

### Week 8: Testing, system design, and the defense document

Goal: a complete suite, system-design breadth, and a document that proves you can articulate it all.

- Day 1: Fill test gaps. Unit-test the domain in isolation. Notice that good DDD made this easy, because pure domain logic needs no database. Learn the test pyramid.
- Day 2: Be able to explain what you fake versus what you do not and why. Run Prompt 2 on the suite.
- Day 3: Write a "survive 100x traffic" document for your own app: Postgres read replicas, connection pooling with PgBouncer (because Postgres uses a process per connection), partitioning, a faster idempotency store, scaled queue workers, caching, webhook reliability.
- Day 4: Drill load balancing and caching out loud with Prompt 3.
- Day 5: Drill replication, sharding versus Postgres partitioning, queues, and back-of-the-envelope estimation.
- Day 6: Write DESIGN.md: every feature, the chosen option, the rejected option, why, plus the ubiquitous language and the one bounded context.
- Day 7: Final session. Have Claude Code run Prompt 3 across the whole project as one mock senior interview.

Prompt rhythm: Day 1 start, Prompt 1 on the test pyramid. Day 2 end, Prompt 2 on the full suite. Days 4 and 5, Prompt 3 to drill system design patterns out loud. Day 7 end, Prompt 3 as a full mock interview across the whole project, then Prompt 4 on anything still weak.

Threads: testing, system design, Postgres at scale, DDD (bounded context, documenting the language). Reading: Pest docs, Fowler's Practical Test Pyramid, DDIA (the whole book over time), Alex Xu's System Design Interview volumes 1 and 2, the system-design-primer repository, ByteByteGo, PostgreSQL docs on partitioning and replication.

You must be able to answer: how you test that a payment cannot be charged twice, what you fake and why, the test pyramid, why Postgres needs connection pooling, and how your system scales.

Done when: DESIGN.md is complete and you can defend the whole project end to end in a mock interview.

---

## Extension: weeks 9 to 13 (the full rounding-out)

Weeks 1 to 8 repair what has been failing you. These five make the project a complete, deployed, production-shaped system, and cover the senior topics that live outside the framework: auth, caching, code quality tooling, containers, deployment, and operating the thing.

Treat these as a menu, not a queue. Everything in weeks 9 to 13 is breadth, the exact thing the core plan argues against, so do not grind them completionist-style. Pick the two that match the roles you are actually targeting and go deep on those; skim or skip the rest. If a job description leans on infrastructure and deployment, do weeks 11 and 12. If it leans on performance and scale, do weeks 10 and 13. Auth (week 9) is the one most loops assume you already know, so it is the safest default pick. Each follows the same format and the same prompt rhythm.

### Week 9: Authentication and authorization

Goal: a properly secured API, authenticated and authorized, not an open endpoint.

- Day 1: Concept first on auth. Stateless token versus session, and where authorization belongs (not in the controller).
- Day 2: Add token authentication with Laravel Sanctum. Protect the payment endpoints.
- Day 3: Scope bills and contributions to the authenticated user, so a user can only act on their own.
- Day 4: Authorization policies for who may view, contribute to, or settle a bill.
- Day 5: Per-user rate limiting on the payment endpoint.
- Day 6: Tests: the unauthenticated are rejected, the wrong user is forbidden. Run Prompt 2.
- Day 7: Run Prompt 3 on auth versus authz, token versus session, and access-control models.

Prompt rhythm: Day 1 start, Prompt 1 on authentication and authorization. Day 6 end, Prompt 2 on the auth layer. Day 7 end, Prompt 3, then Prompt 4.

Threads: security, SOLID (authorization as policy objects). Reading: Laravel Sanctum, Laravel authorization (policies and gates), OWASP.

You must be able to answer: stateless versus session auth, where authorization belongs, role-based versus attribute-based access at a high level, and how you test authorization.

Done when: endpoints reject the unauthenticated and forbid the wrong user, proven by tests.

### Week 10: Caching and Redis

Goal: a cache layer you can reason about, with correct invalidation.

- Day 1: Concept first on caching. Cache-aside versus write-through, TTLs, the invalidation problem, and cache stampede.
- Day 2: Add Redis. Cache a bill's read state with cache-aside.
- Day 3: Invalidate the cache correctly on every write. This is the hard part, get it right.
- Day 4: Move the idempotency store and the rate limiter to Redis, and be able to argue the durability tradeoff against Postgres.
- Day 5: Use Redis as the queue driver and compare it to the Postgres SKIP LOCKED queue you already built.
- Day 6: Tests proving stale data never serves. Run Prompt 2.
- Day 7: Run Prompt 3 on invalidation, stampede, and when not to cache.

Prompt rhythm: Day 1 start, Prompt 1 on caching strategy and invalidation. Day 6 end, Prompt 2 on the cache layer. Day 7 end, Prompt 3, then Prompt 4.

Threads: performance, reliability. Reading: Laravel cache and Redis docs, and articles on cache invalidation and cache stampede.

You must be able to answer: cache-aside versus write-through, how you invalidate correctly, what a cache stampede is and how to prevent it, and when caching makes things worse.

Done when: reads are cached and correctly invalidated, with a test that proves no stale read.

### Week 11: Code quality tooling and Docker

Goal: a codebase a machine keeps honest, running entirely in containers.

- Day 1: Concept first on the three different jobs. Static analysis (PHPStan) finds type and logic errors without running the code, a linter flags suspect patterns, a formatter (Pint) enforces style, and a refactoring tool (Rector) automates mechanical changes. Know what each catches and what it cannot.
- Day 2: Add PHPStan with Larastan. Start at a low level, fix every error it reports, then raise the level one step at a time. Understand each fix, do not silence it.
- Day 3: Add Laravel Pint for PSR-12 formatting, and try Rector to see what automated refactors it proposes. Read its suggestions before accepting any.
- Day 4: Wire all three into a pre-commit hook so they run before every commit. Understand why catching this locally is better than catching it in CI.
- Day 5: Learn Docker. Write a Dockerfile for the app and understand what each layer does.
- Day 6: Use docker compose to bring up the whole stack, app plus Postgres plus Redis, with no local installs. Run Prompt 2 on your Dockerfile and compose config.
- Day 7: Run Prompt 3 on static analysis versus linting versus formatting, on images versus containers and layers, and on why you containerize at all.

Prompt rhythm: Day 1 start, Prompt 1 on tooling and containers. Day 6 end, Prompt 2 on the Dockerfile and compose. Day 7 end, Prompt 3, then Prompt 4.

Threads: code quality, operations. Reading: PHPStan, Larastan, Laravel Pint, Rector, Docker docs (Dockerfile and compose).

You must be able to answer: the difference between static analysis, linting, and formatting; what PHPStan levels mean; an image versus a container; and what a Dockerfile layer is.

Done when: PHPStan passes at a high level, Pint reports clean, and `docker compose up` runs the entire stack.

### Week 12: CI/CD and deployment

Goal: every push is checked automatically, and the app runs in production.

- Day 1: Concept first on CI versus CD and the twelve-factor app. Understand the pipeline as a quality gate that runs without you.
- Day 2: Write a GitHub Actions workflow that runs Pest, PHPStan, and Pint on every push and pull request. Make it fail loudly when any of them fails.
- Day 3: Add Postgres and Redis as services in the workflow so your tests run against real engines in CI, not mocks.
- Day 4: Deploy to a real host (Fly.io, Railway, or a VPS). Configure environment variables and secrets properly, never in git.
- Day 5: Make deploys run migrations safely, applying the safe-migration rules, and set up a basic release process. Understand zero-downtime deploys and rollback.
- Day 6: Run Prompt 2 on your pipeline and deploy configuration.
- Day 7: Run Prompt 3 on CI versus CD, twelve-factor, secrets management, zero-downtime deploys, and rollback.

Prompt rhythm: Day 1 start, Prompt 1 on CI/CD and deployment. Day 6 end, Prompt 2 on the pipeline. Day 7 end, Prompt 3, then Prompt 4.

Threads: operations, safe migrations, security (secrets). Reading: GitHub Actions docs, your host's docs, the twelve-factor app.

You must be able to answer: CI versus CD, what twelve-factor says about config and process, how you manage secrets, and how you deploy without downtime and roll back.

Done when: a green pipeline on every push and a live URL deployed automatically.

### Week 13: Load testing, observability, and polish

Goal: prove it under load, see inside it, and make it presentable.

- Day 1: Load-test concurrent contributions with k6 or ab. Watch your locking and isolation behave under real concurrency, not just a two-writer test.
- Day 2: Read the results, find the bottleneck, and tune an index or query based on real numbers.
- Day 3: Instrument structured logging around payments, and wire an error tracker or know exactly where it slots in.
- Day 4: Finalize the append-only audit log and add basic metrics (request counts, latency) you can talk to.
- Day 5: Write an OpenAPI spec for the API and polish the README.
- Day 6: Finalize DESIGN.md across the whole project. Run Prompt 2 on the docs.
- Day 7: Record yourself walking through the project as if to an interviewer. Run Prompt 3 as a final mock across everything.

Prompt rhythm: Day 1 start, Prompt 1 on load testing and observability. Day 6 end, Prompt 2 on the docs. Day 7 end, Prompt 3 as a full mock, then Prompt 4 on anything still weak.

Threads: observability, performance, system design made concrete. Reading: k6 docs, your error tracker's docs, OpenAPI, Laravel logging.

You must be able to answer: how you load-test, how you find a bottleneck, logs versus metrics versus traces, and how you would debug a production incident.

Done when: you have load-test numbers, instrumentation, an OpenAPI spec, and a recorded walkthrough you would be proud to show.

---

## The defense document

DESIGN.md is the single highest-value artefact in the project. For each feature: the problem, the option you chose, the option you rejected, and why, written in the ubiquitous language. It forces you to articulate every decision, which is the exact skill these interviews test. Half of failing a senior interview is knowing the thing but not being able to say it cleanly under pressure. This is where you practise saying it.

## The through-line

A senior answer is always "I hit this, here is what I chose, and here is what I rejected." That is why you build the rejected option too. The tradeoff is the signal an interviewer listens for, not the working code. One project you can defend line by line beats five you cannot.

---

## What this plan does not cover

This project makes you strong on the engineering depth that senior interviews probe, but a real loop has rounds it does not touch. Be honest with yourself about these.

- The live coding or data structures round. Many senior loops still include one. Keep your algorithm practice running in parallel, because this project does not replace it.
- The behavioural round. Prepare three or four stories using the situation, task, action, result shape. The good news is this project hands you the raw material: "the hardest bug you fixed" is the concurrency race, "a time you improved performance" is the N+1, "a design decision you are proud of" is the two-provider gateway. Mine the build for stories.
- Negotiation. Breaking past your current ceiling is part interview skill and part negotiation. When an offer comes, do not take the first number. That conversation deserves its own preparation.

A triage, because this is a lot for eight weeks. If you fall behind, protect weeks 3 and 4 (concurrency and isolation) and week 6 (architecture, SOLID, DDD). Those carry the most senior-interview weight. Idempotency in week 2 is next. Everything else strengthens the story, but those are the spine. Better to defend three topics deeply than to skim eight.

On being fully ready. The core weeks repair the exact gap that has been failing you, and the extension weeks round you into a complete senior profile. That is as ready as solo work can make you. The last stretch of readiness does not come from another project, it comes from interviewing. Real rounds are the only true test of whether you can say this cleanly under pressure, and they are the fastest feedback you will get. Start applying while you finish the build, not after. Treat the first few as practice. Let what they expose tell you where to go deeper, instead of guessing. Waiting until you feel no fear is the one plan that does not work, because that feeling does not arrive on its own, it arrives on the other side of doing it.

---

## Resources

Links I have verified, grouped by topic and mapped to the weeks. Books are named without links because they have no single canonical URL. One line each on what it is best for.

### Concurrency, transactions, isolation (weeks 3 and 4)

- Designing Data-Intensive Applications, Martin Kleppmann, chapter 7. Book. The single best explanation of isolation, lost updates, and write skew. Read this above all else.
- PostgreSQL concurrency control: https://www.postgresql.org/docs/current/mvcc.html . How MVCC works and why readers do not block writers.
- PostgreSQL transaction isolation: https://www.postgresql.org/docs/current/transaction-iso.html . Read Committed, Repeatable Read as snapshot isolation, and Serializable as SSI.
- PostgreSQL explicit locking: https://www.postgresql.org/docs/current/explicit-locking.html . Row locks (FOR UPDATE) and advisory locks.
- MySQL InnoDB isolation, for the contrast: https://dev.mysql.com/doc/refman/8.0/en/innodb-transaction-isolation-levels.html
- MySQL InnoDB locking, for the contrast: https://dev.mysql.com/doc/refman/8.0/en/innodb-locking.html
- Fowler, Optimistic Offline Lock: https://martinfowler.com/eaaCatalog/optimisticOfflineLock.html
- Fowler, Pessimistic Offline Lock: https://martinfowler.com/eaaCatalog/pessimisticOfflineLock.html

### Idempotency (week 2)

- Stripe idempotent requests reference: https://docs.stripe.com/api/idempotent_requests . The clear, canonical behaviour.
- Stripe blog, designing robust APIs with idempotency: https://stripe.com/blog/idempotency . The why, in depth.
- Brandur Leach, idempotency keys in Postgres: https://brandur.org/idempotency-keys . The deepest practical write-up, with the failure modes.

### Schema, indexing, query performance (weeks 1 and 5)

- SQL Antipatterns, Bill Karwin. Book. The best practical guide to schema mistakes and how to avoid them.
- Use The Index, Luke, Markus Winand: https://use-the-index-luke.com . Indexing and query performance, from the ground up.
- No Offset (keyset pagination), Markus Winand: https://use-the-index-luke.com/no-offset . Why offset pagination is wrong and what to use.
- PostgreSQL indexes: https://www.postgresql.org/docs/current/indexes.html . B-tree, partial, expression, and covering indexes.
- PostgreSQL EXPLAIN: https://www.postgresql.org/docs/current/using-explain.html . How to read a query plan.
- PostgreSQL data types: https://www.postgresql.org/docs/current/datatype.html . For your money, identity, and enum choices.
- Laravel Eloquent relationships and eager loading: https://laravel.com/docs/eloquent-relationships . The N+1 fix.
- Laravel query builder: https://laravel.com/docs/queries . When you drop below Eloquent.
- Laravel pagination: https://laravel.com/docs/pagination . Including cursor pagination.

### Architecture, SOLID, DDD (weeks 2, 5, 6)

- Domain-Driven Design Distilled, Vaughn Vernon. Book. The short, readable starting point. Read this first for DDD.
- Implementing Domain-Driven Design, Vaughn Vernon. Book. The deeper tactical reference.
- Learning Domain-Driven Design, Vlad Khononov. Book. A modern, approachable take.
- Matthias Noback's blog, DDD and architecture in PHP: https://matthiasnoback.nl . The best PHP-specific source.
- Fowler, Dependency Injection: https://martinfowler.com/articles/injection.html . The canonical explanation of DI and IoC containers.
- Refactoring Guru, Strategy pattern: https://refactoring.guru/design-patterns/strategy . Plain-language patterns.
- Laravel service container: https://laravel.com/docs/container . DI and binding interfaces to implementations.
- spatie/laravel-data: https://github.com/spatie/laravel-data . Compare against your hand-built DTOs.

### Validation, async, webhooks (weeks 2 and 7)

- Laravel validation and Form Requests: https://laravel.com/docs/validation
- Laravel queues: https://laravel.com/docs/queues
- Laravel events: https://laravel.com/docs/events
- PostgreSQL SELECT and SKIP LOCKED: https://www.postgresql.org/docs/current/sql-select.html . The locking clause that makes a database job queue work.
- Stripe webhooks are handled in the Stripe docs alongside the API reference above; Paystack webhooks: https://paystack.com/docs/payments/webhooks/ . Note the x-paystack-signature HMAC SHA512 verification.

### Security and operations (cross-cutting)

- OWASP Top 10: https://owasp.org/www-project-top-ten/ . The baseline web security checklist.
- PostgreSQL CREATE INDEX (see CONCURRENTLY): https://www.postgresql.org/docs/current/sql-createindex.html . Building indexes without locking the table.
- Laravel mass assignment is covered in the Eloquent docs, and rate limiting in the routing and middleware docs, both under https://laravel.com/docs .

### Auth, caching, tooling, deployment, operations (extension weeks 9 to 13)

- Laravel Sanctum (token auth): https://laravel.com/docs/sanctum
- Laravel authorization (policies and gates): https://laravel.com/docs/authorization
- Laravel cache and Redis: https://laravel.com/docs/cache and https://laravel.com/docs/redis
- PHPStan: https://phpstan.org . Larastan, the Laravel extension: https://github.com/larastan/larastan
- Laravel Pint (PSR-12 formatting): https://laravel.com/docs/pint
- Rector (automated refactoring): https://getrector.com
- Docker: https://docs.docker.com
- GitHub Actions: https://docs.github.com/actions
- The Twelve-Factor App: https://12factor.net . The baseline for config, deploys, and process model.
- k6 load testing: https://k6.io

### Testing (weeks 4, 6, 8)

- Pest: https://pestphp.com . The modern Laravel test framework.
- Laravel testing: https://laravel.com/docs/testing . HTTP tests, mocking, factories.
- Fowler, The Practical Test Pyramid: https://martinfowler.com/articles/practical-test-pyramid.html

### System design (week 8)

- Designing Data-Intensive Applications, Martin Kleppmann. Book. The foundation under most answers.
- System Design Interview volumes 1 and 2, Alex Xu. Books. The standard prep.
- The System Design Primer: https://github.com/donnemartin/system-design-primer . Large, free, well organized.
- ByteByteGo: https://bytebytego.com . Digestible pattern explainers.
- PostgreSQL partitioning: https://www.postgresql.org/docs/current/ddl-partitioning.html . For the scaling document.

A caution on links: official docs (Laravel, PostgreSQL, MySQL, Stripe, Paystack) are the versions to trust and they stay current. Everything else is a named author or book you can find even if a URL ever moves.
