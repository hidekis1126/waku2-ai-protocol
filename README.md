# waku2-ai-protocol

A teachable protocol note for human-governed AI collaboration workflows.

> SSE event = notification
> DB state = source of truth

AI workflows should feel alive through streaming events, but they should be trusted through durable state.

`waku2-ai-protocol` is an experimental protocol note for designing AI collaboration workflows that can be paused, reviewed, approved, resumed, audited, and taught.

It starts from a simple idea:

* streaming events are useful for showing progress;
* durable state is necessary for trust;
* human approval should be a first-class part of AI workflows;
* AI collaboration should be explainable enough to teach.

This project is proposed and maintained by **島田 英紀 (`Hideki Shimada`)**, founder of **waku2 / waku2プログラミングスクール**.

---

## Status

**Experimental protocol note.**

This repository is not a production standard, runtime, SDK, SaaS implementation, governance gateway, or billing system.

Version `v0.1.0` is intended to publish a small vocabulary and design direction for human-governed AI collaboration workflows.

---

## Core rule

```txt
SSE event = notification
DB state = source of truth
```

In many AI applications, streaming output makes the system feel alive. However, streaming alone should not be treated as the final truth of the workflow.

In this protocol note:

* **SSE events** are used to notify the user interface about progress, messages, and state transitions.
* **Durable state** such as database records is treated as the source of truth.
* **Approval decisions, artifacts, usage, and final results** should be recorded durably.
* **Human approval gates** should be explicit, inspectable, and resumable.

---

## Why this exists

Many AI tools can generate text, code, plans, designs, and documents. But practical AI collaboration needs more than generation.

It needs a workflow that can answer questions such as:

* What is the AI doing now?
* Which role or agent produced this output?
* What artifact was created?
* Has a human reviewed it?
* Was the workflow approved, rejected, or paused?
* Can the work be resumed later?
* What state should the system trust?
* Can this process be explained to another person?

`waku2-ai-protocol` explores a minimal vocabulary for these questions.

The goal is not to replace existing agent frameworks or UI protocols. The goal is to make human-governed AI collaboration easier to understand, build, review, and teach.

---

## Design principles

### 1. Alive through events, trusted through state

AI workflows should feel responsive through streaming events, but their trusted state should live in durable records.

Events may be missed, duplicated, delayed, or replayed. Durable state should remain the canonical reference.

### 2. Human approval is part of the workflow

Human review should not be treated as an external interruption or an afterthought.

A workflow should be able to reach an `approval_required` state, pause safely, show the relevant context, and resume after a human decision.

### 3. Roles make collaboration teachable

AI collaboration becomes easier to understand when responsibilities are named.

Instead of treating the AI as a single black box, this note uses role names such as `architect`, `coordinator`, and `implementer` as a small educational vocabulary.

### 4. Artifacts should be durable

Outputs such as specifications, drafts, code patches, review notes, slide outlines, and delivery packages should be treated as artifacts.

Artifacts should be reviewable and connected to the workflow state that produced them.

### 5. Usage should be visible

AI workflows often involve cost, credits, rate limits, or provider usage.

This protocol note treats usage events as part of the workflow vocabulary, so users and operators can understand what happened.

---

## Minimal role vocabulary

`waku2-ai-protocol` starts with three basic roles.

### `architect`

The role responsible for understanding the request, shaping the strategy, and proposing the structure of the work.

### `coordinator`

The role responsible for keeping the workflow organized, deciding the next step, and managing transitions between phases.

### `implementer`

The role responsible for producing concrete outputs such as code, documents, plans, or artifacts.

These roles are not fixed identities. They are a teachable vocabulary for explaining AI collaboration.

---

## Minimal event vocabulary

The following event names are a starting point, not a final standard.

```txt
run_started
phase_started
role_message
artifact_created
artifact_updated
usage_recorded
approval_required
approval_decided
run_completed
run_failed
```

### `run_started`

A workflow run has started.

### `phase_started`

A new phase of the workflow has started.

### `role_message`

A role or agent has produced a message.

### `artifact_created`

A new artifact has been created.

### `artifact_updated`

An existing artifact has been updated.

### `usage_recorded`

A usage or cost-related event has been recorded.

### `approval_required`

The workflow has reached a human approval gate and should pause safely.

This is a soft terminal event for the current step. The workflow is not complete, but it should not continue until a human decision is recorded.

### `approval_decided`

A human approval decision has been recorded.

