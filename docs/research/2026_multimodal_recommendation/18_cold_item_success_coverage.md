# 冷物品曝光均衡，不等于成功命中覆盖充分

## P28 已改善曝光分布的模型仍有大量冷物品零成功命中

- **条件/影响**：SEMCo Electronics 使用图像4096维、文本384维和交互；随机20%物品不参加训练、分作验证/测试。冷测试top20评估中，推荐次数分布改善，仍不保证各物品获得成功命中。
- **证据**：§4.1.1/Table 1确认图文输入；§4.2/Fig.1 所画方法至少60%冷物品 item MDG@20=0。SEMCo-Online几乎所有物品已被推荐至少10次，故**无成功命中≠未被曝光**。
- **已缓解/残余**：方法已改善公平性及用户准确率、减轻CF表示模仿；没有消除上述成功命中覆盖缺口。不以仅文本的Clothing支持此多模态结论，不推断真实用户必然不喜欢零命中物品。
- **类型**：作者明确指出、实验支持，限所画方法、Electronics、cold-test/top20与有限日志；未识别全部原因。
- **代码**：[官方SEMCo](https://github.com/gmeehan96/SEMCo)，SHA `0ae1effb23ddac7339666c9af5324711aa909282`；[`SEMCo_Learner` L152–206](https://github.com/gmeehan96/SEMCo/blob/0ae1effb23ddac7339666c9af5324711aa909282/models/SEMCo.py#L152-L206)多模态编码及用户聚合；[`LearnedWeightedSum.forward` L11–40](https://github.com/gmeehan96/SEMCo/blob/0ae1effb23ddac7339666c9af5324711aa909282/util/utils.py#L11-L40)融合。未定位Fig.1的item-MDG绘图脚本，不声称复现，也不据此声称没有实现。
- **状态**：SIGIR2026 **short补充来源**，[官方名单](https://sigir2026.org/en-AU/pages/program/accepted-papers)、[DOI](https://doi.org/10.1145/3805712.3809975)、[作者全文](https://arxiv.org/html/2604.12990v1)。

不同于 P02 的缺失特征图补全：这里内容完整，问题是零训练交互新物品的最终成功命中分布，独立保存。
