# M1. Chromosomal-Domain Callers

`tools/13-methods.zip` contains the 13 caller archives used in this benchmark: Armatus, Arrowhead, deDoc, rGMAP (referred to as GMAP in the manuscript), GRiNCH, HiCKey, HiTAD, Matryoshka, OnTAD, SpectralTAD, SuperTAD-fast, TADpole and TADtree.

## Execution Principles

1. Run each method independently for every species, assay, resolution and chromosome.
2. Use the parameters documented in `docs/Supplementary_Protocol_Methods_Detail.md`; local path changes must not alter scientific parameters.
3. Preserve completed, zero-output, timeout, OOM and unsupported-input states as separate outcomes.
4. Convert raw outputs to BED-compatible coordinates before downstream analysis.
5. Treat domain count and hierarchy as output features, not as standalone evidence of accuracy.

Upstream addresses, archived versions, licenses and publications are listed in `THIRD_PARTY_SOURCES.md`. Installation and redistribution requirements remain those of the upstream projects.

## Resource Monitoring

```bash
python tools/runtime_monitor.py --output run_metrics.tsv -- <caller command and arguments>
```

The monitor samples parent and descendant RSS every 0.5 s and records wall-clock time, maximum combined RSS and exit code. When a wrapper processes several conditions sequentially, the recorded value describes the complete wrapper run rather than a standardized method-condition runtime.

