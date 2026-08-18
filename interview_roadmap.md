# 🎯 30-Day COMPLETE Interview Preparation Roadmap — Service-Based Companies

**Profile**: Angooj Kumar Singh | ~5+ Years Experience | Java / Spring Boot / SQL
**Target**: Service-based companies (TCS, Infosys, Wipro, HCL, Capgemini, Accenture, DXC, LTIMindtree, Tech Mahindra, Mphasis, etc.)
**Timeline**: 30 Days (Aug 18, 2026 → Sep 16, 2026)
**Daily Commitment**: 4–5 hours/day (weekdays), 6–7 hours/day (weekends)

---

> [!IMPORTANT]
> This roadmap is **exhaustive** — covering every topic from basic to advanced. Nothing is skipped.
> Service-based company interviews typically have these rounds:
> 1. **Online Assessment** — MCQs + 1-2 coding questions
> 2. **Technical Round 1** — Core Java, Java 8, Collections, OOP
> 3. **Technical Round 2** — Spring Boot, Microservices, SQL, Project discussion
> 4. **Managerial / System Design** — Design patterns, SOLID, architecture
> 5. **HR Round** — Behavioral, salary negotiation, cultural fit

---

## 📋 MASTER TOPIC CHECKLIST

Use this checklist to track your progress. Every topic listed here is covered in the day-wise plan below.

### ☕ Core Java Topics
- [ ] Data Types — primitive types, ranges, default values, type casting (widening/narrowing), type promotion
- [ ] Variables — local, instance, static, transient, volatile
- [ ] Operators — arithmetic, relational, logical, bitwise, ternary, instanceof, operator precedence
- [ ] Control Flow — if-else, switch (incl. enhanced switch Java 14+), for, while, do-while, for-each, break, continue, labeled loops
- [ ] Arrays — declaration, initialization, 1D, 2D, jagged arrays, `Arrays` utility class, array copying
- [ ] OOP Pillar 1: Encapsulation — access modifiers, getters/setters, data hiding
- [ ] OOP Pillar 2: Inheritance — single, multilevel, hierarchical, `extends`, `super`, method overriding, constructor chaining
- [ ] OOP Pillar 3: Polymorphism — compile-time (overloading), runtime (overriding), covariant return types, dynamic method dispatch
- [ ] OOP Pillar 4: Abstraction — abstract classes, interfaces, abstract vs interface, when to use which
- [ ] `this` keyword — all 6 uses
- [ ] `super` keyword — all 3 uses
- [ ] `static` keyword — static variables, methods, blocks, nested classes, static imports
- [ ] `final` keyword — final variables, methods, classes, blank final, static final
- [ ] Constructors — default, parameterized, copy constructor, constructor chaining (`this()`, `super()`)
- [ ] Object class methods — `toString()`, `equals()`, `hashCode()`, `clone()`, `getClass()`, `finalize()`, `wait()`, `notify()`, `notifyAll()`
- [ ] String — String Pool, immutability reasons, `intern()`, `String` vs `StringBuilder` vs `StringBuffer`, string concatenation performance
- [ ] String methods — `charAt()`, `substring()`, `indexOf()`, `split()`, `replace()`, `trim()`, `strip()` (Java 11), `isBlank()`, `repeat()`, `equals()`, `compareTo()`
- [ ] Wrapper Classes — autoboxing, unboxing, Integer cache (-128 to 127), parsing methods
- [ ] Enums — enum basics, enum with constructors/methods/fields, enum in switch, `EnumSet`, `EnumMap`, enum singleton
- [ ] Inner Classes — member inner class, static nested class, local inner class, anonymous inner class
- [ ] Exception Handling — exception hierarchy, `Error` vs `Exception`, checked vs unchecked, `try-catch-finally`, `throw` vs `throws`, custom exceptions, `try-with-resources`, multi-catch, exception propagation, exception chaining, `StackOverflowError`, `OutOfMemoryError`
- [ ] `final` vs `finally` vs `finalize()`
- [ ] Multithreading — `Thread` class vs `Runnable` interface, thread lifecycle (NEW, RUNNABLE, BLOCKED, WAITING, TIMED_WAITING, TERMINATED), `start()` vs `run()`, `sleep()`, `join()`, `yield()`, thread priority, daemon threads
- [ ] Synchronization — `synchronized` method, `synchronized` block, `volatile`, `wait()` / `notify()` / `notifyAll()`, deadlock, livelock, starvation, race condition
- [ ] Concurrency API — `ExecutorService`, `ThreadPoolExecutor`, `Callable` vs `Runnable`, `Future`, `CountDownLatch`, `CyclicBarrier`, `Semaphore`, `ReentrantLock`, `ReadWriteLock`, `CompletableFuture`
- [ ] Collections — `Collection` interface hierarchy, `Iterable` → `Collection` → `List` / `Set` / `Queue`
- [ ] List — `ArrayList` (internal array, grow factor 50%), `LinkedList` (doubly linked), `Vector`, `Stack`, `CopyOnWriteArrayList`
- [ ] Set — `HashSet` (backed by HashMap), `LinkedHashSet`, `TreeSet` (Red-Black tree), `EnumSet`
- [ ] Queue — `PriorityQueue`, `ArrayDeque`, `LinkedList` as Queue
- [ ] Map — `HashMap` (bucket array + linked list/tree), `LinkedHashMap`, `TreeMap`, `Hashtable`, `ConcurrentHashMap`, `WeakHashMap`, `EnumMap`, `IdentityHashMap`
- [ ] `hashCode()` and `equals()` contract
- [ ] `Comparable` vs `Comparator`
- [ ] `Iterator` vs `ListIterator` vs `Enumeration`
- [ ] `fail-fast` vs `fail-safe` iterators
- [ ] `Collections` utility class — `sort()`, `reverse()`, `shuffle()`, `unmodifiableList()`, `synchronizedList()`, `singletonList()`, `emptyList()`
- [ ] Generics — type parameters, bounded types (`extends`, `super`), wildcards (`?`), type erasure, generic methods, generic classes
- [ ] Serialization — `Serializable`, `serialVersionUID`, `transient`, `Externalizable`, custom serialization (`writeObject` / `readObject`), serialization proxy pattern
- [ ] Cloning — shallow copy vs deep copy, `Cloneable` interface, `clone()` method
- [ ] Reflection API — `Class.forName()`, `getMethod()`, `invoke()`, `getDeclaredFields()`, accessing private members
- [ ] Annotations — built-in (`@Override`, `@Deprecated`, `@SuppressWarnings`, `@FunctionalInterface`), custom annotations, meta-annotations (`@Target`, `@Retention`, `@Inherited`, `@Documented`)
- [ ] I/O Streams — byte streams (`InputStream`/`OutputStream`), character streams (`Reader`/`Writer`), buffered streams, `FileInputStream`, `FileOutputStream`, `BufferedReader`, `BufferedWriter`, `PrintWriter`
- [ ] NIO — `Path`, `Files`, `Channels`, `Buffers`, non-blocking I/O concepts
- [ ] JVM Architecture — ClassLoader subsystem, Runtime Data Areas (Method Area, Heap, Stack, PC Register, Native Method Stack), Execution Engine (Interpreter, JIT Compiler)
- [ ] ClassLoaders — Bootstrap, Extension/Platform, Application, custom classloader, class loading delegation model (parent delegation)
- [ ] Memory Management — Stack vs Heap, Young Generation (Eden, S0, S1), Old Generation, Metaspace (replaced PermGen in Java 8)
- [ ] Garbage Collection — GC roots, Mark & Sweep, Minor GC vs Major GC, GC algorithms (Serial, Parallel, CMS, G1, ZGC), `System.gc()`, `finalize()`, memory leaks, `WeakReference`, `SoftReference`, `PhantomReference`
- [ ] Java Memory Model (JMM) — happens-before relationship, visibility, atomicity, `volatile` semantics

### ☕ Java 8+ Features
- [ ] Lambda Expressions — syntax, functional interfaces, variable capture, effectively final
- [ ] Functional Interfaces — `@FunctionalInterface`, `Predicate`, `Function`, `Consumer`, `Supplier`, `BiFunction`, `BiConsumer`, `BiPredicate`, `UnaryOperator`, `BinaryOperator`
- [ ] Method References — static reference, instance reference, arbitrary object, constructor reference
- [ ] Stream API — creating streams, intermediate ops (`filter`, `map`, `flatMap`, `distinct`, `sorted`, `peek`, `limit`, `skip`), terminal ops (`forEach`, `collect`, `reduce`, `count`, `min`, `max`, `findFirst`, `findAny`, `anyMatch`, `allMatch`, `noneMatch`, `toArray`)
- [ ] Stream: lazy evaluation — how pipelines work, short-circuiting operations
- [ ] Stream: `Collectors` — `toList()`, `toSet()`, `toMap()`, `joining()`, `groupingBy()`, `partitioningBy()`, `counting()`, `summarizingInt()`, `averagingDouble()`, `reducing()`
- [ ] Stream: parallel streams — `parallelStream()`, `ForkJoinPool`, when to use, thread safety concerns
- [ ] `Optional` — `of()`, `ofNullable()`, `empty()`, `isPresent()`, `ifPresent()`, `get()`, `orElse()`, `orElseGet()`, `orElseThrow()`, `map()`, `flatMap()`, `filter()`
- [ ] `default` methods in interfaces — purpose, diamond problem, resolution rules
- [ ] `static` methods in interfaces
- [ ] Date/Time API (java.time) — `LocalDate`, `LocalTime`, `LocalDateTime`, `ZonedDateTime`, `Instant`, `Duration`, `Period`, `DateTimeFormatter`, `TemporalAdjusters`, converting from legacy `Date`
- [ ] `Nashorn` JavaScript engine (deprecated) — awareness only
- [ ] Java 9 — modules (JPMS), `List.of()`, `Set.of()`, `Map.of()` (immutable collections), private methods in interfaces, `try-with-resources` enhancement, `Optional.ifPresentOrElse()`, `Stream.takeWhile()`, `dropWhile()`, `ofNullable()`, JShell
- [ ] Java 10 — `var` (local variable type inference)
- [ ] Java 11 — `String` new methods (`isBlank()`, `strip()`, `repeat()`, `lines()`), `Files.readString()`, `Files.writeString()`, `HttpClient` API, running `.java` files directly
- [ ] Java 14+ — `switch` expressions, `Records`, `instanceof` pattern matching, text blocks, sealed classes (Java 17)

### 🍃 Spring Ecosystem
- [ ] Spring Core — IoC Container, Dependency Injection, `ApplicationContext` vs `BeanFactory`
- [ ] DI types — constructor injection, setter injection, field injection, `@Autowired`, `@Qualifier`, `@Primary`, `@Value`
- [ ] Bean lifecycle — instantiation → populate properties → `BeanNameAware` → `BeanFactoryAware` → `ApplicationContextAware` → `@PostConstruct` / `InitializingBean` → ready → `@PreDestroy` / `DisposableBean` → destroyed
- [ ] Bean scopes — `singleton`, `prototype`, `request`, `session`, `application`, `websocket`
- [ ] Configuration — `@Configuration`, `@Bean`, `@ComponentScan`, `@Component`, `@Service`, `@Repository`, `@Controller`
- [ ] Spring Boot — auto-configuration (`@EnableAutoConfiguration`, `spring.factories` / `AutoConfiguration.imports`), starters, `@SpringBootApplication`, `@Conditional` annotations
- [ ] Spring Boot properties — `application.properties` vs `application.yml`, profiles (`@Profile`, `spring.profiles.active`), externalized config, property source priority
- [ ] Spring Boot Actuator — health endpoints, custom health indicators, metrics
- [ ] Spring MVC — `DispatcherServlet`, handler mapping, view resolver, `@RequestMapping`, `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`, `@PatchMapping`
- [ ] Request handling — `@PathVariable`, `@RequestParam`, `@RequestBody`, `@RequestHeader`, `@CookieValue`, `@ModelAttribute`
- [ ] Response handling — `ResponseEntity`, `@ResponseBody`, `@ResponseStatus`, content negotiation
- [ ] Validation — `@Valid`, `@Validated`, `@NotNull`, `@NotBlank`, `@NotEmpty`, `@Size`, `@Min`, `@Max`, `@Email`, `@Pattern`, custom validators, `BindingResult`
- [ ] Exception handling — `@ExceptionHandler`, `@ControllerAdvice`, `@RestControllerAdvice`, `ResponseEntityExceptionHandler`, custom error responses
- [ ] Filters vs Interceptors vs AOP — differences, use cases, order of execution
- [ ] Spring AOP — aspect, advice (`@Before`, `@After`, `@AfterReturning`, `@AfterThrowing`, `@Around`), pointcut, join point, weaving, proxy pattern
- [ ] Spring Data JPA — `JpaRepository`, `CrudRepository`, `PagingAndSortingRepository`, derived query methods, `@Query` (JPQL & native), named queries
- [ ] JPA/Hibernate — entity mapping (`@Entity`, `@Table`, `@Id`, `@GeneratedValue`, `@Column`), relationships (`@OneToOne`, `@OneToMany`, `@ManyToOne`, `@ManyToMany`), `@JoinColumn`, `@JoinTable`, cascade types, orphan removal
- [ ] Fetch types — `LAZY` vs `EAGER`, N+1 problem, `@EntityGraph`, `JOIN FETCH`
- [ ] JPA — `EntityManager`, persistence context, entity states (transient, managed, detached, removed), dirty checking, first-level cache, second-level cache
- [ ] Transactions — `@Transactional`, propagation types (REQUIRED, REQUIRES_NEW, NESTED, SUPPORTS, NOT_SUPPORTED, MANDATORY, NEVER), isolation levels (READ_UNCOMMITTED, READ_COMMITTED, REPEATABLE_READ, SERIALIZABLE), rollback rules
- [ ] Spring Security — authentication vs authorization, `SecurityFilterChain`, `UserDetailsService`, `PasswordEncoder`, `@PreAuthorize`, `@Secured`, `@RolesAllowed`, CORS configuration, CSRF protection
- [ ] JWT — token structure (header.payload.signature), token generation, validation, refresh tokens, stateless authentication flow
- [ ] OAuth2 basics — grant types (authorization code, client credentials), resource server, authorization server
- [ ] Spring Boot Testing — `@SpringBootTest`, `@WebMvcTest`, `@DataJpaTest`, `@MockBean`, `MockMvc`, `@Test`, JUnit 5, Mockito (`when().thenReturn()`, `verify()`, `ArgumentCaptor`)
- [ ] Logging — SLF4J, Logback, log levels (TRACE, DEBUG, INFO, WARN, ERROR), MDC
- [ ] Caching — `@Cacheable`, `@CachePut`, `@CacheEvict`, cache providers (EhCache, Redis concepts)
- [ ] Scheduling — `@Scheduled`, `@EnableScheduling`, cron expressions, `@Async`, `@EnableAsync`
- [ ] REST API best practices — resource naming conventions, versioning (URI, header, param), pagination, HATEOAS, idempotency, PUT vs PATCH vs POST, status codes (200, 201, 204, 400, 401, 403, 404, 409, 500)
- [ ] API documentation — Swagger / OpenAPI / SpringDoc

