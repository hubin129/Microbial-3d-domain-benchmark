# M4. 结构验证

三项结构验证回答不同问题，应分别运行和解释。

## Fold-change

```bash
python progress/2-analyse/A4x-foldchange-reanalysis-exact-condition.py
```

该脚本比较单个结构域内部接触与局部域外背景。level 1使用与左右最近同层级结构域之间的间隔或染色体侧翼，嵌套结构域优先在最近父结构域内构建背景。验证标准为`log2FC > 0`且精确条件单元内`BH-FDR < 0.05`。

## EVRC局部背景紧密性

```bash
python progress/2-analyse/A10t-centroid-distance-local-background-validation.py \
  --n-random 1000 \
  --evrc-pdb-root <PDB_ROOT> \
  --tad-root progress/1-TAD-level-data

python progress/2-analyse/A10u-merge-local-background-sensitivity.py
```

结构域至少覆盖4个重构bin。主分析使用1,000个唯一随机集合，敏感性分析可使用50、100、200、500和1,000次随机抽样。验证标准为`EVRC score > 0`且`BH-FDR < 0.05`。

## coolpup聚合接触形态

使用coolpup.py v1.1.0将每个结构域重缩放到99×99网格，并按染色体聚合。示例命令：

```bash
coolpup.py <matrix.cool> <domains.bed> \
  --local --rescale --rescale_size 99 \
  --outname <output.clpy>
```

具体命令选项应以安装版本的`coolpup.py --help`为准。生成`.clpy`后运行：

```bash
python progress/2-analyse/A9d-coolpup-chromosome-domain-structure-validation.py
python progress/2-analyse/A9e-coolpup-chromosome-domain-structure-figures.py
python progress/2-analyse/A9f-coolpup-method-share-figure.py
```

验证标准为中心区块相对相邻跨边界区块的效应量大于0，且完全匹配条件内`BH-FDR < 0.05`。统计单位为染色体级聚合矩阵，不是单个结构域。
