# Customer Support Q&A Portal

This is the sample project for the Agentic Engineer course.

Students will use this repository to build a customer support Q&A application end to end with an AI coding agent. The finished app will have a Python backend, a TypeScript frontend, simple markdown document loading, and grounded answers with policy source attribution.

The repository starts intentionally small. The first source of truth is the project brief:

- [docs/projectbrief.md](docs/projectbrief.md)

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

## Getting Started

```bash
git clone https://github.com/the-ai-engineer/hr-policy-chatbot.git
cd hr-policy-chatbot
```

Start by reading `docs/projectbrief.md`. Do not assume the application structure yet; the course will create it through the agentic engineering workflow.
