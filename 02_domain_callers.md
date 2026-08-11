# M1. 结构域识别方法

`tools/13-methods.zip`包含本研究使用的13种方法归档：Armatus、Arrowhead、deDoc、GMAP、GRiNCH、HiCKey、HiTAD、Matryoshka、OnTAD、SpectralTAD、SuperTAD-fast、TADpole和TADtree。

## 使用原则

1. 每个物种、数据类型、分辨率和染色体独立运行。
2. 使用补充方法文档记录的参数，不因本地路径变化修改科学参数。
3. 保留完成、零输出、超时、内存溢出和不支持输入等不同运行状态。
4. 原始输出统一转换为BED兼容坐标后，再进入后续模块。
5. TAD数量和层级是输出特征，不单独代表识别准确性。

完整命令和参数见`docs/Datas_Supplementary_Protocol_Methods_Detail.docx`。各方法的原始地址、归档版本、许可证和引用见`THIRD_PARTY_SOURCES.md`；安装和再分发要求仍以各上游项目为准。

## 资源监控

通用命令：

```bash
python tools/runtime_monitor.py --output run_metrics.tsv -- <caller command and arguments>
```

监控器每0.5秒采样父进程及所有后代进程的RSS，记录wall-clock时间、最大合计RSS和退出码。若一个wrapper顺序处理多个条件，记录值属于整个wrapper运行，不应写成单个method-condition的标准化资源消耗。
