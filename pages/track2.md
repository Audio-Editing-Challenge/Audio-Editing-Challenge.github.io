---
layout: page
title: Track 2
permalink: /track2/
---

## Track 2: Agent Track

Participants must build an **autonomous audio editing agent** that independently plans and invokes locally deployed open-source models or signal-processing tools, inspects intermediate results, and iteratively refines its output. This track evaluates system-level planning, tool selection, execution, and self-correction.

**Task Scope:** Tasks may use **any MMAE audio modality and any MMAE complexity category**, including single-step, multi-part, multi-instruction, multi-audio, multi-round interaction, and multi-hop tasks. Final evaluation will use the corresponding portion of an organizer-held internal test set. **No human involvement is permitted during inference.**

**Rules and Restrictions:**

1. **Open-source models, tools, and data only.** Every component and data resource must be publicly available under research-permissive terms. The specific versions and weights of **all model components** in the agent system must have been publicly released **before October 1, 2026**. **Closed-source models are prohibited.**
2. **LLM deployment and API access.** Large language models (LLMs) used by the system may be deployed locally or accessed through cloud APIs, provided that the API-served version corresponds to publicly released model weights. Closed-source LLMs are prohibited. **All other models and tools must run locally.**
3. **Reproducibility and auditing.** Teams must provide model versions, links to model weights, and evidence of their public release dates, along with deployment and API invocation configurations and execution logs. Finalists must also provide runnable code, environment specifications, prompts, tool-call records, intermediate artifacts, random seeds, runtimes, and final outputs for audit.
4. **No human-in-the-loop.** Inference-time human assistance, output selection, and manual curation or post-processing are strictly prohibited.
5. **Common resource envelope.** All final submissions will follow the same announced limits on compute, runtime, storage, and tool calls within this track.

## Baseline

See the [official baselines and code](../#baselines) on the challenge homepage.
