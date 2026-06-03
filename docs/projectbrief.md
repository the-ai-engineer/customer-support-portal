# Client Brief: Customer Support Portal

Working product name: Northstar Support

## Course Note

This brief is intentionally written like an early customer brief, not a technical specification.

The goal of the course is to use this brief as the starting point for an AI-assisted software delivery workflow: clarify requirements, write a spec, break the work into tickets, build with AI coding agents, test the result, review the work, and deploy it.

Students should treat this document as raw customer context. It contains the business problem, desired outcomes, provided reference material, and constraints. It does not prescribe the final architecture or implementation details.

## Background

Northstar Outfitters is a fictional e-commerce company that sells travel, home, and lifestyle products online.

The company has grown quickly over the last year. More customers are placing orders, more products are being shipped internationally, and the support team is receiving the same policy questions every day.

The support team already has written policy documents for refunds, shipping, warranties, accounts, and privacy. Those documents are accurate enough for a first version, but customers rarely read them. Instead, they contact support and wait for a person to answer.

## The Problem

Customer support is becoming expensive and slow.

Northstar's support staff spend a lot of time manually answering repetitive questions such as:

- Can I return an opened item?
- How long does shipping take?
- What happens if my order is lost?
- Does the warranty cover accidental damage?
- Can I delete my account?
- Do you store my payment details?

This creates two problems.

First, customers get frustrated because they have to wait for answers to simple questions. Many of these questions could be answered immediately from existing policy documents.

Second, support staff spend too much time on repetitive policy lookups instead of helping customers with complex or sensitive issues.

Northstar wants to explore whether AI can make customer support more effective without replacing the written policies or inventing answers.

## Desired Outcome

Northstar wants a simple customer-facing support portal where a customer can ask a question in natural language and receive a clear answer based on the approved policy documents.

The experience should feel like a helpful online support assistant, not a developer demo.

The system should:

- answer common customer policy questions quickly
- use the provided policy documents as its source of truth
- show which policy document or documents were used
- say when the available documents do not contain the answer
- avoid answering unrelated questions
- help reduce repetitive support contacts
- be deployable so stakeholders can try it in a real browser

The first version does not need to solve every support workflow. It should prove that the company can answer common policy questions automatically and safely from approved documents.

## Provided Reference Documents

Northstar has provided five policy documents:

- `docs/policies/refund-policy.md`
- `docs/policies/shipping-policy.md`
- `docs/policies/warranty-policy.md`
- `docs/policies/account-policy.md`
- `docs/policies/privacy-policy.md`

These documents should be treated as approved business policy for the first version.

The app should not rewrite the policy, silently change the policy, or invent policy details that are not present in the documents.

## Target Users

The primary users are customers who want fast answers before contacting support.

The secondary users are support staff and operations managers who want fewer repetitive tickets and more consistent answers.

## Customer Experience

A customer should be able to open the support portal, type a question, and get a useful answer.

Good example questions include:

- Can I return an opened backpack?
- Can I get a refund for a final sale item?
- How long does standard shipping take to Canada?
- My tracking has not updated for 7 business days. What should I do?
- Does the warranty cover accidental damage?
- Can support tell me my password?
- Can I delete my account and personal data?
- Do you store my full card number?

The answer should be concise and practical. It should be written for a customer, not for an internal engineer.

If the answer uses a policy document, the customer should be able to see which document was used.

## Unsupported Or Unsafe Answers

The support portal should not pretend to know things it cannot know.

For example, it should not claim to have checked:

- live order status
- live courier tracking
- stock availability
- payment history
- a customer's private account details
- internal support systems

If a customer asks for something the policy documents do not answer, the system should say that it cannot answer from the available policy documents and suggest contacting support.

If a customer asks an unrelated question, such as travel recommendations, homework help, or general shopping advice, the system should politely explain that it can only answer questions about Northstar's support policies.

## Business Constraints

Northstar wants the first version to stay focused.

The first version should not include:

- customer login
- live order lookup
- live courier tracking lookup
- payment processing
- ticket creation
- document upload
- admin dashboards
- analytics dashboards
- multi-company support

The company is open to future improvements, but the first version should be small enough to build, test, review, and deploy quickly.

## Implementation Freedom

Northstar is not prescribing a specific technical architecture in this brief.

The build team should decide the appropriate application structure, API shape, model integration, tests, and deployment approach during the specification and planning stages.

The only strong product requirement is that answers must be grounded in the provided policy documents and must not invent policy.

## Success Criteria

Northstar will consider the first version successful if:

- customers can ask policy questions through a web interface
- common questions about refunds, shipping, warranties, accounts, and privacy receive useful answers
- answers clearly show the source policy document or documents used
- unsupported questions receive a safe fallback response
- unrelated questions are politely refused
- the system does not expose secrets or private implementation details to customers
- the app can be run locally by the team
- the app can be deployed and tested through a live URL

## Example Interactions

```text
Customer: Can I return an opened backpack?

Assistant: You can usually return an opened backpack if it was only lightly inspected, is complete and undamaged, and includes its accessories and packaging where possible. If it has already been used on a trip, it would not normally be returnable unless it is faulty.

Sources: refund-policy.md
```

```text
Customer: My tracking has not updated for 7 business days. What should I do?

Assistant: The shipping policy says an order is considered potentially lost when tracking has not updated for 7 business days after dispatch. Contact support with your order number. Support may ask you to confirm the shipping address and check nearby delivery locations before opening a courier investigation.

Sources: shipping-policy.md
```

```text
Customer: Can you recommend a hiking route near Edinburgh?

Assistant: I can only answer questions about Northstar Outfitters support policies. Please ask about refunds, shipping, warranties, accounts, or privacy.

Sources: none
```

