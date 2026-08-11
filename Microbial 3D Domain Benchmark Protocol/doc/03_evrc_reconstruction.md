# M2. EVRC Three-Dimensional Reconstruction

The EVRC source archive is `tools/EVRC-main.zip`. After extraction, run one chromosome at a time:

```bash
python tools/EVRC-main/evrc.py \
  --intra_chr <single_chromosome_dense_directory> \
  --chr_num 1 \
  -o <output_directory> \
  --seed 29 \
  --thread 10
```

Each input directory in this study contains one chromosome, so `--chr_num 1` is used. Parameters not shown above retain EVRC defaults. Local paths may change, but chromosome count, random seed and thread settings should be recorded with each analysis.

`tools/evrc_reference_wrappers/` retains the yeast and *E. coli* batch wrappers used to document the original invocation. Their old local paths are not required by this protocol. For a new analysis, use the single-chromosome command above or write a local batch loop.

The resulting PDB files are read by `A10t-centroid-distance-local-background-validation.py`. EVRC reconstruction is an input to structural validation, not an independent gold standard.

