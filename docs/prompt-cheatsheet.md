# Agentic Engineer Prompt Cheat Sheet

Use these prompts to drive the Customer Support Portal project on camera.

The fictional product is **Northstar Support**. It answers customer questions for an e-commerce store using the policy documents in `docs/policies/`.

The prompts are written for Codex, but the workflow transfers to any coding agent. Each one follows the same shape — outcome first, then grounding, then what "done" looks like, then the boundaries:

```text
goal -> grounding -> done when -> boundaries
```

That shape is deliberate. We tell the agent the destination and what proof we need, and let it choose the path, instead of dictating every step.

Many of these are also packaged as Blueprint skills — `$spec`, `$plan`, `$implement`, `$tdd`, `$review`, `$commit`, `$branch`, `$browser-verify`. The prompt is what's inside the skill. Before lesson 6 we type the prompt; after it, we invoke the skill. The steps without a skill stay raw prompts.

Don't use every prompt in one session. Pick the one that matches the lesson moment.

## 1. First Repo Inspection

Use this at the start, before asking for any code.

```text
Read this repository and tell me what you looked at.

Goal: a grounded picture of where the project stands, so the next engineering step is obvious.

Cover the project brief, the policy documents, the current structure, what already exists, and what doesn't yet.

Base it on the files you actually read — name them. Don't write code yet.
```

Filming point: the agent has to inspect files before it can make a useful plan.

## 2. Turn The Brief Into Requirements

Use this when teaching the difference between a brief and buildable requirements.

```text
Read docs/projectbrief.md and turn it into a clear requirements summary.

Goal: separate what the product must do from how we'll build it, so we can review the decisions before any code.

Pull out user goals, functional requirements, non-functional requirements, non-goals, open questions, and the decisions we need to make before implementation.

Ground it in the brief. Flag anything the brief leaves unclear instead of guessing. Don't change files yet.
```

Filming point: the agent can structure fuzzy product context, but the human still approves the decisions.

## 3. Draft The Implementation Spec

Use this when introducing spec-driven development. Skill: `$spec`.

```text
Write the V1 implementation spec, grounded in docs/projectbrief.md.

Goal: a spec a fresh agent could build from without guessing the decisions that matter.

Cover the decisions that change the build: product behavior, the frontend and backend API shapes, the model/prompt contract, where policy documents live, and the behavior for errors, unsupported questions, and off-topic questions. Note how we'll verify it and what's out of scope.

Ground every decision in the brief. If a decision isn't in the brief and would change the build, ask instead of inventing it.

Save it as docs/spec.md. Don't write application code yet.
```

Filming point: the spec is a review checkpoint before code starts.

## 4. Review The Spec Like A Human Owner

Use this once the spec exists. Skill: `$review`.

```text
Review docs/spec.md against docs/projectbrief.md.

Goal: catch the problems now, while they're cheap to fix in a document.

Look for missing requirements, invented scope, vague behavior, risky assumptions, unclear API contracts, and test gaps — anything that would make an implementation agent guess.

Give me the findings first, ordered by how much they'd hurt, then suggest specific edits. Don't change files yet.
```

Filming point: review is part of the workflow, not something saved for the end.

## 5. Break The Spec Into Agent-Sized Tasks

Use this before opening GitHub Issues or starting implementation. Skill: `$plan`.

```text
Read docs/projectbrief.md and docs/spec.md, then break the project into small implementation tasks.

Goal: tasks small enough that each can be built, tested, reviewed, and merged on its own in one focused session.

For each task give a title, the goal, the files or areas it likely touches, acceptance criteria, how to verify it, and what it depends on.

Order them so dependencies come first. Don't start implementation.
```

Filming point: this is where the course moves from "build an app" to controllable units of work.

## 6. Create Project Instructions

Use this when teaching context engineering.

```text
Create an AGENTS.md for this repository.

Goal: durable guidance a future agent can rely on without re-reading the whole brief each time.

Include the project goal, the source-of-truth documents, where policy docs live, the expected stack, workflow and verification expectations, scope boundaries and non-goals, and a reminder to keep the API key server-side.

Keep it concise — point at the brief, don't copy it.
```

Filming point: durable context belongs in the repo, not only in a chat message.

## 7. Start The First Implementation Task

Use this once a task is chosen. Skill: `$implement`.

