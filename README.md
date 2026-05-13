# BenchmarkCards for Healthcare LLMs

Healthcare LLM benchmarks report accuracy. They rarely report what they assume.

A model that scores 95% on a medical benchmark and 35% when deployed with real patients
is not a flawed model — it is a model evaluated under assumptions that do not hold in
deployment. The gap is not random noise; it traces to specific, documentable assumptions
about who writes the queries, whether interactions are single or multi-turn, and whether
LLM output translates into human action.

This repository introduces **BenchmarkCards**: structured documentation templates that
make these assumptions explicit. The format is adapted from Model Cards and Datasheets,
but targeted specifically at the connection between evaluation conditions and deployment
conditions. The full argument is in our paper:

> **Position: Healthcare LLM Benchmarks Are Necessary but Not Sufficient: The Case for Assumption-Explicit Evaluation**  
> Naveen Raman et al., NeurIPS 2025  
> [arXiv:XXXX.XXXXX]

---

## What a BenchmarkCard looks like

Each card has two halves. Benchmark designers fill the left side once, at publication time.
Practitioners fill the right side when they want to deploy the benchmark's findings in a
specific context.

| Question | Assumption | Answer | Holds at deployment? |
|---|---|---|---|
| What is the intended use case? | — | LLM guidance to clinicians on which tests to run. | Use case: clinicians interact with LLMs iteratively. |
| Who created the examples? | Contextual | Licensing board clinicians and teachers. | Partially. Queries differ from real patient scenarios. |
| Are examples information-complete? | Contextual | Yes, all contain sufficient information. | No. Clinicians must gather information iteratively. |
| Are examples single or multi-turn? | Contextual | Single-shot prompts only. | No. Deployment features multi-turn interactions. |
| Does the benchmark treat LLM output as the final decision? | Consequential | Yes, the LLM decides directly. | No. Physicians retain discretion over diagnosis. |
| What outcome is measured? | Consequential | Accuracy on licensing exam questions. | No. Real outcome is diagnosis on actual patient cases. |

The distinction between **contextual** and **consequential** assumptions matters because
they require different tests. Contextual assumptions (query authorship, interaction format,
information completeness) are testable from interaction data. Consequential assumptions
(decision mediation, outcome validity) require behavioral experiments to quantify.

---

## Cards in this repository

| Benchmark | Contextual assumptions documented | Consequential assumptions documented |
|---|---|---|
| [nature_ai_medical_assistants](cards/nature_ai_medical_assistants.yaml) | ✓ | ✓ |
| [limitations_evaluation_medicine](cards/limitations_evaluation_medicine.yaml) | ✓ | ✓ |

---

## Adding a card

Copy `template.yaml` to `cards/<your_benchmark>.yaml` and fill in the fields. The left
column (benchmark designer half) documents what the benchmark assumes. The right column
(`holds_at_deployment`) is optional at first — it can be filled later by practitioners
assessing fit for a specific deployment.

```bash
cp template.yaml cards/your_benchmark.yaml
# fill in the fields, then open a pull request
```

Cards are validated against `schema.json` on pull request. The required fields are
`benchmark_name`, `citation`, and `intended_use_case.answer`. Everything else is
recommended but not enforced, since incomplete documentation is more useful than none.

---

## Citation

```bibtex
hi
```