### ☁️ Microservices
- [ ] Monolith vs Microservices — pros/cons, when to use which
- [ ] Microservice principles — single responsibility, loose coupling, high cohesion, bounded context (DDD)
- [ ] Inter-service communication — synchronous (REST, gRPC), asynchronous (message queues)
- [ ] API Gateway — Spring Cloud Gateway / Netflix Zuul, routing, rate limiting, authentication
- [ ] Service Discovery — Eureka (client-side), Consul, service registration & discovery
- [ ] Config Server — Spring Cloud Config, centralized configuration, environment-specific configs
- [ ] Circuit Breaker — Resilience4j / Hystrix, fallback methods, states (CLOSED, OPEN, HALF_OPEN), bulkhead pattern
- [ ] Load Balancing — client-side (Ribbon/Spring Cloud LoadBalancer), server-side
- [ ] Distributed Tracing — Sleuth + Zipkin / Micrometer Tracing concepts
- [ ] Messaging — Kafka basics (topics, partitions, consumer groups, offset), RabbitMQ basics (exchange, queue, binding)
- [ ] Saga Pattern — choreography vs orchestration for distributed transactions
- [ ] CQRS — Command Query Responsibility Segregation (awareness)
- [ ] 12-Factor App — all 12 factors explained
- [ ] Containerization — Docker basics (Dockerfile, image, container, `docker-compose`), Kubernetes awareness (Pod, Service, Deployment)

