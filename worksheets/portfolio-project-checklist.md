# Portfolio Project Checklist (Appendix K)

*Blank template from* How to Become an AI Engineer *(First Edition) by Mikaël Meyer, MSc. — posted on the book's online companion for the reader's personal use (see the book's copyright page).*

This appendix is Chapter 23 in checklist form: the three principal projects, the variations, and the presentation standards, reduced to the boxes a finished project must be able to tick. Work a project down its list in order — the order is the chapter's: problem, architecture, implementation, evaluation, security, deployment, documentation, and how you will talk about it.

One sentence of Chapter 23 governs everything below, and it is repeated here so the checklists cannot be misread as a promise: **a strong portfolio does not guarantee a job, an interview, or an offer.** Hiring depends on timing, budgets, teams, and factors no candidate controls. What a checked-off portfolio does is remove the avoidable reason for rejection — the reviewer who cannot tell what you built, why, and whether it worked.

## Before you start: the reviewer's four questions

Every project, principal or variation, must be able to answer all four, in its README, within a reviewer's first two minutes:

- [ ] What problem does it solve, and for whom — stated plainly, including what a wrong answer costs the user?
- [ ] What did you actually build — as opposed to configure, assemble from a framework demo, or follow from a tutorial?
- [ ] How do you know it works — where is the evaluation?
- [ ] What went wrong, and what did you do about it — named specifically, not gestured at?

## Project 1 — Production RAG application

**Problem and corpus**

- [ ] Corpus chosen with real texture (policy documents, support documentation, research papers, contracts) — not a clean toy set
- [ ] The user stated plainly: who asks, what they ask, what a wrong answer costs them

**Architecture and implementation**

- [ ] Ingestion half built: documents split into chunks, converted to embeddings, stored in a searchable index with source text and metadata
- [ ] Query half built: question → retrieve relevant chunks → assemble grounded prompt → generate answer → return it with citations to the sources used
- [ ] Every generated citation verified against the retrieved source before the answer is presented
- [ ] Chunk size and overlap decided by testing an alternative, and the reasoning recorded
- [ ] Embedding approach chosen against at least one compared alternative
- [ ] Number of chunks retrieved decided and recorded
- [ ] Prompt instructs the model to answer only from the retrieved material — and to say so when the material does not contain the answer

**Evaluation**

- [ ] Evaluation set built: a few dozen questions with known answers and known source passages
- [ ] Retrieval measured separately: does retrieval find the right passages?
- [ ] Generation measured separately: does the answer stay faithful to the retrieved passages?
- [ ] Results reported including the failures — no flawless-answer claims
- [ ] At least one concrete improvement made because the evaluation exposed a weakness (a chunking change, a metadata filter, a re-ranking step), and documented

**Security**

- [ ] Retrieved content treated as data, never as commands — the indirect prompt injection case addressed explicitly
- [ ] If the corpus mixes sensitivity levels: access enforced so no user receives an answer grounded in a document they could not open themselves
- [ ] What the system logs — and what it must not log — written down

**Deployment and documentation**

- [ ] Deployed somewhere reachable (a small cloud instance or managed hosting), behind a simple interface
- [ ] Corpus rebuildable from a script, not by hand
- [ ] A reviewer can run the evaluation with one command
- [ ] Interview answers ready for the decisions: why this chunking, what the evaluation caught, how the system behaves when the answer is not in the corpus

## Project 2 — AI agent with evaluation, safety, and monitoring

**Problem and scope**

- [ ] Task chosen where agency is genuinely needed and the stakes are bounded (triaging and drafting, researching across provided sources into a structured brief, flagging data anomalies for review)
- [ ] No agent that spends money, sends messages, or modifies records without approval
- [ ] Judgement recorded: where a simpler script would have done the job — and if part of the task turned out not to need a model at all, that conclusion stated

**Architecture and implementation**

- [ ] The loop described honestly: how the goal is represented, how the model plans, which tools it may call, how results return to the context
- [ ] A stopping rule exists: a completion condition, a step limit, a budget limit
- [ ] Toolset small and typed, with explicit input and output schemas, so malformed calls fail loudly

**Evaluation**

- [ ] Task-level success criteria defined in advance: the output contains these elements, cites these sources, never performs this forbidden action
- [ ] A fixed set of scenarios run repeatedly — one successful run of a stochastic system demonstrates little
- [ ] Failures logged by type: planning errors, tool misuse, premature stopping, loops
- [ ] Scenario results presented as a table, with the failure taxonomy

**Safety and monitoring**

- [ ] Least privilege applied: each tool can do only what the task requires
- [ ] Human approval step in front of any consequential or irreversible action — and the approval shows the reviewer exactly what will happen
- [ ] Execution sandboxed where code or queries run
- [ ] Structured logs of every step and tool call; traces a human can replay
- [ ] Running totals of cost and latency per task, with alerts or hard stops when a run exceeds its budget
- [ ] One incident from your own testing written up — a loop, a runaway cost, a near-miss on a forbidden action — and the control added because of it

**Deployment and documentation**

- [ ] Runs as a scheduled or on-demand service with the monitoring visible (log files and a simple dashboard are enough)
- [ ] Interview lead prepared: the controls — approval gates, budgets, evaluation scenarios — before the capabilities

## Project 3 — ML/LLM optimisation

**Problem and baseline**

- [ ] A working baseline system chosen (an inference pipeline, a fine-tuned small model, a RAG system's generation step)
- [ ] The constraint defined concretely: a latency target, a cost ceiling per thousand requests, or a memory limit — never "make it faster"

**Method and implementation**

- [ ] Benchmarking harness built first: a fixed workload, a fixed evaluation set, repeatable timing and cost measurement
- [ ] Techniques applied one at a time, re-measuring after each: quantisation; a smaller or distilled model for part of the workload; caching repeated or prefix-shared computation; routing easy requests to a cheaper model and hard ones to a stronger one; batching; trimming prompt and context length where the evaluation shows the material was not earning its tokens

**Evaluation and the trade-off table**

- [ ] The deliverable table exists: configuration × quality score on the evaluation set × latency × cost × memory — the baseline row and each technique's row, measured identically
- [ ] At least one technique that did not help, or that bought speed at an unacceptable quality price, reported as measured

**Security, deployment, and documentation**

- [ ] The applicable security dimension addressed: where data flows when a smaller model runs at the edge; cache keys that cannot leak one user's context into another's; a distilled model's inherited failure modes
- [ ] Optimised configuration deployed beside the baseline where possible, so the comparison stays reproducible
- [ ] Harness documented well enough for a reviewer to re-run it and get your numbers, within reason
- [ ] Interview language prepared in trade-offs, never triumphs: what it costs, what it saved, what quality did on this evaluation — and the table to prove it

## Variations on the pattern

Adapt at least one slot to the work you actually want, keeping the pattern's skeleton — a real problem, decisions you can defend, an evaluation with numbers, a security consideration, and a write-up that admits what failed:

- [ ] **Document intelligence** — structured data extracted from invoices, forms, or reports; follows the RAG project's shape, with extraction accuracy as its evaluation
- [ ] **Enterprise assistant** — retrieval combined with the agent project's tool use and approval gates, aimed at internal workflows
- [ ] **Data pipeline** — ingestion, validation, enrichment with model calls, monitoring for drift: the unglamorous engineering production AI stands on
- [ ] **Multimodal** — image or audio input added to any of the above, with the new modality evaluated separately
- [ ] **Cloud-hosted variant** — an existing project re-platformed onto managed services: infrastructure defined in code, cost tracking, access control done properly

## Presenting the work: standards for every project

**The README**

- [ ] Opens with the problem in two sentences
- [ ] Architecture in one diagram or short section
- [ ] How to run it
- [ ] The evaluation and its results
- [ ] Limitations stated unprompted
- [ ] Text stands alone without screenshots or a recorded demonstration (they may help; they may not carry the evidence)

**GitHub hygiene**

- [ ] Commit history shows the project evolving — not a single upload the night before
- [ ] The repositories that represent you are pinned
- [ ] Tutorial exercises archived or clearly labelled, so they are not mistaken for principal work
- [ ] No credentials and no data in the repository
- [ ] A licence and a requirements file included, so the work is runnable

**Demo discipline**

- [ ] The failure case rehearsed as well as the success case: the question the corpus cannot answer, the scenario the agent escalates to a human
- [ ] Graceful refusal and escalation demonstrated unprompted
- [ ] No recording ever presented as live output
- [ ] No guided tutorial build ever presented as an original system

## The final consistency check

Before applying anywhere, read the three views of your evidence in one sitting, as a stranger would:

- [ ] Portfolio, resume, and LinkedIn tell the same story, in substance, word for word where they overlap
- [ ] Every credential is listed as exactly what it is — a course completion as a completion, a proctored certification as a certification (Chapter 23's integrity test)
- [ ] Every skill listed is one you can discuss for ten minutes under questioning
- [ ] Every exaggeration found has been removed — because one caught inflation discounts everything else on the page
