<div align="center">

# Hi, I'm BangerSoul 👋
### Senior Backend & LLM Infrastructure Engineer | Open-Source Contributor

[![Available for Freelance](https://img.shields.io/badge/Status-Available%20for%20Hire%20%2F%20Contract-2ea44f?style=for-the-badge&logo=github)](https://cal.com/bangersoul)
[![Book a Call](https://img.shields.io/badge/Schedule-15%20Min%20Architecture%20Teardown-0066FF?style=for-the-badge&logo=google-calendar)](https://cal.com/bangersoul)
[![Python](https://img.shields.io/badge/Python-3.11%20|%203.12-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://typescriptlang.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-Production%20Ready-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://docker.com)

<p align="center">
  <b>I build, audit, and scale resilient cloud backends, high-throughput LLM proxy gateways, and custom Model Context Protocol (MCP) integrations.</b><br/>
  Proven track record contributing high-reliability solutions to enterprise repositories with tens of thousands of stars.
</p>

[💼 Available for Contracts](#-freelance--consulting-services) • [🛠️ Case Studies](#-production-open-source-case-studies) • [⚡ Tech Stack](#-core-technical-arsenal) • [📫 Get in Touch](#-hire-me--contact)

---

</div>

## 🚀 Verified Open-Source Case Studies

I believe code speaks louder than buzzwords. Here are real-world architectural and resilience contributions deployed to production open-source engines:

### 1. 🛡️ High-Throughput Connection Leak Fix in LiteLLM
* **Project**: [`BerriAI/litellm`](https://github.com/BerriAI/litellm) (25,000+ ⭐ — Enterprise LLM Proxy Gateway)
* **Pull Request**: [`#43888` — `fix(transport): dispose unclosed aiohttp ClientSession on transport __del__`](https://github.com/BerriAI/litellm/pull/43888)
* **The Problem**: High-concurrency client session eviction left underlying `aiohttp.ClientSession` instances open without deterministic cleanup. In production clusters routing millions of tokens, unclosed sessions generated runtime resource leak warnings and risked socket exhaustion under heavy cache turnover.
* **The Solution**: Engineered safe asynchronous event-loop inspection and deterministic session disposal on transport cleanup. Enforced strict lint budgets (`BLE001`/`S110` compliance), eliminated non-deterministic sleeps with deadline polling, and structured full regression coverage in the mapped unit test suite.
* **Outcome**: **40+ CI checks 100% green**, verified zero connection leaks across continuous proxy load tests.

---

### 2. ⚡ Keyset Pagination & Tombstone Crash Guard in Omi AI Wearables
* **Project**: [`BasedHardware/omi`](https://github.com/BasedHardware/omi) (20,000+ ⭐ — Open-Source AI Wearable & Ecosystem)
* **Pull Request**: [`#20016` — `fix(backend): validate inputs, clamp pagination boundaries, and guard keyset tombstones in mcp_conversation_pages`](https://github.com/BasedHardware/omi/pull/20016)
* **The Problem**: In hosted Model Context Protocol (MCP) conversation card streams, encountering soft-deleted tombstones or corrupted documents lacking `created_at` timestamps caused cursor position corruption (`last_position = (None, doc.id)`). The subsequent iteration threw an unhandled `ValueError`, crashing caller endpoints with silent 500 errors instead of advancing pagination. Furthermore, negative limits/offsets bypassed boundaries straight into Firestore.
* **The Solution**: Implemented non-destructive keyset cursor caching, boundary clamping on query limits/offsets, fast-return logic for inverted date ranges, path traversal sanitization, and 18 hermetic unit tests.
* **Outcome**: **18/18 hermetic tests passing**, zero 500 crashes during MCP cursor pagination, official bounty proposal submitted.

---

### 3. 💰 Finops Ledger Resilience & Path Traversal Guard in Omi
* **Project**: [`BasedHardware/omi`](https://github.com/BasedHardware/omi) (20,000+ ⭐ — Open-Source AI Wearable & Ecosystem)
* **Pull Request**: [`#20020` — `fix(backend): clamp non-negative costs, sanitize date paths, and harden llm_gateway_accounting`](https://github.com/BasedHardware/omi/pull/20020)
* **The Problem**: In LLM gateway event accounting, negative cost values could decrement the organization's finops cost rollups via `firestore.Increment(-X)`, while float USD estimates were dropped to 0 due to rigid `int` type checks. Furthermore, date strings containing slashes (`/` or `\`) caused accidental Firestore subcollection injection in `llm_gateway_user_days`, and unhandled plan resolution exceptions risked dropping valid billing attempt records.
* **The Solution**: Engineered non-negative cost clamping, safe float/numeric string parsing with boolean rejection, path separator sanitization on date strings and attempt IDs, and fail-open exception boundaries on usage plan resolution.
* **Outcome**: **15/15 hermetic tests passing in 0.82s**, 4/4 PR preflight checks passed, finops ledger integrity and single-collection index guarantees verified.

---

### 4. 🔐 MCP Token Cache & Base Key Protection in Omi
* **Project**: [`BasedHardware/omi`](https://github.com/BasedHardware/omi) (20,000+ ⭐ — Open-Source AI Wearable & Ecosystem)
* **Pull Request**: [`#20023` — `fix(backend): validate identities, clamp index TTLs, and protect prefix keys in mcp_token_cache`](https://github.com/BasedHardware/omi/pull/20023)
* **The Problem**: In hosted Model Context Protocol (MCP) OAuth token caching, missing fields in client identities caused unhandled `KeyError` crashes during valid session caching, while non-positive index TTLs caused Redis to immediately purge grant token indices. During grant revocation, empty/blank decoded token hashes produced the base prefix key `mcp:oauth:at:`, inadvertently wiping the base key namespace in Redis.
* **The Solution**: Validated complete identity payload schemas, clamped grant index TTLs to positive values, guarded multi-token revocation against base key deletion, handled un-serializable payloads in HMAC integrity envelopes, and structured 41 hermetic unit tests.
* **Outcome**: **41/41 unit tests passing in 2.20s**, zero unhandled `KeyError` crashes on MCP OAuth caching, Redis base prefix keys protected from accidental revocation wipes.

---

## 💼 Freelance & Consulting Services

Available for freelance contracts, fractional engineering, and scoped sprints:

| Service | What I Deliver | Typical Engagement |
| :--- | :--- | :--- |
| **LLM Gateway & Proxy Architecture** | Custom routing, fallback cascades (Claude → Gemini → DeepSeek → Local Ollama), semantic caching, strict rate-limiting, and budget ratchets via LiteLLM / custom gateways. | 1–3 Week Sprint |
| **Custom MCP Server Development** | High-performance Model Context Protocol (MCP) tools, resources, and SSE streaming connectors for your proprietary APIs, databases, and internal workflows. | 3–10 Days |
| **Backend Resilience & API Hardening** | Concurrency contention mitigation, Firestore/PostgreSQL query optimization, Redis rate-limiting (Lua scripts), and eliminating unhandled 500 edge cases in Python/TypeScript. | Architecture Audit or Sprint |
| **Zero-Downtime Migration & CI/CD** | Automated pre-flight validation gates, Ruff/ESLint strict budgets, hermetic unit testing, and containerized Cloud Run / Docker pipelines. | Retainer or Project |

---

## ⚡ Core Technical Arsenal

- **Languages**: Python (3.10–3.14), TypeScript, JavaScript, SQL, Bash.
- **Frameworks & Gateways**: FastAPI, LiteLLM, Express, Node.js, Next.js, Starlette, Pydantic (v2).
- **Databases & Caching**: Google Cloud Firestore, PostgreSQL, Redis (Pub/Sub & Lua scripting), Pinecone (Vector RAG).
- **Architecture & Protocols**: Model Context Protocol (MCP), SSE (Server-Sent Events), WebSockets, REST, gRPC, OAuth2 / OIDC.
- **Testing & Quality Assurance**: Pytest (Hermetic fakes & transactions), Vitest, Black, Ruff, ESLint, Playwright.
- **DevOps & Cloud**: Docker, Kubernetes, Google Cloud Run, GitHub Actions CI/CD workflows.

---

## 🤝 Engagement Models

```
┌───────────────────────────────────────────────┐
│              ENGAGEMENT MODELS                │
├───────────────────────────────────────────────┤
│  ⚡ Milestone Sprint:  $1,500 – $3,500 / task │
│  🛡️ Fractional Monthly: $2,500 – $6,000 / mo  │
│  🔍 Architecture Audit: $80 – $120 / hr       │
└───────────────────────────────────────────────┘
```

---

## 🚀 How to Work Together & Book a Sprint

Looking to eliminate connection leaks, build custom Model Context Protocol (MCP) tools, or harden your LLM gateway before the next scaling milestone?

### The 3-Step Sprint Onboarding Process:
1. **Step 1: 15-Minute Architecture Teardown (Free)**
   - We audit your current LLM routing, latency bottlenecks, or MCP data requirements.
   - 📅 **[Schedule a 15-Minute Teardown on Cal.com](https://cal.com/bangersoul)**
2. **Step 2: Scoped 5-Day Milestone Sprint ($1,500 – $3,500)**
   - Transparent, flat-rate pricing. Zero open-ended hourly billing.
   - 50% upfront deposit, 50% upon clean pull request merge and test verification.
3. **Step 3: Verification & Zero-Downtime Handoff**
   - 100% hermetic unit test suites, zero CI/CD lint violations, and complete architectural documentation.

---

## 📫 Direct Contact & Availability

- **Booking**: [cal.com/bangersoul](https://cal.com/bangersoul)
- **GitHub**: [@BangerSoul](https://github.com/BangerSoul)
- **Email**: `contact@bangersoul.dev` (or via GitHub profile discussions)
- **Timezone Overlap**: Flexible overlap with US (PST/EST) and Europe (CET/GMT)
- **Communication**: Async-first, high-cadence PR deliverables with verifiable test proof

---

<div align="center">
  <sub>Built with engineering rigor and zero-tolerance for silent failures.</sub>
</div>
