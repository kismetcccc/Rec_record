# 共用户行为校准的证据精度与候选内作用范围

本文件仅使用 **CIKM 2026 Full Research 已录用**的 BRIDGE 补充来源。两个问题发生在同一局部行为校准流程，但一个关乎证据是否可靠，另一个关乎哪些物品能直接受到修正，不合并计数。

## P20 稀少重叠或突发局部交互削弱行为校准证据
- **问题/条件**：共用户支持少或局部突发时，邻域统计精度不足，候选内修正不稳定。
- **证据**：BRIDGE §7.1、§7.3 作者明确限制；没有可引用的统一稀疏阈值/失败率。
- **已处理/剩余**：使用训练统计、局部候选与保守系数限制影响，仍依赖共用户统计可靠性。
- **类型**：作者明确指出，代码观察佐证依赖。
- **代码**：[`_build_sparse_behavior_evidence` L226–265](https://github.com/LIZESHENG13/bridge/blob/4ee976f5f1715ff9c186aac8a8ddd44a74a41ece/src/models/bridge.py#L226-L265)；[`_candidate_behavior_scores` L315–340](https://github.com/LIZESHENG13/bridge/blob/4ee976f5f1715ff9c186aac8a8ddd44a74a41ece/src/models/bridge.py#L315-L340)。

## P21 基础候选未覆盖的物品不能获得直接残差校准
- **问题/条件**：基础 top-K 外的相关物品不进入局部残差修正，作用范围受初始覆盖限制。
- **证据**：BRIDGE §7.1、§7.3 承认候选依赖；§6.4/Table 3 表明全局作用并非无代价替代。
- **代码限定**：[`full_sort_predict` L561–610](https://github.com/LIZESHENG13/bridge/blob/4ee976f5f1715ff9c186aac8a8ddd44a74a41ece/src/models/bridge.py#L561-L610) 只对候选 scatter_add，但返回全物品分数。因此**候选外不直接修正，不等于其相对排名绝不变化**。
- **已处理/剩余**：局部性减少全局干扰，也保留直接作用范围限制。
- **类型**：作者明确指出、代码观察；不把作者简写解释成更强的实现定理。

[官方仓库](https://github.com/LIZESHENG13/bridge)；[作者全文 v2](https://arxiv.org/html/2605.22073v2)；[CIKM 官方议程](https://cikm2026.diag.uniroma1.it/program/)。与 P02 的冷启动补全不同：这里是非缺失场景的评分校准，目标和作用环节不同。
