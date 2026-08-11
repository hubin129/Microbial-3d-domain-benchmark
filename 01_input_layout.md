# 输入目录与命名规范

## 发布包内示例数据

版本1.1.0提供每个物种一条染色体的分析起始输入：

- 酵母`chr1`：Hi-C 500、1,000、2,000、5,000和10,000 bp，Micro-C 200和500 bp。
- 大肠杆菌`NC_000913.3`：Hi-C 500、1,000、2,000、5,000和10,000 bp，Micro-C 200和500 bp。
- 表达模块：两物种表达表和对应参考GFF。
- 酵母功能模块：ATAC-seq bigWig、GO注释和KEGG映射。

上述文件是本研究实际使用的分析起始数据。未经处理的FASTQ不在本Protocol范围内。caller输出、层级结构域、EVRC重构、coolpup、SSIM及统计结果应由相应模块生成，不作为输入数据重复打包。

完整文件清单及逐文件SHA256见`docs/included_input_data.tsv`。

## 接触矩阵

将平衡后的`.cool`文件放在：

```text
progress/1-balanced-cool/<species>/<data_type>/<resolution>/<chrom>.cool
```

本研究物种名为`BY4741`和`E.coli`，数据类型为`HiC`和`Micro-C`。酵母染色体使用`chr1`至`chr16`，大肠杆菌使用`NC_000913.3`。包内文件名保留分辨率，例如`chr1_1000.cool`和`NC_000913.3_1000.cool`。

## caller原始输出

统一转换后的三列BED文件放在：

```text
progress/1-TAD-data/<species>/<method>/<data_type>/<resolution>/<chrom>.bed
```

至少包含`chromosome`、`start`和`end`。坐标使用0-based half-open。完全相同区间应仅保留一条，非法坐标不得进入评价。

`progress/2-analyse/summary.xlsx`记录每种方法在各数据条件中的染色体结构域数量及OOM、Timeout或零输出状态。`time_memory-useage.xlsx`记录资源监控结果。包内文件对应本研究数据；分析新数据时必须更新。

## 层级结构域

`3-domain-level.py`输出到：

```text
progress/1-TAD-level-data/<species>/<method>/<data_type>/<resolution>/<chrom>.bed
```

输出至少包含`chromosome`、`start`、`end`和`level`。

## EVRC

平衡dense矩阵按单染色体准备，每个输入目录仅包含一条染色体。PDB输出建议放在：

```text
progress/1-EVRC-data/<species>/<data_type>/<resolution>/<chrom>/
```

## coolpup

`.clpy`文件放在：

```text
progress/1-coolpup-data/<species>/2-coolpup/<data_type>/<resolution>/<method>/
```

BY4741文件名需包含染色体，例如`HiC_chr1_1000.clpy`。E. coli为单染色体，可使用条件级文件并映射为`NC_000913.3`。

## 表达和功能数据

放在`progress/1-expression-data/`。包内提供`BY4741-TPM-FPKM.tsv`、`Ecoli_expression_annotated_readable.tsv`及对应GFF作为canonical映射的起始输入。运行`A5-prep-canonical-gene-expression.py`后，在`gene-level/`生成以S288C或ASM584v2权威gene ID和坐标为唯一记录的canonical基因表。下游保留数值型`TPM > 0`的基因。酵母ATAC-seq bigWig路径为`progress/1-expression-data/ATAC/A5-1.rmdup.last.bw`。
