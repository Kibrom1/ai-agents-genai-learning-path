# Chapter 14: Security Review

*Phase 5 — Production Hardening & Review*
## What you need to know

**Prompt injection via ingested documents is the most likely real-world attack surface for this system.** Any document your pipeline ingests from an untrusted source (a vendor upload, an inbound email) could contain text engineered to manipulate the agent — re-check the defenses from Chapter 10 specifically against the documents this system actually processes, not just synthetic test cases.

**Tool-call exfiltration risk**: if any tool in your pipeline can send data externally (an email, an API call, a webhook), consider whether a manipulated agent could be tricked into using it to leak data. The mitigation is usually an allowlist of what a tool can target (not an arbitrary destination the model supplies) plus never letting untrusted document content alone trigger a side-effecting tool call.

**PII handling in extracted data**: know what sensitive fields your extraction pipeline touches (names, account numbers, addresses) and whether your logging (Chapter 11's audit trail) is storing more of that raw content than it needs to. Logs that capture full raw documents "just in case" are a liability — log what's needed to debug and audit, not everything.

## Do

Audit both capstones against the OWASP LLM Top 10 categories, focusing specifically on: prompt injection (via ingested documents), excessive agency (can a tool call cause unintended side effects), and sensitive information disclosure (in logs, in error messages, in model outputs).

## Deliverable

A security checklist covering each relevant OWASP category, with findings and fixes (or an explicit "not applicable, because..." for categories that don't apply to this system).

## Insurance Claims Example
Claims files routinely contain sensitive data — medical information on bodily-injury claims, financial details, addresses, sometimes SSNs on older intake forms. Audit what your extraction and logging pipeline actually captures and stores: does your audit log (Ch. 11) retain full raw medical narratives when it only needs a reference ID? And since claims documents come from claimants and third parties — genuinely external, sometimes adversarial input — re-check the prompt-injection defenses from Chapter 10 specifically against real document types in your pipeline (a scanned letter, an emailed estimate) rather than only synthetic test cases.


## Resources
- [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- [OWASP GenAI LLM Top 10 (2026)](https://genai.owasp.org/resource/owasp-genai-llm-top-10-2026/)
- [LLM Prompt Injection Prevention — OWASP Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html)
