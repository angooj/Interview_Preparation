# 🏦 Project Story Bank — Interview-Ready Technical Stories

> **Purpose**: When an interviewer asks about a technical topic, don't just explain the concept — connect it to YOUR real project work. This document maps every major topic to a ready-to-use story from your projects.
>
> **How to use**: For each topic, you have a **ready answer** that combines the concept + your project experience. Practice saying these out loud until they feel natural.

---

## Your Projects — Quick Reference

| # | Project | Domain | Tech Stack | Duration |
|---|---------|--------|-----------|----------|
| 1 | **Healthcare** (Primary) | Patient management, clinical documentation | Spring Boot, Spring MVC, JPA/Hibernate, MS SQL Server, Java 8 | Main project |
| 2 | **Timesheet & Attendance** | Employee time tracking | PL/SQL packages, procedures, functions | Secondary |
| 3 | **Supply Chain Central Tower** | Supply chain operations | SQL Server, stored procedures, database objects | Secondary |

---

## Part 1: Core Java Stories

---

### When asked: "Have you used OOP principles in your project?"

**Your Story**:
> "In the Healthcare project, we designed the system using all four OOP principles. **Encapsulation** — all entity fields like patient name, age, and medical history were private with validated getters/setters. For example, the `setAge()` method validated that age was between 0 and 150. **Inheritance** — we had a base `Assessment` class that `AdmissionAssessment` and `DischargeAssessment` extended, inheriting common fields like `assessmentDate`, `assessedBy`, and `notes`. **Polymorphism** — a method like `processAssessment(Assessment a)` would work with any assessment type, and the correct processing logic was called at runtime. **Abstraction** — we used interfaces like `Signable` for documents that required DocuSign integration, so any document type could be signed without knowing the signing details."

---

### When asked: "Have you used Java 8 features? Give examples."

**Your Story**:
> "Yes, extensively in the Healthcare project. Let me give you specific examples:
>
> **Streams**: When building the Patient E-Chart module, we needed to retrieve patients filtered by admission date, sorted by severity, and grouped by department. I replaced nested for-loops with a Stream pipeline:
> ```java
> Map<String, List<Patient>> byDept = patients.stream()
>     .filter(p -> p.getAdmissionDate().isAfter(cutoffDate))
>     .filter(p -> p.getStatus() == AdmissionStatus.ADMITTED)
>     .sorted(Comparator.comparing(Patient::getSeverity).reversed())
>     .collect(Collectors.groupingBy(Patient::getDepartment));
> ```
> This improved readability significantly and leveraged lazy evaluation — the filters and sort only process elements that pass the previous stage.
>
> **Optional**: We used `Optional` to handle cases where a patient might not have a primary doctor assigned:
> ```java
> String doctorName = patient.getPrimaryDoctor()
>     .map(Doctor::getName)
>     .orElse("Not Assigned");
> ```
> This eliminated null checks scattered throughout the code.
>
> **Lambda with Comparator**: For sorting patients by multiple criteria:
> ```java
> patients.sort(Comparator.comparing(Patient::getSeverity)
>     .thenComparing(Patient::getAdmissionDate));
> ```"

---

### When asked: "How did you handle exceptions in your project?"

**Your Story**:
> "In the Healthcare project, I implemented a layered exception handling strategy:
>
> 1. **Custom exceptions**: We created business-specific exceptions like `PatientNotFoundException`, `DuplicateAdmissionException`, and `InvalidAssessmentException`. These extended `RuntimeException` so they were unchecked — the service layer threw them without cluttering method signatures.
>
> 2. **Global exception handler**: I used `@RestControllerAdvice` with `@ExceptionHandler` methods to catch all exceptions in one place and convert them to standardized error responses:
> ```java
> @RestControllerAdvice
> public class GlobalExceptionHandler {
>     @ExceptionHandler(PatientNotFoundException.class)
>     public ResponseEntity<ErrorResponse> handlePatientNotFound(PatientNotFoundException ex) {
>         ErrorResponse error = new ErrorResponse(404, ex.getMessage(), LocalDateTime.now());
>         return ResponseEntity.status(HttpStatus.NOT_FOUND).body(error);
>     }
>     
>     @ExceptionHandler(Exception.class)
>     public ResponseEntity<ErrorResponse> handleGeneric(Exception ex) {
>         ErrorResponse error = new ErrorResponse(500, "Internal Server Error", LocalDateTime.now());
>         return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body(error);
>     }
> }
> ```
>
> 3. **Validation exceptions**: For input validation failures, we used `@Valid` on request DTOs and handled `MethodArgumentNotValidException` to return field-level error details.
>
> This approach kept our controller and service code clean while providing consistent error responses to the frontend team."

