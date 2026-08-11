# M5. Structural Concordance Between Callers

All comparisons must be restricted to an exactly matched `species + data type + resolution + chromosome` unit and require at least two methods with valid output.

```bash
python progress/2-analyse/A2b-jaccard-exact-same-condition.py
python progress/2-analyse/A3b-moc-coverage-same-condition.py
python progress/2-analyse/A4b-consensus-exact-same-condition.py
python progress/2-analyse/A8c-ssim-same-condition.py
python progress/2-analyse/A12-structure-robustness-fair-same-condition.py
```

- Boundary Jaccard compares exact boundary coordinates without positional tolerance.
- Coverage Jaccard compares the merged domain-coverage intervals from each method.
- Consensus F1 compares one method with the strict-majority consensus boundary set.
- MOC retains individual domain identities and evaluates interval correspondence.
- SSIM compares the overall morphology of domain-hierarchy occupancy matrices.

These metrics describe relationships among caller outputs. They are not independent structural validation and cannot replace biological accuracy. Cross-species summaries should retain the number of valid comparison units and the coverage for each species.

