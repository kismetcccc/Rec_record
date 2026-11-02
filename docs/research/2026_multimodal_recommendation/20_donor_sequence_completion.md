# 相似用户行为补齐策略依赖交互密度与行为可复用性

## P30 更多供体或更精细子序列选择，并非跨数据稳定增益

- **问题/条件**：MARS的多模态用户检索之后，将供体行为补入目标序列。多供体混合或DP子序列选择的收益随密度和兴趣分布变化，不是补得更多就更准确。
- **证据**：§V-H/Fig.5，Kth-Similar/DP在dense ML-1M退化；Kth-Similar在稀疏Beauty/Toys有益；DP在Beauty较好而Toys下降。热门/重复行为及兴趣碎片化是作者解释，未做独立因果检验，不猜图上未标的跌幅。
- **已处理/残余**：已进行模态对齐及高活跃供体检索/筛选；残余限这些补齐策略和数据条件，不说MARS未考虑语义。
- **代码**：[官方 MARS](https://github.com/wangshukuan/MARS)，SHA `4522c566cfad079a5c3eb326ad65ddb4b623b4c2`；[`KthSimilarUserPadding.pad` L19–26](https://github.com/wangshukuan/MARS/blob/4522c566cfad079a5c3eb326ad65ddb4b623b4c2/PaddingStrategy/KthSimilarUserPadding.py#L19-L26)合并top-k供体序列；[`FilteredMostSimilarUserPadding.pad` L15–31](https://github.com/wangshukuan/MARS/blob/4522c566cfad079a5c3eb326ad65ddb4b623b4c2/PaddingStrategy/FilteredMostSimilarUserPadding.py#L15-L31)筛内容相似度。快照早于所读v2，仅定位策略，不声称等于全部线上运行版。
- **类型**：实验支持、作者解释、代码观察；未运行。
- **完整身份**：*Modality-Aligned Retrieval for Sequence Augmented CTR Prediction*，[IEEE正式Early Access记录](https://ieeexplore.ieee.org/abstract/document/11699087/)，2026-09-22，TKDE，[DOI](https://doi.org/10.1109/TKDE.2026.3735698)；读[作者v2](https://arxiv.org/html/2509.01184v2)，未逐字比终稿。旧台账仅缩写MARS和ICLR提交态，没有唯一ID，不能默认为同篇并直接升级。

与P07共同涉及候选范围，但其对象是物品关系，而本项是检索后的用户序列补齐及策略选择，故独立保存；不是缺失物品特征插值P02。
