[README.md](https://github.com/user-attachments/files/30919248/README.md)
# Microbial 3D Domain Benchmark

Version: 1.1.1  
Last updated: 2026-07-26

This repository provides the modular protocol used to benchmark 13 chromosomal interaction-domain callers across budding yeast and *Escherichia coli*. The benchmark covers Hi-C and Micro-C contact matrices at multiple resolutions and evaluates computational resources, detection coverage, domain-output characteristics, structural validation, structural concordance, biological associations, and context-specific method selection.

The modules can be run independently. This release is not designed as a single-command workflow because the 13 callers and EVRC use different software environments and input formats.

## Modules

| Module | Scope | Documentation |
|---|---|---|
| M1 | Thirteen chromosomal-domain callers | `docs/02_domain_callers.md` |
| M2 | EVRC three-dimensional reconstruction | `docs/03_evrc_reconstruction.md` |
| M3 | Output standardization, hierarchy, resource use, and detection coverage | `docs/04_output_and_resources.md` |
| M4 | Fold-change, EVRC, and coolpup structural validation | `docs/05_structural_validation.md` |
| M5 | Boundary Jaccard, Coverage Jaccard, Consensus F1, MOC, and SSIM | `docs/06_structural_concordance.md` |
| M6 | Gene expression, ATAC-seq, and GO/KEGG analyses | `docs/07_biological_association.md` |
| M7 | Evidence-stratified evaluation and method-selection guide | `docs/08_comprehensive_evaluation.md` |

## Repository Structure

```text
TAD-benchmark-protocol/
|-- README.md
|-- VERSION
|-- RELEASE_NOTES.md
|-- THIRD_PARTY_NOTICE.md
|-- THIRD_PARTY_SOURCES.md
|-- docs/
|-- environment/
|-- examples/
|-- tools/
|   |-- 13-methods.zip
|   |-- EVRC-main.zip
|   |-- runtime_monitor.py
|   `-- evrc_reference_wrappers/
`-- progress/
    |-- 1-TAD-data/
    |-- 1-TAD-level-data/
    |-- 1-balanced-cool/
    |-- 1-EVRC-data/
    |-- 1-coolpup-data/
    |-- 1-expression-data/
    |-- 1-SSIM-data/
    |-- 2-analyse/
    `-- 3-result/
```

`progress/2-analyse/` contains the current analysis scripts used in the study. Relative paths are resolved against the directory structure shown above.

The release includes one representative chromosome for each species. Yeast chromosome `chr1` and *E. coli* chromosome `NC_000913.3` are each represented by five Hi-C resolutions and two Micro-C resolutions. The package also includes the starting inputs required for the gene-expression, reference-annotation, ATAC-seq, and GO/KEGG modules.

The included matrices are analysis-ready inputs used in the benchmark, not unprocessed sequencing reads. All contact matrices used for caller execution and downstream contact-matrix analyses are ICE-balanced. File extensions such as `.cool`, `.hic`, dense matrices, and sparse matrices represent caller-specific input formats rather than different normalization procedures. Complete data sources and upstream-processing boundaries are recorded in `docs/Datas_Table_S2_Data_Sources.tsv`.

FASTQ files, complete caller outputs, hierarchical BED files, EVRC PDB files, coolpup output, SSIM intermediates, and complete statistical result tables are not included.

## Included Callers

The archived caller package contains Armatus, Arrowhead, deDoc, rGMAP, GRiNCH, HiCKey, HiTAD, Matryoshka, OnTAD, SpectralTAD, SuperTAD-fast, TADpole, and TADtree. Their upstream repositories, versions, licenses, and original publications are listed in `THIRD_PARTY_SOURCES.md` and `docs/Datas_Table_S1_Methods_Overview.tsv`.

The third-party archives are distributed for reproducibility and remain subject to their original licenses. Their inclusion does not imply authorship or ownership by this benchmark project. See `THIRD_PARTY_NOTICE.md` before redistributing or modifying them.

## Recommended Execution Order

1. Test the protocol with the representative inputs provided in the release, or prepare new data according to `docs/01_input_layout.md`.
2. Run the required callers independently and convert their outputs to three-column BED-compatible coordinates.
3. Run `3-domain-level.py` to standardize, sort, deduplicate, and assign domain hierarchy.
4. Evaluate resource use, detection coverage, and domain-output characteristics.
5. Run Fold-change, EVRC, and coolpup as separate structural-validation modules.
6. Calculate method concordance only within exactly matched species, assay, resolution, and chromosome conditions.
7. Run expression, ATAC-seq, and functional-enrichment analyses when matched functional data are available.
8. Run the comprehensive evaluation only after the required upstream canonical tables have been generated.

## Basic Environment

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r environment/requirements.txt
```

For Windows PowerShell:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r environment\requirements.txt
```

Each caller and EVRC has its own dependencies. Consult the upstream documentation, `THIRD_PARTY_SOURCES.md`, and `docs/Datas_Supplementary_Protocol_Methods_Detail.docx` before installation.

## Statistical Scope

- Fold-change and EVRC use individual predicted domains as their statistical units.
- coolpup uses a `method + species + assay + resolution + chromosome` pileup as its statistical unit.
- Method concordance is calculated only within exactly matched input conditions.
- Effect direction and statistical significance are evaluated separately. A result is counted as supported only when it has the prespecified effect direction and `BH-FDR < 0.05`.
- Structural validation, method concordance, and biological association are separate evidence categories. They do not replace one another and do not constitute a common biological ground truth.
- The comprehensive evaluation preserves the statistical unit of each metric and does not combine all metrics into a universal accuracy score.

## Path Configuration

Most analysis scripts infer the `progress/` root from their own locations, so the directory structure should be preserved. When inputs are stored elsewhere, modify the input constants in the release copy or use directory links. The EVRC local-background validation script accepts PDB and domain roots through command-line arguments or environment variables.

## Integrity and Provenance

- `docs/script_manifest.tsv` records each script, module, role, primary input, and primary output.
- `docs/included_input_data.tsv` records the 24 included input files, their data roles, species, conditions, sizes, and SHA256 checksums.
- `MANIFEST_SHA256.tsv` records the size and SHA256 checksum of every release file.
- `docs/Datas_Table_S1_Methods_Overview.tsv` records caller versions, parameters, upstream sources, licenses, and publications.
- `docs/Datas_Table_S2_Data_Sources.tsv` records the biological data sources and processing scope.
- `THIRD_PARTY_SOURCES.md` maps the bundled third-party archives to their upstream projects.

To verify a downloaded release, compare the archive SHA256 value with the checksum reported on the GitHub Release page, then use `MANIFEST_SHA256.tsv` to verify the extracted files.

## Scope and Interpretation

This protocol reproduces the benchmark design and evaluation modules used in the associated study. The same framework can be extended to other species, but chromosome naming, reference assemblies, domain terminology, matched functional data, and background construction must be reviewed for each new application.

Fold-change, EVRC, and coolpup provide complementary structural evidence. None of these metrics should be interpreted alone as a gold-standard measure of the biological accuracy of a predicted domain.

## Releases

The complete protocol archive is distributed through GitHub Releases because the compressed package is larger than GitHub's standard per-file repository limit. The source tree may also contain the individual caller archive, which remains below that limit. Release changes are documented in `RELEASE_NOTES.md`.

