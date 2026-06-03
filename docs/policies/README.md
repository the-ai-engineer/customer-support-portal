# Starter Policy Documents

These are the policy documents for the Agentic Engineer customer support Q&A course project.

They describe a fictional e-commerce store called Northstar Outfitters. The company sells everyday travel, home, and lifestyle products online. The store is deliberately ordinary: students should not need domain expertise to understand the policies or ask useful questions.

In the starter application repo, copy these files into:

```text
docs/policies/
```

The V1 app should load these markdown files and answer customer questions using only their contents. This keeps the project simple and avoids turning Agentic Engineer into a production RAG course.

## Files

- `refund-policy.md`: returns, exchanges, store credit, refund timing, return shipping, and edge cases.
- `shipping-policy.md`: processing times, delivery regions, shipping speeds, tracking, lost packages, address changes, and split shipments.
- `warranty-policy.md`: warranty length, covered defects, exclusions, claim evidence, remedies, and refurbished replacements.
- `account-policy.md`: account creation, password resets, guest checkout, order history, saved addresses, deletion, and support identity checks.
- `privacy-policy.md`: collected data, payment data, service providers, retention, deletion requests, marketing preferences, and security.

## Teaching Notes

These docs are intentionally more detailed than tiny demo snippets, but still small enough to send directly in a prompt. They are good starter material for:

- document loading tests
- source attribution tests
- unsupported-answer behaviour
- off-topic refusal behaviour
- frontend source display
- live smoke checks after deployment

The docs include overlapping topics on purpose. For example, a question about a faulty returned item may involve both `refund-policy.md` and `warranty-policy.md`. A question about account deletion may involve both `account-policy.md` and `privacy-policy.md`.

Students should not edit these policy files during the first implementation tasks unless the lesson explicitly asks them to. Treat them as approved business documents.

## Example Questions

- Can I return an opened item?
- How long does standard shipping take to Canada?
- My order tracking has not updated for a week. What should I do?
- What does the warranty cover?
- Can I delete my account and all my data?
- Do you store my full card number?
- Can I get a refund for a final sale item?
- Can support tell me my password?
