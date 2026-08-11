# M2. EVRC三维重构

EVRC原始程序位于`tools/EVRC-main.zip`。解压后，对每条染色体独立运行：

```bash
python tools/EVRC-main/evrc.py \
  --intra_chr <single_chromosome_dense_directory> \
  --chr_num 1 \
  -o <output_directory> \
  --seed 29 \
  --thread 10
```

本研究每个输入目录仅包含一条染色体，因此`--chr_num 1`。未显式设置的参数使用EVRC默认值。本地路径可以变化，但`chr_num`、随机种子和线程参数应按研究设计记录。

`tools/evrc_reference_wrappers/`保留酵母和大肠杆菌原始批处理脚本，仅用于证明本研究实际调用参数。脚本中的旧绝对路径不是Protocol路径要求，复现时应使用上面的单染色体命令或自行编写批处理循环。

PDB结果随后由`A10t-centroid-distance-local-background-validation.py`读取。EVRC重构是结构验证输入，不是独立金标准。
