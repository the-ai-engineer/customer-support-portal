# Agentic Engineer Prompt Cheat Sheet

Use these prompts to kick off the Customer Support Q&A Portal project on camera.

The fictional product name is Northstar Support. It answers customer questions for an e-commerce store using the policy documents in `docs/policies/`.

They are written for Codex, but the workflow transfers to other coding agents. The important pattern is:

```text
context -> decision -> plan -> implementation -> verification -> review
```

Do not use every prompt in one session. Pick the prompt that matches the lesson moment.

## 1. First Repo Inspection

Use this at the start of the project, before asking for code.

```text
Read this repository and tell me what you inspected.

Focus on:
- the project brief
- the policy documents
- the current file structure
- what exists already
- what does not exist yet
- the likely next engineering step

Do not write code yet. I want a grounded summary based on files in the repo.
```

Filming point: show that the agent must inspect files before it can make a useful plan.

## 2. Turn The Brief Into Requirements

Use this when teaching the difference between a brief and buildable requirements.

```text
Read docs/projectbrief.md and turn it into a clear requirements summary.

Separate:
- user goals
- functional requirements
- non-functional requirements
- non-goals
- open questions
- risks or decisions we need to make before implementation

Do not change files yet.
```

Filming point: the agent can help structure fuzzy product context, but the human still approves the decisions.

## 3. Draft The Implementation Spec

Use this when introducing spec-driven development.

```text
Write an implementation spec for the first version of this project.

Use docs/projectbrief.md as the source of truth.

The spec should cover:
- product behaviour
- frontend shape
- backend API shape
- policy document format and location
- model/prompt contract
- error, unsupported-question, and off-topic behaviour
- testing strategy
- deployment assumptions
- explicit non-goals

Save it as docs/spec.md.

Do not implement the app yet.
```

Filming point: the spec is a review checkpoint before code starts.

## 4. Review The Spec Like A Human Owner

Use this after the spec exists.

```text
Review docs/spec.md against docs/projectbrief.md.

Look for:
- missing requirements
- invented scope
- vague behaviour
- risky assumptions
- unclear API contracts
- test gaps
- anything that would confuse an implementation agent

Return findings first, then suggest specific edits.
Do not change files yet.
```

Filming point: review is part of the workflow, not something saved for the end.

## 5. Break The Spec Into Agent-Sized Tasks

Use this before opening GitHub Issues or starting implementation.

```text
Read docs/projectbrief.md and docs/spec.md.

Break the project into small implementation tasks that can each be built, tested, reviewed, and merged independently.

For each task include:
- title
- goal
- files or areas likely touched
- acceptance criteria
- suggested verification
- dependencies on other tasks

Keep tasks small enough for one focused agent session.
```

Filming point: this is where the course moves from "build an app" to controllable units of work.

## 6. Create Project Instructions

Use this when teaching context engineering.

```text
Create an AGENTS.md file for this repository.

It should give future agents durable project guidance:
- project goal
- source of truth documents
- policy document location
- expected stack
- workflow expectations
- testing and verification expectations
- scope boundaries and non-goals
- security reminders around API keys

Keep it concise. Do not duplicate the entire project brief.
```

Filming point: durable context belongs in the repo, not only in a chat message.

## 7. Start The First Implementation Task

Use this once a task has been chosen.

```text
Implement the first task: set up the project skeleton for the Customer Support Q&A Portal.

Before editing, inspect the repo and explain the structure you are going to create.

Constraints:
- Python backend
- TypeScript frontend
- simple markdown policy documents in docs/policies
- no embeddings or vector database
- no live order lookup or account-specific actions
- keep the change focused on project setup
- include basic commands in the README if needed

After implementation, run the relevant checks and report what changed.
```

Filming point: one task, one branch-sized change, one verification loop.

## 8. Build The Backend Document Loader

Use this for the first meaningful backend feature.

```text
Implement the backend document-loading path.

The backend should load markdown customer support policy documents from disk and expose that logic through a small, testable module.

Acceptance criteria:
- policy files have a predictable location
- exactly the provided policy files are loaded
- loader returns document name and content
- empty or missing document directories are handled deliberately
- tests cover the loader behaviour
- no model API call is required for this task

Keep the change focused.
```

Filming point: useful tests start before the AI integration.

## 9. Build The Answer API With A Mockable Model Boundary

Use this when connecting product behaviour to backend architecture.

```text
Implement the backend question-answer API.

Use the policy document loader and create a model boundary that can be mocked in tests.

The API should accept a question and return:
- answer
- sources
- status for answered, unsupported, or off-topic

Do not expose API keys to the frontend.
Add tests for the API behaviour using a fake model response.
```

Filming point: keep model calls behind a boundary so the app is testable.

## 10. Build The Frontend Flow

Use this for the main user-facing screen.

```text
Build the TypeScript frontend for the Customer Support Q&A Portal.

The page should include:
- a polished e-commerce support interface
- question input
- example prompts
- answer display
- source display
- loading state
- error state
- unsupported and off-topic states

Match the project brief. Do not make a marketing landing page.
Run the relevant frontend checks and, if possible, verify the flow in a browser.
```

Filming point: the UI should become the product, not a wrapper around a demo API.

## 11. Ask For A Review Before Merging

Use this after a meaningful change.

```text
Review the current diff like a senior engineer.

Prioritise:
- correctness
- scope creep
- missing tests
- broken contracts
- security issues
- confusing code or docs

Findings first, ordered by severity.
If there are no findings, say that and identify any remaining risks.
```

Filming point: the agent can help review, but the human still owns the merge decision.

## 12. Prepare A Pull Request

Use this when teaching GitHub workflow.

```text
Summarise the current branch for a pull request.

Include:
- what changed
- why it changed
- how it was tested
- screenshots or browser checks if relevant
- known limitations
- follow-up tasks

Keep it concise and useful for review.
```

Filming point: the PR is a communication artifact, not just a code container.

## 13. Deployment Planning

Use this before deploying.

```text
Create a deployment plan for this app.

Cover:
- frontend hosting
- backend hosting
- environment variables and secrets
- build commands
- health checks
- smoke test steps
- rollback plan
- logs to inspect if something fails

Do not deploy yet. Save the plan as docs/deployment.md.
```

Filming point: deployment is planned and verified like any other engineering task.

## 14. Live Verification

Use this after deployment.

```text
Verify the deployed Customer Support Q&A Portal.

Check:
- the frontend loads
- the question flow works
- answers show sources
- unsupported questions behave correctly
- off-topic questions are refused
- no secrets are exposed in browser code or logs
- backend logs look healthy

Report the live URL, checks performed, and any issues found.
```

Filming point: "deployed" only counts after the live system is checked.

## Good Prompt Habits To Call Out

- Ask the agent what it inspected.
- Tell it when not to write code yet.
- Name the source-of-truth files.
- Put boundaries and non-goals in the prompt.
- Ask for acceptance criteria and verification.
- Keep each implementation prompt to one task.
- Review the diff before committing.
- Prefer tests, browser checks, logs, and live smoke tests over vibes.

## Short Opening Prompt

Use this when you want the smallest possible on-camera start.

```text
Read this repository, especially docs/projectbrief.md, and tell me the next sensible step for building this project through the Agentic Engineer workflow. Do not edit files yet.
```
