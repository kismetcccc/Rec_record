# 稀疏图输出与训练免费，不代表预处理没有密集矩阵开销

## P13 大目录的密集预构图资源需求与规模相关退化路径
- **问题与条件**：最终只保留 kNN/稀疏图，但构造过程先分配全物品矩阵；目录扩大时，中间存储至少按物品数平方增长，部分实现还有边数×物品数张量。
- **论文证据**：MMWave IV-D/Table V 明确排除特征分解预处理；Sports 训练内存/每 epoch 为 4.67 GB/10.41 s，LGMRec 为 2.89 GB/8.46 s。IIMRec §6.5/Table 4 评估预构图之后的训练。不能据这些局部指标宣称端到端扩展性已获保证。
- **代码证据**：
  - GMI [`impute.py::get_item_item` L11–23](https://github.com/danielemalitesta/Graph-Missing-Modalities-TKDE/blob/1d7607027f6b52ca48281aec67fb542f96a6978e/impute.py#L11-L23) 先 `.toarray()` 再 top-k；PersPageRank L220–225、HEAT L305–310 还有密集求逆/矩阵指数。
  - MMWave [`eigen_decomposition_fusion` L242–272](https://github.com/kennethorq/MMWave/blob/51e761d6dc18125aa7d1a58764de2061bfdb457c/src/models/mmwave.py#L242-L272) 将图转密集 CPU 矩阵，求特征值并形成密集加权结果。
  - IIMRec（作者确认录用，出版方独立核验未完成，仅作补证）[`_knn_from_feat` L283–305](https://github.com/Jinfeng-Xu/IIMRec/blob/b22a36911e3f41412de99102040b99cb0019872c/src/models/iimrec.py#L283-L305) 先全相似度；[`_apply_ncer` L428–485](https://github.com/Jinfeng-Xu/IIMRec/blob/b22a36911e3f41412de99102040b99cb0019872c/src/models/iimrec.py#L428-L485) 分支前分配 n*n；n≤50000 时生成 E×n 邻居数组，n>50000 时内层 n<30000 恒假，若先前分配成功则直接返回未 NCER 重加权的图。
- **已处理/剩余**：方法减少训练或传播负担，但当前预处理仍有上述资源/规模边界。IIMRec 大图 fallback 是同一规模问题的实现证据，不另拆一个痛点凑数。
- **类型**：代码观察 + 复杂度推断；论文实验只支持其报告阶段。没有运行内存压测，不声称 OOM 阈值、实测预处理时长或论文数据集无法运行。
- **官方仓库**：[GMI](https://github.com/danielemalitesta/Graph-Missing-Modalities-TKDE)、[MMWave](https://github.com/kennethorq/MMWave)、[IIMRec](https://github.com/Jinfeng-Xu/IIMRec)。

共同对象是离线建图的中间资源，而非线上 agentic 推理成本，后者另文。
