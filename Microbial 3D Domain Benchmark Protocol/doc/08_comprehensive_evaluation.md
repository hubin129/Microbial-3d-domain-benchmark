# M7. Comprehensive Evaluation and Method-Selection Guide

The comprehensive matrix keeps runtime, peak memory, chromosome coverage, Fold-change, EVRC, coolpup, Boundary Jaccard, Coverage Jaccard, Consensus F1, MOC, SSIM and yeast boundary-expression association as separate metrics. Each metric retains its own statistical unit and direction; the metrics are not collapsed into a universal accuracy score.

```bash
python progress/2-analyse/A13-comprehensive-method-recommendation.py
python progress/2-analyse/A13c-method-recommendation-compact-guide.py
```

For each species and metric, methods are ranked in the prespecified direction. Lower runtime and memory are preferred; higher values are preferred for the other metrics. The color score is a within-metric descriptive score. Recommendation strength additionally accounts for valid coverage and a minimum output quantity of 10 domains per valid condition.

The guide first separates hardware conditions at 10 GB peak memory and 1 h runtime, using the recorded *E. coli* resource values as the operational reference. It then separates structural research from yeast boundary-expression or functional research. Structural branches use the three structural-validation metrics and the five concordance metrics; functional branches use yeast boundary-expression association with ATAC-seq and enrichment as supporting evidence.

The main figure shows representative candidates. The canonical recommendation tables retain the complete candidate set and special runtime states. Recommendations are context-specific and must be checked against the target species, assay, resolution and available resources.

