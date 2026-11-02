# 图文离散表示的token容量与稀疏惩罚：两种不同边界

共同对象是图文离散表示，但一个是**扩大词表/序列空间**，另一个是**增加稀疏惩罚**。原因、方向和受影响人群不同，同文分项；不是同一问题换词。

## P31 码本或语义ID变大后，可学性未随容量单调增加

- **条件/影响**：MACRec完整模型的Instruments参数分析，码本容量及ID长度改变后，排序收益非单调。
- **证据**：RQ5/Fig.3(a)(b)：码本128/256/512的HR@10为 .1334/.1363/.1342；ID长度3/4/5为 .1314/.1363/.1328。更大码本稀释token曝光、更长ID增加生成空间是作者解释，不是本轮独立因果实验。
- **已处理/残余**：跨模态量化、重分配和多方面对齐已改善结果；完整方法仍有容量边界。码字碰撞已有重分配处理，不能据量化中间冲突率再称最终检索碰撞未解决。
- **类型**：实验支持、作者解释；不声称所有模型容量增大都退化。
- **代码**：[官方MACRec](https://github.com/zhangfw123/MACRec)，SHA `7a48e7429a8806e2290a1fc6ac5661c1ff934b51`；[`CrossRQVAE.__init__` L10–40](https://github.com/zhangfw123/MACRec/blob/7a48e7429a8806e2290a1fc6ac5661c1ff934b51/cross_index/models/rqvae.py#L10-L40)设置每层容量，[`ResidualVectorQuantizer` L13–59](https://github.com/zhangfw123/MACRec/blob/7a48e7429a8806e2290a1fc6ac5661c1ff934b51/cross_index/models/rq.py#L13-L59)构建码本及残差索引。静态定位机制，不冒称运行。
- **正式状态/版本**：[AAAI2026正式条目](https://ojs.aaai.org/index.php/AAAI/article/view/38664)；[作者v2](https://arxiv.org/abs/2511.15122v2)，未逐字核对出版社终稿。

## P32 固定码本下增强稀疏惩罚，对低交互物品更敏感

- **条件/影响**：MoToRec固定K=1024，提高稀疏正则强度，对低交互测试子集的影响大于总体指标显示的变化。
- **证据**：Hyperparameter Study/Fig.5，Sports γ=.10→.20，overall N@20 .0529→.0519，cold .0183→.0145；作者明确指出cold对稀疏偏差更敏感。只比较图中数值，不声称统计显著性。
- **已处理/残余**：稀疏token化、稀有度加权及融合已经改善冷启动，消融去稀疏项更差；剩余是强度偏离后的子集敏感性，不是“稀疏化总是有害”。这里cold定义为**训练交互少于10的测试物品**，不等同严格零交互。
- **类型**：实验支持、作者明确指出；不是仅据最佳超参数不同推断。
- **源码**：本轮未找到可核验、可读取的官方实现；第三方候选仓库404不能当代码证据，类/函数不猜测。
- **状态**：[AAAI2026条目](https://ojs.aaai.org/index.php/AAAI/article/view/38558)、[大学正式记录](https://scholars.cityu.edu.hk/en/publications/motorec-sparse-regularized-multimodal-tokenization-for-cold-start/)，15324–15332；读[作者v2](https://arxiv.org/abs/2602.11062v2)。

两项都不是P09的频域平滑或P24的渲染截断；数据对象虽同为物品信息，损失发生环节不同。
