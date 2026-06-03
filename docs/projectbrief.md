# Project Brief: Customer Support Q&A Portal

## What We're Building

This project is a customer support Q&A portal for a fictional e-commerce store.

The store has five existing policy documents. Customers should be able to visit a clean, modern support page, ask a question in natural language, and get a helpful answer grounded in those documents.

This is intentionally **not** a production RAG system. There are no embeddings, vector databases, chunking pipelines, rerankers, or eval suites in this course project. The application uses a simple prompt-based document flow so the course can focus on the agentic software delivery workflow: requirements, spec, GitHub Issues, implementation, testing, review, deployment, and operations.

## Scenario

You have been asked to build a support portal for an e-commerce store.

The business already has written policies for refunds, shipping, warranties, account help, and privacy. Support volume is increasing, and customers are asking the same questions repeatedly:

- "Can I return an opened item?"
- "How long does shipping take?"
- "What happens if my product breaks?"
- "How do I delete my account?"
- "Do you store my payment details?"

The business wants a simple web application that can answer those questions quickly without inventing policy.

## Target User

The primary user is an e-commerce customer who wants a quick answer before contacting support.

The secondary user is the support team, who want fewer repetitive tickets and clearer answers based on the current policy documents.

## Product Shape

The app is a small full-stack web application:

- **Frontend:** TypeScript web UI with a polished e-commerce support-page design.
- **Backend:** Python API that loads the policy documents and calls the Claude SDK.
- **Documents:** Five markdown files included in the starter repo.
- **AI flow:** Prompt Claude with the customer's question and the available policy documents.
- **Deployment:** Deployed as a real web application with environment variables, logs, and live verification.

The UI should feel like a modern store support portal, not a developer demo. It should have:

- a support-center landing section
- a chat or question input
- example question prompts
- an answer area
- clear source/policy attribution
- helpful empty, loading, error, and unsupported-question states

## Provided Policy Documents

The course provides starter documents in `agentic-engineer/starter-docs/`. In the starter application repo, these should live at:

- `docs/policies/refund-policy.md`
- `docs/policies/shipping-policy.md`
- `docs/policies/warranty-policy.md`
- `docs/policies/account-policy.md`
- `docs/policies/privacy-policy.md`

Students do not need to invent documents. The documents are intentionally small enough to load directly into the prompt.

## Core Behavior

When a customer asks a question, the system should:

1. Load the five policy documents.
2. Ask Claude to identify which document or documents are relevant.
3. Answer using only the relevant policy content.
4. Include the policy document name or names used.
5. Say it does not know when the documents do not contain the answer.
6. Refuse off-topic questions politely.

## Prompt Contract

The backend should use a prompt with this shape:

```text
You are a customer support assistant for an e-commerce store.

Answer customer questions using only the policy documents provided.

Available documents:
- refund-policy.md: refunds, returns, exchanges, store credit
- shipping-policy.md: shipping options, delivery windows, tracking, lost packages
- warranty-policy.md: warranty coverage, replacements, repairs, exclusions
- account-policy.md: account access, password resets, billing profiles, account deletion
- privacy-policy.md: personal data, retention, deletion requests, payment data

Rules:
1. First decide which policy document or documents are relevant.
2. Use only the provided policy content to answer.
3. If the answer is not in the policies, say you do not know and suggest contacting support.
4. Do not answer off-topic questions.
5. Do not invent policy.
6. Include the policy document names used.
```

The exact prompt can evolve during implementation, but those rules are product requirements.

## V1 Requirements

- Customer can type a question.
- Customer receives a concise answer grounded in the policy documents.
- Answer shows which policy document or documents were used.
- Unsupported questions produce a clear "I don't know based on these policies" response.
- Off-topic questions are refused politely.
- The backend does not expose the API key.
- The app has useful loading and error states.
- The app can be deployed and verified live.

## Non-Goals

- No embeddings or vector database.
- No document upload UI.
- No admin dashboard.
- No user accounts.
- No analytics dashboard.
- No ticket creation workflow.
- No production-grade eval suite.
- No multi-tenant support.
- No payment or checkout integration.

## Technical Notes

Suggested stack:

- Python backend, probably FastAPI.
- TypeScript frontend, probably React/Next.js or a similarly familiar web stack.
- Claude SDK for inference.
- Markdown policy documents checked into the repo.
- GitHub Issues for tasks.
- GitHub Pull Requests for review.
- GitHub Actions for basic checks.

The stack is intentionally conventional. The course is about using a coding agent to build the app professionally, not about teaching a novel framework.

## Success Criteria

By the end of the course, the project should have:

- a working local app
- five provided policy documents
- a tested document-loading path
- a tested answer API
- a polished support portal UI
- a GitHub issue/branch/PR workflow
- meaningful tests and CI
- a deployed live version
- documented deployment and rollback steps

## Teaching Boundary

This app contains AI, but the course is not about production AI architecture.

The AI feature exists so students build something realistic and exciting while practicing the agentic engineering workflow. Production RAG, embeddings, retrieval evaluation, tracing, observability, and model operations belong in AI Architect.