### 🗄️ SQL & Database
- [ ] DDL — `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME`, constraints (`PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, `NOT NULL`, `CHECK`, `DEFAULT`)
- [ ] DML — `INSERT`, `UPDATE`, `DELETE`, `MERGE`/`UPSERT`
- [ ] DQL — `SELECT`, `WHERE`, `ORDER BY`, `GROUP BY`, `HAVING`, `DISTINCT`, `LIMIT`/`TOP`/`FETCH`, `LIKE`, `IN`, `BETWEEN`, `IS NULL`
- [ ] DCL — `GRANT`, `REVOKE`
- [ ] TCL — `COMMIT`, `ROLLBACK`, `SAVEPOINT`
- [ ] Joins — `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL OUTER JOIN`, `CROSS JOIN`, `SELF JOIN`, `NATURAL JOIN`
- [ ] Subqueries — scalar, column, row, table subqueries, correlated subqueries, `EXISTS` vs `IN`
- [ ] Set operations — `UNION`, `UNION ALL`, `INTERSECT`, `EXCEPT`/`MINUS`
- [ ] Aggregate functions — `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`, `STRING_AGG()`/`GROUP_CONCAT()`
- [ ] Window functions — `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, `NTILE()`, `LEAD()`, `LAG()`, `FIRST_VALUE()`, `LAST_VALUE()`, `SUM() OVER()`, `AVG() OVER()`, `PARTITION BY`, `ORDER BY`, frame clause (`ROWS BETWEEN`)
- [ ] String functions — `CONCAT()`, `SUBSTRING()`, `LEN()`/`LENGTH()`, `UPPER()`, `LOWER()`, `TRIM()`, `REPLACE()`, `CHARINDEX()`/`POSITION()`, `STUFF()`/`INSERT()`
- [ ] Date functions — `GETDATE()`/`NOW()`, `DATEADD()`, `DATEDIFF()`, `DATEPART()`, `FORMAT()`, `CAST()`, `CONVERT()`
- [ ] CASE expression — simple CASE, searched CASE, CASE in SELECT/WHERE/ORDER BY
- [ ] Views — simple views, complex views, indexed/materialized views, `WITH CHECK OPTION`
- [ ] Indexes — clustered vs non-clustered, composite index, covering index, index scan vs seek, when to create/avoid indexes, filtered indexes
- [ ] Stored Procedures — input/output parameters, `EXEC`, error handling (`TRY...CATCH`), dynamic SQL, `sp_executesql`
- [ ] Functions — scalar functions, table-valued functions (inline vs multi-statement)
- [ ] Triggers — `AFTER` triggers, `INSTEAD OF` triggers, `INSERTED`/`DELETED` tables
- [ ] Cursors — declaration, types (static, dynamic, forward-only, keyset), why to avoid cursors
- [ ] CTE — Common Table Expressions, recursive CTE
- [ ] Temp tables vs Table variables vs CTE — differences, performance implications
- [ ] Normalization — 1NF, 2NF, 3NF, BCNF, 4NF, 5NF, denormalization trade-offs
- [ ] ACID properties — Atomicity, Consistency, Isolation, Durability
- [ ] Transaction isolation levels — Read Uncommitted, Read Committed, Repeatable Read, Serializable, Snapshot
- [ ] Locking — shared lock, exclusive lock, update lock, deadlocks, lock escalation
- [ ] Execution Plans — reading query plans, table scan vs index scan vs index seek, key lookups
- [ ] Query optimization — indexing strategies, avoiding SELECT *, query hints, sargable queries, parameter sniffing
- [ ] Pivot / Unpivot
- [ ] `MERGE` statement

### 📊 Data Structures & Algorithms
- [ ] Time & Space Complexity — Big O notation, best/average/worst case, amortized analysis
- [ ] Arrays — traversal, insertion, deletion, reversal, rotation, two-pointer, sliding window, prefix sum, Kadane's algorithm
- [ ] Strings — palindrome, anagram, pattern matching (naive, KMP awareness), longest substring without repeating, string to integer
- [ ] Linked List — singly, doubly, circular, reversal, cycle detection (Floyd's), merge two sorted lists, find middle, remove nth from end
- [ ] Stack — array/linked list implementation, balanced parentheses, next greater element, min stack, infix/prefix/postfix conversion, stock span
- [ ] Queue — array/linked list implementation, circular queue, deque, priority queue, sliding window maximum, implement queue using stacks
- [ ] Hashing — hash function, collision resolution (chaining, open addressing — linear probing, quadratic probing, double hashing), HashMap implementation
- [ ] Binary Tree — traversals (inorder, preorder, postorder — recursive & iterative), level order (BFS), height, diameter, mirror, lowest common ancestor, path sum, views (left, right, top, bottom)
- [ ] Binary Search Tree — search, insert, delete, validate BST, kth smallest, inorder successor, convert sorted array to BST
- [ ] Heap — min heap, max heap, heapify, insert, extract, heap sort, kth largest element, merge k sorted lists
- [ ] Trie — insert, search, prefix search, auto-complete (awareness)
- [ ] Graph — representations (adjacency matrix, adjacency list), BFS, DFS, connected components, cycle detection (directed & undirected), topological sort, shortest path (Dijkstra's, Bellman-Ford awareness), minimum spanning tree (Prim's, Kruskal's awareness)
- [ ] Sorting — Bubble, Selection, Insertion, Merge Sort, Quick Sort, Heap Sort, Counting Sort, Radix Sort — time/space complexity of each
- [ ] Searching — Linear Search, Binary Search (iterative & recursive), search in rotated sorted array, first/last occurrence, peak element
- [ ] Recursion & Backtracking — factorial, Fibonacci, power set, permutations, N-Queens (awareness), subset sum
- [ ] Dynamic Programming — memoization vs tabulation, Fibonacci, 0/1 knapsack, longest common subsequence, longest increasing subsequence, coin change, matrix chain multiplication (awareness), climbing stairs
- [ ] Greedy — activity selection, fractional knapsack, Huffman coding (awareness), job sequencing
- [ ] Bit Manipulation — AND, OR, XOR, NOT, left shift, right shift, check if power of 2, count set bits, single number in array

### 🏗️ Design Patterns (All 23 GoF + more)
**Creational (5)**:
- [ ] Singleton — eager, lazy, thread-safe (synchronized, double-checked locking, Bill Pugh — inner static class, enum singleton), breaking singleton (reflection, serialization, cloning) and prevention
- [ ] Factory Method — interface for creating objects, subclass decides which class to instantiate
- [ ] Abstract Factory — factory of factories
- [ ] Builder — step-by-step construction, immutable objects, Lombok `@Builder`
- [ ] Prototype — cloning, shallow vs deep copy

**Structural (7)**:
- [ ] Adapter — converting one interface to another
- [ ] Bridge — separating abstraction from implementation
- [ ] Composite — tree structure, part-whole hierarchy
- [ ] Decorator — adding behavior dynamically (I/O streams example)
- [ ] Facade — simplified interface to a complex subsystem
- [ ] Flyweight — sharing to support large number of fine-grained objects
- [ ] Proxy — surrogate object (Spring AOP proxies)

**Behavioral (11)**:
- [ ] Chain of Responsibility — pass request along a chain (servlet filters, Spring Security filter chain)
- [ ] Command — encapsulate request as an object
- [ ] Interpreter — grammar and interpretation (awareness)
- [ ] Iterator — traverse collection without exposing representation
- [ ] Mediator — reduce direct communication between objects
- [ ] Memento — capture and restore state
- [ ] Observer — one-to-many dependency (event listeners, pub-sub)
- [ ] State — alter behavior when state changes
- [ ] Strategy — define family of algorithms, make them interchangeable (Comparator)
- [ ] Template Method — define skeleton, let subclasses override steps (JdbcTemplate, RestTemplate)
- [ ] Visitor — add operations without modifying classes (awareness)

### 🏛️ System Design & Architecture
- [ ] SOLID Principles — SRP, OCP, LSP, ISP, DIP with code examples
- [ ] DRY, KISS, YAGNI
- [ ] Layered Architecture — Controller → Service → Repository
- [ ] MVC vs MVP vs MVVM (awareness)
- [ ] CAP Theorem — Consistency, Availability, Partition Tolerance
- [ ] Load Balancing — Round Robin, Least Connections, IP Hash
- [ ] Caching — cache-aside, read-through, write-through, write-behind, TTL, eviction policies (LRU, LFU)
- [ ] Database scaling — vertical vs horizontal, sharding, replication (master-slave), read replicas
- [ ] CDN — Content Delivery Network
- [ ] Message Queues — producer-consumer, pub-sub, use cases
- [ ] Rate Limiting — token bucket, sliding window
- [ ] Design exercises — URL shortener, notification system, task scheduler, simple e-commerce

### 🛠️ Tools & DevOps
- [ ] Git — `init`, `clone`, `add`, `commit`, `push`, `pull`, `fetch`, `merge`, `rebase`, `cherry-pick`, `stash`, `reset` (soft/mixed/hard), `revert`, `log`, `diff`, `blame`, branching strategies (GitFlow, trunk-based), merge conflicts
- [ ] Maven — POM, lifecycle (validate → compile → test → package → install → deploy), dependencies, plugins, profiles, `mvn clean install`
- [ ] Docker — Dockerfile, image, container, `docker build`, `docker run`, `docker-compose`, volumes, networking, multi-stage builds
- [ ] CI/CD — concepts, Jenkins pipeline (awareness), GitHub Actions (awareness)
- [ ] Postman — collections, environments, pre-request scripts, tests
- [ ] Agile/Scrum — sprint, product backlog, sprint backlog, daily standup, sprint planning, sprint review, retrospective, story points, velocity, Kanban awareness
- [ ] SDLC — Waterfall, Agile, V-Model, Iterative, Spiral

### 🤝 HR & Behavioral
- [ ] Self-introduction — 2-min version
- [ ] Tell me about yourself
- [ ] Strengths and weaknesses
- [ ] Why are you leaving current company?
- [ ] Where do you see yourself in 5 years?
- [ ] Why this company?
- [ ] Describe a challenging situation (STAR method)
- [ ] Conflict with team member
- [ ] Time you failed and learned
- [ ] Leadership / mentoring examples
- [ ] Salary negotiation
- [ ] Notice period discussion
- [ ] Questions to ask the interviewer

---

## 📅 WEEK 1 (Days 1–7): Core Java — Basic to Advanced + Java 8/11

---

### Day 1 (Mon, Aug 18) — Java Basics + OOP Fundamentals

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 45 min | **Data Types & Variables** | All 8 primitive types with ranges and default values. Type casting — widening (implicit) vs narrowing (explicit). Type promotion in expressions (`byte + byte = int`). Local vs instance vs static vs transient vs volatile variables. |
| 45 min | **Operators & Control Flow** | All operators including bitwise (`&`, `\|`, `^`, `~`, `<<`, `>>`, `>>>`). Operator precedence table. `if-else`, nested `if`, `switch` (traditional + enhanced Java 14+). `for`, `while`, `do-while`, `for-each`. `break`, `continue`, labeled `break`/`continue`. |
| 45 min | **OOP — Encapsulation & Inheritance** | Access modifiers (private, default, protected, public) — visibility across same class, same package, subclass, other package. Getters/setters. Inheritance — `extends`, method overriding rules (access modifier, return type, exceptions). Constructor chaining with `super()`. Why Java doesn't support multiple inheritance of classes. |
| 45 min | **OOP — Polymorphism & Abstraction** | Compile-time polymorphism (method overloading — rules, ambiguity). Runtime polymorphism (method overriding, dynamic method dispatch, upcasting, downcasting, `instanceof`). Covariant return types. Abstract classes vs Interfaces (pre and post Java 8). When to use abstract class vs interface. |
| 30 min | **`this`, `super`, `static`, `final`** | `this` — all 6 uses (refer variable, invoke method, invoke constructor, pass as argument, return, used in constructor). `super` — all 3 uses. `static` — variables, methods, blocks, nested classes, import. `final` — variables, methods, classes, blank final. |
| 30 min | **Practice** | Write code for: method overloading with type promotion ambiguity; runtime polymorphism with 3-level hierarchy; abstract class with constructor; interface with default method. 10 output-prediction questions. |

---

### Day 2 (Tue, Aug 19) — Strings, Wrappers, Enums, Inner Classes

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1 hr | **String Deep Dive** | String Pool mechanism — heap vs pool. Why Strings are immutable (security, caching, synchronization, hashcode caching, class loading). `intern()` method. `==` vs `.equals()` for Strings. `String` vs `StringBuilder` (non-synchronized) vs `StringBuffer` (synchronized). String concatenation — how `+` works internally (StringBuilder in older Java, `invokedynamic` in Java 9+). All important String methods: `charAt()`, `substring()`, `indexOf()`, `lastIndexOf()`, `split()`, `replace()`, `replaceAll()`, `trim()`, `strip()` (Java 11), `isBlank()` (Java 11), `repeat()` (Java 11), `lines()` (Java 11), `equals()`, `equalsIgnoreCase()`, `compareTo()`, `contains()`, `startsWith()`, `endsWith()`, `toCharArray()`, `valueOf()`. |
| 45 min | **Wrapper Classes & Autoboxing** | All 8 wrapper classes. Autoboxing & unboxing. Integer cache (-128 to 127) — `Integer.valueOf()` vs `new Integer()`. Unboxing `NullPointerException` trap. Parsing methods — `Integer.parseInt()`, `Integer.valueOf()`, `Double.parseDouble()`. Compare with `==` vs `.equals()`. |
| 45 min | **Enums** | Enum basics — declaration, values, ordinal. Enum with fields, constructors, methods. Enum in `switch`. Enum implementing interfaces. `EnumSet` and `EnumMap`. Enum as Singleton pattern. Why enum constructor is private. |
| 45 min | **Inner Classes** | Member inner class — accessing outer class members. Static nested class — when to use. Local inner class — inside a method. Anonymous inner class — implementing interface/extending class inline. Relationship to lambdas (Java 8). |
| 30 min | **Practice** | String pool prediction questions (10). Autoboxing edge cases (5). Create an enum `OrderStatus` with transitions. |

---

### Day 3 (Wed, Aug 20) — Exception Handling (Complete)

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1 hr | **Exception Hierarchy** | `Throwable` → `Error` (JVM errors: `StackOverflowError`, `OutOfMemoryError`, `VirtualMachineError`) and `Exception` → `RuntimeException` (unchecked: `NullPointerException`, `ArrayIndexOutOfBoundsException`, `ClassCastException`, `ArithmeticException`, `IllegalArgumentException`, `NumberFormatException`, `ConcurrentModificationException`, `UnsupportedOperationException`) and checked exceptions (`IOException`, `SQLException`, `ClassNotFoundException`, `FileNotFoundException`, `InterruptedException`). |
| 1 hr | **Exception Handling Mechanisms** | `try-catch-finally` — execution flow in all scenarios (no exception, caught exception, uncaught exception, exception in catch, exception in finally). `throw` (throw exception) vs `throws` (declare exception). Exception propagation (up the call stack). Multi-catch (`catch (IOException \| SQLException e)`). `try-with-resources` (`AutoCloseable`, suppressed exceptions). Exception chaining (`initCause()`, constructor with cause). |
| 45 min | **Custom Exceptions & Best Practices** | Create custom checked and unchecked exceptions. When to use checked vs unchecked. Best practices: catch specific exceptions, don't swallow exceptions, use finally/try-with-resources for cleanup, don't use exceptions for flow control, document with `@throws`. `final` vs `finally` vs `finalize()` — complete comparison. |
| 45 min | **`Object` Class Methods** | All 11 methods: `toString()`, `equals()`, `hashCode()`, `clone()`, `getClass()`, `finalize()`, `wait()` (3 overloads), `notify()`, `notifyAll()`. Deep dive into `equals()` and `hashCode()` contract. How to properly override `equals()` and `hashCode()`. |
| 30 min | **Practice** | Output prediction with try-catch-finally (10 tricky questions). Write custom exception hierarchy for your Healthcare project. Override equals/hashCode for a `Patient` class. |

---

### Day 4 (Thu, Aug 21) — Collections Framework (Complete — Part 1)

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 30 min | **Collections Hierarchy** | `Iterable` → `Collection` → `List`, `Set`, `Queue`. `Map` (separate hierarchy). Draw the complete hierarchy diagram from memory. |
| 1 hr | **List Implementations** | `ArrayList` — internal array, default capacity (10), grow factor (50% — `newCapacity = oldCapacity + oldCapacity >> 1`), `add()` amortized O(1), `get()` O(1), `remove()` O(n). `LinkedList` — doubly linked list, implements both `List` and `Deque`, `add()` O(1), `get()` O(n). `Vector` — synchronized ArrayList, legacy. `Stack` — extends Vector, LIFO. `CopyOnWriteArrayList` — thread-safe, new copy on write, good for read-heavy scenarios. When to use which. |
| 1 hr | **Set Implementations** | `HashSet` — backed by `HashMap`, no order, O(1) add/contains/remove. `LinkedHashSet` — maintains insertion order. `TreeSet` — Red-Black tree, sorted order, O(log n), `NavigableSet` interface. `EnumSet` — specialized for enums, backed by bit vector. `hashCode()` and `equals()` contract — why both must be overridden together. What happens if only one is overridden. |
| 1 hr | **Map Implementations — HashMap Deep Dive** | `HashMap` internal structure: array of `Node<K,V>` (bucket array). Default capacity (16), load factor (0.75), threshold (capacity × load factor). `put()` flow: `hashCode()` → hash function (key.hashCode() ^ (key.hashCode() >>> 16)) → bucket index (hash & (n-1)) → check for collision. Collision handling: Java 7 (linked list — head insertion) vs Java 8 (linked list → red-black tree when bucket size ≥ 8, TREEIFY_THRESHOLD). Rehashing when size > threshold. `get()` flow. `null` key handling (bucket 0). Time complexity: O(1) average, O(log n) worst case (Java 8). |
| 30 min | **Practice** | Draw HashMap internal structure. Trace `put()` and `get()` for 5 entries. Explain what happens when load factor is exceeded. |

---

### Day 5 (Fri, Aug 22) — Collections Framework (Complete — Part 2) + Generics

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 45 min | **More Map Implementations** | `LinkedHashMap` — maintains insertion order (or access order for LRU cache). `TreeMap` — Red-Black tree, sorted by keys, `NavigableMap`. `Hashtable` — legacy, synchronized, no null keys/values. `WeakHashMap` — weak references, entries removed when key is GC'd. `IdentityHashMap` — uses `==` instead of `equals()`. `EnumMap` — keys are enum, backed by array. |
| 45 min | **ConcurrentHashMap** | Java 7: segment-based locking (16 segments). Java 8: `CAS` (Compare-And-Swap) + `synchronized` on individual bucket (Node). No locking for reads. `putIfAbsent()`, `computeIfAbsent()`, `compute()`, `merge()`. vs `Hashtable` vs `Collections.synchronizedMap()` — detailed comparison. |
| 30 min | **Queue Implementations** | `PriorityQueue` — min-heap by default, `Comparator` for custom ordering. `ArrayDeque` — resizable array, used as stack or queue (faster than `Stack` and `LinkedList`). `LinkedList` as Queue/Deque. |
| 30 min | **Iterators & Utility Classes** | `Iterator` vs `ListIterator` vs `Enumeration` — features comparison. `fail-fast` (`ArrayList`, `HashMap`) vs `fail-safe` (`CopyOnWriteArrayList`, `ConcurrentHashMap`). `ConcurrentModificationException` — when and why. `Collections` utility: `sort()`, `reverse()`, `shuffle()`, `min()`, `max()`, `frequency()`, `unmodifiableList()`, `synchronizedList()`, `singletonList()`, `emptyList()`, `checkedList()`. `Arrays` utility: `sort()`, `binarySearch()`, `copyOf()`, `fill()`, `asList()` (fixed-size list trap). `Comparable` vs `Comparator` — single vs multiple sort criteria, `compareTo()` vs `compare()`, natural ordering. |
| 1 hr | **Generics (Complete)** | Why generics — type safety, no casting. Generic classes, generic methods, generic interfaces. Type parameters (`T`, `E`, `K`, `V`, `?`). Bounded type parameters — `<T extends Number>`, `<T extends Comparable<T>>`. Wildcards — `?` (unbounded), `? extends T` (upper bound — producer), `? super T` (lower bound — consumer). PECS principle (Producer Extends, Consumer Super). Type erasure — how generics work at compile time, bridge methods. Restrictions: no primitive types, no `new T()`, no `new T[]`, no `instanceof` with parameterized type. |
| 30 min | **Practice** | ConcurrentHashMap vs Hashtable comparison table. Generic method to find max in a list. PECS example with `List<? extends Number>` and `List<? super Integer>`. |

---

### Day 6 (Sat, Aug 23) — Multithreading & Concurrency (Complete)

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1 hr | **Thread Basics** | Creating threads — `Thread` class vs `Runnable` interface vs `Callable` interface. Thread lifecycle — NEW → RUNNABLE → (BLOCKED / WAITING / TIMED_WAITING) → TERMINATED. `start()` vs `run()`. `sleep()` — releases CPU but not lock. `join()` — wait for thread to complete. `yield()` — hint to scheduler. `isAlive()`, `setName()`, `getName()`, `currentThread()`. Thread priority (1-10, `MIN_PRIORITY`, `NORM_PRIORITY`, `MAX_PRIORITY`). Daemon threads (`setDaemon()`, `isDaemon()`). |
| 1 hr | **Synchronization** | Race condition — what & why. `synchronized` method — intrinsic lock on `this` (instance) or `Class` (static). `synchronized` block — fine-grained locking. `volatile` — visibility guarantee, no caching in thread-local. Difference: `synchronized` (mutual exclusion + visibility) vs `volatile` (visibility only). `wait()` / `notify()` / `notifyAll()` — inter-thread communication, must be called from synchronized context, spurious wakeups. Producer-Consumer problem implementation. |
| 1 hr | **Concurrency Issues** | Deadlock — conditions (mutual exclusion, hold & wait, no preemption, circular wait), detection, prevention. Livelock — threads actively responding but making no progress. Starvation — thread never gets CPU. Thread safety techniques — synchronization, immutable objects, thread-local, atomic classes. |
| 1.5 hr | **java.util.concurrent Package** | `ExecutorService` — `newFixedThreadPool()`, `newCachedThreadPool()`, `newSingleThreadExecutor()`, `newScheduledThreadPool()`. `ThreadPoolExecutor` — core pool size, max pool size, keep alive time, work queue, rejection policies (AbortPolicy, CallerRunsPolicy, DiscardPolicy, DiscardOldestPolicy). `Callable` vs `Runnable` — return value, checked exception. `Future` — `get()`, `isDone()`, `cancel()`. `CountDownLatch` — count down and await. `CyclicBarrier` — barrier point, reusable. `Semaphore` — permits-based access control. `ReentrantLock` — explicit lock, `tryLock()`, `lockInterruptibly()`, fairness. `ReadWriteLock` — multiple readers, single writer. `CompletableFuture` (Java 8) — `supplyAsync()`, `thenApply()`, `thenAccept()`, `thenRun()`, `thenCombine()`, `thenCompose()`, `allOf()`, `anyOf()`, exception handling (`exceptionally()`, `handle()`). `Atomic` classes — `AtomicInteger`, `AtomicLong`, `AtomicBoolean`, `AtomicReference`, CAS operation. |
| 30 min | **Practice** | Implement producer-consumer using `wait()`/`notify()` and using `BlockingQueue`. Create a deadlock scenario and fix it. Use `CompletableFuture` to chain 3 async operations. |

---

### Day 7 (Sun, Aug 24) — Java 8/9/11+ Features + Serialization + Reflection + JVM

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1.5 hr | **Java 8 — Lambda & Functional Interfaces** | Lambda syntax — `() -> {}`, `(a) -> expression`, `(a, b) -> { return result; }`. Functional interface — exactly one abstract method. `@FunctionalInterface`. All built-in functional interfaces: `Predicate<T>` (`test()`), `Function<T,R>` (`apply()`), `Consumer<T>` (`accept()`), `Supplier<T>` (`get()`), `BiPredicate<T,U>`, `BiFunction<T,U,R>`, `BiConsumer<T,U>`, `UnaryOperator<T>` (extends Function), `BinaryOperator<T>` (extends BiFunction). Method references — 4 types: static (`Integer::parseInt`), instance of particular object (`System.out::println`), instance of arbitrary object (`String::toLowerCase`), constructor (`ArrayList::new`). Variable capture — effectively final. |
| 1.5 hr | **Java 8 — Streams (Complete)** | Creating streams: `Collection.stream()`, `Stream.of()`, `Arrays.stream()`, `Stream.iterate()`, `Stream.generate()`, `IntStream.range()`, `Files.lines()`. Intermediate operations (lazy, return stream): `filter()`, `map()`, `flatMap()`, `distinct()`, `sorted()` / `sorted(Comparator)`, `peek()`, `limit()`, `skip()`, `mapToInt()` / `mapToLong()` / `mapToDouble()`. Terminal operations (trigger pipeline): `forEach()`, `forEachOrdered()`, `collect()`, `toArray()`, `reduce()`, `count()`, `min()`, `max()`, `findFirst()`, `findAny()`, `anyMatch()`, `allMatch()`, `noneMatch()`. `Collectors` in detail: `toList()`, `toSet()`, `toMap()`, `toUnmodifiableList()`, `joining()`, `counting()`, `summarizingInt()`, `averagingDouble()`, `groupingBy()` (single & multi-level), `partitioningBy()`, `reducing()`, `collectingAndThen()`. Parallel streams: `parallelStream()`, `parallel()`, ForkJoinPool, ordering, thread safety, when to use/avoid. Stream pipeline internals — lazy evaluation, short-circuiting. |
| 1 hr | **Java 8 — Optional + Date/Time** | `Optional` — why (avoid NullPointerException). `Optional.of()`, `Optional.ofNullable()`, `Optional.empty()`. `isPresent()`, `isEmpty()` (Java 11), `ifPresent()`, `ifPresentOrElse()` (Java 9). `get()`, `orElse()`, `orElseGet()` (lazy), `orElseThrow()`. `map()`, `flatMap()`, `filter()`. Anti-patterns: `Optional.get()` without check, `Optional` for fields/parameters. **Date/Time API**: `LocalDate`, `LocalTime`, `LocalDateTime`, `ZonedDateTime`, `OffsetDateTime`, `Instant`, `Duration` (time-based), `Period` (date-based), `DateTimeFormatter`, `TemporalAdjusters` (`firstDayOfMonth()`, `next(DayOfWeek.MONDAY)`). Converting from legacy: `Date.toInstant()`, `Instant.toEpochMilli()`. |
| 1 hr | **Java 9/10/11/14/17 Features** | **Java 9**: Modules (JPMS — `module-info.java`), immutable collections (`List.of()`, `Set.of()`, `Map.of()`), private methods in interfaces, `Optional.ifPresentOrElse()`, `Optional.or()`, `Stream.takeWhile()`, `Stream.dropWhile()`, `Stream.ofNullable()`, `Collectors.toUnmodifiableList()`, JShell. **Java 10**: `var` (local variable type inference — where allowed and not). **Java 11**: `String.isBlank()`, `String.strip()`, `String.repeat()`, `String.lines()`, `Files.readString()`, `Files.writeString()`, `HttpClient` API, `Predicate.not()`, `Optional.isEmpty()`, `var` in lambdas. **Java 14+**: `switch` expressions (`->`, `yield`), Records (`record Point(int x, int y) {}`), `instanceof` pattern matching (`if (obj instanceof String s)`), text blocks (`"""`). **Java 17**: Sealed classes (`sealed`, `permits`, `non-sealed`). |
| 30 min | **Serialization & Cloning** | `Serializable` — marker interface, `serialVersionUID` (why important), `transient` keyword. Custom serialization — `writeObject()`, `readObject()`. `Externalizable` — `writeExternal()`, `readExternal()`. Serialization proxy pattern. Shallow copy vs deep copy. `Cloneable` interface, `clone()` method, implementing deep clone. |
| 30 min | **Reflection & Annotations** | `Class.forName()`, `getClass()`, `getConstructors()`, `getMethods()`, `getDeclaredFields()`, `setAccessible(true)`, `invoke()`. Why reflection breaks encapsulation. Use in frameworks (Spring DI, Hibernate). Built-in annotations: `@Override`, `@Deprecated`, `@SuppressWarnings`, `@FunctionalInterface`, `@SafeVarargs`. Meta-annotations: `@Target`, `@Retention` (SOURCE, CLASS, RUNTIME), `@Inherited`, `@Documented`, `@Repeatable`. Custom annotation creation. |
| 30 min | **JVM, Memory & GC** | JVM architecture: ClassLoader → Runtime Data Areas → Execution Engine. ClassLoaders: Bootstrap (rt.jar) → Extension/Platform → Application. Parent delegation model. Runtime Data Areas: Method Area / Metaspace (class metadata), Heap (objects), Stack (frames — local variables, operand stack, frame data), PC Register, Native Method Stack. Execution Engine: Interpreter, JIT Compiler (C1, C2), GC. **Memory**: Stack vs Heap. Heap divisions: Young Gen (Eden + S0 + S1) → Old Gen. Metaspace (Java 8+, replaced PermGen). **GC**: GC roots (local variables, static references, active threads). Mark & Sweep algorithm. Minor GC (Young Gen) vs Major/Full GC (Old Gen). GC algorithms: Serial, Parallel, CMS (Concurrent Mark Sweep), G1 (Garbage First — Java 9+ default), ZGC (Java 11+). `System.gc()` — suggestion only. Memory leaks in Java — common causes. `WeakReference`, `SoftReference`, `PhantomReference`. **JMM**: happens-before, volatile semantics, atomicity. |
| 30 min | **I/O & NIO** | Byte streams: `InputStream`, `OutputStream`, `FileInputStream`, `FileOutputStream`, `BufferedInputStream`, `BufferedOutputStream`. Character streams: `Reader`, `Writer`, `FileReader`, `FileWriter`, `BufferedReader`, `BufferedWriter`, `PrintWriter`. `InputStreamReader`, `OutputStreamWriter` — bridge. NIO: `Path`, `Paths`, `Files` (`readAllLines()`, `write()`, `copy()`, `move()`, `delete()`, `exists()`, `walk()`). Channels and Buffers (conceptual). |
| 30 min | **Week 1 Comprehensive Revision** | Review all notes from Days 1–6. Quick-fire: answer 30 Java Core + Java 8 questions aloud. |

---

## 📅 WEEK 2 (Days 8–14): Spring Ecosystem + SQL & Database — Basic to Advanced

---

### Day 8 (Mon, Aug 25) — Spring Core + Spring Boot Fundamentals

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1 hr | **Spring Core — IoC & DI** | Inversion of Control — framework controls object creation. Dependency Injection — 3 types: constructor injection (recommended), setter injection, field injection (not recommended — why). `@Autowired` — by type, `@Qualifier` — by name, `@Primary` — default bean. `@Value` — inject properties. `ApplicationContext` vs `BeanFactory` — eager vs lazy, additional features (events, i18n, AOP). XML config vs Java config vs Annotation config — evolution. |
| 1 hr | **Bean Lifecycle & Scopes** | Complete lifecycle: Instantiation → Populate Properties → `BeanNameAware.setBeanName()` → `BeanFactoryAware.setBeanFactory()` → `ApplicationContextAware.setApplicationContext()` → `BeanPostProcessor.postProcessBeforeInitialization()` → `@PostConstruct` / `InitializingBean.afterPropertiesSet()` → `BeanPostProcessor.postProcessAfterInitialization()` → **Bean Ready** → `@PreDestroy` / `DisposableBean.destroy()`. Scopes: `singleton` (default — one per Spring container), `prototype` (new instance each time — no destroy callback), `request` (per HTTP request), `session` (per HTTP session), `application` (per ServletContext), `websocket`. Scope gotcha: injecting prototype into singleton (use `ObjectFactory`, `Provider`, or `@Lookup`). |
| 1 hr | **Spring Boot Fundamentals** | `@SpringBootApplication` = `@Configuration` + `@EnableAutoConfiguration` + `@ComponentScan`. Auto-configuration: `spring.factories` / `AutoConfiguration.imports`, `@Conditional` annotations (`@ConditionalOnClass`, `@ConditionalOnMissingBean`, `@ConditionalOnProperty`). Starters — what they contain (dependencies + auto-config). `application.properties` vs `application.yml`. Profiles — `@Profile`, `spring.profiles.active`, profile-specific files. Externalized configuration — property source priority order (command line > env variables > application.properties > defaults). Embedded server (Tomcat/Jetty/Undertow). Spring Boot DevTools — auto-restart, live reload. |
| 1 hr | **Stereotype Annotations & Component Scanning** | `@Component` — generic. `@Service` — business logic. `@Repository` — data access (exception translation). `@Controller` — web MVC. `@RestController` = `@Controller` + `@ResponseBody`. `@Configuration` — Java config class. `@Bean` — method-level bean declaration. `@ComponentScan` — base packages. `@Lazy` — lazy initialization. `@Scope` — bean scope. `@Order` / `@Priority` — bean ordering. |
| 30 min | **Practice** | Draw the complete Spring Bean lifecycle from memory. Explain `@SpringBootApplication` auto-configuration flow. List all `@Conditional` annotations you know. |

---

### Day 9 (Tue, Aug 26) — Spring MVC + REST API (Complete)

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 45 min | **Spring MVC Architecture** | `DispatcherServlet` — front controller. Request flow: Client → `DispatcherServlet` → `HandlerMapping` → `HandlerAdapter` → `Controller` → `ViewResolver` → View → Response. `@EnableWebMvc`. Content negotiation. |
| 1 hr | **Request Handling Annotations** | `@RequestMapping` (method, path, params, headers, consumes, produces). Shortcut annotations: `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`, `@PatchMapping`. `@PathVariable` — URI template variables. `@RequestParam` — query parameters (required, defaultValue). `@RequestBody` — JSON → Java object (Jackson). `@RequestHeader` — access HTTP headers. `@CookieValue` — access cookies. `@ModelAttribute` — bind form data. `@CrossOrigin` — CORS at controller/method level. |
| 1 hr | **Response Handling & Validation** | `ResponseEntity<T>` — status code + headers + body. `@ResponseBody` — Java object → JSON. `@ResponseStatus` — set HTTP status. HTTP status codes: 200 OK, 201 Created, 204 No Content, 301 Moved Permanently, 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found, 405 Method Not Allowed, 409 Conflict, 415 Unsupported Media Type, 500 Internal Server Error. **Validation**: `@Valid`, `@Validated`. `@NotNull`, `@NotBlank`, `@NotEmpty`, `@Size`, `@Min`, `@Max`, `@Email`, `@Pattern`, `@Past`, `@Future`, `@Positive`, `@Negative`. `BindingResult`. Custom validator — implement `ConstraintValidator`. Validation groups. |
| 1 hr | **Exception Handling** | `@ExceptionHandler` — method-level. `@ControllerAdvice` / `@RestControllerAdvice` — global. `ResponseEntityExceptionHandler` — extend for custom handling. Custom error response DTO. Mapping exceptions to HTTP status codes. `@ResponseStatus` on custom exception class. Problem Details (RFC 7807) — `ProblemDetail` (Spring 6+). |
| 45 min | **Filters, Interceptors & AOP** | `Filter` (Servlet spec) — `doFilter()`, `FilterChain`, `@Order`, applies to all requests. `HandlerInterceptor` (Spring MVC) — `preHandle()`, `postHandle()`, `afterCompletion()`, applies to controller requests only. `@ControllerAdvice` — aspect-oriented for controllers. Order of execution: Filter → Interceptor → AOP → Controller. When to use which. |
| 30 min | **Practice** | Design complete REST API for Patient E-Chart module: all endpoints, request/response DTOs, validation, exception handling, status codes. |

---

### Day 10 (Wed, Aug 27) — Spring Data JPA + Hibernate + Transactions

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1 hr | **JPA Basics & Entity Mapping** | JPA vs Hibernate — specification vs implementation. `@Entity`, `@Table(name)`, `@Id`, `@GeneratedValue` (strategies: AUTO, IDENTITY, SEQUENCE, TABLE). `@Column` (name, nullable, unique, length, precision, scale). `@Temporal`, `@Lob`, `@Enumerated` (ORDINAL vs STRING). `@Transient` (JPA) vs `transient` (Java). `@Embeddable` / `@Embedded` — composite value type. `@MappedSuperclass` — common fields (id, createdDate, updatedDate). |
| 1 hr | **Relationships** | `@OneToOne` — shared primary key, foreign key, join table. `@OneToMany` / `@ManyToOne` — bidirectional (owning side has `@JoinColumn`, inverse side has `mappedBy`). `@ManyToMany` — `@JoinTable`, junction table. Cascade types: `PERSIST`, `MERGE`, `REMOVE`, `REFRESH`, `DETACH`, `ALL`. `orphanRemoval = true`. Fetch types: `LAZY` (proxy/collection wrapper) vs `EAGER` (immediate loading). Defaults: `@OneToMany` → LAZY, `@ManyToOne` → EAGER. |
| 1 hr | **N+1 Problem & Solutions + JPA Internals** | N+1 problem — what, why, detection (Hibernate SQL logs). Solutions: `JOIN FETCH` in JPQL, `@EntityGraph` (named and ad-hoc), `@BatchSize`, `@Fetch(FetchMode.SUBSELECT)`. **EntityManager**: `persist()`, `merge()`, `remove()`, `find()`, `createQuery()`. Entity states: Transient → Managed (attached) → Detached → Removed. Persistence context — first-level cache, dirty checking (automatic flush). First-level cache vs Second-level cache (EhCache, Redis). `@Cacheable` (JPA). |
| 45 min | **Spring Data JPA Repositories & Queries** | `CrudRepository` → `PagingAndSortingRepository` → `JpaRepository` — method hierarchy. Derived query methods: `findByName()`, `findByNameAndAge()`, `findByNameOrderByAgeDesc()`, `findByNameContaining()`, `findByAgeGreaterThan()`, `countByStatus()`, `deleteByName()`, `existsByEmail()`. `@Query` — JPQL (`@Query("SELECT p FROM Patient p WHERE p.name = :name")`). `@Query` — native SQL (`nativeQuery = true`). Named parameters (`:name`) vs positional parameters (`?1`). `@Modifying` + `@Query` for UPDATE/DELETE. Pagination: `Pageable`, `PageRequest.of()`, `Page<T>`, `Slice<T>`. Sorting: `Sort.by()`. Specifications — dynamic queries using `Specification<T>`. Projections — interface-based, class-based, dynamic. Auditing — `@CreatedDate`, `@LastModifiedDate`, `@CreatedBy`, `@LastModifiedBy`, `@EnableJpaAuditing`. |
| 45 min | **Transactions** | `@Transactional` — how it works (AOP proxy). Propagation types: `REQUIRED` (default — join existing or create new), `REQUIRES_NEW` (always new, suspend existing), `NESTED` (savepoint within existing), `SUPPORTS` (use if exists, else non-transactional), `NOT_SUPPORTED` (suspend existing), `MANDATORY` (must exist, else exception), `NEVER` (must not exist, else exception). Isolation levels: `READ_UNCOMMITTED` (dirty read), `READ_COMMITTED` (no dirty read), `REPEATABLE_READ` (no non-repeatable read), `SERIALIZABLE` (no phantom read). `readOnly = true` — optimization hint. `rollbackFor`, `noRollbackFor`. `@Transactional` pitfalls: self-invocation (proxy bypass), private methods, exception handling (only unchecked exceptions rollback by default). |
| 30 min | **Practice** | Design JPA entities for Patient-Admission-Doctor with all relationships. Explain N+1 problem and fix it. Explain `@Transactional` propagation with real scenarios. |

---

### Day 11 (Thu, Aug 28) — Spring Security + AOP + Testing + Caching + Scheduling

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1 hr | **Spring Security** | Authentication (who are you?) vs Authorization (what can you do?). `SecurityFilterChain` configuration. `UserDetailsService` / `UserDetails`. `PasswordEncoder` — `BCryptPasswordEncoder`. Form login, HTTP Basic. Method security: `@PreAuthorize("hasRole('ADMIN')")`, `@PostAuthorize`, `@Secured`, `@RolesAllowed`. CORS configuration — `@CrossOrigin`, global config via `WebMvcConfigurer`. CSRF protection — when to enable/disable. Security filter chain order. |
| 45 min | **JWT Authentication** | JWT structure: Header (algorithm, type) + Payload (claims — `sub`, `exp`, `iat`, custom) + Signature. Flow: login → validate credentials → generate JWT → return token → client sends token in `Authorization: Bearer <token>` header → filter validates token → set authentication in `SecurityContext`. Refresh token concept. Stateless authentication — no server-side session. JWT advantages and disadvantages. |
| 45 min | **Spring AOP** | Cross-cutting concerns — logging, security, transactions, caching. Terminology: Aspect, Advice, Pointcut, Join Point, Weaving. Advice types: `@Before`, `@After`, `@AfterReturning`, `@AfterThrowing`, `@Around` (most powerful — `ProceedingJoinPoint`). Pointcut expressions: `execution()`, `within()`, `@annotation()`. AOP proxy — JDK Dynamic Proxy (interface-based) vs CGLIB Proxy (class-based). How `@Transactional` uses AOP. Custom AOP for logging, performance measurement. |
| 45 min | **Testing** | JUnit 5 — `@Test`, `@BeforeEach`, `@AfterEach`, `@BeforeAll`, `@AfterAll`, `@DisplayName`, `@Disabled`, `@ParameterizedTest`, `@ValueSource`, assertions (`assertEquals`, `assertTrue`, `assertThrows`, `assertAll`). Mockito — `@Mock`, `@InjectMocks`, `when().thenReturn()`, `when().thenThrow()`, `verify()`, `times()`, `never()`, `ArgumentCaptor`, `@Spy`, `doReturn().when()`. Spring Boot testing: `@SpringBootTest`, `@WebMvcTest` (controller layer), `@DataJpaTest` (repository layer), `@MockBean`. `MockMvc` — `perform()`, `andExpect()`, `status()`, `content()`, `jsonPath()`. Test slices — testing individual layers. |
| 45 min | **Caching, Scheduling, Async, Logging** | **Caching**: `@EnableCaching`, `@Cacheable(value, key)`, `@CachePut`, `@CacheEvict(allEntries)`. Cache providers — default (ConcurrentHashMap), EhCache, Redis (conceptual). **Scheduling**: `@EnableScheduling`, `@Scheduled(fixedRate, fixedDelay, cron)`. Cron expression — `second minute hour dayOfMonth month dayOfWeek`. **Async**: `@EnableAsync`, `@Async`, `CompletableFuture` return type, custom `TaskExecutor`. **Logging**: SLF4J facade, Logback implementation, log levels (TRACE < DEBUG < INFO < WARN < ERROR), `@Slf4j` (Lombok), MDC (Mapped Diagnostic Context). |
| 30 min | **REST API Design Best Practices + Swagger** | Resource naming: nouns, plural (`/api/patients`, not `/api/getPatient`). Versioning: URI (`/api/v1/`), header, query param. HATEOAS (awareness). Idempotency: GET, PUT, DELETE are idempotent; POST is not. PUT (full update) vs PATCH (partial update). Pagination: `?page=0&size=10&sort=name,asc`. Swagger / OpenAPI / SpringDoc — `@Operation`, `@ApiResponse`, `@Schema`. |

---

### Day 12 (Fri, Aug 29) — Microservices Architecture (Complete)

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 45 min | **Monolith vs Microservices** | Monolith — single deployable unit, advantages (simple development, testing, deployment), disadvantages (tight coupling, scaling limitations, technology lock-in, large codebase). Microservices — independently deployable services, advantages (independent scaling, technology diversity, fault isolation, team autonomy), disadvantages (complexity, distributed system challenges, data consistency, network latency). When to use each. Strangler Fig pattern — migrating monolith to microservices. |
| 45 min | **Communication & API Gateway** | Synchronous: REST (HTTP), gRPC (Protocol Buffers — awareness). Asynchronous: message queues (Kafka, RabbitMQ), event-driven architecture. API Gateway: single entry point, responsibilities (routing, authentication, rate limiting, load balancing, request/response transformation, circuit breaking). Spring Cloud Gateway — routes, predicates, filters. Netflix Zuul (legacy). Backend for Frontend (BFF) pattern. |
| 45 min | **Service Discovery & Config** | Service Discovery: why needed (dynamic IP/port). Client-side discovery — Eureka (Netflix). Server-side discovery — Consul, Kubernetes DNS. Eureka Server (`@EnableEurekaServer`), Eureka Client (`@EnableEurekaClient`). Service registry, heartbeat, self-preservation mode. Spring Cloud Config Server: centralized configuration, Git-backed, `@RefreshScope`, bus refresh. Config client — bootstrap.yml. |
| 45 min | **Resilience Patterns** | Circuit Breaker: states (CLOSED → OPEN → HALF_OPEN), failure threshold, wait duration. Resilience4j — `@CircuitBreaker`, fallback methods. Retry: `@Retry`, max attempts, wait duration. Rate Limiter: `@RateLimiter`, limit for period. Bulkhead: `@Bulkhead`, thread pool isolation, semaphore isolation. Time Limiter: `@TimeLimiter`, timeout duration. |
| 45 min | **Distributed Systems Concepts** | Load Balancing: client-side (Spring Cloud LoadBalancer, Ribbon — legacy), server-side (Nginx, HAProxy). Distributed Tracing: Sleuth + Zipkin / Micrometer Tracing, trace ID, span ID — tracing request across services. Centralized Logging: ELK stack (Elasticsearch, Logstash, Kibana) awareness. Health Checks: Actuator `/health`, `/info`, readiness vs liveness probes. |
| 45 min | **Advanced Patterns & Concepts** | Saga Pattern: distributed transactions — choreography (events) vs orchestration (central coordinator). CQRS: separate read and write models. Event Sourcing (awareness). 12-Factor App: codebase, dependencies, config, backing services, build/release/run, processes, port binding, concurrency, disposability, dev/prod parity, logs, admin processes. Containerization: Docker basics (Dockerfile, image, container, multi-stage build), docker-compose, Kubernetes awareness (Pod, Service, Deployment, ConfigMap, Secret). |
| 30 min | **Practice** | Draw a complete microservices architecture for a healthcare system with all patterns. Explain how a request flows from API Gateway through service discovery to the target service and back. |

---

### Day 13 (Sat, Aug 30) — SQL & Database (Part 1 — Fundamentals to Intermediate)

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 45 min | **SQL Categories & Basics** | DDL: `CREATE TABLE` (with all constraints — `PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, `NOT NULL`, `CHECK`, `DEFAULT`), `ALTER TABLE` (ADD, DROP, MODIFY column, ADD/DROP constraint), `DROP TABLE`, `TRUNCATE TABLE` (vs DELETE — no logging, resets identity), `RENAME`. DML: `INSERT INTO` (single row, multi-row, INSERT INTO...SELECT), `UPDATE` (single/multi table), `DELETE` (single/multi table, DELETE vs TRUNCATE vs DROP). DCL: `GRANT`, `REVOKE`. TCL: `COMMIT`, `ROLLBACK`, `SAVEPOINT`, `SET TRANSACTION`. |
| 1 hr | **SELECT & Filtering** | `SELECT` all columns, specific columns, aliases. `WHERE` clause — comparison operators (`=`, `<>`, `<`, `>`, `<=`, `>=`), `AND`, `OR`, `NOT`, `IN`, `NOT IN`, `BETWEEN`, `LIKE` (wildcards: `%`, `_`), `IS NULL`, `IS NOT NULL`. `ORDER BY` (ASC, DESC, multiple columns). `DISTINCT`. `LIMIT`/`TOP`/`FETCH FIRST`. `GROUP BY` — grouping rules (every non-aggregated column must be in GROUP BY). `HAVING` — filter after grouping (vs WHERE — filter before grouping). Aggregate functions: `COUNT(*)`, `COUNT(column)`, `COUNT(DISTINCT column)`, `SUM()`, `AVG()`, `MIN()`, `MAX()`, `STRING_AGG()`/`GROUP_CONCAT()`. |
| 1.5 hr | **Joins (Complete)** | `INNER JOIN` — matching rows in both tables. `LEFT JOIN` (LEFT OUTER JOIN) — all from left + matching from right. `RIGHT JOIN` — all from right + matching from left. `FULL OUTER JOIN` — all from both. `CROSS JOIN` — Cartesian product. `SELF JOIN` — join table with itself (manager-employee, recursive relationships). `NATURAL JOIN` — join on common column names (avoid in production). Multiple joins in single query. Join vs subquery — performance comparison. Practice queries: employees with their departments, employees without departments (LEFT JOIN + IS NULL), employees and their managers (SELF JOIN), all combinations of products and categories (CROSS JOIN). |
| 1 hr | **Subqueries & Set Operations** | Scalar subquery — returns single value. Column subquery — returns single column. Row subquery — returns single row. Table subquery — returns multiple rows and columns. Correlated subquery — references outer query (executed once per outer row). `EXISTS` vs `IN` — performance difference (EXISTS for large subquery, IN for small). `NOT EXISTS`, `NOT IN` (NULL trap). Subquery in SELECT, WHERE, FROM (derived table), HAVING. Set operations: `UNION` (distinct), `UNION ALL` (with duplicates), `INTERSECT`, `EXCEPT`/`MINUS`. Rules — same number of columns, compatible data types. |
| 1 hr | **CTE & CASE** | CTE: `WITH cte_name AS (SELECT ...) SELECT * FROM cte_name`. Multiple CTEs. Recursive CTE — anchor member + recursive member (hierarchical queries: org chart, category tree). CTE vs subquery vs temp table — readability, reuse, performance. `CASE` expression: simple (`CASE column WHEN value THEN result`) and searched (`CASE WHEN condition THEN result`). CASE in SELECT, WHERE, ORDER BY, UPDATE, GROUP BY. `IIF()` (SQL Server), `DECODE()` (Oracle). `COALESCE()`, `NULLIF()`, `ISNULL()`/`IFNULL()`. |
| 30 min | **Practice** | Write queries: 2nd highest salary (3 different ways), employees earning more than their manager (SELF JOIN), departments with more than 5 employees, employees who joined in the last 30 days. |

---

### Day 14 (Sun, Aug 31) — SQL & Database (Part 2 — Advanced) + Week 2 Revision

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1.5 hr | **Window Functions (Complete)** | Syntax: `function() OVER (PARTITION BY col ORDER BY col ROWS BETWEEN ...)`. Ranking: `ROW_NUMBER()` (unique sequential), `RANK()` (gaps on ties), `DENSE_RANK()` (no gaps), `NTILE(n)` (divide into n groups). Value: `LEAD(col, offset, default)` — next row value, `LAG(col, offset, default)` — previous row value, `FIRST_VALUE()`, `LAST_VALUE()`. Aggregate as window: `SUM() OVER()`, `AVG() OVER()`, `COUNT() OVER()`, `MIN() OVER()`, `MAX() OVER()` — running totals, moving averages. Frame clause: `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`, `ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING`, `RANGE BETWEEN`. `PARTITION BY` — window within groups. Practice: nth highest salary per department, running total, year-over-year comparison, consecutive days of activity. |
| 1 hr | **Indexes & Query Optimization** | Clustered index — physical data order, only one per table, primary key auto-creates. Non-clustered index — separate structure, pointer to data, multiple per table. Composite index — multiple columns, column order matters (leftmost prefix rule). Covering index — includes all columns needed by query (no key lookup). Unique index, filtered index, full-text index. Index scan vs index seek — seek is better (uses index tree). Key lookup — additional read for non-covered columns. When to create indexes (frequent WHERE, JOIN, ORDER BY columns). When NOT to (small tables, frequently updated columns, low cardinality). Execution plans — how to read (SQL Server: `SET SHOWPLAN_TEXT ON`, SSMS graphical plan). Query optimization: avoid `SELECT *`, avoid functions on indexed columns (non-sargable), use EXISTS instead of COUNT for existence check, avoid implicit type conversion, use parameterized queries. |
| 1 hr | **Stored Procedures, Functions & Triggers** | Stored Procedure: `CREATE PROCEDURE`, input/output parameters, `EXEC`, `BEGIN...END`, variables (`DECLARE`, `SET`), control flow (`IF...ELSE`, `WHILE`, `CASE`), `TRY...CATCH` (error handling), `@@ERROR`, `RAISERROR`/`THROW`. Dynamic SQL — `sp_executesql` (parameterized — prevents SQL injection), `EXEC(@sql)`. Functions: scalar (returns single value), inline table-valued (returns table, single SELECT), multi-statement table-valued. Function vs procedure — function in SELECT, procedure standalone. Triggers: `AFTER`/`FOR` triggers (after DML), `INSTEAD OF` triggers (replaces DML). `INSERTED` and `DELETED` special tables. Use cases — audit logging, cascading updates. Why to use triggers carefully. Cursors: `DECLARE CURSOR`, `OPEN`, `FETCH NEXT`, `CLOSE`, `DEALLOCATE`. Types: `STATIC`, `DYNAMIC`, `FORWARD_ONLY`, `KEYSET`. Why to avoid (row-by-row processing — prefer set-based operations). |
| 1 hr | **Normalization, ACID & Transactions** | Normalization: 1NF (atomic values, no repeating groups), 2NF (1NF + no partial dependency — all non-key columns depend on entire primary key), 3NF (2NF + no transitive dependency — non-key columns depend only on primary key), BCNF (every determinant is a candidate key), 4NF (no multi-valued dependencies), 5NF (no join dependencies). Denormalization — when and why (performance, reporting, read-heavy workloads). ACID: Atomicity (all or nothing), Consistency (valid state to valid state), Isolation (concurrent transactions), Durability (committed = permanent). Transaction isolation levels: Read Uncommitted (dirty read), Read Committed (no dirty read — SQL Server default), Repeatable Read (no non-repeatable read — MySQL InnoDB default), Serializable (no phantom read), Snapshot (MVCC — row versioning). Locking: shared lock (S — read), exclusive lock (X — write), update lock (U — intent to write), intent locks (IS, IX). Deadlock — detection, prevention (consistent lock order, timeout). Lock escalation — row → page → table. |
| 1 hr | **Advanced SQL** | Temp tables: `#temp` (local), `##temp` (global) — scope, performance. Table variables: `DECLARE @t TABLE(...)` — scope within batch. CTE vs temp table vs table variable — comparison. `MERGE` statement — UPSERT (`WHEN MATCHED THEN UPDATE`, `WHEN NOT MATCHED THEN INSERT`, `WHEN NOT MATCHED BY SOURCE THEN DELETE`). PIVOT: rows to columns. UNPIVOT: columns to rows. String functions: `CONCAT()`, `SUBSTRING()`, `LEN()`, `UPPER()`, `LOWER()`, `TRIM()`, `LTRIM()`, `RTRIM()`, `REPLACE()`, `STUFF()`, `CHARINDEX()`, `PATINDEX()`, `REVERSE()`, `REPLICATE()`, `LEFT()`, `RIGHT()`, `FORMAT()`. Date functions: `GETDATE()`, `SYSDATETIME()`, `DATEADD()`, `DATEDIFF()`, `DATEPART()`, `DATENAME()`, `YEAR()`, `MONTH()`, `DAY()`, `EOMONTH()`, `FORMAT()`, `CAST()`, `CONVERT()`. |
| 1.5 hr | **Practice + Week 2 Revision** | Complex queries: running total using window functions, employees with consecutive absences (LAG/LEAD), department-wise salary percentile (NTILE), pivot sales data by month. **Week 2 Revision**: Rapid-fire 30 questions covering Spring Boot + SQL. Review all annotation cheat sheets. |

---

## 📅 WEEK 3 (Days 15–21): DSA + Design Patterns + System Design + Tools

---

### Day 15 (Mon, Sep 1) — Arrays & Strings (All Patterns)

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 30 min | **Time & Space Complexity** | Big O notation — O(1), O(log n), O(n), O(n log n), O(n²), O(2ⁿ), O(n!). Best, average, worst case. Amortized analysis (ArrayList `add()`). Space complexity — auxiliary space vs total space. Analyzing nested loops, recursive calls. |
| 1.5 hr | **Arrays — All Patterns** | Traversal: reverse array, rotate array (left/right by k), move zeros to end. Two-pointer: two sum (sorted array), container with most water, remove duplicates from sorted array, sort colors (Dutch National Flag). Sliding window: max sum subarray of size k, longest substring with k distinct characters, minimum window substring. Prefix sum: subarray sum equals k, range sum query. Kadane's algorithm: maximum subarray sum. Other: merge two sorted arrays, find missing number, majority element (Boyer-Moore), stock buy/sell, product of array except self, trap rain water (awareness). |
| 1.5 hr | **Strings — All Patterns** | Basic: reverse string, check palindrome, check anagram, count characters/words. Pattern: longest substring without repeating characters (sliding window + hashmap), longest palindromic substring, string to integer (atoi), group anagrams, valid parentheses (stack), longest common prefix, string compression ("aabccc" → "a2b1c3"). Conversion: string → integer, integer → string, Roman to integer. |
| 30 min | **Practice** | Solve 8 problems: 3 array (two-pointer, sliding window, Kadane's), 3 string (palindrome, anagram, longest substring), 2 mixed. |

---

### Day 16 (Tue, Sep 2) — Sorting, Searching & Hashing

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1.5 hr | **Sorting Algorithms (All)** | Bubble Sort — O(n²), stable, adaptive (best O(n)). Selection Sort — O(n²), unstable, not adaptive. Insertion Sort — O(n²), stable, adaptive, good for small/nearly sorted. Merge Sort — O(n log n), stable, not in-place (O(n) space), divide and conquer. Quick Sort — O(n log n) average / O(n²) worst, unstable, in-place, pivot selection (first, last, random, median-of-three), Lomuto vs Hoare partition. Heap Sort — O(n log n), unstable, in-place. Counting Sort — O(n+k), stable, non-comparison, for limited range integers. Radix Sort — O(d × (n+k)), stable, digit-by-digit. Comparison table: time (best/avg/worst), space, stable?, in-place?, adaptive?. |
| 1 hr | **Searching Algorithms** | Linear Search — O(n), unsorted data. Binary Search — O(log n), sorted data only. Iterative vs recursive implementation. Variations: first occurrence, last occurrence, lower bound, upper bound. Search in rotated sorted array. Find peak element. Square root using binary search. Search in 2D sorted matrix. Binary search on answer (awareness). |
| 1 hr | **Hashing** | Hash function — converting key to index. Collision resolution: chaining (linked list at each slot), open addressing (linear probing, quadratic probing, double hashing). Load factor and rehashing. HashMap problems: two sum, group anagrams, longest consecutive sequence, subarray sum equals k (prefix sum + hashmap), find duplicates, first non-repeating character, intersection of two arrays, top k frequent elements. HashSet problems: contains duplicate, happy number, longest substring without repeating characters. |
| 30 min | **Practice** | Implement merge sort and quick sort from scratch. Solve 5 hashing problems. |

---

### Day 17 (Wed, Sep 3) — Linked List, Stack & Queue

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1.5 hr | **Linked List** | Singly linked list — insert (beginning, end, position), delete (beginning, end, by value), search, reverse (iterative, recursive). Doubly linked list — insert, delete, reverse. Circular linked list — insert, delete, detect cycle. Problems: reverse linked list, detect cycle (Floyd's — slow/fast pointer), find cycle start, find middle (slow/fast), merge two sorted lists, remove nth node from end (two-pointer), check palindrome, intersection of two lists, add two numbers, remove duplicates from sorted/unsorted list, reverse in groups of k. |
| 1 hr | **Stack** | Implementation: array-based, linked list-based. Operations: push, pop, peek, isEmpty, size — all O(1). Problems: balanced parentheses (3 types), next greater element (monotonic stack), next smaller element, stock span, min stack (O(1) getMin), evaluate postfix expression, infix to postfix conversion, sort a stack using recursion, largest rectangle in histogram (awareness), implement two stacks in one array. Java: `Stack` class (legacy) vs `ArrayDeque` (recommended). |
| 1 hr | **Queue & Deque** | Queue: FIFO — enqueue, dequeue, front, rear. Implementation: array (circular), linked list. Circular queue — front and rear pointers, full vs empty condition. Deque (Double-Ended Queue): insert/delete from both ends. `ArrayDeque` — Java implementation. Priority Queue: min-heap by default, `Comparator` for max-heap. Problems: implement queue using stacks (2 stacks), implement stack using queues, sliding window maximum (deque), generate binary numbers 1 to n, first non-repeating character in stream, rotten oranges (BFS — awareness). |
| 30 min | **Practice** | Solve 3 linked list, 3 stack, 2 queue problems from the above lists. |

---

### Day 18 (Thu, Sep 4) — Trees, Heaps & Tries

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1.5 hr | **Binary Tree** | Terminology: root, node, edge, leaf, parent, child, sibling, depth, height, level, degree. Types: full, complete, perfect, balanced, degenerate/pathological. Traversals: Inorder (left-root-right), Preorder (root-left-right), Postorder (left-right-root) — both recursive and iterative (using stack). Level order (BFS — using queue). Problems: height/max depth, diameter, check if balanced, mirror/invert tree, lowest common ancestor (LCA), path sum, root-to-leaf paths, views (left view, right view, top view, bottom view — using queue + level mapping), zigzag level order traversal, serialize/deserialize (awareness), check if two trees are identical, count nodes in complete binary tree. |
| 1 hr | **Binary Search Tree** | Properties: left < root < right. Operations: search O(h), insert O(h), delete O(h) — 3 cases (leaf, one child, two children — inorder successor/predecessor). Problems: validate BST (inorder should be sorted), kth smallest element (inorder + count), inorder successor, convert sorted array to BST, BST to sorted doubly linked list (awareness), LCA in BST (simpler than binary tree). Self-balancing BSTs (conceptual): AVL tree (balance factor ≤ 1, rotations), Red-Black tree (used in Java TreeMap/TreeSet — properties, color rules). |
| 1 hr | **Heap (Priority Queue)** | Min heap, max heap. Array representation: parent = (i-1)/2, left child = 2i+1, right child = 2i+2. Operations: insert (add at end, bubble up) — O(log n), extractMin/Max (remove root, replace with last, heapify down) — O(log n), peek — O(1), heapify — O(n). Heap Sort — build max heap, extract max repeatedly — O(n log n). Problems: kth largest element, kth smallest element, merge k sorted lists, top k frequent elements, find median from data stream (two heaps), sort nearly sorted array. Java `PriorityQueue` — default min-heap, custom `Comparator` for max-heap. |
| 30 min | **Trie** | Structure: array/map of children, boolean `isEndOfWord`. Operations: insert O(m), search O(m), prefix search O(m) — where m is word length. Applications: autocomplete, spell checker, prefix matching. Space optimization: compressed trie (awareness). |
| 30 min | **Practice** | Solve: BST validation, kth smallest, level order traversal, LCA, kth largest element using heap. |

---

### Day 19 (Fri, Sep 5) — Graphs, Recursion, DP, Greedy & Bit Manipulation

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1 hr | **Graphs** | Terminology: vertex, edge, directed/undirected, weighted/unweighted, degree (in-degree, out-degree), path, cycle, connected component. Representations: adjacency matrix O(V²) space, adjacency list O(V+E) space. BFS — level-by-level traversal, queue-based, shortest path in unweighted graph, time O(V+E). DFS — depth-first traversal, stack/recursion-based, time O(V+E). Connected components — BFS/DFS on unvisited nodes. Cycle detection: undirected (DFS — back edge to non-parent), directed (DFS — back edge / recursion stack). Topological sort — DAG only, DFS-based (reverse postorder), Kahn's algorithm (BFS with in-degree). Shortest path: Dijkstra's (greedy, non-negative weights, O(V²) or O(E log V) with min-heap), Bellman-Ford (handles negative weights, O(VE)). MST: Prim's (greedy, grow tree), Kruskal's (greedy, sort edges, union-find). |
| 1 hr | **Recursion & Backtracking** | Recursion: base case, recursive case, stack overflow. Problems: factorial, Fibonacci, power, sum of digits, reverse string, check palindrome, Tower of Hanoi, print all subsequences. Backtracking: try → check → undo. Problems: generate all subsets (power set), generate all permutations, N-Queens (awareness), Sudoku solver (awareness), rat in a maze, word search, combination sum, letter combinations of phone number. |
| 1.5 hr | **Dynamic Programming** | Memoization (top-down) vs Tabulation (bottom-up). Identifying DP problems: optimal substructure + overlapping subproblems. Steps: define state, write recurrence, add memoization/build table, optimize space if possible. **Must-know problems**: Fibonacci (O(n) time, O(1) space), climbing stairs (1 or 2 steps), coin change (min coins), 0/1 knapsack (include/exclude), longest common subsequence (LCS), longest increasing subsequence (LIS), edit distance (awareness), matrix chain multiplication (awareness), longest palindromic subsequence, subset sum, unbounded knapsack, unique paths in grid. |
| 30 min | **Greedy Algorithms** | Greedy choice: locally optimal → globally optimal. Problems: activity selection (max non-overlapping), fractional knapsack (sort by value/weight), job sequencing with deadlines, minimum platforms, coin change (greedy — when it works and when it doesn't), Huffman coding (awareness), interval scheduling. Greedy vs DP — when greedy works. |
| 30 min | **Bit Manipulation** | Operators: AND (`&`), OR (`\|`), XOR (`^`), NOT (`~`), left shift (`<<`), right shift (`>>`), unsigned right shift (`>>>`). Tricks: check if power of 2 (`n & (n-1) == 0`), count set bits (Brian Kernighan's), toggle bit, set bit, clear bit. Problems: single number (XOR all — duplicates cancel), find two non-repeating numbers, swap without temp (XOR), reverse bits, missing number (XOR approach). |

---

### Day 20 (Sat, Sep 6) — Design Patterns (All) + SOLID + Architecture Principles

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1.5 hr | **Creational Patterns (5)** | **Singleton**: eager (static final instance), lazy (null check), thread-safe synchronized (performance issue), double-checked locking (volatile + synchronized), Bill Pugh (static inner class — best), enum singleton (safest). Breaking singleton: reflection (setAccessible), serialization (readResolve), cloning (override clone). **Factory Method**: define interface, let subclass decide. Example: `ShapeFactory.getShape("circle")`. **Abstract Factory**: factory of related factories. Example: `GUIFactory` → `WindowsFactory`, `MacFactory`. **Builder**: step-by-step construction, immutable objects. Example: `Patient.builder().name("John").age(30).build()`. Lombok `@Builder`. **Prototype**: `clone()`, shallow vs deep copy. Example: `cache.getShape("circle").clone()`. |
| 1.5 hr | **Structural Patterns (7)** | **Adapter**: convert interface A to interface B. Example: `XMLToJSONAdapter`. **Bridge**: decouple abstraction from implementation. Example: `Shape` (abstraction) + `Color` (implementation). **Composite**: tree structure, treat individual and group uniformly. Example: `FileSystem` — File and Directory implement same interface. **Decorator**: add behavior dynamically without subclassing. Example: Java I/O — `BufferedReader(FileReader(file))`. **Facade**: simplified interface to complex subsystem. Example: `OrderFacade` wrapping inventory, payment, shipping services. **Flyweight**: share common state to save memory. Example: `String` pool, `Integer` cache. **Proxy**: surrogate for another object. Types: virtual (lazy loading), protection (access control), remote. Example: Spring AOP proxies, lazy loading in Hibernate. |
| 1.5 hr | **Behavioral Patterns (11)** | **Chain of Responsibility**: pass request along handler chain. Example: Servlet filters, Spring Security filter chain, logging handlers. **Command**: encapsulate request as object. Example: undo/redo, task queue. **Interpreter**: define grammar and interpret sentences. Example: SQL parser, regular expressions (awareness). **Iterator**: traverse collection without exposing internals. Example: Java `Iterator`, `for-each` loop. **Mediator**: reduce direct communication. Example: chat room, air traffic controller. **Memento**: capture and restore state. Example: undo mechanism, game save. **Observer**: one-to-many notification. Example: event listeners, pub-sub, Spring `ApplicationEventPublisher`. **State**: behavior changes based on internal state. Example: order states (NEW → PAID → SHIPPED → DELIVERED). **Strategy**: interchangeable algorithms. Example: `Comparator`, sorting strategies, payment methods. **Template Method**: define algorithm skeleton, let subclasses fill in steps. Example: `JdbcTemplate`, `RestTemplate`, `AbstractController`. **Visitor**: add operations to objects without modifying them. Example: AST traversal, document export (awareness). |
| 1 hr | **SOLID + Other Principles** | **S** — Single Responsibility: one class, one reason to change. Example: separate `UserService` and `EmailService`. **O** — Open/Closed: open for extension, closed for modification. Example: Strategy pattern, new payment methods without changing existing code. **L** — Liskov Substitution: subtypes must be substitutable for base types. Example: Square is NOT a proper subtype of Rectangle (setWidth changes behavior). **I** — Interface Segregation: no client should depend on methods it doesn't use. Example: `Printer`, `Scanner`, `Fax` instead of `MultiFunctionDevice`. **D** — Dependency Inversion: depend on abstractions, not concretions. Example: `OrderService` depends on `PaymentGateway` interface, not `StripePayment` class. **DRY** (Don't Repeat Yourself), **KISS** (Keep It Simple, Stupid), **YAGNI** (You Aren't Gonna Need It). Relate each SOLID principle to your Healthcare project with concrete examples. |
| 1 hr | **System Design Fundamentals** | Layered architecture: Controller → Service → Repository (your project architecture). MVC vs MVP vs MVVM (awareness). CAP Theorem: Consistency, Availability, Partition Tolerance — pick 2. Load Balancing: Round Robin, Least Connections, IP Hash, Weighted. Caching: cache-aside (lazy loading), read-through, write-through, write-behind/write-back. TTL, eviction policies (LRU — Least Recently Used, LFU — Least Frequently Used, FIFO). Redis (key-value store, data types, pub-sub, TTL). CDN: content delivery network, edge servers. Database scaling: vertical (bigger machine) vs horizontal (sharding). Sharding strategies: hash-based, range-based, directory-based. Replication: master-slave (read replicas), master-master. Message Queues: decoupling, asynchronous processing, producer-consumer, pub-sub. Rate Limiting: token bucket, sliding window, fixed window. |
| 30 min | **System Design Practice** | Design a URL shortener (high level): requirements, API design, database schema, hash function, read/write flow, scaling considerations. |

---

### Day 21 (Sun, Sep 7) — Git, Maven, Docker, Agile + Week 3 Revision

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1.5 hr | **Git (Complete)** | Basics: `init`, `clone`, `add`, `commit`, `status`, `log`, `diff`. Branching: `branch`, `checkout`, `switch` (Git 2.23+), `merge`, `rebase`. `merge` vs `rebase` — merge creates merge commit (preserves history), rebase replays commits (linear history). When to use each. `cherry-pick` — apply specific commit. `stash` — `stash`, `stash pop`, `stash list`, `stash drop`, `stash apply`. `reset` — `--soft` (uncommit, keep staged), `--mixed` (uncommit, unstage, keep changes), `--hard` (uncommit, discard changes). `revert` — create new commit that undoes changes (safe for shared branches). `reset` vs `revert` — reset rewrites history, revert adds to history. `fetch` vs `pull` — fetch downloads, pull = fetch + merge. `blame` — who changed each line. `reflog` — recovery. Branching strategies: GitFlow (main, develop, feature, release, hotfix), GitHub Flow (main + feature branches), trunk-based development. Merge conflicts — detection, resolution, tools. `.gitignore`. Pull requests — code review process. |
| 1 hr | **Maven** | POM (Project Object Model) — `groupId`, `artifactId`, `version`, packaging, dependencies. Maven lifecycle — `validate` → `compile` → `test` → `package` → `verify` → `install` → `deploy`. `mvn clean`, `mvn clean install`, `mvn clean install -DskipTests`. Dependency management: `<dependencies>`, `<dependencyManagement>`, scope (compile, provided, runtime, test, system). Plugins — `maven-compiler-plugin`, `maven-surefire-plugin`, `spring-boot-maven-plugin`. Profiles — environment-specific configurations. Multi-module projects. Maven vs Gradle (comparison). |
| 1 hr | **Docker & CI/CD** | Docker: containerization vs virtualization. Image vs container. Dockerfile instructions: `FROM`, `RUN`, `COPY`, `ADD`, `WORKDIR`, `EXPOSE`, `ENV`, `CMD`, `ENTRYPOINT` (CMD vs ENTRYPOINT). Multi-stage build — smaller images. `docker build -t name .`, `docker run -p 8080:8080 name`, `docker ps`, `docker stop`, `docker rm`, `docker images`, `docker rmi`. `docker-compose.yml` — multi-container setup. Volumes — persistent data. Networking — bridge, host, none. CI/CD: Continuous Integration (build + test on each commit), Continuous Delivery (automated deployment to staging), Continuous Deployment (automated deployment to production). Jenkins pipeline stages (awareness). GitHub Actions (awareness). |
| 1 hr | **Agile & SDLC** | SDLC models: Waterfall (linear, sequential), V-Model (verification & validation), Iterative, Spiral, Agile. Agile principles: individuals over processes, working software over documentation, customer collaboration, responding to change. Scrum: roles (Product Owner, Scrum Master, Development Team), artifacts (Product Backlog, Sprint Backlog, Increment), ceremonies (Sprint Planning, Daily Standup, Sprint Review, Sprint Retrospective). Sprint — 2-4 weeks. Story points — Fibonacci (1, 2, 3, 5, 8, 13, 21). Velocity — average story points per sprint. User stories — "As a [user], I want [feature], so that [benefit]". Acceptance criteria. Definition of Done. Kanban — visual board, WIP limits, continuous flow. |
| 30 min | **Postman** | Collections, environments, variables (global, collection, environment). HTTP methods. Request: params, headers, body (raw JSON, form-data). Response: status code, body, headers. Pre-request scripts, tests (`pm.test()`, `pm.expect()`). Runner — batch execution. |
| 1.5 hr | **Week 3 Comprehensive Revision** | Revise all DSA patterns (two-pointer, sliding window, hashing, stack, BFS/DFS). Practice explaining design patterns aloud — relate each to Spring. Revise SOLID with your project examples. Quick-fire 30 questions across all topics. |

---

## 📅 WEEK 4 (Days 22–28): HR Prep, Mock Interviews & Intensive Revision

---

### Day 22 (Mon, Sep 8) — Behavioral & HR Round (Complete Preparation)

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1.5 hr | **STAR Method Stories** | Prepare 8 stories using **S**ituation-**T**ask-**A**ction-**R**esult format. Each story should be 2-3 minutes. |

**Must-Prepare STAR Stories**:

| # | Story Theme | Suggested Context | Key Points to Highlight |
|---|-------------|------------------|------------------------|
| 1 | Led a challenging feature | DocuSign Integration (Healthcare) | Technical complexity, research, integration with 3rd party API |
| 2 | Solved a critical performance issue | Stored procedure optimization (Supply Chain) | Root cause analysis, query optimization, measurable improvement |
| 3 | Team conflict / disagreement | Cross-team collaboration at Cognizant | Communication, empathy, finding common ground |
| 4 | Tight deadline delivery | Sprint-based delivery of Admission Assessment module | Prioritization, time management, quality under pressure |
| 5 | Learned new technology quickly | Spring Boot / Microservices adoption | Self-learning, applying to project, sharing knowledge |
| 6 | Made a mistake and learned | Production bug / deployment issue | Ownership, root cause analysis, preventive measures |
| 7 | Mentored / helped a teammate | Guiding junior developers | Leadership, patience, knowledge sharing |
| 8 | Achievement you're proud of | Smart India Hackathon Win 🏆 | Innovation, teamwork, problem-solving under pressure |

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1.5 hr | **All HR Questions (Prepare Answers)** | |

**Complete HR Question Bank with Tips**:

| # | Question | Tips |
|---|----------|------|
| 1 | **Tell me about yourself** | 2-min structured: education → experience summary → current role → key achievements → what you're looking for. NOT a resume recitation. |
| 2 | **Walk me through your resume** | Chronological, highlight growth, connect experiences to target role. |
| 3 | **Why are you leaving Cognizant?** | Positive framing — seeking growth, new challenges, broader exposure. NEVER badmouth. |
| 4 | **Why do you want to join [company]?** | Research the company: projects, clients, culture, growth opportunities. Be specific. |
| 5 | **Where do you see yourself in 5 years?** | Growth in technical skills, leadership aspirations, contributing to company. |
| 6 | **What are your strengths?** | 3 strengths with examples: problem-solving (competitive programming), quick learner (SIH), collaborative (Agile team). |
| 7 | **What are your weaknesses?** | Genuine but not disqualifying. Show improvement efforts. E.g., "I tend to deep-dive into optimization — I've learned to balance perfection with delivery." |
| 8 | **What is your greatest achievement?** | Smart India Hackathon Win — describe the problem, your contribution, and impact. |
| 9 | **Describe a challenging project** | Use STAR method — Healthcare project, DocuSign integration. |
| 10 | **How do you handle pressure/stress?** | Prioritization, breaking tasks down, communication with team. Give example from sprint delivery. |
| 11 | **Describe a conflict with a coworker** | Emphasize communication, understanding their perspective, finding a solution. |
| 12 | **What motivates you?** | Solving complex problems, building quality software, continuous learning. |
| 13 | **Why should we hire you?** | Unique combination: strong fundamentals (ICPC, CodeChef Div 1) + production experience (5+ years) + team player. |
| 14 | **Do you prefer working alone or in a team?** | Both — independent work for deep focus, teamwork for complex features. Give examples. |
| 15 | **What do you know about our company?** | Always research beforehand: company size, key clients, tech stack, recent news. |
| 16 | **Salary expectations** | Research market rate. Give a range. "Based on my experience and market standards, I'm looking at X-Y range." |
| 17 | **Notice period** | Be honest. Negotiate if possible. Mention if buyout is an option. |
| 18 | **Are you open to relocation?** | Be honest about preferences but show flexibility. |
| 19 | **Do you have any questions for us?** | Always ask 2-3: team structure, tech stack, growth opportunities, typical day, training programs. |

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1 hr | **Salary Negotiation** | Research market rates: use Glassdoor, Levels.fyi, AmbitionBox for 5-year Java developer in your city. Know your current CTC breakdown (basic, HRA, special allowance, bonus, PF). Calculate expected hike (30-50% for lateral move in service-based companies). Practice negotiation scripts. Know when to negotiate (after offer, not during interview). Counter-offer etiquette. |

---

### Day 23 (Tue, Sep 9) — Project Deep Dive & Self-Introduction Polish

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1.5 hr | **Project Explanations** | Prepare 3-minute AND 7-minute versions for each of your 3 projects. |

**Project 1: Healthcare (Primary — Most Detail)**
```
1. Business Context (30 sec)
   - Healthcare management system for [hospital/clinic chain]
   - Manages patient records, admissions, clinical documentation, e-signatures

2. Your Role (30 sec)
   - Software Engineer — backend development
   - Designed and developed RESTful APIs, integrated third-party services
   - Worked in Agile team with 2-week sprints

3. Architecture & Tech Stack (1 min)
   - Layered architecture: Controller → Service → Repository
   - Spring Boot, Spring MVC, Spring Data JPA
   - Microsoft SQL Server, JPA/Hibernate for ORM
   - Git for version control, Postman for API testing
   - Deployed on [environment]

4. Key Modules You Built (1-2 min)
   - Patient E-Chart: CRUD operations for patient records, search/filter
   - Admission Assessment: complex forms, multi-step workflow, validations
   - DocuSign Integration: third-party API integration for e-signatures,
     webhook handling for completion callbacks

5. Challenges & Solutions (1-2 min)
   - Performance: slow queries → optimized with stored procedures,
     database views, proper indexing
   - Code quality: applied SOLID principles, standardized exception
     handling with @ControllerAdvice
   - Java 8 Streams: replaced imperative loops with functional style,
     leveraged lazy evaluation for large datasets

6. Impact (30 sec)
   - Improved data retrieval performance by X%
   - Reduced code duplication, improved maintainability
   - Successfully delivered features in [X] sprints
```

**Project 2: Timesheet And Attendance (Secondary)**
```
1. Business Context: internal time tracking and attendance management
2. Your Role: backend development using PL/SQL
3. Tech Stack: PL/SQL, Oracle/SQL Server
4. Key Work: packages, procedures, functions, schema design
5. Challenges: complex business rules, data validation, workflow efficiency
6. Impact: improved processing time, reduced errors
```

**Project 3: Supply Chain Central Tower (Secondary)**
```
1. Business Context: supply chain operations management
2. Your Role: full lifecycle — requirement gathering to deployment
3. Tech Stack: SQL Server, stored procedures, database objects
4. Key Work: tables, views, indexes, backend workflows
5. Challenges: SQL optimization, handling large datasets
6. Impact: improved database performance, optimized query execution
```

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1 hr | **Architecture Walkthrough** | Draw architecture diagrams for Healthcare project: component diagram (showing Controller, Service, Repository layers), data flow diagram (request → response), integration diagram (showing DocuSign, SQL Server). Be ready to explain any design decision. |
| 1 hr | **Deep-Dive Questions Preparation** | Prepare answers for project deep-dive questions: Why Spring Boot? Why layered architecture? How did you handle errors? How did you test? What would you do differently? How did you handle data validation? How did DocuSign integration work? What stored procedures did you write? How did you optimize SQL? |
| 1 hr | **Self-Introduction Practice** | Record yourself giving 2-minute self-introduction. Listen back. Refine. Record again. Aim for: confident, structured, engaging, highlights achievements naturally. |

---

### Day 24 (Wed, Sep 10) — Mock Interview #1: Full Java + Spring Boot

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 2.5 hr | **Self-Mock Interview** | Simulate a 90-minute technical interview. Use timer. Answer aloud (not in your head). |

**Mock Interview #1 — Question Set (45 questions)**:

**Java Core (15)**:
1. What is the difference between JDK, JRE, and JVM?
2. Explain all 4 OOP pillars with examples.
3. What is method overloading vs overriding? Can we override static methods?
4. Explain `final`, `finally`, `finalize()` with examples.
5. Why is `String` immutable in Java? Explain String Pool.
6. Difference between `==` and `.equals()`? What is the `hashCode()` contract?
7. Explain `HashMap` internal working in Java 8. What happens during collision?
8. `ArrayList` vs `LinkedList` — internal structure, time complexity, when to use?
9. `ConcurrentHashMap` vs `Hashtable` vs `SynchronizedMap` — how do they achieve thread safety?
10. Explain checked vs unchecked exceptions with examples.
11. What is `try-with-resources`? What is `AutoCloseable`?
12. Explain thread lifecycle. Difference between `start()` and `run()`?
13. What is deadlock? How to detect and prevent it?
14. Explain Generics — bounded types, wildcards, PECS.
15. What is serialization? What is `transient`? What is `serialVersionUID`?

**Java 8 (10)**:
16. What is a functional interface? Name 4 built-in functional interfaces.
17. Write a lambda to filter even numbers from a list and find their sum.
18. Explain `map()` vs `flatMap()` in Streams with example.
19. What are intermediate vs terminal operations? Give 5 examples of each.
20. Explain lazy evaluation in Streams.
21. What is `Optional`? How to avoid `NullPointerException` using `Optional`?
22. Difference between `orElse()` and `orElseGet()`?
23. What are method references? Explain 4 types.
24. What are `default` methods in interfaces? How is diamond problem resolved?
25. What new features were added in Java 9, 11, and 17?

**Spring Boot (15)**:
26. What is Spring IoC? Explain Dependency Injection types.
27. `@Component` vs `@Service` vs `@Repository` vs `@Controller` — differences?
28. Explain Spring Bean lifecycle.
29. What are bean scopes? What happens when you inject prototype into singleton?
30. How does Spring Boot auto-configuration work?
31. `@RestController` vs `@Controller` — what's the difference?
32. How do you handle exceptions globally in Spring Boot?
33. Explain `@Transactional` — propagation types and isolation levels.
34. What is the N+1 problem? How do you solve it?
35. What is `LAZY` vs `EAGER` fetching?
36. How does Spring Security work? Explain JWT authentication flow.
37. What is AOP? Explain `@Around` advice with example.
38. How do you test a Spring Boot REST API?
39. `@Cacheable` vs `@CachePut` vs `@CacheEvict`?
40. What is the difference between PUT and PATCH?

**Microservices (5)**:
41. Monolith vs Microservices — when would you NOT use microservices?
42. What is an API Gateway? What does it do?
43. Explain Circuit Breaker pattern with states.
44. How do microservices communicate? Sync vs Async?
45. What is the Saga pattern?

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1.5 hr | **Review & Gap Analysis** | Score yourself on each question (✅ confident, ⚠️ partial, ❌ couldn't answer). Study the ❌ and ⚠️ topics immediately. |

---

### Day 25 (Thu, Sep 11) — Mock Interview #2: SQL + DSA + Design

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 2.5 hr | **Self-Mock Interview** | |

**Mock Interview #2 — Question Set**:

**SQL (15)**:
1. `WHERE` vs `HAVING` — when to use which?
2. Explain all types of JOINs with examples.
3. Write: find the 2nd highest salary (3 different approaches).
4. Write: find employees earning more than their manager.
5. `ROW_NUMBER()` vs `RANK()` vs `DENSE_RANK()` — explain with example.
6. Write: nth highest salary per department using window function.
7. What is a CTE? Write a recursive CTE for an org chart.
8. Explain clustered vs non-clustered index.
9. What makes a query non-sargable?
10. Explain ACID properties.
11. What are transaction isolation levels? What is a dirty read?
12. Write a stored procedure with error handling.
13. What is normalization? Explain up to 3NF with examples.
14. What is a deadlock in database? How to prevent?
15. `DELETE` vs `TRUNCATE` vs `DROP` — differences?

**DSA (10)**:
16. Two Sum — solve using HashMap.
17. Reverse a linked list (iterative).
18. Check balanced parentheses using stack.
19. Find the kth largest element in an array.
20. Binary search — find first occurrence of a target.
21. Level order traversal of a binary tree.
22. Detect cycle in a linked list.
23. Maximum subarray sum (Kadane's algorithm).
24. Merge two sorted arrays.
25. Longest substring without repeating characters.

**Design (10)**:
26. Explain Singleton pattern — thread-safe implementations.
27. Factory vs Abstract Factory — when to use?
28. Explain Observer pattern with a real example.
29. What is Strategy pattern? How is it used in Java?
30. Explain SOLID principles — give example for each.
31. What is DRY? How do you ensure it in your code?
32. Draw architecture for a URL shortener.
33. What is caching? Explain cache-aside pattern.
34. What is load balancing? Types?
35. What is CAP theorem?

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1.5 hr | **Review & Gap Analysis** | Score each answer. Focus on ❌ topics. Write down key formulas/patterns to memorize. |

---

### Day 26 (Fri, Sep 12) — Intensive Revision: Java + Java 8 (All Topics)

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1 hr | **OOP + Core Concepts** | Quick notes review: OOP pillars, access modifiers, `static`/`final`, constructors, `this`/`super`, inner classes, enums. 10 output prediction questions. |
| 1 hr | **Strings + Exceptions + Object class** | String pool, immutability reasons, `StringBuilder` vs `StringBuffer`. Exception hierarchy, try-with-resources, custom exceptions. All `Object` class methods. `equals()`/`hashCode()` contract. |
| 1 hr | **Collections — Complete Review** | Draw complete hierarchy from memory. `ArrayList` vs `LinkedList`, `HashSet` vs `TreeSet`, `HashMap` internal working (bucket, collision, treeification, rehashing), `ConcurrentHashMap`. `Comparable` vs `Comparator`. `fail-fast` vs `fail-safe`. |
| 1 hr | **Multithreading & Concurrency** | Thread lifecycle, `synchronized`, `volatile`, `wait`/`notify`, deadlock. `ExecutorService`, `CompletableFuture`, `CountDownLatch`, `CyclicBarrier`, atomic classes. |
| 1 hr | **Java 8/11/17 Features** | Lambda, functional interfaces (all 8), method references. Stream API — all intermediate & terminal ops, `Collectors` (all methods). `Optional` — all methods. Date/Time API. Java 9/11/17 features. Practice: 10 Stream coding problems. |

---

### Day 27 (Sat, Sep 13) — Intensive Revision: Spring + SQL (All Topics)

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1 hr | **Spring Core + Boot** | IoC, DI types, bean lifecycle (draw from memory), scopes, auto-configuration, profiles, all annotations. |
| 1 hr | **Spring MVC + REST + Security** | Request flow, all annotations (`@PathVariable`, `@RequestBody`, etc.), validation, exception handling, filters vs interceptors. Security filter chain, JWT flow. |
| 1 hr | **JPA + Hibernate + Transactions** | Entity mapping, relationships, fetch types, N+1 problem & solutions, entity states, `@Transactional` propagation & isolation. |
| 1 hr | **Microservices** | Architecture diagram, all patterns (gateway, discovery, circuit breaker, saga), 12-factor app, Docker basics. |
| 1.5 hr | **SQL — Complete Review** | Write 15 queries covering: joins (all types), window functions (`ROW_NUMBER`, `RANK`, `DENSE_RANK`, `LEAD`, `LAG`, running total), subqueries (correlated, EXISTS), CTE (recursive), CASE, stored procedure with error handling. Review indexes, normalization, ACID, isolation levels. |
| 30 min | **Rapid-fire 40 questions** | 10 Java + 5 Java 8 + 10 Spring + 10 SQL + 5 Microservices — answer each in 30 seconds. |

---

### Day 28 (Sun, Sep 14) — Full Mock Interview + Final Gap Analysis

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 3 hr | **Complete Mock Interview Simulation** | |

**Round 1 — Self Introduction (5 min)**
- 2-minute self-introduction
- Project walkthrough questions

**Round 2 — Technical (45 min)**
- 15 min: Core Java + Java 8
- 15 min: Spring Boot + Microservices
- 15 min: SQL queries (write on paper/whiteboard)

**Round 3 — Coding (30 min)**
- Problem 1: Array/String (medium)
- Problem 2: HashMap/Set (medium)

**Round 4 — Design (15 min)**
- Explain 3 design patterns
- SOLID principles
- High-level system design

**Round 5 — HR (15 min)**
- Tell me about yourself
- Why leaving?
- Challenging situation (STAR)
- Salary expectations

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 2 hr | **Final Gap Analysis & Targeted Study** | List ALL weak areas identified across all 3 mock interviews. Create a focused 1-page revision sheet for each weak area. Study only the gaps. |
| 1.5 hr | **Create Cheat Sheets** | Prepare 4 one-page cheat sheets: (1) Java Core + Java 8, (2) Spring Boot annotations, (3) SQL patterns, (4) Design patterns + SOLID. These are your last-day revision material. |

---

## 📅 Final Sprint (Days 29–30): Polish & Confidence Building

---

### Day 29 (Mon, Sep 15) — Final Comprehensive Revision

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1.5 hr | **Java Cheat Sheet Revision** | Go through your Java cheat sheet. Focus on: HashMap internals, Collections comparison, Java 8 Streams, `CompletableFuture`, Generics PECS, Serialization. |
| 1 hr | **Spring Boot Cheat Sheet Revision** | All annotations. Bean lifecycle. `@Transactional` propagation table. JPA relationships. Security flow. |
| 1 hr | **SQL Cheat Sheet Revision** | Join syntax, window function syntax, CTE syntax, stored procedure template. Normalization rules. ACID. Isolation levels table. |
| 1 hr | **Design + DSA Cheat Sheet Revision** | Design patterns — one-line summary of each. SOLID — one example each. DSA patterns — two-pointer, sliding window, hashing, stack, BFS/DFS. |
| 1 hr | **Top 80 Questions Speed Run** | Answer all 80 must-know questions (listed below) — 45 seconds each. |

---

### Day 30 (Tue, Sep 16) — Confidence Day 🎯

| Time | Topic | Detailed Action Items |
|------|-------|----------------------|
| 1 hr | **Self-Introduction** | Record your final 2-minute self-introduction. Listen. It should sound natural, confident, and structured. Practice in front of a mirror. |
| 1 hr | **Project Walkthrough** | Practice explaining your Healthcare project fluently — 3-minute and 7-minute versions. Anticipate follow-up questions. |
| 30 min | **Logistics** | Update resume (latest format, no typos). Prepare copies. Keep all documents ready (ID, degree certificates, experience letters, pay slips). Test video/audio setup if interview is virtual. Prepare a quiet interview space. |
| 30 min | **Company Research Template** | For each company you'll interview at, note: company overview, key clients, tech stack, recent news, Glassdoor reviews, why you want to join. |
| 30 min | **Mental Preparation** | Light revision only — browse through cheat sheets casually. Visualize a successful interview. Get good sleep. Don't cram new material. |

---

## 📌 TOP 80 MUST-KNOW INTERVIEW QUESTIONS

### Core Java (15)
1. Explain the 4 pillars of OOP with examples
2. `HashMap` internal working in Java 8 (buckets, collision, treeification)
3. `==` vs `.equals()` vs `hashCode()` — explain the contract
4. Why is `String` immutable? Explain String Pool
5. `ArrayList` vs `LinkedList` — internals, when to use
6. `Comparable` vs `Comparator` — when to use each
7. Checked vs Unchecked exceptions — hierarchy, examples
8. `final` vs `finally` vs `finalize()`
9. Thread lifecycle — all 6 states
10. `synchronized` vs `volatile` vs `ReentrantLock`
11. Deadlock — what, why, how to prevent
12. `ConcurrentHashMap` vs `Hashtable` — internal difference
13. Generics — type erasure, PECS principle
14. `fail-fast` vs `fail-safe` iterators
15. Garbage Collection — GC roots, generations, G1 GC

### Java 8+ (10)
16. What is a functional interface? Name all built-in ones
17. Lambda vs Anonymous inner class — differences
18. `Stream` — intermediate vs terminal operations (5 each)
19. `map()` vs `flatMap()` — explain with examples
20. `Collectors.groupingBy()` vs `partitioningBy()`
21. Parallel streams — when to use, thread safety
22. `Optional` — all methods, best practices, anti-patterns
23. `orElse()` vs `orElseGet()` — lazy evaluation difference
24. `CompletableFuture` — `supplyAsync()`, `thenApply()`, `exceptionally()`
25. What's new in Java 9, 11, 17?

### Spring Boot (15)
26. What is IoC? Explain DI types — which is recommended and why?
27. `@Component` vs `@Service` vs `@Repository` — semantic differences
28. Bean lifecycle — complete steps from instantiation to destruction
29. Bean scopes — all 6, prototype-in-singleton problem
30. Spring Boot auto-configuration — how does it work internally?
31. `@RestController` vs `@Controller`
32. `@PathVariable` vs `@RequestParam` vs `@RequestBody`
33. Global exception handling — `@ControllerAdvice` + `@ExceptionHandler`
34. `@Transactional` — propagation types (REQUIRED, REQUIRES_NEW, NESTED)
35. `@Transactional` — isolation levels, rollback behavior
36. JPA `LAZY` vs `EAGER` — defaults, N+1 problem, solutions
37. Spring Security — JWT authentication flow
38. AOP — `@Around` advice, how `@Transactional` uses AOP
39. Filters vs Interceptors — order of execution
40. Spring Boot testing — `@WebMvcTest`, `@MockBean`, MockMvc

### Microservices (8)
41. Monolith vs Microservices — pros/cons, when to use which
42. API Gateway — responsibilities, routing
43. Service Discovery — Eureka flow
44. Circuit Breaker — 3 states, fallback, Resilience4j
45. Inter-service communication — sync vs async, REST vs messaging
46. Saga pattern — choreography vs orchestration
47. 12-Factor App — name all 12 factors
48. Docker — Dockerfile, image vs container, docker-compose

### SQL & Database (20)
49. `INNER JOIN` vs `LEFT JOIN` vs `FULL OUTER JOIN` vs `CROSS JOIN`
50. `WHERE` vs `HAVING`
51. `ROW_NUMBER()` vs `RANK()` vs `DENSE_RANK()`
52. Write: 2nd highest salary (3 approaches)
53. Write: nth highest salary per department
54. Write: employees earning more than their manager
55. Write: running total using window function
56. Write: find duplicate records
57. `LEAD()` and `LAG()` — explain with example
58. CTE — when to use, recursive CTE example
59. Indexes — clustered vs non-clustered, composite, covering
60. When to create/avoid indexes?
61. Explain ACID properties
62. Transaction isolation levels — dirty read, phantom read
63. Stored procedure vs function — differences
64. `DELETE` vs `TRUNCATE` vs `DROP`
65. Normalization — 1NF, 2NF, 3NF with examples
66. What is denormalization? When to use?
67. What is a deadlock in SQL? How to prevent?
68. Execution plan — index scan vs index seek

### Design Patterns & Architecture (12)
69. Singleton — 5 implementations, which is best and why
70. Factory Method — when to use, example
71. Builder — why needed, Lombok `@Builder`
72. Observer — real-world example, Spring events
73. Strategy — `Comparator` as strategy
74. Decorator — Java I/O streams example
75. Template Method — `JdbcTemplate`, `RestTemplate`
76. SOLID — explain each with code example
77. DRY, KISS, YAGNI
78. Layered architecture — Controller → Service → Repository
79. CAP theorem
80. Design a URL shortener (high-level)

---

## 📚 Recommended Resources

| Resource | Purpose | Priority |
|----------|---------|----------|
| **JavaTpoint / GeeksForGeeks** | Quick concept revision | ⭐⭐⭐ |
| **Baeldung** | Spring Boot & Java 8 in-depth | ⭐⭐⭐ |
| **LeetCode (Easy/Medium)** | DSA practice — aim for 50–60 problems | ⭐⭐⭐ |
| **HackerRank SQL** | SQL query practice | ⭐⭐⭐ |
| **YouTube — Java Techie** | Spring Boot, Microservices | ⭐⭐⭐ |
| **YouTube — Daily Code Buffer** | Spring Boot project tutorials | ⭐⭐ |
| **YouTube — Concept && Coding** | Design patterns, LLD | ⭐⭐⭐ |
| **YouTube — Neetcode** | DSA patterns explanation | ⭐⭐ |
| **InterviewBit** | Curated interview questions | ⭐⭐ |
| **DigitalOcean / JavaGuides blog** | Spring Boot tutorials | ⭐⭐ |
| **SQL Practice — SQLZoo / W3Schools** | Interactive SQL practice | ⭐⭐ |
| **Head First Design Patterns** | Design patterns (if time permits) | ⭐ |
| **AmbitionBox / Glassdoor** | Company-specific interview experiences | ⭐⭐⭐ |

---

## 🏆 Your Competitive Advantages (Highlight in Every Interview!)

| Advantage | How to Frame It |
|-----------|----------------|
| 🏆 **Smart India Hackathon Winner** | "I won the national-level SIH 2019, demonstrating innovation and problem-solving under pressure" |
| 🌐 **ACM ICPC Regionalist (2x)** | "My team qualified for ICPC regionals twice, which built strong algorithmic thinking" |
| 📊 **CodeChef Div 1 (1835)** | "My competitive programming background gives me strong DSA foundations" |
| 💼 **5+ Years Production Experience** | "I've delivered multiple production systems across healthcare and supply chain domains" |
| 🔄 **Full Lifecycle Development** | "I've been involved from requirement gathering through deployment and optimization" |
| 📐 **Xplorica Core Committee (3 years)** | "Leading technical events developed my leadership and communication skills" |

---

## 📋 Daily Routine Template

```
☀️ Morning (2 hrs)     → Theory / Concept deep dive
🌤️ Afternoon (1.5 hrs)  → Coding practice / SQL queries
🌙 Evening (1 hr)       → Revision + Mock Q&A (answer aloud)
📝 Before bed (30 min)  → Flashcard review / Day's notes summary
```

---

> [!TIP]
> **Execution Tips**:
> - ✅ Explain concepts ALOUD — speaking activates different memory pathways
> - ✅ Write code on paper/whiteboard — many interviews are whiteboard-style
> - ✅ Draw diagrams (architecture, HashMap, bean lifecycle) — interviewers love visual explanations
> - ✅ For each topic, think "How did I use this in my project?" — project mapping = strong answers
> - ✅ Read Glassdoor/AmbitionBox reviews for target companies — know what they ask

> [!CAUTION]
> **Critical Mistakes to Avoid**:
> - ❌ Don't just read — understanding without practice = forgetting in 2 days
> - ❌ Don't skip SQL — it's asked in 100% of service-based company interviews
> - ❌ Don't memorize answers — understand the "WHY" behind every concept
> - ❌ Don't neglect project explanation — it's 30-40% of the interview
> - ❌ Don't ignore HR round — many candidates get rejected here despite good technical rounds
> - ❌ Don't cram on the last day — revise, don't learn new things
> - ❌ Don't skip mock interviews — the gap between "I know it" and "I can explain it" is massive
> - ❌ Don't skip behavioral prep — "Tell me about yourself" is always the first question
