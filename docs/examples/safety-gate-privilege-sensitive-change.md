# Example: Safety Gate for a Privilege-Sensitive Change

A privilege-sensitive change can require Safety Gate review regardless of its apparent size.

## Scenario

An AI proposes changing how a system behaves when a dependency or internal decision path fails.

When behavior affects access, privilege, denial, escalation, or recovery semantics, the review lane should be determined by meaning, reversibility, blast radius, and auditability rather than apparent size.

## Derived lane

Safety Gate Lane

## Why

- privilege-sensitive behavior
- access-control related semantics
- high blast radius if incorrect
- failure-mode behavior may affect whether access is granted, denied, or escalated
- requires explicit review
- requires externally auditable evidence

## Public lesson

Measure risk by meaning, reversibility, blast radius, and auditability, not by line count.

A large documentation change can be easy to audit.
A privilege-sensitive change can require Safety Gate review.
