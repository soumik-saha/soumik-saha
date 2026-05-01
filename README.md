# Soumik Saha — Backend Engineer | Java · Spring Boot · System Design

<p align="left">
  <a href="https://linkedin.com/in/soumikisonline"><img src="https://img.shields.io/badge/LinkedIn-soumikisonline-0A66C2?style=flat&logo=linkedin" alt="LinkedIn"/></a>
  <a href="https://www.soumik.co.in"><img src="https://img.shields.io/badge/Portfolio-www.soumik.co.in-4A90E2?style=flat&logo=googlechrome&logoColor=white" alt="Portfolio"/></a>
  <a href="mailto:sahasoumik1573@gmail.com"><img src="https://img.shields.io/badge/Email-sahasoumik1573@gmail.com-D14836?style=flat&logo=gmail&logoColor=white" alt="Email"/></a>
  <img src="https://komarev.com/ghpvc/?username=soumik-saha&label=Profile+Views&color=0e75b6&style=flat" alt="profile views"/>
</p>

---

## What I Do

- Design and build REST APIs with clear contracts, layered service boundaries, and explicit error handling
- Apply correctness-first patterns — idempotency keys for deduplication, pessimistic locking for concurrent writes, and audit trails for observability
- Structure Spring Boot applications with separation of concerns: controller → service → repository, with profile-based config for dev/prod parity
- Decompose systems into cooperating services: Java backend + Python microservice + Helm-based Kubernetes deployment (see **Briefly**)
- Integrate security at the infrastructure layer — custom JWT filter chain, role-scoped endpoints, and admin registration gated by a shared secret header

---

## Tech Stack

**Backend**
`Java 17` · `Spring Boot 3.x` · `Spring Security` · `Spring Data JPA` · `Python 3` · `FastAPI` · `Node.js` · `Express.js`

**Databases**
`PostgreSQL` · `MySQL` · `MongoDB` · `H2 (testing)`

**Infrastructure & Tools**
`Docker` · `Docker Compose` · `Helm` · `Kubernetes` · `Maven` · `Gradle` · `Git` · `Caffeine Cache`

---

## Featured Projects

### [ecommerce-application](https://github.com/soumik-saha/ecommerce-application)
> Production-grade e-commerce REST API — cart, checkout, order lifecycle, payments, returns, audit trail.

**Engineering Highlights**

| Area | Decision |
|---|---|
| **API Design** | Role-scoped endpoints (`USER` / `ADMIN`); admin registration protected by `X-Admin-Secret` header to prevent privilege escalation without a separate admin service |
| **Authentication** | Custom `JwtAuthenticationFilter` injects principal before the security chain; access + refresh token pair with configurable expiry; `401` / `403` handled by dedicated entry points |
| **Database** | PostgreSQL (prod) / H2 (test) via Spring profiles; `findByIdForUpdate` (pessimistic lock) on product rows during checkout prevents oversell under concurrent requests |
| **Idempotency** | Order creation checks for an existing `idempotencyKey` before inserting — a duplicate POST returns the original order, not a second charge |
| **Async processing** | Order confirmation dispatched to a dedicated `notificationExecutor` thread pool via `@Async` — API response is not blocked by downstream notification latency |
| **Caching** | Caffeine in-process cache with the Spring Cache abstraction; designed to swap to Redis by changing a single dependency |
| **Audit logging** | Batch audit upload with per-entry idempotency keys; `successCount` / `duplicateCount` / `failureCount` breakdown; filterable CSV export for admin review |
| **Observability** | AOP-based request/response logging; order and payment status history tables capture every state transition with timestamps |
| **Ops** | Multi-stage Docker build; Docker Compose starts app only after `pg_isready` healthcheck passes; environment secrets injected at runtime, not baked into the image |

**Impact**
Full e-commerce lifecycle in a single deployable unit: auth → catalog → cart → checkout (with promo codes) → order tracking → return requests → audit export. Documented via Swagger UI.

---

