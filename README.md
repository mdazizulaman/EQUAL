# EQUAL: Evaluating Pluralistic Alignment of LLMs Across Educational Perspectives

> Benchmark, evaluation framework, and code for **EQUAL**, a benchmark for pluralistic alignment in the **education** domain.

## Overview

Large Language Models are increasingly used in educational settings such as tutoring, feedback, and instructional support. However, many alignment methods optimize toward a single aggregated notion of human preference, which is a poor fit for education, where legitimate disagreement is common across students, parents, teachers, administrators, and policymakers.

**EQUAL** is a benchmark designed to evaluate how well LLMs represent and navigate this diversity of viewpoints.
<br />

<div align="center">

<table>
  <tr>
    <td align="center">
      <img width="500" alt="Pluralistic alignment example from EQUAL" src="https://github.com/user-attachments/assets/c36c2dc0-157a-4e97-a5c9-dba36841a5e8" />
      <p><strong>A pluralistic alignment example from the EQUAL dataset</strong></p>
    </td>
  </tr>
</table>

</div>

<br />

## Contributions

- **A new benchmark for pluralistic alignment in education.**  
  EQUAL is, to our knowledge, the first benchmark designed to evaluate pluralistic alignment in the education domain across all three established modes: **Overton**, **Steerable**, and **Distributional**.

- **A domain-tailored curation pipeline.**  
  The benchmark is constructed from six sources using a lexicon-based filtering pipeline with contextual disambiguation and human validation, designed to improve education-domain precision.

- **A systematic evaluation across models and methods.**  
  We benchmark nine LLMs, each in aligned and unaligned variants, under four inference strategies: **standard inference**, **pluralistic prompting**, **Mixture of Experts (MoE)**, and **Modular Pluralism (ModPlural)**.

- **Empirical findings on the limits of current methods.**  
  Results show that no single technique dominates across all pluralistic modes: prompting performs best for Overton, standard inference remains competitive for Steerable, and unaligned models best match population-level distributions in Distributional evaluation.


## Dataset Statistics
 
| Alignment Mode | Text | QnA | Total | Avg. Options |
|---|---|---|---|---|
| Overton | 728 | – | 728 | 7.00 |
| Steerable | 5,096 | 660 | 5,756 | 3.03 |
| Distributional | – | 7,786 | 7,786 | 3.71 |
| **Overall** | **5,824** | **8,446** | **14,270** | **3.60** |
 
## Data Sources
 
| Source | Samples | Mode(s) |
|---|---|---|
| [ValueKaleidoscope](https://arxiv.org/pdf/2309.00779) | 5,824 | Overton, Steerable |
| [OpinionQA](https://github.com/tatsu-lab/opinions_qa) | 660 | Steerable |
| [GlobalOpinionQA](https://arxiv.org/abs/2306.16388) | 1,117 | Distributional |
| [Scherrer et al. (2023)](https://arxiv.org/abs/2307.14324) | 160 | Distributional |
| [Scruples](https://github.com/allenai/scruples) | 3,709 | Distributional |
| [PDK Polls](https://pdkpoll.org/) | 2,800 | Steerable, Distributional |


## Dataset Construction

EQUAL is curated through a **domain-tailored lexicon-based filtering pipeline** with **human validation**.

At a high level, the pipeline:

1. collects candidate samples from six public sources,
2. segments raw text into stem/scenario and options when needed,
3. applies **education anchor matching** and **pluralism cue matching**,
4. uses contextual disambiguation to remove false positives caused by polysemous words,
5. validates retained samples with human annotators.

### Lexicon categories

The filtering pipeline uses five lexicon categories:

- **Strong anchors**: unambiguously educational terms (e.g., `student`, `curriculum`, `GPA`)
- **Weak anchors**: potentially educational but ambiguous terms (e.g., `discipline`, `performance`, `dropout`)
- **Context indicators**: terms that confirm educational usage (e.g., `teacher`, `classroom`, `school board`)
- **Pluralism triggers**: terms signaling contested values or disagreement (e.g., `equity`, `religion`, `funding`, `banned books`)
- **Negative guards**: patterns used to filter non-educational noise

## Evaluation Modes

### 1) Overton
Measures how well a response covers the range of value perspectives annotated for a scenario.

- Primary metric: **value coverage percentage** using sentence-level NLI
- Supplementary analyses: human evaluation, judge-model evaluation, variance, and threshold-based coverage

### 2) Steerable
Measures whether the model can generate a response aligned with a specified target perspective or stakeholder condition.

- Primary metrics: **balanced accuracy** and **accuracy**

### 3) Distributional
Measures whether model outputs match real-world preference distributions.

- Primary metric: **Jensen-Shannon Distance (JSD)**
- Supplementary diagnostic: **entropy of predicted answer distributions**

## Models and Methods

EQUAL benchmarks **9 LLMs** across both **aligned** and **unaligned** variants, using four inference-time approaches:

- **Standard Inference/ Vanilla**
- **Pluralistic Prompting**
- **Mixture of Experts (MoE)**
- **ModPlural**

## Main Findings

Across the benchmark, no single method dominates all pluralistic modes.

- **Prompting** performs best on **Overton** coverage on average
- **Standard inference** remains competitive for **Steerable** evaluation
- **Unaligned models** better match population-level distributions in **Distributional** evaluation than aligned counterparts in many cases
- Even the best-performing configurations leave a substantial portion of the educational value space uncovered

## Repository Status

This repository is being prepared for public release. The dataset, code, prompts, and evaluation scripts will be added after anonymization and final cleanup.

Planned contents include:
- dataset release and documentation
- filtering pipeline implementation
- evaluation scripts for Overton / Steerable / Distributional
- prompts and inference templates
- benchmark result tables
- reproduction instructions

## Code Base

Our evaluation code is built upon the work of [Modular Pluralism](https://github.com/BunsenFeng/modular_pluralism) (Feng et al., EMNLP 2024). We adapt their evaluation pipeline for the education domain and extend it with our lexicon-based filtering and domain-specific analysis.

## Release Note

We will release the full EQUAL dataset, together with the complete lexicon-based filtering pipeline and associated code, after acceptance.

## License

License information will be added with the public release.


