# M6. 生物学关联

本模块需要与接触数据来源匹配的表达、染色质可及性或功能注释。缺少匹配数据时可跳过。

发布包已包含本研究使用的表达表、参考GFF、酵母ATAC-seq bigWig、GO注释和KEGG映射。`gene-level/`中的canonical表不是随包提供的过程数据，应先运行下述准备脚本生成。

## canonical基因表

```bash
python progress/2-analyse/A5-prep-canonical-gene-expression.py
```

以S288C和ASM584v2权威gene ID及坐标建立一行一个基因的canonical表。下游仅保留有效坐标和数值型`TPM > 0`，不再次按区域去重。

## 边界与内部表达

```bash
python progress/2-analyse/A5m-boundary-3bin-gene-level-expression.py
```

边界窗口为结构域起止位置两侧各3个接触图bin，内部为去除两侧窗口后的同一结构域区域。每个结构域分别计算边界和内部基因TPM中位数，并在method-condition内进行配对检验。

## ATAC-seq边界关联

```bash
python progress/2-analyse/A14-atac-random-background.py
```

真实边界与同染色体1:1唯一随机位置均提取中心两侧各20个接触图bin。正式检验使用紧邻中心的上游和下游两个bin。随机位置不得重复或与真实边界中心重合。

## 高表达基因功能富集

```bash
python progress/2-analyse/A5ab-by4741-global-top10-boundary-high-gene-go-kegg-enrichment.py
```

本研究在5,782个酵母核基因中定义固定的全基因组TPM前10%集合。Boundary-high和Nonboundary-high均相对于同一个具有注释的高表达基因背景进行单侧Fisher精确检验，并在`method + condition + side + database`内进行BH校正。