```text
Implement the first task: set up the project skeleton, grounded in the spec.

Goal: a runnable skeleton for the customer support portal — Python backend, TypeScript frontend, markdown policy docs in docs/policies — and nothing more.

Before editing, inspect the repo and tell me the structure you'll create.

Done when the skeleton is in place and the basic run commands are in the README. Keep it to setup — no retrieval, no model calls, no deployment yet. Run the relevant checks and report what changed.
```

Filming point: one task, one branch-sized change, one verification loop.

## 8. Build The Backend Document Loader

Use this for the first meaningful backend feature. Skill: `$implement` (or `$tdd` for test-first).

```text
Implement the backend document-loading path.

Goal: a small, testable module that loads the markdown policy documents from disk.

Done when:
- the policy files have a predictable location
- it loads exactly the provided files and returns each document's name and content
- missing or empty directories are handled deliberately
- tests cover that behavior

No model call is needed for this task. Keep the change focused.
```

Filming point: useful tests start before the AI integration.

## 9. Build The Answer API With A Mockable Model Boundary

Use this when connecting product behavior to backend architecture. Skill: `$tdd`.

```text
Implement the question-answer API in the backend.

Goal: an endpoint that answers from the policy documents, with the model call behind a boundary a test can replace with a fake.

Done when:
- it returns { answer, sources, status } where status is answered / unsupported / off-topic
- tests cover all three cases using the fake model boundary
- the API key never reaches the frontend

Keep the change to the API and its tests.
```

Filming point: keep model calls behind a boundary so the app stays testable.

## 10. Build The Frontend Flow

Use this for the main user-facing screen. Skill: `$implement`, then `$browser-verify`.

```text
Build the TypeScript frontend for the customer support portal.

Goal: the support page that is the product — not a wrapper around the API.

Match the brief. The page needs a question input, example prompts, the answer and its sources, and clear loading, error, unsupported, and off-topic states.

Done when the main question-to-answer flow works in the browser. Run the frontend checks and verify the flow in a browser if you can. Don't build a marketing landing page.
```

Filming point: the UI should become the product, not a wrapper around a demo API.

## 11. Ask For A Review Before Merging

Use this after a meaningful change. Skill: `$review`.

```text
Review the current diff like a senior engineer.

Goal: decide whether this is safe to merge, with reasons.

Prioritize correctness, scope creep, missing tests, broken contracts, and security.

Findings first, ordered by severity, each tied to a file or behavior. If there's nothing to fix, say so and name the risks that remain. Don't change code yet.
```

Filming point: the agent can help review, but the human still owns the merge decision.

## 12. Prepare A Pull Request

Use this when teaching the GitHub workflow.

```text
Summarize this branch for a pull request.

Goal: a PR a reviewer can understand without reading every line.

Include what changed, why, how it was tested, browser checks or screenshots if relevant, known limitations, and any follow-ups.

Keep it concise. Don't open the PR yet.
```

Filming point: the PR is a communication artifact, not just a code container.

## 13. Deployment Planning

Use this before deploying.

```text
Write a deployment plan for this app. Save it as docs/deployment.md.

Goal: a plan someone else could follow to deploy the app and recover it if it breaks.

Cover frontend hosting, backend hosting, environment variables and secrets, build commands, health checks, smoke-test steps, the rollback plan, and which logs to read when something fails.

Don't deploy yet.
```

Filming point: deployment is planned and verified like any other engineering task.

## 14. Live Verification

Use this after deployment. Skill: `$browser-verify`.

```text
Verify the deployed customer support portal.

Goal: confirm the live system works for a real user, not just that it deployed.

Check that the frontend loads, the question flow works, answers show their sources, unsupported and off-topic questions behave, no secrets appear in browser code or logs, and the backend logs look healthy.

Report the live URL, what you checked, and anything that's off.
```

Filming point: "deployed" only counts after the live system is checked.

## Good Prompt Habits To Call Out

- Lead with the goal and what "done" looks like, not a list of steps.
- Name the source-of-truth files.
- Put boundaries and non-goals in the prompt.
- Reserve "never" and "must" for real invariants, like keeping secrets server-side.
- Ask the agent what it inspected.
- Tell it when not to write code yet.
- Keep each implementation prompt to one task.
- Prefer tests, browser checks, logs, and live smoke tests over vibes.

## Short Opening Prompt

Use this when you want the smallest possible on-camera start.

```text
Read this repository, especially docs/projectbrief.md, and tell me the next sensible step for building this through the Agentic Engineer workflow. Don't edit files yet.
```
