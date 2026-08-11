# Output Contracts

| Module | Canonical output directory | Statistical level |
|---|---|---|
| Domain standardization | `progress/1-TAD-level-data/` | Domain |
| Fold-change | `progress/3-result/4-foldchange/` | Domain |
| EVRC | `progress/3-result/evrc_reconstruction_reanalysis/` | Domain |
| coolpup | `progress/3-result/9-coolpup/` | Chromosome-level pileup |
| Boundary Jaccard | `progress/3-result/5-jaccard/` | Matched method pair and condition |
| Coverage Jaccard and MOC | `progress/3-result/6-MOC-coverage/` | Matched method pair and condition |
| Consensus F1 | `progress/3-result/7-consensus/` | Method and condition |
| SSIM | `progress/3-result/8-ssim/` | Method and condition |
| Expression | `progress/3-result/8-expression/` | Paired domains within method-condition |
| ATAC-seq | `progress/3-result/13-atac-random-background/` | Method-condition |
| Recommendation | `progress/3-result/12-comprehensive-recommendation/` | Method and evidence category |

Every canonical table should preserve species, method, assay, resolution, chromosome, statistical unit, valid-object count, exclusion state, effect size, P value and FDR when those fields apply.

