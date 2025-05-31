# Concept Model Experiment: Predicting Protein Disorder via Constraint Satisfaction

## Overview

This project demonstrates a **concept-based reasoning** approach to predicting protein disorder by evaluating physical property constraints, rather than relying on statistical learning or black-box models. The method uses curated datasets from DisProt (disordered proteins) and the Protein Data Bank (folded proteins) to test whether **simple, interpretable physical features** can differentiate folded from disordered proteins.

This serves as an experimental prototype for broader validation of **concept models**—a proposed alternative to probabilistic language models for machine reasoning.

https://kevinmesiab.substack.com/p/emergent-concept-modeling-a-paradigm

---

## Objectives

- Validate whether a small set of human-interpretable amino acid features can reliably distinguish folded and disordered proteins.
- Use constraint satisfaction on normalized biochemical properties to emulate first-principles reasoning.
- Demonstrate that **conceptual separability** emerges from feature thresholds without a trained model.

---

## Pipeline Summary

1. **Data Collection**:
    - 100 disordered proteins downloaded from DisProt.
    - PDB chain sequences downloaded from RCSB.

2. **Feature Encoding**:
    - 7 global features per sequence derived from amino acid properties:
        - Normalized hydrophobicity
        - Net charge
        - Hydrogen donor/acceptor sum
        - Relative flexibility
        - Normalized polarity
        - Aromaticity + helix-forming propensity
        - Relative accessible surface area

3. **Threshold Derivation**:
    - Midpoint thresholds computed from DisProt vs. PDB means.

4. **Classification**:
    - Sequences classified as folded if they meet ≥ _k_ of 7 feature thresholds.
    - Performance evaluated as _k_ increases.

---

## Results Summary

| k (min # features) | TP | FN | TN   | FP   | Accuracy |
|--------------------|----|----|------|------|----------|
| 1                  | 70 | 0  | 3048 | 9739 | 24.25%   |
| 4                  | 64 | 6  | 9123 | 3664 | 71.46%   |
| 6                  | 39 | 31 |11645 | 1142 | 90.88%   |
| 7                  | 12 | 58 |12576 |  211 | 97.91%   |

Higher values of _k_ sharply reduce false positives, supporting the hypothesis that constraint satisfaction on physical properties can delineate protein foldability.

---

## Conceptual Contribution

This experiment provides empirical support for **concept-based reasoning models**, where cognition emerges from constraint satisfaction on interpretable, low-dimensional representations—not opaque statistical correlations.

The success of this simple model affirms that **concepts can operate in predictive reasoning tasks** without deep learning or probabilistic fitting.

---

## Requirements

- Python 3.8+
- `requests`, `pandas`, `numpy`, `scikit-learn` (for metrics)

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Running the Notebook

1. Open the notebook in any Jupyter environment.
2. Run all cells sequentially. It will:
    - Download both FASTA datasets
    - Compute features
    - Print classification performance by threshold

---

## License

This project is released under the MIT License. Use, modify, and share freely.

---

## Contact

For questions or collaboration, contact the author or open an issue on the associated repository.
