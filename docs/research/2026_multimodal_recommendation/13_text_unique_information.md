# 图像压缩表示之外，文本独有且推荐相关的细节仍难充分提取

## P22 视觉重叠内容掩盖了文本真正有用的补充
- **问题与条件**：用图像高效承载物品信息时，文本还有图像不能完整表示的细微属性/语境；从重复视觉信息中分离出有推荐价值的文本补充仍困难。
- **证据**：I-LLMRec Appendix G 明确列出这一限制；§4.2 的加入文本收益有限。不是所有文本都无用或都被浪费。
- **已处理/剩余**：已有单 token 图像表示、推荐对齐和多特征融合，仍未充分提取文本独有信息；不能说“没有融合文本”。
- **类型**：作者明确指出；不是本轮量化的信息损失率。
- **代码**：[`ILLMRec.py` L82–126](https://github.com/rlqja1107/torch-I-LLMRec/blob/a778ec752233305a488ad3db28d8fec9ce4d82ba/ILLMRec/model/ILLMRec.py#L82-L126) 包含 `visual_feature_to_LLM`、`encode_visual_feature`、`encode_textual_feature`；[`eval.py::compute_rank` L179–202](https://github.com/rlqja1107/torch-I-LLMRec/blob/a778ec752233305a488ad3db28d8fec9ce4d82ba/ILLMRec/eval.py#L179-L202) 实际合并图像、CF、文本分数。未据等权实现推断缺陷。
- **来源**：[官方仓库](https://github.com/rlqja1107/torch-I-LLMRec)、[论文入口](https://arxiv.org/abs/2503.06238)、[ICLR 2026 官方目录](https://iclr.cc/Downloads/2026)。

不同于内容污染、图文冲突或平滑去细节，本项针对**文本独有信息的提取**，独立保存。
