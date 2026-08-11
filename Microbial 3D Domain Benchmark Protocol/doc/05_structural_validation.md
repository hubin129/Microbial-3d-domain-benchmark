# M4. Structural Validation

The three structural-validation modules answer different questions and must be run and interpreted separately.

## Fold-change

```bash
python progress/2-analyse/A4x-foldchange-reanalysis-exact-condition.py
```

This module compares contact values inside each predicted domain with a local outside-domain background. For level 1 domains, the background is the interval between the nearest same-level domains or the chromosome flank. For nested domains, the background is first constructed within the nearest parent domain. A domain is counted as supported when `log2FC > 0` and the exact condition unit has `BH-FDR < 0.05`.

## EVRC Local-background Compactness

```bash
python progress/2-analyse/A10t-centroid-distance-local-background-validation.py \
  --n-random 1000 \
  --evrc-pdb-root <PDB_ROOT> \
  --tad-root progress/1-TAD-level-data

python progress/2-analyse/A10u-merge-local-background-sensitivity.py
```

Domains must cover at least four reconstructed bins. The main analysis uses 1,000 unique random sets. Sensitivity analyses can use 50, 100, 200, 500 and 1,000 draws. A domain is counted as supported when `EVRC score > 0` and `BH-FDR < 0.05`.

## coolpup Aggregate Contact Morphology

Use coolpup.py v1.1.0 to rescale each domain to a 99 x 99 grid and aggregate domains by chromosome:

```bash
coolpup.py <matrix.cool> <domains.bed> \
  --local --rescale --rescale_size 99 \
  --outname <output.clpy>
```

Consult `coolpup.py --help` for version-specific options. After `.clpy` files are generated, run:

```bash
python progress/2-analyse/A9d-coolpup-chromosome-domain-structure-validation.py
python progress/2-analyse/A9e-coolpup-chromosome-domain-structure-figures.py
python progress/2-analyse/A9f-coolpup-method-share-figure.py
```

A pileup is supported when the center block has a positive effect relative to adjacent cross-boundary blocks and the exactly matched condition has `BH-FDR < 0.05`. The statistical unit is a chromosome-level aggregate matrix, not an individual domain.

