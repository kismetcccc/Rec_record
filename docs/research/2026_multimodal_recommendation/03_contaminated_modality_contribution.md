# 模态额外贡献不足与已观测内容受损后的残余退化

## P05 新增模态不保证带来稳定的额外收益
- **问题与条件**：将更多模态加入现有表示时，额外内容不必转化为稳定排序收益。
- **已处理的基线动机**：MMWave Introduction/Table I 的 TikTok LGMRec R@10 为图文 .0588、全模态 .0502。这是基线抑制现象，不是完整 MMWave 的残余负收益证据。
- **完整方法的剩余证据**：MMWave IV-E/Fig.13 的污染条件下，视觉+音频与全模态结果接近；只能说明该条件下文本额外收益有限，不能把“接近”写成精确零或负收益。
- **已处理/剩余**：MMWave 已针对模态抑制提出整合，不能说没有处理；残余严格限定上述污染设置，不推广为全领域新增模态无效。
- **类型**：实验支持；对文本可靠性的解释为作者解释，非独立因果验证。
- **代码**：[官方仓库](https://github.com/kennethorq/MMWave)，[`MMWave.forward` L450–513](https://github.com/kennethorq/MMWave/blob/51e761d6dc18125aa7d1a58764de2061bfdb457c/src/models/mmwave.py#L450-L513) 已实现多路融合与权重；[作者全文](https://arxiv.org/html/2610.16229v1)。

共同基础是模态提供的有效信息；P05 比较模态集合的额外贡献，下一项保持输入集合但改变内容质量，两者不等价。与缺失恢复问题也分开。

## P06 输入质量下降后，已有处理仍保留排序退化

- **问题与条件**：保持输入模态集合但降低其质量，相似关系增强或融合后的最终质量仍可能下降；不同方法的具体传导机制不假设相同。与 P05 改变模态集合的对象不同，所以同文保留第二项。
- **类型**：实验支持；不把不同扰动协议视为同一分布。
- **已处理/剩余**：所列方法都有增强/净化/多路融合缓解，指定受损条件下仍存在数值损失；未据此推广为真实部署必然失败。

### 来源与不同受损条件
- **OrthoRec §4.4/Fig.4**：训练和推理均视觉错配，30% 扰动下 Recall@20 仍相对下降 10.6%，LGMRec 为 11.6%。净化/路由降低损失但未消除；自然污染仍未验证，不称自然污染必败。代码 [`purify_modality/forward` L67–137](https://github.com/Camilla-jl/Orthorec/blob/631138035a562db09ac8931d113ff41d27db07dd/models/orthorec.py#L67-L137)；[正式大学记录](https://scholars.cityu.edu.hk/en/publications/beyond-modality-harmony-orthogonal-purification-and-topology-guid/)。
- **VI-MMRec §5.6/Table 5**：Baby、LGMRec+VI-O 的 R@10 从 .0681 降至最大高斯扰动/内容交换条件的 .0640。相似度增强已有缓解但不能消除受损输入影响；噪声生成脚本未核验。定位 [`build_virtual_interactions` L9–48](https://github.com/Jinfeng-Xu/Vi-MMRec/blob/b793b9076430e93d9ab8c3f475a212326907a19f/VI-MMRec.py#L9-L48)。[作者稿](https://arxiv.org/abs/2512.08702)。
- **I-LLMRec Appendix E.9/Table 9**：Amazon Sport 原低清图下，图像+CF+文本 Hit@5/NDCG@5 为 .4459/.3597，高清为 .4570/.3711；多路融合明显缓解但仍有数值差距，未据此声称统计显著。代码 [`eval.py::compute_rank` L179–202](https://github.com/rlqja1107/torch-I-LLMRec/blob/a778ec752233305a488ad3db28d8fec9ce4d82ba/ILLMRec/eval.py#L179-L202) 确实使用三路分数。[作者论文入口](https://arxiv.org/abs/2503.06238)。
- **TGQ-Former 作者稿 Appendix D.2/Table 9、D.4/Table 10**：人工背景/促销装饰 heavy 条件，完整模型 H@10 46.02→44.91，仍优于 NoteLLM-2 的 44.28。研究基于用户加购共现的 I2I 召回，并非最终用户个性化排序；论文模板仍有旧页眉，正式录用由 KDD 名单独立确认，所读作者稿与终稿未逐字比对。未找到官方代码。[作者稿入口](https://arxiv.org/abs/2605.17366)、[KDD 名单](https://kdd2026.kdd.org/papers/)。该条只作范围标明的补证，不单独计数。

这些证据共同支持受损输入下的条件性退化；数值扰动、物品内容错配、低清图和海报装饰各自保留，不能视为同一个噪声分布或互相比强弱。