---

### When asked: "Have you used Collections? Which ones and why?"

**Your Story**:
> "In the Healthcare project:
> - **ArrayList**: Used for ordered lists of patient records, admission history, and assessment items where we needed index-based access and iteration.
> - **HashMap**: Used extensively for caching — we cached patient records by `patientId` to avoid repeated database calls within the same request. Also used in service methods to build response maps grouping data by category.
> - **LinkedHashMap**: Used when we needed to maintain insertion order — for example, the assessment questionnaire items needed to appear in the order they were defined.
> - **TreeMap**: Used in reporting modules where we needed patients sorted by admission date automatically.
> - **HashSet**: Used to track unique values — for example, finding all unique departments or unique diagnoses across a patient cohort.
>
> For thread safety in a multi-user environment, we used `ConcurrentHashMap` for shared caches that multiple request threads could access simultaneously, instead of `Collections.synchronizedMap()`, because ConcurrentHashMap has better concurrent read performance with its segment-level locking (Java 7) / CAS operations (Java 8)."

---

### When asked: "Have you worked with Multithreading?"

**Your Story**:
> "While the Healthcare project primarily relied on Spring's thread management (each HTTP request is handled by a thread from Tomcat's thread pool), I used multithreading concepts in a few specific areas:
>
> 1. **@Async for DocuSign callbacks**: When a document was sent for e-signature, the response processing was asynchronous. We used `@Async` with a custom `ThreadPoolTaskExecutor` so the callback processing didn't block the main request thread.
>
> 2. **CompletableFuture for parallel data loading**: On the patient dashboard, we needed to load data from multiple services (patient info, admission history, lab results, medications). Instead of sequential calls, I used `CompletableFuture.supplyAsync()` to make parallel calls and `CompletableFuture.allOf()` to wait for all results:
> ```java
> CompletableFuture<PatientInfo> infoFuture = CompletableFuture.supplyAsync(() -> patientService.getInfo(id));
> CompletableFuture<List<Admission>> admFuture = CompletableFuture.supplyAsync(() -> admissionService.getHistory(id));
> CompletableFuture.allOf(infoFuture, admFuture).join();
> ```
> This reduced the dashboard load time from ~3 seconds (sequential) to ~1 second (parallel).
>
> 3. **Thread-safe caching**: Used `ConcurrentHashMap` for in-memory caches shared across threads."

---

## Part 2: Spring Boot Stories

---

### When asked: "Explain the architecture of your project."

**Your Story**:
> "The Healthcare project followed a **layered architecture** with Spring Boot:
>
> ```
> Client (Angular) → API Gateway → Spring Boot Application
>                                         │
>                                    ┌─────┴──────┐
>                                    │ Controller  │  ← REST endpoints, validation
>                                    │  (@RestController)
>                                    ├─────────────┤
>                                    │  Service    │  ← Business logic, orchestration
>                                    │  (@Service) │
>                                    ├─────────────┤
>                                    │ Repository  │  ← Data access, queries
>                                    │(@Repository)│
>                                    └─────┬───────┘
>                                          │
>                                    MS SQL Server
> ```
>
> - **Controller Layer**: Handled HTTP requests, input validation with `@Valid`, and response mapping. Used `ResponseEntity` for proper HTTP status codes.
> - **Service Layer**: Contained all business logic — patient admission rules, assessment workflows, DocuSign integration orchestration. Used `@Transactional` for database operations.
> - **Repository Layer**: Spring Data JPA repositories with derived query methods and custom `@Query` annotations for complex queries. Also called stored procedures for performance-critical operations.
> - **DTO Pattern**: We used separate DTOs for request and response payloads, keeping entity classes decoupled from the API contract. MapStruct handled the mapping."

---

### When asked: "How did you use Spring Data JPA / Hibernate?"

