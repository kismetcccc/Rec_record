# 高比例文本缺失下，补全仍有下游模型相关的恢复差距

## P04 缺失文本的信息不能稳定恢复到完整输入水平
- **问题、条件、影响**：文本大量缺失时，补全后的排序性能仍可能下降，补全方法的名次依赖下游推荐器。不能拆成“缺文”和“模态不平衡”重复计数。
- **证据**：GMI VI-E/Table V，Baby、90% 文本缺失：FREEDOM 完整 Recall@20 为 8.95%，HEAT 为 7.19±0.17%，AutoEnc 为 7.70±0.11%；LGMRec 完整 8.87%，HEAT 为 7.96±0.15%。这是论文结果，未重跑。
- **已处理/剩余**：图补全在许多设置有效；这里限定为文本缺失及指定模型，既未恢复完整性能，也不是任何图方法都优于传统补全。不能概括为“补全无效”。
- **类型**：实验支持、作者明确指出。
- **代码**：[官方仓库](https://github.com/danielemalitesta/Graph-Missing-Modalities-TKDE)；[`mask_items.py` L64–101 文本遮蔽](https://github.com/danielemalitesta/Graph-Missing-Modalities-TKDE/blob/1d7607027f6b52ca48281aec67fb542f96a6978e/mask_items.py#L64-L101)；[`impute.py` HEAT L278–354](https://github.com/danielemalitesta/Graph-Missing-Modalities-TKDE/blob/1d7607027f6b52ca48281aec67fb542f96a6978e/impute.py#L278-L354)。[作者论文状态页](https://arxiv.org/abs/2602.17354)。

与供体质量相关，但本项是**特定缺失条件下的恢复结果**，未证明所有差距都由 P01–P03 导致，因此单独保存。