Possible decisions may include `approved`, `rejected`, or `needs_revision`.

### `run_completed`

The workflow run has completed successfully.

### `run_failed`

The workflow run has failed.

---

## Human Approval Gate

A Human Approval Gate is a point where the workflow should stop and ask for human judgment.

Examples:

* before sending an email;
* before publishing a document;
* before charging credits;
* before deploying code;
* before sharing private information;
* before accepting an AI-generated plan as final.

A useful approval gate should show:

* what was produced;
* which role or agent produced it;
* what risks or uncertainties remain;
* what decision is being requested;
* what will happen after approval.

The approval decision should be recorded in durable state.

---

## Suggested state model

This note assumes that a workflow implementation may keep durable records for concepts such as:

```txt
Run
Phase
RoleMessage
Artifact
ApprovalRequest
ApprovalDecision
UsageRecord
```

These names are illustrative. Implementations may use different schemas.

The important point is that final workflow truth should be recoverable from durable state, not from streaming events alone.

---

## What this is not

`waku2-ai-protocol` is not:

* a replacement for AG-UI, MCP, A2A, LangGraph, Temporal, EGAP, or other AI/agent frameworks;
* a production-ready protocol standard;
* a runtime;
* an SDK;
* a SaaS product;
* a billing system;
* a security boundary;
* a guarantee that AI outputs are correct.

It is a small protocol note and vocabulary for human-governed AI collaboration workflows.

---

## Relationship to existing work

This project is intended to be complementary to existing AI and workflow technologies.

* **AG-UI** focuses on the event-based connection between AI agents and user-facing applications. `waku2-ai-protocol` focuses on durable workflow state, human approval gates, and teachable role/state vocabulary.
* **LangGraph** and **Temporal** provide practical approaches for persistence, interrupts, and durable execution. `waku2-ai-protocol` is not a workflow engine; it describes a small vocabulary that can be implemented on top of such systems.
* **EGAP** focuses on governance concerns such as authentication, authorization, audit, approvals, and alerts. `waku2-ai-protocol` is smaller and education-oriented, but it shares the belief that AI agent actions should be governed and auditable.
* **Waku / WAKU2** networking and messaging protocols are unrelated to this project.

`waku2-ai-protocol` focuses on a smaller educational layer: how to describe a human-governed AI collaboration workflow in a way that is understandable, reviewable, and teachable.

A more detailed prior-art note may be added in a future version.

---

## Naming note

This project is named `waku2-ai-protocol`.

It is unrelated to Waku / WAKU2 networking or messaging protocols.

The project name is composed of three parts:

* `waku2`: the waku2 project and related educational work;
* `ai`: AI collaboration workflows;
* `protocol`: a protocol note and vocabulary.

Maintainer:

* **島田 英紀**
* English notation: `Hideki Shimada`

---

## Japan-origin note

`waku2-ai-protocol` is a Japan-origin protocol note shaped by education, small-business practice, software development, and human-centered AI collaboration.

It is written from the belief that AI should not merely automate human work, but help people think, review, learn, decide, and recover their dignity as human beings.

The protocol vocabulary is intentionally small because it should be possible to teach it to non-specialists, students, small teams, and people who are learning how to collaborate with AI.

## 日本語メモ

`waku2-ai-protocol` は、AIに人間の判断を預けきるためのものではありません。
人がAIとともに考え、確かめ、学び、決め、そして人としての尊厳を保ったまま
前に進むための、小さな設計の作法です。

AIの動きはイベントで「見せる」。
信頼してよい状態は、永続的な記録に「残す」。
止まるべきところでは、人の承認を「待つ」。

この語彙をあえて小さく保つのは、専門家でなくても——
学生でも、小さなチームでも、これから学ぶ人でも——
教えられるものであってほしいからです。

---

## Roadmap

Possible future work includes:

* clearer JSON examples;
* sample event payloads;
* approval gate examples;
* artifact lifecycle examples;
* Japanese documentation;
* comparison notes with related protocols and frameworks;
* a small reference implementation;
* SDK or CLI experiments;
* integration with future waku2-gateway work.

No timeline is guaranteed.

---

## Support

This repository is maintained on a best-effort basis.

There is no SLA, no production support guarantee, and no warranty.

Issues and discussions may be opened in the future after the project direction becomes clearer.

---

## License

Apache License 2.0.

Copyright 2026 Hideki Shimada (島田 英紀).

See [LICENSE](./LICENSE).
