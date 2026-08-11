# M5. 方法间结构一致性

所有比较必须限定在完全相同的`species + data type + resolution + chromosome`单元内，并要求至少两种方法获得有效输出。

```bash
python progress/2-analyse/A2b-jaccard-exact-same-condition.py
python progress/2-analyse/A3b-moc-coverage-same-condition.py
python progress/2-analyse/A4b-consensus-exact-same-condition.py
python progress/2-analyse/A8c-ssim-same-condition.py
python progress/2-analyse/A12-structure-robustness-fair-same-condition.py
```

- Boundary Jaccard比较完全相同的边界坐标，不设置位置容差。
- Coverage Jaccard比较每种方法合并后的结构域覆盖区域。
- Consensus F1比较单个方法与严格多数共识边界。
- MOC保留单个结构域身份，评价区间对应程度。
- SSIM比较结构域层级占用矩阵的整体形态。

一致性结果反映caller输出关系，不是独立结构验证，也不能替代生物学准确性。跨物种汇总时应保留每个物种的有效比较单元和覆盖范围。
