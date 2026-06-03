# Project Brief: Customer Support Q&A Portal

Working product name: Northstar Support

## What We're Building

This project is a customer support Q&A portal for a fictional e-commerce store called Northstar Outfitters.

The store has five existing policy documents. Customers should be able to visit a clean, modern support page, ask a question in natural language, and get a helpful answer grounded in those documents.

This is intentionally **not** a production RAG system. There are no embeddings, vector databases, chunking pipelines, rerankers, or eval suites in this course project. The application uses a simple prompt-based document flow so the course can focus on the agentic software delivery workflow: requirements, spec, GitHub Issues, implementation, testing, review, deployment, and operations.

The point of the app is not e-commerce domain depth. The point is to give students a realistic, understandable product surface while they learn how to direct AI coding agents through a professional build workflow.

## Why This Project

## Scenario

You have been asked to build a support portal for an e-commerce store.

The business already has written policies for refunds, shipping, warranties, account help, and privacy. Support volume is increasing, and customers are asking the same questions repeatedly:

- "Can I return an opened item?"
- "How long does shipping take?"
- "What happens if my product breaks?"
- "How do I delete my account?"
- "Do you store my payment details?"

The business wants a simple web application that can answer those questions quickly without inventing policy.

This scenario works well for the course because:

- customers can ask natural questions without needing specialist knowledge
- the policies are concrete enough to test source grounding
- unsupported answers are easy to recognise
- several questions require more than one policy document
- the UI can be polished without needing authentication, payments, or admin workflows
- the AI feature is useful but small enough to build in a teaching sequence

## Target User

The primary user is an e-commerce customer who wants a quick answer before contacting support.

The secondary user is the support team, who want fewer repetitive tickets and clearer answers based on the current policy documents.

## User Jobs

Customers should be able to:

- understand whether they can return an item
- find expected shipping times and tracking guidance
- understand what to do when an order is missing or delayed
- check whether a broken product may be covered by warranty
- understand account access, password reset, and account deletion basics
- ask privacy questions about payment data, retention, and deletion requests

Support staff should be able to trust that the app:

- cites the policy documents used
- avoids inventing policy
- tells customers when the policies do not contain the answer
- refuses unrelated questions

## Product Shape

The app is a small full-stack web application:

- **Frontend:** TypeScript web UI with a polished e-commerce support-page design.
- **Backend:** Python API that loads the policy documents and calls the Claude SDK.
- **Documents:** Five markdown files included in the starter repo.
- **AI flow:** Prompt Claude with the customer's question and the available policy documents.
- **Deployment:** Deployed as a real web application with environment variables, logs, and live verification.

The UI should feel like a modern store support portal, not a developer demo or a generic chatbot page. It should have:

- a support-center landing section
- a chat or question input
- example question prompts
- an answer area
- clear source/policy attribution
- helpful empty, loading, error, and unsupported-question states

The first screen should let a customer ask a question immediately. Avoid a marketing-style landing page that delays the support workflow.

## Provided Policy Documents

The course provides starter documents in `agentic-engineer/starter-docs/`. In the starter application repo, these should live at:

- `docs/policies/refund-policy.md`
- `docs/policies/shipping-policy.md`
- `docs/policies/warranty-policy.md`
- `docs/policies/account-policy.md`
- `docs/policies/privacy-policy.md`

Students do not need to invent documents. The documents are intentionally small enough to load directly into the prompt.

Treat these documents as approved business policy. The app should not alter their meaning.

## Example Customer Questions

These are good test questions for demos, implementation checks, and live smoke tests:

- Can I return an opened item?
- Can I get a refund for a final sale item?
- How long does shipping take to Canada?
- My tracking has not updated for 7 business days. What happens next?
- Does the warranty cover accidental damage?
- Can I delete my account?
- Do you store my full payment card number?
- Can support tell me my password?
- Can you recommend a birthday present for my dad?

The last question is intentionally off-topic. The app should politely refuse it.

## Core Behavior

When a customer asks a question, the system should:

1. Load the five policy documents.
2. Ask Claude to identify which document or documents are relevant.
3. Answer using only the relevant policy content.
4. Include the policy document name or names used.
5. Say it does not know when the documents do not contain the answer.
6. Refuse off-topic questions politely.

The answer should be concise, but not so terse that it becomes unhelpful. A good answer is usually one to three short paragraphs plus a source list.

The system should not claim to have checked order status, account data, payment history, shipping carrier systems, or live inventory. It only has access to the policy documents.

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

## Expected Response Shape

The backend should return structured data, not just a text blob. The exact schema can be decided in the implementation spec, but it should include:

- `answer`: the customer-facing answer
- `sources`: policy document names used
- `status`: answered, unsupported, or off_topic

The frontend should render those fields clearly.

## Example Interactions

```text
Customer: Can I return an opened backpack?

Assistant: You can usually return an opened backpack if it was only lightly inspected, is complete and undamaged, and includes its accessories and packaging where possible. If it has been used on a trip, it would not normally be returnable unless it is faulty.

Sources: refund-policy.md
```

```text
Customer: My tracking has not updated for 7 business days. Is it lost?

Assistant: The policy says an order is considered potentially lost when tracking has not updated for 7 business days after dispatch. You should contact support with your order number. Support may ask you to confirm the shipping address and check nearby delivery locations before opening a courier investigation.

Sources: shipping-policy.md
```

```text
Customer: Can you suggest a hiking route near Edinburgh?

Assistant: I can only answer questions about Northstar Outfitters support policies. Please ask about refunds, shipping, warranties, accounts, or privacy.

Sources: none
```

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
- No live order lookup.
- No live courier tracking lookup.
- No customer-specific account actions.
- No legal advice.

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

The first implementation should prefer simple direct document loading over abstractions. If the five markdown files can fit in the model prompt, do that. Complexity should be introduced only when a later lesson explicitly asks for it.

## Testing Expectations

The project should collect evidence at each layer:

- document loader tests prove the five policy files can be found and read
- API tests prove questions produce structured answers with sources
- mocked model tests prove unsupported and off-topic statuses are handled
- frontend checks prove customers can submit a question and see an answer with sources
- deployment smoke tests prove the live app can complete the main flow

Tests should not depend on live model calls unless a lesson explicitly asks for a live integration check.

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
