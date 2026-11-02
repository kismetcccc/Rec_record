# 官方发布物的可解析性、输入工件与论文实现对应关系

三项共同影响**依据公开发布物重现论文的能力**；分别是语法阻断、输入缺失、目标定义差异，不合并为同一模型缺陷。

## P15 官方模型文件存在静态解析阻断
- **问题/影响**：VI-MMRec 指定发布快照不能直接被 Python 解析，接入推荐框架前即受阻。
- **证据与位置**：[`VI-MMRec.py::get_knn_adj_mat` L96–120](https://github.com/Jinfeng-Xu/Vi-MMRec/blob/b793b9076430e93d9ab8c3f475a212326907a19f/VI-MMRec.py#L96-L120) 第104行额外缩进；本轮仅标准库 `ast.parse` 返回 `IndentationError: unexpected indent`，未 import 或训练。
- **已处理/剩余**：README 提供 MMRec/MRLib 接入说明，但所查文件仍有解析障碍。
- **类型**：代码观察，经静态解析核验。只限此 SHA，不否定论文指标或方法有效性。

## P16 公开代码依赖的实际数据划分/映射未随快照提供
- **问题/影响**：HSD 仓库内仅有数据占位，加载器需要具体 train/test pickle，单靠当前仓库不能还原同一输入协议。
- **证据与位置**：[`README.md` L10–11](https://github.com/Tuo97/HSD/blob/9c0b2647a5d28eda95048cfcfa9ba98ed82a1520/README.md#L10-L11) 明说 placeholders；三数据目录各仅一个 1-byte 文件；[`utility/load_data.py::Data.__init__` L18–39](https://github.com/Tuo97/HSD/blob/9c0b2647a5d28eda95048cfcfa9ba98ed82a1520/utility/load_data.py#L18-L39) 要求 train.pickle/test.pickle，并有 Beauty 用户/物品数常量。
- **已处理/剩余**：作者公开了模型实现且披露占位原因；本轮未确认其他分发渠道，不能说作者从未提供或数据不存在。
- **类型**：作者明确指出、代码观察。属于公开工件完整性，不是实证性能缺陷。

## P17 论文蒸馏目标与当前实现的定义不等价
- **问题/影响**：MTS²-4MM §3.5 描述 batch 候选 rank KD、均匀教师集成及 embedding KD；当前源码采用正负 pair margin、选择优于学生且 margin>0 的教师，损失汇总无论文所述 embedding KD 分项。因此按论文和当前代码执行的目标不完全一致。
- **证据与位置**：[`src/models/mts4mm.py::_rank_kd_loss_logits / calculate_loss` L323–382](https://github.com/MICLab-Rec/MTS4MM/blob/4157dbb7d8b31a0f3f205c4c29eb7e6be64d65bc/src/models/mts4mm.py#L323-L382)；[IJCAI 官方论文页](https://ijcai.org/proceedings/2026/348)。
- **已处理/剩余**：README implementation notes 主动说明 pairwise KD 与教师筛选，并非隐瞒；代码—论文结果对应和等价性未核验，不能断言准确率下降。
- **类型**：代码观察，对照论文目标。该项为 IJCAI 2026 扩展来源，单独标注，不混称全部来源为同级顶会。

官方仓库：[VI-MMRec](https://github.com/Jinfeng-Xu/Vi-MMRec)、[HSD](https://github.com/Tuo97/HSD)、[MTS4MM](https://github.com/MICLab-Rec/MTS4MM)。上述发现均未改动任何源码。

## P18 生成式推荐器对上游依赖版本敏感，跨版本结果不直接可比
- **问题/影响**：SynGR 作者报告更换 Transformers 到 4.45.0 以上后指标明显下降，复现不能只对齐模型名称而忽略依赖。
- **证据与位置**：[官方 README L21](https://github.com/gxingyu/SynGR/blob/60c76cb48880ed4580fb77d3a53365321111dd20/README.md#L21) 明确要求 4.45.0；[ICML 2026 官方目录](https://icml.cc/Downloads/2026) 列出该论文。
- **已处理/剩余**：固定版本建议降低复现风险；作者未解释根因或完整受影响版本集合，本轮未重跑。不能猜测 attention/cache/算子为原因。
- **类型**：作者明确指出（官方源码说明），不是本轮实验支持；不包装成理论模型研究空白。
- **来源**：[官方仓库](https://github.com/gxingyu/SynGR)、[论文入口](https://arxiv.org/abs/2605.18920)。
