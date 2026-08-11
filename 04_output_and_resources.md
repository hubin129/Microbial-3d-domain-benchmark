# M3. 输出标准化、资源与识别覆盖

## 运行顺序

```bash
python progress/2-analyse/3-domain-level.py
python progress/2-analyse/A0-runtime-memory-analysis.py
python progress/2-analyse/A1b-tad-result-overview.py
python progress/2-analyse/A1c-tad-size-level-overview.py
```

本研究的`summary.xlsx`和`time_memory-useage.xlsx`随包保存在`progress/2-analyse/`，用于复现当前benchmark的完成状态、结构域数量和资源记录。应用于新数据时，应按相同工作簿结构更新这两个文件，不能沿用本研究数值。

## 输出标准化

`3-domain-level.py`读取`progress/1-TAD-data/`，移除完全重复或非法区间，按起点升序和终点降序排序，并依据坐标包含关系定义层级。最外层为level 1，子结构域层级为最近父结构域level加1。相交但不存在包含关系的区间不建立父子关系。

## 资源统计

`A0-runtime-memory-analysis.py`汇总资源监控日志。运行时间和峰值内存必须保留实际监控单位。若wrapper处理多个条件，则不能把其总时间拆写为单条件时间。

## 覆盖和输出特征

`A1b`按chromosome-condition统计是否获得至少一个有效结构域。`A1c`统计结构域数量、大小、层级、嵌套和连续性。覆盖、零输出、超时、OOM和不支持输入必须分开保存。