**Your Story**:
> "In the Healthcare project, we used Spring Data JPA with Hibernate as the ORM:
>
> **Entity Mapping**: Entities like `Patient`, `Admission`, `Assessment` were mapped with `@Entity`, `@Table`, `@Id`, `@GeneratedValue`. Relationships were mapped using `@OneToMany`, `@ManyToOne` — for example, a Patient had a `@OneToMany` relationship with Admission records.
>
> **Fetch Strategy**: We defaulted to `LAZY` loading and used `@EntityGraph` or `JOIN FETCH` in JPQL queries where we specifically needed eager loading. This helped us avoid the N+1 problem.
>
> **N+1 Problem — Real Experience**: Initially, when loading a list of patients with their admissions, Hibernate was firing 1 query for patients + N queries for each patient's admissions. We detected this by enabling Hibernate SQL logging. I fixed it using:
> ```java
> @Query(\"SELECT p FROM Patient p JOIN FETCH p.admissions WHERE p.department = :dept\")
> List<Patient> findByDepartmentWithAdmissions(@Param(\"dept\") String department);
> ```
> This reduced 101 queries (for 100 patients) to 1 query.
>
> **Stored Procedures**: For complex reporting queries where JPQL was too slow, we called stored procedures directly using `@Procedure` annotation or native queries. This was especially common in the Supply Chain project."

---

### When asked: "How did you handle transactions?"

**Your Story**:
> "We used `@Transactional` from Spring on our service methods. Here's a specific scenario:
>
> During patient admission, multiple tables needed to be updated atomically — the Patient record, Admission record, Bed Assignment, and initial Assessment. If any step failed, everything should roll back.
>
> ```java
> @Transactional(rollbackFor = Exception.class)
> public AdmissionResponse admitPatient(AdmissionRequest request) {
>     Patient patient = patientRepository.findById(request.getPatientId())
>         .orElseThrow(() -> new PatientNotFoundException(request.getPatientId()));
>     
>     Admission admission = createAdmission(patient, request);
>     assignBed(admission, request.getPreferredWard());
>     createInitialAssessment(admission);
>     
>     return mapper.toResponse(admission);
> }
> ```
>
> We used `REQUIRED` propagation (default) for most methods. For audit logging, we used `REQUIRES_NEW` so that the audit log was saved even if the main transaction rolled back:
> ```java
> @Transactional(propagation = Propagation.REQUIRES_NEW)
> public void logAuditEvent(String action, String details) {
>     auditRepository.save(new AuditLog(action, details, LocalDateTime.now()));
> }
> ```"

---

### When asked: "How did you integrate DocuSign? How do you integrate third-party APIs?"

**Your Story**:
> "The DocuSign integration in the Healthcare project was one of the more complex features I worked on. Here's how it worked:
>
> 1. **REST API Integration**: I used `RestTemplate` (later migrated to `WebClient`) to call DocuSign's REST API for creating envelopes and sending documents for signature.
>
> 2. **Authentication**: We used OAuth 2.0 JWT grant type — our backend generated a JWT assertion signed with our private key, exchanged it for an access token, and cached the token until expiry.
>
> 3. **Webhook for completion callbacks**: When a document was signed, DocuSign sent a webhook notification to our endpoint. I created a dedicated controller to receive these callbacks, validate the payload, and update the document status in our database.
>
> 4. **Error handling**: DocuSign API could fail due to rate limiting, network issues, or invalid document format. I implemented retry logic with exponential backoff for transient failures and proper error logging for permanent failures.
>
> **Challenge**: The biggest challenge was handling webhook reliability — sometimes DocuSign sent duplicate callbacks or we missed one due to temporary downtime. I implemented an idempotent webhook handler using the envelope ID as a deduplication key."

---

## Part 3: SQL & Database Stories

---

### When asked: "How did you optimize SQL queries / database performance?"

**Your Story**:
> "I have multiple examples across projects:
>
> **Healthcare Project**: The Patient E-Chart had a search feature that was slow (~5 seconds). I analyzed the query using the SQL Server execution plan and found a table scan on the 500K-row Patient table. The query was:
> ```sql
> SELECT * FROM patients WHERE LOWER(name) LIKE '%john%' AND status = 'ACTIVE'
> ```
> **Problems found**: (1) `LOWER(name)` made the query non-sargable — it couldn't use the index on `name`. (2) `SELECT *` was returning 30+ columns when we only needed 5.
>
> **Fixes**: (1) Created a filtered index on `(name, status)` for active patients. (2) Changed to `SELECT patientId, name, age, department, admissionDate` — only needed columns. (3) Used full-text index for the LIKE search. Query time dropped from 5 seconds to 200ms.
>
> **Supply Chain Project**: A reporting stored procedure was taking 45 seconds. The execution plan showed a nested loop join on two large tables (2M+ rows each). I rewrote it to use a HASH JOIN by restructuring the query, added a composite index on `(order_date, status, warehouse_id)`, and replaced a correlated subquery with a CTE + JOIN. Processing time dropped to 2 seconds."

