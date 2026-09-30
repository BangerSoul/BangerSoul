<div align="center">

# Hi, I'm BangerSoul 👋
### Senior Backend & LLM Infrastructure Engineer | Open-Source Contributor

[![Available for Freelance](https://img.shields.io/badge/Status-Available%20for%20Hire%20%2F%20Contract-2ea44f?style=for-the-badge&logo=github)](mailto:contact@bangersoul.dev)
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

## 📫 Hire Me & Contact

Looking to solve a tough backend problem, build a custom LLM gateway, or implement private MCP connectors for your team?

- **GitHub**: [@BangerSoul](https://github.com/BangerSoul)
- **Email**: Reach out via GitHub profile or repository discussions
- **Timezone**: Flexible overlap with US (PST/EST) and Europe (CET/GMT)
- **Turnaround**: Fast, async-first communication with clear PR deliverables and test proof

---

<div align="center">
  <sub>Built with engineering rigor and zero-tolerance for silent failures.</sub>
</div>
