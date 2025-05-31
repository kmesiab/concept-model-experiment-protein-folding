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
- Compare threshold-based and logistic regression approaches to feature-based classification.

---

## Pipeline Summary

1. **Data Collection**:
    - 25,000 disordered proteins downloaded from DisProt API.
    - 15,000 PDB chain sequences downloaded from RCSB's HTTPS mirror.

2. **Feature Encoding**:
    - 7 global features per sequence derived from amino acid properties:
        - Normalized hydrophobicity
        - Net charge
        - Hydrogen donor/acceptor sum
        - Relative flexibility
        - Normalized polarity
        - Aromaticity + helix-forming propensity
        - Relative accessible surface area

3. **Classification Approaches**:
    a) **Threshold-Based**:
        - Midpoint thresholds computed from DisProt vs. PDB means
        - Sequences classified as folded if they meet ≥ _k_ of 7 feature thresholds
    
    b) **Logistic Regression**:
        - Standardized features used to train a logistic classifier
        - Learned weights provide interpretable feature importance
        - Probability threshold optimized for balanced performance

---

## Results Summary

### Threshold-Based Classification

| k (min # features) | TP   | FN   | TN    | FP    | Accuracy |
|--------------------|------|------|-------|-------|----------|
| 1                  | 14844| 156  | 3116  | 9671  | 64.63%   |
| 2                  | 14352| 648  | 6381  | 6406  | 74.61%   |
| 3                  | 13540| 1460 | 8143  | 4644  | 78.03%   |
| 4                  | 12615| 2385 | 9485  | 3302  | 79.53%   |
| 5                  | 11090| 3910 | 10689 | 2098  | 78.38%   |
| 6                  | 8258 | 6742 | 11669 | 1118  | 71.71%   |
| 7                  | 2679 | 12321| 12591 | 196   | 54.95%   |

### Logistic Regression Results

The logistic regression model achieved optimal performance with a threshold of 0.02:

- **Feature Weights**:
  - Hydrophobicity: +1.164
  - Charge: +1.857
  - H-bond capacity: +3.499
  - Flexibility: -1.849
  - Polarity: -0.910
  - Aromatic+Helix: +2.029
  - Surface area: -0.315

- **Performance at threshold = 0.02**:
  - Accuracy: 81%
  - Precision (DisProt): 100%
  - Recall (DisProt): 81%
  - F1-score (DisProt): 89%

---

## Key Insights

1. **Feature Importance**: The logistic regression weights reveal that hydrogen bonding capacity and aromatic+helix propensity are the strongest predictors of protein disorder.

2. **Threshold Selection**: Both approaches show that moderate thresholds (k=4 for threshold-based, p=0.02 for logistic) provide optimal balance between accuracy and coverage.

3. **Conceptual Validation**: The success of both simple threshold-based and logistic approaches supports the hypothesis that protein disorder can be predicted through interpretable physical properties.

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
    - Train and evaluate both classification approaches
    - Print detailed performance metrics

---

## License

This project is released under the MIT License. Use, modify, and share freely.

---

## Contact

For questions or collaboration, contact the author or open an issue on the associated repository.
