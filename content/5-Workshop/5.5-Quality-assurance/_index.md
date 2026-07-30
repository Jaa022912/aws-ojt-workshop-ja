---
title: "Quality Assurance & Testing"
date: 2026-05-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

# Section 5.5 - Quality Assurance & Testing Strategy

To guarantee the high reliability, resilience, and data integrity of **AI AWS Advisor**, the project implements a comprehensive dual-layered automated unit testing architecture.

---

## 1. Backend Testing Framework (Pytest + Moto)

The backend utilizes `pytest` with specialized AWS mocking libraries to test business logic and cloud integrations without making real AWS API calls or incurring cloud charges.

### Key Tools & Mocking Architecture:
- **`pytest` & `pytest-mock`:** Test discovery, assertions, and fixture mocking.
- **`moto`:** Intercepts `boto3` AWS SDK calls, creating an in-memory virtual DynamoDB database and STS service.
- **Bedrock Mocking:** Intercepts `boto3.client('bedrock-runtime').invoke_model()` calls to return deterministic JSON responses, testing AI output parsing and fallback handlers.

```bash
cd backend
python -m pytest tests/ -v
```

---

## 2. Frontend Testing Framework (Vitest + React Testing Library)

The React client implements component testing focusing on user interaction and data visual rendering.

### Key Tools:
- **`Vitest`:** Lightning-fast Vite-native testing framework.
- **`React Testing Library (RTL)`:** Renders components in `jsdom` headless DOM environment.
- **`vi.mock()`:** Intercepts TanStack React Query and Axios HTTP calls.

```bash
cd frontend
npm run test
```

---

## 3. Continuous Integration Readiness

Both test suites execute independently in under 10 seconds without external internet or cloud dependencies, making them fully ready for integration into **GitHub Actions** or **AWS CodePipeline** CI/CD quality gates.