### [briefly](https://github.com/soumik-saha/briefly)
> Multi-service URL summarization app: Spring Boot API + FastAPI LLM microservice + React UI, deployable to Kubernetes via Helm.

**Engineering Highlights**

- **Service decomposition:** Spring Boot (Java/Gradle) owns API routing and summary persistence; FastAPI (Python) isolates LLM inference — two runtimes, each independently scalable and replaceable
- **Deployment:** Helm chart for Kubernetes; root-level Docker Compose for local parity; each service ships its own Dockerfile
- **Separation of concerns:** The Java backend treats the LLM service as an internal dependency — callers never talk to the model server directly

**Impact**
Demonstrates polyglot service design and cloud-native deployment readiness beyond a single Spring Boot monolith.

---

### [SkyPulse](https://github.com/soumik-saha/SkyPulse)
> Automated aircraft damage detection system — built for Airbus Aerothon 6.0.

**Engineering Highlights**

- Fine-tuned **YOLOv5** on a custom aviation dataset (Roboflow) to detect and localize cracks, dents, and deformities on fuselage and wings
- **Random Forest classifier** trained on image-extracted features to flag faulty wiring within aircraft harnesses
- **Streamlit** backend integrates model inference with file upload, result visualization, and repair recommendation output
- End-to-end pipeline: image upload → preprocessing (OpenCV) → damage classification → repair suggestion

**Impact**
Working prototype delivered under hackathon time constraints; covers the full detection-to-recommendation loop for three damage categories.

---

### [PulseConnect](https://github.com/soumik-saha/PulseConnect)
> Blood donation matching platform connecting donors, recipients, and blood banks.

**Engineering Highlights**

- **JWT + Google OAuth2** via Passport.js — local and social auth strategies, session-aware cookie handling
- **MongoDB/Mongoose** schema design for donor profiles, donation requests, and bank inventory
- Express middleware chain: CORS → cookie-parser → auth → route handlers

**Impact**
Full-stack MERN application with dual auth strategies and geo-aware donor matching flow.

---

## Engineering Mindset

I start with correctness before optimizing for performance. That means: define the contract, handle the failure modes, make operations safe to retry, then add caching or async paths where the profiling justifies it. I prefer explicit over implicit — if a service has a side effect (audit log, notification, stock decrement), that effect is visible in code, not hidden in an interceptor with no obvious trigger.

---

## Current Focus

- Distributed systems fundamentals: consensus, replication, and partition tolerance trade-offs
- High-level and low-level system design (rate limiters, notification fan-out, distributed queues)
- Deepening Spring ecosystem knowledge: reactive streams, Spring Batch, Spring Cloud patterns

---

## Contact

| | |
|---|---|
| **LinkedIn** | [linkedin.com/in/soumikisonline](https://linkedin.com/in/soumikisonline) |
| **Portfolio** | [www.soumik.co.in](https://www.soumik.co.in) |
| **Email** | sahasoumik1573@gmail.com |
| **GitHub** | [github.com/soumik-saha](https://github.com/soumik-saha) |
| **LeetCode** | [leetcode.com/soumiksaha](https://leetcode.com/soumiksaha) |

---

<details>
<summary><strong>Profile Notes (for reviewers)</strong></summary>

**Repositories not worth your time:**
`DN3.0_Exercises` (training coursework), `CrackYourPlacement` / `6-Companies-30-Days` (DSA grind repos), `Number-Guessing-Game`, `Rock-Paper-Scissor`, `Simon-Game`, `dice-challenge`, `drum-kit` (toy/tutorial projects), `tindog`, `Space-Tourism`, `EliteTask-Dynamics` (HTML/CSS clones with no backend).

**High-impact projects I'm building next:**
1. **Rate Limiter Service** — token bucket + sliding window, Redis-backed, exposed as a library and as a standalone gRPC endpoint
2. **Distributed Task Queue** — delayed job scheduling, priority queue, at-least-once delivery with retry/backoff, worker pool management
3. **Real-time Notification System** — SSE + WebSocket fan-out, subscription management, delivery guarantee with inbox persistence

</details>
