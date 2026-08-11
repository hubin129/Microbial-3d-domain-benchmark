# M6. Biological Association

## Gene Expression

```bash
python progress/2-analyse/A5m-boundary-3bin-gene-level-expression.py
```

For each domain, compare the median TPM of complete genes in the boundary windows with the median TPM of complete genes in the same-domain interior. Boundary windows extend three contact-map bins on either side of each domain boundary. The primary effect is `log2[(boundary median TPM + 1)/(interior median TPM + 1)]`. Yeast and *E. coli* results are analyzed separately.

## ATAC-seq

```bash
python progress/2-analyse/A14-atac-random-background.py
```

The ATAC-seq module uses yeast boundaries and chromosome-matched, one-to-one random centers. Real and random centers are sampled with the same plus or minus 20 contact-map bins. The primary comparison is the mean signal in the two bins adjacent to each center. A result is supported when the boundary-to-random effect is positive and the BH-adjusted P value is below 0.05.

## GO and KEGG Enrichment

The enrichment module uses the fixed global top 10% TPM gene set. For each method-condition, high-expression genes overlapping merged three-bin boundary windows are labeled `Boundary-high`; the remaining high-expression genes are labeled `Nonboundary-high`. Each set is tested against the annotated top 10% background with a one-sided Fisher exact test and BH correction. The main figure is a compact summary; the complete results remain in the canonical tables.

Biological association is a separate evidence category from structural validation and method concordance. It should not be interpreted as a gold-standard label for predicted domains.

