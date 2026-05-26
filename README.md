# BenchmarkCards for LLMs
This repository introduces **BenchmarkCards**, a structured documentation templates that make these assumptions explicit. 
The format is adapted from Model Cards and Datasheets,but targeted specifically at the connection between evaluation conditions and deployment
conditions. 

The full argument is in our paper:

> **Healthcare LLM Benchmarks Are Necessary but Not Sufficient: The Case for Assumption-Explicit Evaluation**  
> [ArXiv link](https://arxiv.org/abs/2605.22612) 

---

## What a BenchmarkCard looks like

Each card consists of two parts. 
One part is for the Benchmark designer, with information on the assumptions separating evaluation and deployment. 
The other part is for practitioners, who identify whether the assumptions hold true in reality. 
We show an example below: 

| Question | Assumption | Answer | Holds at deployment? |
|---|---|---|---|
| What is the intended use case? | — | LLM guidance to clinicians on which tests to run. | Use case: clinicians interact with LLMs iteratively. |
| Who created the examples? | Task | Licensing board clinicians and teachers. | Partially. Queries differ from real patient scenarios. |
| Are examples information-complete? | Task | Yes, all contain sufficient information. | No. Clinicians must gather information iteratively. |
| Are examples single or multi-turn? | Task | Single-shot prompts only. | No. Deployment features multi-turn interactions. |
| Does the benchmark treat LLM output as the final decision? | Outcome | Yes, the LLM decides directly. | No. Physicians retain discretion over diagnosis. |
| What outcome is measured? | Outcome | Accuracy on licensing exam questions. | No. Real outcome is diagnosis on actual patient cases. |

The assumptions are split into two parts: **task** and **outcome**. 
Task assumptions, such as interaction format and query authorship, can be addressed through modifications to benchmarks.
Outcome assumptions, such as decision mediation and outcome validity, require behavioral experiments. 
The two types of assumptions make clear which gaps can be bridged from benchmarks alone and which requires additional real-world experiments. 

## Filling out a Card

To fill out a card, copy `template.yaml` and fill in the fields. 
The "Holds at Deployment?" field should be filled out by practitioners, while the remaining fields should be completed by benchmark designers. 
---

## Cards in this repository

| Benchmark | Location |
|---|---|
| [Bean et al. 2026](https://www.nature.com/articles/s41591-025-04074-y) | `cards/bean2026.yaml`|
| [Hager et al. 2024](https://www.nature.com/articles/s41591-024-03097-1) |`cards/hager2024.yaml`|
| [HealthBench](https://openai.com/index/healthbench/) |`cards/healthbench.yaml`|
---

## Citation

```bibtex
@article{raman2026healthcare,
  title={Healthcare LLM Benchmarks Are Only as Good as Their Explicit Assumptions},
  author={Raman, Naveen and Cortes-Gomez, Santiago and Rubio, Mateo Dulce and Fang, Fei and Wilder, Bryan},
  journal={arXiv preprint arXiv:2605.22612},
  year={2026}
}
```
