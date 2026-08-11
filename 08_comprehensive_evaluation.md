# M7. 综合评价和方法使用指南

仅在上游canonical表齐全并完成一致性检查后运行：

```bash
python progress/2-analyse/A13-comprehensive-method-recommendation.py
python progress/2-analyse/A13c-method-recommendation-compact-guide.py
```

综合矩阵保留运行资源、识别覆盖、结构验证、方法间结构一致性和酵母生物学关联等证据类别。不同指标保留自身统计单位和方向，不合并为统一准确率。

推荐强度同时考虑：

1. 单项指标内的相对表现。
2. 对应物种范围内的染色体任务覆盖度。
3. 平均每个有效数据条件至少识别10个结构域的最低输出量要求。

使用指南先按运行时间和峰值内存划分资源条件，再按结构研究或酵母边界表达与功能研究划分研究目标。ATAC-seq和功能富集用于解释酵母生物学关联，不直接进入所有物种共有的统一分数。

主图可以只展示代表性方法，完整候选集合必须来自canonical推荐表。
