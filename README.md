# Customer Support Q&A Portal

This is the sample project for the Agentic Engineer course.

Students will use this repository to build a customer support Q&A application end to end with an AI coding agent.

The fictional product is **Northstar Support**, a support portal for an e-commerce store called Northstar Outfitters. Customers ask questions about refunds, shipping, warranties, accounts, and privacy. The app answers only from the provided policy documents and shows which documents it used.

The finished app will have a Python backend, a TypeScript frontend, simple markdown document loading, and grounded answers with policy source attribution.

The repository starts intentionally small. The first source of truth is the project brief:

- [docs/projectbrief.md](docs/projectbrief.md)

The brief is written as customer context, not a technical spec. The course workflow turns that brief into requirements, an implementation spec, tickets, code, tests, review, and deployment.

For course demos and filming, use the starter prompts in:

- [docs/prompt-cheatsheet.md](docs/prompt-cheatsheet.md)

## Project Shape

The course builds this project in stages:

- understand the brief
- write a spec
- break the work into tasks
- implement one task at a time with an AI coding agent
- test and review the result
- deploy the finished app

The AI feature is deliberately simple: load a small set of markdown customer support policy documents and ask the model to answer only from those documents. This is not a vector database or production RAG project.

The starter policy documents live in:

- [docs/policies](docs/policies)

Those documents are part of the teaching setup. Students should not need to invent fake data before they can start building.

## Getting Started

```bash
git clone https://github.com/the-ai-engineer/customer-support-portal.git
cd customer-support-portal
```

Start by reading `docs/projectbrief.md`. Do not assume the application structure yet; the course will create it through the agentic engineering workflow.

Useful first prompts:

- Ask the agent to inspect the repo and summarize what exists.
- Ask the agent to turn `docs/projectbrief.md` into requirements.
- Ask the agent to draft an implementation spec before writing code.
