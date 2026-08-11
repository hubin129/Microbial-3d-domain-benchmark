# 主要输出契约

| 模块 | 主要输出目录 | 关键统计单位 |
|---|---|---|
| 资源 | `progress/3-result/0-runtime-memory/` | method wrapper run |
| 覆盖 | `progress/3-result/0-tad-result-overview/` | chromosome-condition |
| 输出特征 | `progress/3-result/3-level/A1c-size-level-overview/` | domain和condition |
| Fold-change | `progress/3-result/4-foldchange/foldchange_reanalysis_exact_condition/` | domain |
| EVRC | `progress/3-result/evrc_reconstruction_reanalysis/` | domain |
| coolpup | `progress/3-result/9-coolpup/A9d-coolpup-chromosome-domain-structure-validation/` | chromosome pileup |
| 一致性 | `progress/3-result/structure_robustness_fair_same_condition/`及各单项目录 | matched condition和method pair |
| 表达 | `progress/3-result/8-expression/boundary_3bin_expression_by_method/` | domain及method-condition |
| ATAC | `progress/3-result/13-atac-random-background/` | boundary center及method-condition |
| 富集 | `progress/3-result/8-expression/by4741_global_top10_boundary_high_gene_go_kegg_enrichment/` | method-condition-side-term |
| 综合评价 | `progress/3-result/12-comprehensive-recommendation/` | method-evidence category |

每张论文图使用的数据应从这些canonical输出同步到论文数据归档目录。同步时需核对SHA256、行列数和关键统计量。
