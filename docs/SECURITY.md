# Security

Baseline security guardrails for projects using this blueprint.
This is a **one-pager** meant to prevent common “agent gotchas”.

## Non-negotiables

- **Secrets never enter the repo.**
  - No API keys, tokens, private URLs, customer data, or credentials in code, docs, examples, or tests.
  - Do not log secrets.
- **Server enforces trust.**
  - Authn/authz, validation, and side effects are enforced server-side.
  - Never rely on client-only checks for access control.
- **Treat all external input as untrusted.**
  - User input, third-party APIs, file uploads, and web content.
  - Validate and constrain inputs; prefer allowlists for risky surfaces.
- **No surprise dependencies.** Dependency changes are approval-gated.

## Threat model quick pass (when touching auth/data)

Answer in 1–2 minutes:

- What are the entry points? (routes, forms, webhooks, APIs)
- What’s the trust boundary? (public internet vs authenticated vs internal)
- What is the sensitive data? (PII, tokens, payment data)
- What is the worst plausible abuse? (data exfiltration, privilege escalation, spam)

If the answer is unclear, stop and ask.

## Common pitfalls to avoid

- Logging request bodies or tokens.
- Storing secrets in client-side bundles.
- Implicit admin actions (missing authz checks).
- Overly-permissive CORS / route handlers.
- Accepting arbitrary URLs/content without validation.

## Checkpoint security checklist

Use this when a change touches auth, data, or external input:

- [ ] Authn/authz checks happen server-side.
- [ ] Input validation exists at the boundary.
- [ ] Sensitive data is not logged or exposed to the client.
- [ ] Error messages do not leak secrets.
- [ ] Dependency changes (if any) were explicitly approved.

## References

- Reliability guardrails: `docs/RELIABILITY.md`
- Architecture map: `ARCHITECTURE.md`
