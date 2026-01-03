![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Google Colab](https://img.shields.io/badge/Google%20Colab-Compatible-orange)
![SSRN](https://img.shields.io/badge/Paper-SSRN-red)

# High-Confidence Errors in Lightweight Instruction-Tuned Language Models

This repository contains the code and analysis accompanying the paper:

**High-Confidence Errors in Lightweight Instruction-Tuned Language Models**

The project presents an empirical failure analysis of a lightweight, instruction-tuned Large Language Model (LLM), focusing on **high-confidence errors**—cases where the model exhibits strong internal confidence yet produces incorrect outputs.

---

## Overview

Large Language Models are increasingly deployed in decision-support systems, where fluent and confident outputs are often implicitly trusted. However, confidence signals derived from internal model behavior are rarely calibrated against empirical correctness.

This project investigates whether **semantic self-agreement**, measured via agreement across multiple stochastic generations, can serve as a reliable proxy for correctness. Using a controlled and reproducible experimental setup, we demonstrate that **high-confidence errors are prevalent**, even in constrained binary decision tasks.

### Key findings

- Overall accuracy of **55%**
- **44%** of predictions are incorrect despite high semantic confidence
- Weak correlation between confidence and correctness
- Persistent overconfidence across reasoning domains, particularly in economic and logical reasoning

---

## 🚀 Quick Start

To reproduce all results reported in the paper:

1. Open **`High_Confidence_Errors_FLAN_T5.ipynb`** in Google Colab  
2. Install dependencies:
   ```bash
   pip install -r requirements.txt


## Repository Structure

├── High_Confidence_Errors_FLAN_T5.ipynb

├── full_llm_failure_results.csv

├── category_summary.csv

├── requirements.txt

└── README.md


All experiments, analyses, figures, and tables are generated within **a single Google Colab notebook**, organized into clearly labeled cells corresponding to the paper’s methodological steps. The two CSV files are exported directly from the notebook to support transparency and reproducibility.

---

## Dataset

The evaluation dataset consists of **100 binary (Yes/No) questions** curated specifically for this study. Questions and ground-truth labels are **defined directly within the notebook**, eliminating external data dependencies.

The dataset is evenly distributed across four reasoning categories:

- **Factual knowledge** (25)
- **Logical reasoning** (25)
- **Policy-based reasoning** (25)
- **Economic concepts** (25)

Binary questions were selected to minimize ambiguity in correctness evaluation while allowing for plausible distractors that may elicit confident but incorrect responses. Representative examples are provided in **Appendix A** of the accompanying paper.

---

## Methodology Summary

### Model

- **FLAN-T5-Base** (≈250M parameters)
- Open-source, instruction-tuned
- Selected to enable reproducibility on commodity hardware

### Generation

- **7 stochastic generations per question**
- Temperature-based sampling
- First generation used as the final prediction for accuracy evaluation

### Confidence Estimation

Two confidence measures are computed:

1. **Syntactic self-consistency**  
   Exact agreement across generated answers.

2. **Semantic confidence (primary measure)**  
   Mean pairwise cosine similarity between sentence embeddings of generated responses.

An output is classified as a **high-confidence error** if it is incorrect and has a semantic confidence score greater than **0.75**. Full definitions are provided in **Appendix B** of the paper.

---

## Outputs

The notebook produces two primary CSV artifacts:

- **`full_llm_failure_results.csv`**  
  Per-question results, including predicted answers, correctness labels, semantic confidence scores, and failure-type classification.

- **`category_summary.csv`**  
  Aggregated category-level statistics, including accuracy and average semantic confidence for each reasoning domain.

These files correspond directly to the tables reported in the paper and enable independent verification of results.

---

## Evaluation and Analysis

All analyses are performed within the notebook and include:

- Overall accuracy
- Pearson and Spearman correlation between confidence and correctness
- Confidence calibration via binning
- High-confidence error prevalence
- Category-level accuracy and confidence analysis

Figures and tables reported in the manuscript are generated from notebook cells and, where applicable, exported to CSV.

---

## Reproducibility

This project is fully reproducible using a single notebook.

### Environment

- Python ≥ 3.9
- Google Colab recommended
- No proprietary models or datasets required

### Setup

```bash


 ▶️ Execution

To reproduce all results reported in the paper:

1. Open **`High_Confidence_Errors_FLAN_T5.ipynb`** in Google Colab  
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
Run all cells top to bottom

Each notebook section is clearly annotated to correspond directly to sections of the paper.
Key experimental settings are summarized in Appendix C of the manuscript.

📖 Citation

If you use this code or analysis, please cite:
@article{high_confidence_errors_llms,
  title={High-Confidence Errors in Lightweight Instruction-Tuned Language Models},
  author={Ayodele Odugbile},
  journal={SSRN},
  year={2026}
}

📄 License

This repository is released for research and educational use.

📬 Contact

For questions, replication requests, or collaboration inquiries:

Ayodele Odugbile
Email: drolalekan.ayodele@gmail.com

GitHub: https://github.com/odugbile1993

🧠 Final Note

This repository intentionally prioritizes failure-aware evaluation and transparency over benchmark optimization. All reported results are traceable to explicit notebook cells and exported CSV artifacts.



