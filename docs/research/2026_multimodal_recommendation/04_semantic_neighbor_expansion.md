# 扩大语义邻域引入偏好无关关系

## P07 更多相似物品不一定提供更多有效推荐信号
- **问题与条件**：通过内容近邻构造关系或虚拟交互时，扩大邻居数量会纳入偏好不相关/冗余关系，降低排序质量。
- **证据**：MMWave IV-C/Fig.10 增大文本 kNN 在 Baby/Sports 出现退化；VI-MMRec §5.7/Fig.4 中较大 k 在多数数据集引入偏好不相关物品。
- **已处理/剩余**：二者已利用模态相似性改善表示/交互，仍存在邻域扩张的适用范围；不能将“相似关系完全无效”当结论。
- **类型**：实验支持；“冗余”“偏好无关”是作者解释，不是本轮因果测量。
- **代码**：[MMWave 文本邻接 `__init__` L122–130](https://github.com/kennethorq/MMWave/blob/51e761d6dc18125aa7d1a58764de2061bfdb457c/src/models/mmwave.py#L122-L130)；[VI-MMRec 官方模型文件 `get_knn_adj_mat`](https://github.com/Jinfeng-Xu/Vi-MMRec/blob/b793b9076430e93d9ab8c3f475a212326907a19f/VI-MMRec.py#L96-L120)。VI-MMRec 该发布文件另有解析障碍，详见复现文档，不能声称本轮执行过。
- **正文入口**：[MMWave](https://arxiv.org/html/2610.16229v1)；VI-MMRec 正式状态、作者版本和仓库见 SOURCES.md。

二者共享“扩大内容相似候选引入低价值关系”基础，合并计数；与缺失补全的供体是否能恢复目标语义不同，不强行合并 P01。

## P08 相似邻居规模失衡会扭曲偏好优化的难度估计
- **问题与条件**：HaNoRec 用相似物品簇估计偏好样本难度，邻域过窄覆盖不足，过宽引入弱相关项，难度估计及优化效果受损。
- **证据**：§4.5/Fig.5(a)，K=10/20 较好，K=1/50 恶化；图无可读精确跌幅，不猜数值。完整方法已缓解固定 DPO 的难易样本失衡，仍对估计邻域范围敏感。
- **类型**：实验支持、作者解释。影响是训练样本难度，P07 则是扩充交互/传播关系，故同文不同项。
- **代码**：[`hanorec/hars/hardness.py::topk_neighbors`](https://github.com/wangyu0627/HaNoRec/blob/587face74524e4553b5a7aa295fe962004682382/hanorec/hars/hardness.py#L38)；[`build_hardness.py` L108–112](https://github.com/wangyu0627/HaNoRec/blob/587face74524e4553b5a7aa295fe962004682382/hanorec/cli/build_hardness.py#L108-L112)。
- **正式来源**：[SIGIR 2026 full paper DOI](https://doi.org/10.1145/3805712.3809590)、[官方代码](https://github.com/wangyu0627/HaNoRec)、[作者稿](https://arxiv.org/abs/2511.18740)。

## 第二轮关联补证：P07的邻域类型须区分

MAGE Appendix F.1/Fig.8同样报告扩大候选关系范围后性能下降，但它使用的是**异配互补边**，不是P07原例的内容相似边。共同点只在过宽物品关系集合会引入低价值关联，不将两个邻域定义等同，也不据此宣称所有互补传播都如此。[`mage.py::add_edge` L235–275](https://github.com/Alex-bupt/mage/blob/9a1a16c2734ed1f35f0ea175b3bab8eb21fe3348/main/src/models/mage.py#L235-L275)限制`targets[:max_p2b_k]`；[作者全文](https://arxiv.org/html/2610.37409v1)。类型：实验支持、代码观察。作为同一范围敏感性的关联证据保留，不新增痛点、不改变P08的难度估计对象。