---

### When asked: "Have you written stored procedures?"

**Your Story**:
> "Yes, extensively in all three projects:
>
> **Timesheet & Attendance Project** (PL/SQL-heavy): I developed PL/SQL packages that encapsulated the entire attendance calculation logic — computing working hours, overtime, leave deductions, and generating monthly attendance summaries. The packages included:
> - Input validation procedures with custom error messages
> - Cursor-based processing for batch calculations
> - Error handling with `EXCEPTION` blocks and logging to an error table
>
> **Supply Chain Project**: I designed stored procedures for:
> - Report generation with dynamic date ranges and filters
> - Data aggregation across multiple warehouse tables
> - Batch processing of order status updates
>
> The procedures used `TRY...CATCH` for error handling, output parameters to return status codes, and `SET NOCOUNT ON` for performance. For complex logic, I used CTEs and window functions (`ROW_NUMBER`, `RANK`) instead of cursors wherever possible."

---

### When asked: "Have you worked with database design / normalization?"

**Your Story**:
> "In the Supply Chain project, I was involved in database schema design from scratch. We designed the schema following 3NF principles:
>
> - Ensured **1NF**: All columns had atomic values — for example, instead of a comma-separated list of `warehouseIds`, we created a junction table.
> - Ensured **2NF**: For composite keys, all non-key columns depended on the FULL key, not just part of it.
> - Ensured **3NF**: Removed transitive dependencies — for example, `warehouse_city` was moved to a separate `Warehouses` table instead of being repeated in every order record.
>
> We also applied **strategic denormalization** for reporting tables — the monthly summary table was denormalized with pre-computed aggregates to avoid expensive JOINs during dashboard queries. This was a conscious trade-off: slightly more storage and update complexity for dramatically faster read performance."

---

## Part 4: Design & Architecture Stories

---

### When asked: "What design patterns have you used?"

**Your Story**:
> "Several patterns appeared naturally in the Healthcare project:
>
> 1. **Singleton**: Spring Beans are singletons by default. Our `PatientService`, `AdmissionService` — all service-layer beans are singleton-scoped.
>
> 2. **Factory**: We used a `DocumentFactory` that created different document types (Admission Form, Discharge Summary, Consent Form) based on a document type code. Each document type had different templates and validation rules.
>
> 3. **Strategy**: For assessment scoring, different assessment types had different scoring algorithms. We defined a `ScoringStrategy` interface with implementations like `PainScoreStrategy`, `FallRiskStrategy`, `NutritionScoreStrategy`. The `AssessmentService` received the appropriate strategy based on the assessment type.
>
> 4. **Template Method**: Our base `Assessment` processing had common steps (validate → score → save → notify) defined in an abstract class, with subclasses overriding only the parts that differed (scoring logic, notification recipients).
>
> 5. **Builder**: Used Lombok's `@Builder` for constructing complex DTOs with many optional fields, like `PatientSearchRequest.builder().name(\"John\").department(\"Cardiology\").build()`.
>
> 6. **Observer**: Spring's `ApplicationEventPublisher` — when a patient was admitted, we published an `AdmissionEvent` that triggered audit logging, notification sending, and bed management updates without coupling those services together."

---

### When asked: "How did you apply SOLID principles?"

**Your Story**:
> "Let me give a concrete example for each:
>
> **S — Single Responsibility**: `PatientService` handles only patient business logic. Email notifications are handled by `NotificationService`. Audit logging by `AuditService`. Initially, we had patient-related notification code inside `PatientService` — I refactored it out.
>
> **O — Open/Closed**: The assessment scoring system. When a new assessment type was added (e.g., wound assessment), we just created a new `WoundScoreStrategy` implementing `ScoringStrategy`. No existing code was modified.
>
> **L — Liskov Substitution**: All our `Assessment` subtypes (Admission, Discharge, Follow-up) could be passed to `processAssessment(Assessment a)` and everything worked correctly. Each subtype maintained the contract of the base type.
>
> **I — Interface Segregation**: Instead of one fat `DocumentService` interface with sign, print, export, archive methods, we had `Signable`, `Printable`, `Exportable` interfaces. A consent form implemented `Signable + Printable` but not `Exportable`.
>
> **D — Dependency Inversion**: Our service layer depended on repository interfaces, not concrete implementations. `PatientService` had `private final PatientRepository repository` — an interface. The actual implementation (`JpaPatientRepository`) was injected by Spring. This made unit testing easy — we could inject mock repositories."

