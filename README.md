# ContractGraph
### A Contract-Guided Graph Reasoning Framework for Reliable Agentic Software Engineering

**Tagline:** Build Smarter. Code Better.

## Overview
ContractGraph is a proposed research framework for helping AI coding agents understand software repositories, plan changes against explicit task requirements, modify code, and verify the result with tests.

It combines four ideas:
1. **Repository graphs** — represent code entities and relationships such as imports, calls, definitions, and dependencies.
2. **Task contracts** — convert a natural-language request into explicit requirements, constraints, and acceptance checks.
3. **Specialized agent roles** — divide repository analysis, planning, implementation, testing, and verification into focused stages.
4. **Evidence-based verification** — use test outcomes and contract checks to assess whether a proposed patch satisfies the task.

> **Research status:** This document describes the proposed framework and experimental plan. It does not claim that the full system has been implemented or that performance improvements have been measured.

## Problem
Coding agents can produce plausible patches while misunderstanding repository structure, missing hidden dependencies, violating task constraints, or introducing regressions. Long textual context alone may not reliably expose the relationships needed to make safe repository-level changes.

## Proposed approach
1. Parse the task description and build a structured task contract.
2. Inspect the target repository and construct a graph of relevant code entities and relationships.
3. Retrieve graph-linked context for the task.
4. Plan a patch that maps each contract requirement to relevant files and symbols.
5. Generate and apply a candidate change.
6. Run available tests and contract-oriented checks.
7. Report which requirements are supported by evidence, which checks failed, and what remains uncertain.

## Architecture
- **Contract Builder:** extracts requirements, constraints, and acceptance criteria.
- **Repository Graph Engine:** extracts symbols and relationships from source code.
- **Graph Reasoner:** identifies relevant nodes, edges, and dependency paths.
- **Planner:** creates a requirement-to-code change plan.
- **Code Engineer:** proposes the patch.
- **Test Engineer:** selects and runs relevant tests.
- **Verification Agent:** compares test evidence and patch behavior against the contract.

The roles may be implemented as separate agents or as staged calls to one model. The experiment should compare these choices rather than assume multi-agent execution is automatically better.

## Gemma 4 integration
Gemma 4 is the proposed foundation model for task interpretation, reasoning, planning, code generation, and failure analysis. The framework is model-assisted: graph extraction, contract validation, test execution, and evidence collection should use deterministic tools where practical.

## Research questions
- Does contract-guided planning improve task and patch correctness?
- Does graph-aware context improve repository understanding compared with text-only context?
- Which components contribute most to performance?
- What are the trade-offs in runtime, token use, and test execution cost?

## Experimental plan
### Baselines
1. Gemma 4 coding agent with ordinary repository context.
2. Baseline plus graph-derived repository context.
3. Baseline plus structured task contracts.
4. Full ContractGraph workflow.

### Ablations
Remove graph context, contract planning, specialized roles, and verification one at a time. Keep task splits, model settings, and evaluation procedures consistent.

### Metrics
- Pass@1 / task completion rate
- Test pass rate
- Patch correctness and contract compliance
- Regression rate
- Token consumption
- Execution time

Report sample sizes, failures, timeouts, and uncertainty. Do not present expected outcomes as measured results.

## Proposed technology
Python, Gemma 4, PyTorch, AST-based source analysis, NetworkX or an equivalent graph representation, repository tooling, and an automated test harness. Exact implementation choices should be documented in the experiment notebook.

## Reproducibility checklist
- Record model identifier and inference settings.
- Record dataset/task split and repository base commits.
- Version graph extraction and contract schemas.
- Save prompts, generated patches, test logs, and evaluation outputs.
- Use the same evaluation protocol for all baselines and ablations.
- Clearly distinguish successful runs, failures, and missing measurements.

## Current status
**Proposal / research design.** Implementation details, experimental results, and conclusions must be updated only after the corresponding work has actually been completed.

## Research direction
ContractGraph investigates whether combining explicit task contracts with repository-graph reasoning and test-backed verification can make agentic software engineering more reliable and measurable.
