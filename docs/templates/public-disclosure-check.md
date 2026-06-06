# Public Disclosure Check

Use this checklist before publishing public protocol notes, examples, templates, or documentation.

Publishing is an external and hard-to-reverse operation. Treat public documentation as a safety-gated action when it could reveal operational details, internal workflows, sensitive implementation patterns, or private project history.

## Checklist

- No internal repository names, branches, PR numbers, commit hashes, or private file paths are disclosed.
- No database, managed database service, production-like, infrastructure, credential, or environment details are disclosed.
- No concrete internal authorization, privilege, admin, allowlist, bootstrap, or failure-mode behavior is disclosed.
- No raw identity values, raw emails, raw allowlist values, secrets, env values, DB URLs, tokens, cookies, raw sessions, or OAuth codes are disclosed.
- No internal failure history, unresolved risk, operational weakness, or private diagnostic result is disclosed.
- No source excerpts reveal sensitive or identity-like values.
- No example can be traced back to a specific private incident, implementation, PR, commit, date, or project phase.
- Mosaic check: even if each detail is individually abstracted, the combination of details must not allow readers to reconstruct the implementation, timing, scale, target system, or internal operational context.
- The document shares principles, vocabulary, templates, or abstract examples only.
- A separate reviewer or agent should be able to verify this checklist from the published diff.
