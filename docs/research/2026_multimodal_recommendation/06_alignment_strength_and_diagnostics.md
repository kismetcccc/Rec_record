# 对齐强度与排序效用不一致，以及对齐效果的直接诊断不足

共同基础是**跨模态/行为对齐如何被评价**。P10 是过强训练约束损害排序，P11 是用排序增益反推对齐改善的证据不足；因果对象不同，保留两个子项。

## P10 增强一致性不保证增强推荐质量
- **问题与条件**：辅助一致性过强可能损害排序；BRIDGE 的指定诊断还显示较高余弦不保证较高 Recall。不能从权重增大本身断言表示必然更相近。
- **核心证据**：MMWave IV-C/Fig.9，较小对比权重有益，权重为 1 时性能最差。
- **补充证据**：CIKM 2026 AMUR §3.3/Table 3 的共享选择优于 Full space，§3.4/Fig.9 仍有过大权重退化；BRIDGE §4.1 Baby R@20 无/适度/强一致性分别 .0922/.1024/.0836，§4.2 的高余弦并非高 Recall。
- **已处理/剩余**：以上方法已通过各自对齐/整合策略改善效果；残留是约束强度与目标收益仍非单调。不证明所有任务有同一最优强度，也不等同已测量梯度冲突。
- **类型**：实验支持；跨实验归纳限定“相似度不能直接等同排序质量”。
- **代码**：[MMWave.calculate_loss L530–559](https://github.com/kennethorq/MMWave/blob/51e761d6dc18125aa7d1a58764de2061bfdb457c/src/models/mmwave.py#L530-L559) 加权 InfoNCE 与 BPR；[AMUR.calculate_loss L372–403](https://github.com/Wenze1/AMUR/blob/d6d5f86289be1d135328eda7bbac59a72c559e43/model/amur.py#L372-L403) 组合共享/行为目标。

## P11 推荐效果和梯度协调不能替代直接的表示对齐量化
- **问题与条件**：推荐导向 VLM 适配后，主要靠排序差异解释模态对齐，难以直接确定表示对齐程度。
- **证据**：SDA §4 明确将直接、系统的对齐量化留待研究。§3.3.3 已观察共享 LoRA 梯度冲突并改善，但梯度协调和表示空间对齐是不同对象。
- **已处理/剩余**：SDA 结构适配与 MoDA 已提升效果，不能写成没有对齐；剩余是论文承认的诊断直接性不足，不是未报告实验自动推导的缺陷。
- **类型**：作者明确指出；仅属诊断问题，不宣称其准确率不可靠。
- **代码**：[官方 SDA](https://github.com/RaoZhongtao/SDA)；[`llm/qwen_vl.py::Contrastive_Loss.forward` L242–253](https://github.com/RaoZhongtao/SDA/blob/524cf2ab4507ded09038182ecb4773eb39bae3b7/llm/qwen_vl.py#L242-L253)；`analyze_gradient` 位于同文件 L224。静态定位训练/梯度机制，不补造直接对齐指标。
- **发表类型**：SIGIR 2026 **short paper**，单列为补充证据，不冒充正式长文。

正文入口：[MMWave](https://arxiv.org/html/2610.16229v1)、[AMUR](https://arxiv.org/html/2608.27950v1)、[BRIDGE](https://arxiv.org/html/2605.22073v2)、[SDA 作者版本](https://arxiv.org/abs/2512.06883)。版本/状态详见 SOURCES.md。