---

### When asked: "Explain your Agile process."

**Your Story**:
> "We followed Scrum with 2-week sprints:
>
> - **Sprint Planning** (Monday): Product Owner presented user stories from the backlog. We estimated using Fibonacci story points (1, 2, 3, 5, 8, 13). Our velocity was around 40 points per sprint.
>
> - **Daily Standup** (15 min): Three questions — what I did yesterday, what I'll do today, any blockers. I once raised a blocker about a DocuSign API rate limit issue, which the team helped resolve by implementing request queuing.
>
> - **Development**: I picked stories from the sprint board, moved them through 'In Progress' → 'Code Review' → 'Testing' → 'Done'. All code went through peer review via pull requests.
>
> - **Sprint Review**: Demo'd completed features to stakeholders. I demonstrated the Patient Assessment module with live data entry and DocuSign signing flow.
>
> - **Retrospective**: Discussed what went well, what didn't, and action items. One actionable outcome from our retro: we started using database migration scripts (Flyway) instead of manual schema changes after a production incident."

---

## Part 5: Behavioral / STAR Stories

---

### "Tell me about a time you solved a difficult technical problem." (STAR)

> **Situation**: In the Healthcare project, our Patient E-Chart search was timing out in production (~8 seconds for searches) after the patient database grew beyond 500K records. Users were complaining.
>
> **Task**: I was assigned to investigate and fix the performance issue within the current sprint (5 working days).
>
> **Action**: (1) I enabled Hibernate SQL logging and captured the generated queries. (2) I ran the queries in SQL Server Management Studio with the actual execution plan. (3) I found three issues: a table scan due to a non-sargable `LOWER()` function, missing composite index, and `SELECT *` returning unnecessary columns. (4) I created a proper index, rewrote the query to be sargable, selected only needed columns, and added pagination (`Pageable` in Spring Data).
>
> **Result**: Query time dropped from 8 seconds to 300ms. User complaints stopped completely. I also documented the query optimization guidelines for the team, which prevented similar issues in other modules.

---

### "Tell me about a time you worked under a tight deadline." (STAR)

> **Situation**: In the Healthcare project, the Admission Assessment module was due for UAT in 2 weeks, but the requirements were finalized only 3 days before the sprint started, leaving us with an effectively shorter timeline.
>
> **Task**: I needed to build the complete admission assessment workflow — multi-step form submission, validation, scoring, and integration with the existing patient admission flow.
>
> **Action**: (1) I broke the feature into smaller deliverables and identified the critical path. (2) I focused on the backend API first (since the frontend team needed it to start their work). (3) I reused the existing assessment base class instead of building from scratch. (4) I wrote unit tests alongside the code to avoid a testing bottleneck at the end. (5) I communicated daily progress to the team lead and flagged risks early.
>
> **Result**: Delivered the complete backend 1 day before the UAT deadline. The feature passed UAT with only 2 minor cosmetic bugs (fixed same day). The team lead appreciated the proactive communication and task breakdown approach.

---

### "Tell me about your greatest achievement." (STAR)

> **Situation**: During my college years, the Smart India Hackathon 2019 (Software Edition) was announced — a national-level hackathon organized by the Government of India with thousands of teams competing.
>
> **Task**: Our team of 6 was challenged to build a software solution for a real government problem statement within 36 continuous hours.
>
> **Action**: I contributed to the solution architecture and backend development. We divided responsibilities clearly — I handled the API layer and data processing. We collaborated intensely, did rapid iterations, and presented our solution to a panel of industry experts.
>
> **Result**: We **won the Smart India Hackathon 2019**. This experience taught me how to deliver under extreme pressure, collaborate effectively, and present technical solutions to non-technical stakeholders. It also validated my problem-solving skills at a national level.

---

### "Tell me about a time you mentored or helped a team member." (STAR)

> **Situation**: A junior developer joined our Healthcare project team and was struggling with Spring Boot concepts — particularly dependency injection, JPA relationships, and REST API design.
>
> **Task**: As a more experienced team member, I took the initiative to help them become productive.
>
> **Action**: (1) I conducted informal knowledge-sharing sessions during lunch breaks, walking through our codebase architecture. (2) I paired-programmed with them on their first two user stories, explaining design patterns and Spring annotations as we coded. (3) I created a small "Getting Started" document covering our project's conventions, common patterns, and debugging tips. (4) I gave detailed code review feedback on their PRs — not just what to change, but why.
>
> **Result**: Within 3 weeks, they were independently delivering user stories. Within 2 months, they became one of the more productive team members. The "Getting Started" document I created was later used for all new joiners to the project.

---

### "Tell me about a mistake you made and what you learned." (STAR)

> **Situation**: Early in the Healthcare project, I deployed a service update that included a database schema change (adding a new column) but forgot to coordinate with the DBA team for the production migration.
>
> **Task**: The deployment failed in production because the column didn't exist, causing a 30-minute downtime for the patient admission module.
>
> **Action**: (1) I immediately rolled back the deployment. (2) Coordinated with the DBA to apply the schema change. (3) Re-deployed successfully. (4) I took full ownership of the mistake in the retrospective. (5) I proposed implementing Flyway for database migration management — so schema changes would be version-controlled and applied automatically during deployment.
>
> **Result**: The team adopted Flyway. We never had a schema-related deployment failure again. I learned to always have a deployment checklist and to separate database changes from application code deployment when possible. This experience made me much more careful about production deployments.

---

## Part 6: Quick Topic-to-Story Mapping (Reference Card)

Use this as a quick lookup during interview prep:

| Technical Topic | Project | Key Point |
|----------------|---------|-----------|
| OOP (4 pillars) | Healthcare | Patient hierarchy, Signable interface, Assessment polymorphism |
| Java 8 Streams | Healthcare | Patient filtering, grouping by department, lazy evaluation |
| Optional | Healthcare | Handling nullable doctor assignment |
| Exception Handling | Healthcare | Custom exceptions + `@ControllerAdvice` |
| Collections | Healthcare | HashMap cache, TreeMap for sorted reports, ConcurrentHashMap |
| Multithreading | Healthcare | `@Async` for DocuSign, `CompletableFuture` for parallel loading |
| Spring Boot architecture | Healthcare | Controller → Service → Repository, DTO pattern |
| Spring Data JPA | Healthcare | Entity mapping, N+1 fix with JOIN FETCH, `@EntityGraph` |
| Transactions | Healthcare | Patient admission atomicity, `REQUIRES_NEW` for audit |
| REST API design | Healthcare | Proper status codes, global exception handler, validation |
| Spring Security / JWT | Healthcare | JWT authentication for API access |
| Third-party integration | Healthcare | DocuSign OAuth 2.0, webhooks, retry logic |
| SQL optimization | Healthcare + Supply Chain | Execution plans, indexing, sargable queries |
| Stored procedures | Timesheet + Supply Chain | PL/SQL packages, error handling, CTEs |
| Database design | Supply Chain | Normalization to 3NF, strategic denormalization |
| Design Patterns | Healthcare | Factory, Strategy, Template Method, Observer, Builder |
| SOLID principles | Healthcare | Each principle with specific code example |
| Agile / Scrum | All projects | 2-week sprints, daily standup, retrospective |
| Performance issue | Healthcare | E-Chart search optimization (8s → 300ms) |
| Tight deadline | Healthcare | Admission Assessment module delivery |
| Mentoring | Healthcare | Onboarding junior developer |
| Mistake & learning | Healthcare | Deployment failure → Flyway adoption |
| Achievement | College | Smart India Hackathon 2019 Winner |
| Competitive Programming | College | ICPC regionals (2x), CodeChef Div 1 (1835) |

---

> [!TIP]
> **Practice Tip**: For each story, practice telling it in:
> - **30 seconds** (quick mention: "Yes, I used Streams in my Healthcare project to filter and group patient data by department")
> - **2 minutes** (detailed walkthrough with code example)
> - **5 minutes** (deep dive with follow-up questions anticipation)
>
> The interviewer will signal which depth they want. Start concise, expand if they ask follow-ups.
