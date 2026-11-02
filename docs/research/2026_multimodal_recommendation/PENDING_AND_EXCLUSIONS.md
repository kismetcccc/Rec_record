# 待核验、适用边界与明确排除

**全部不计入确认痛点数量。** 这些条目不是可直接采用的研究空白，也不是执行实验或改代码的计划。缺证据的具体位置被保留，避免把猜测写成结论。

## 一、有具体观察，但不足以证明论文性能缺陷

|条目|已经看到的内容|不能下的结论|
|---|---|---|
|SG-URInit 跨 split 数据流|[官方仓库](https://github.com/Jinfeng-Xu/SG-URInit)快照 `c85cb6d75b7fec75a8329ef4d0d10197dd992c7d`，`preprocessing/preprocess_agg.py` L34–58 读交互表无 split 过滤，后续 dataset 按0/1/2拆分，模型加载聚合特征；[SIGIR正式DOI](https://doi.org/10.1145/3805712.3809623)|未取得实际数据/缓存生成记录/论文运行版本，不能断言论文发生泄漏或指标虚高。|
|GMI 零共现/零邻居细节|`impute.py` top-k 后未筛零共现；某些缺失邻居可能参与均值|没有数据触发和效果证据，不确认为性能缺陷。对角填首元素也可能在恒度top-k条件成立，不能直接称归一化bug。|
|SiMGR 的显式评分要求|[AAAI正式条目](https://ojs.aaai.org/index.php/AAAI/article/view/38547)；[代码calculate_loss](https://github.com/DRec4AI/SiMGR2025/blob/e0de90a131fe366b5702727b80db4a5fac628dad/src/models/simgr.py#L438-L465)读rating并与用户阈值比较|说明当前阈值需要评分输入，不证明纯点击场景实测失败。显式反馈语义已经被方法处理。|
|GRE-MC 双缺失条件|§5.1 至少保留一个模态；GMI可以同时遮蔽图文|只说明两个任务条件不同，不证明GRE-MC双缺失必败，也不凭同一缺失率跨论文排序。|
|OrthoRec 自然污染|作者明确将自然损坏留待研究；已有合成视觉错配测试|没验证自然污染，不等于已经证明自然污染必然失败。确认项只采用已报告受损条件。|
|MGR 正式短文与旧长稿对应|正式SIGIR题名为 Beyond Unimodal Perspectives: Generative Retrieval with Multimodal Semantics，[DOI](https://doi.org/10.1145/3805712.3809844)；所读[旧长稿](https://arxiv.org/abs/2503.23333)名为 Beyond Unimodal Boundaries|旧稿的早融合模态主导和语义ID衔接实验未逐项对应正式短稿，不能当正式版已核验证据。其晚融合改进已处理部分问题。|
|MLLMRec 修订版|[官方代码](https://github.com/Yuzhuo-Dang/MLLMRec)明确对应2026-09的[arXiv v3](https://arxiv.org/abs/2508.15304)，[SIGIR正式DOI](https://doi.org/10.1145/3805712.3809749)|不能把v3数字说成会议相机版数字；固定k噪边/行为共现遗漏已被阈值及行为图处理，不再包装成完整方法未解。|

## 二、相邻来源的作者风险或范围边界

- **LEMUR（CIKM Applied，官方录用）**：[官方议程](https://cikm2026.diag.uniroma1.it/program/)，[作者全文](https://arxiv.org/html/2511.10962v2)。§4.1.1 实际编码 title/OCR/ASR/cover OCR 文本，是多模态内容文本化，不冒称已检查直接图像张量。§4.6.3/Table 4 的完全计算与采样缓存有计算/QAUC取舍；§5提到陈旧及长尾覆盖风险。未核验官方源码，采样同时改变前后向，不能把全部指标差额因果归于陈旧。因输入范围和尾部实证不足，单列，不加入直接图文核心计数。
- **MMQ（WSDM 2026 Research）**：[官方论文集目录](https://www.sigweb.sigweb.hosting.acm.org/toc/wsdm26a.html)，[DOI](https://doi.org/10.1145/3773966.3777923)，[作者全文](https://arxiv.org/html/2508.15281v1)。§6承认两阶段复杂度、模态专家数据需求和行为微调的任务特化风险；后两项未有低资源/跨任务失败量化。没有找到官方代码；不将这些条件性风险当已经证实的实际退化。§4.5将机制迁到RQ-VAE不等于已验证微调tokenizer跨任务无损复用。
- **Tlow（CIKM Applied，官方录用）**：[官方代码](https://github.com/wjjln/Tlow)，[作者全文](https://arxiv.org/html/2608.24176v1)。已读 `tokenizer/TextGlow.py`、`train.py`。§3.4.2/Table 5支持所测图文推荐的量化改进，但不能将作者已处理的错位再列未解；存在量化诊断，不得凭猜测说源码没有。未独立测latency不是已知性能故障。

## 三、已发现但正文、代码或正式状态仍不充分的论文

|候选|已核实/来源入口|未用于确认痛点的原因|
|---|---|---|
|DAMPS，KDD2026|[大会名单](https://kdd2026.kdd.org/papers/)，[DOI](https://doi.org/10.1145/3770854.3780208)|全文及官方代码未核验，不能只用摘要。|
|MSCA，WWW2026|[正式名单](https://www2026.thewebconf.org/accepted/research-tracks.html)，[官方代码](https://github.com/recomall/MSCA)，[DOI](https://doi.org/10.1145/3774904.3792192)|源码已读，全文访问受限；未确认残余。|
|TargetMR，WWW2026|[作者仓库](https://github.com/gutang-97/TargetMR/)，[DOI](https://doi.org/10.1145/3774904.3792466)|仓库仅README，全文未得，不说已有开源实现。|
|Drifting with Intent，WWW2026|[DOI](https://doi.org/10.1145/3774904.3792375)，大会名单确认|全文/源码未核验。|
|RecCLIP，WWW2026|[官方代码](https://github.com/jinliwei-1/RecCLIP)，[DOI](https://doi.org/10.1145/3774904.3792523)|交互矩阵视觉化是否符合真实物品图文范围仍需明确。|
|PNGRec，SIGIR2026|[官方代码](https://github.com/orangeheyue/PNGRec)，[DOI](https://doi.org/10.1145/3805712.3809608)|全文访问受限，不以摘要认定残余。|
|DIGEST，SIGIR2026|[DOI](https://doi.org/10.1145/3805712.3809642)|全文及官方源码未核验。|
|QAMR-CRS，RecSys2026 short|[官方程序](https://programs.sigchi.org/recsys/2026/program/content/270623)|未取得充分正文证据；短文不冒充长文。|
|SGP4SR，AAAI2026|[正式条目](https://ojs.aaai.org/index.php/AAAI/article/view/38528)，[官方代码](https://github.com/changhongli1/SGP4SR)|代码已读，正文访问受限；动机已有缓解。|
|DHMRec，AAAI2026|[正式条目](https://ojs.aaai.org/index.php/AAAI/article/view/38661)，[作者仓库](https://github.com/cheer-io/DHMRec)|只见论文附件，无源码；不能标为开源实现。|
|SCALE，AAAI2026|[正式条目](https://ojs.aaai.org/index.php/AAAI/article/view/38533)|没有可核验官方源码及完整残余证据。|
|M²VAE，AAAI2026|[正式条目](https://ojs.aaai.org/index.php/AAAI/article/view/38501)，[官方代码](https://github.com/chuanhe1999/M2VAE)|图像/类别属性/交互，非标准图文输入；未完成残余核验。|
|MACRec，AAAI2026|[正式条目](https://ojs.aaai.org/index.php/AAAI/article/view/38664)，[官方代码](https://github.com/zhangfw123/MACRec)|语义冲突已被作者方法处理，不只据动机新增。|
|MoToRec，AAAI2026|[正式条目](https://ojs.aaai.org/index.php/AAAI/article/view/38558)|全文残余和源码未核验。|
|DASGRec，ACM MM2026|[官方技术日程](https://2026.acmmm.org/site/technical-programme.html)|只有程序线索，完整证据不足。|
|LoCroMI，TOIS2026|[DOI](https://doi.org/10.1145/3831682)、[出版社元数据](https://api.crossref.org/works/10.1145/3831682)：online 08-26、print 09-30；[官方仓库](https://github.com/ZhuoxinHe/LoCroMI)|未获取可读全文；README不能证明残余模型局限。|
|Adaptive Graph Convolution With Diffusion Models for Multimodal Recommendation，TKDE2026|[出版社元数据](https://api.crossref.org/works/10.1109/TKDE.2026.3706381)print=2026-09，[IEEE记录](https://ieeexplore.ieee.org/document/11575085)|全文与官方代码未核验；created=06-23不当首次上线日。|
|LETTER，Self-Harmonized Representation Learning for Multimodal Recommendation|[DOI](https://doi.org/10.1109/TMM.2025.3623549)，元数据print=2026、created=2025-10-20|首次在线与卷期边界、全文及官方源码未完全核验。|
|NLGCL+，TORS2026|[DOI元数据](https://api.crossref.org/works/10.1145/3806231)online=03-31，[官方代码](https://github.com/Jinfeng-Xu/NLGCL-Plus)|全文未得，不把RecSys2025原文当2026扩展版。|
|LOBSTER，Information Fusion 127B (2026)|[出版社页](https://www.sciencedirect.com/science/article/pii/S1566253525008401)，[官方代码](https://github.com/Jinfeng-Xu/LOBSTER)|2025 online/2026卷期应区分；全文实验未核验，不称同级顶刊。|
|A Comprehensive Survey on Multimodal Recommender Systems，TPAMI2026|[记录](https://pubmed.ncbi.nlm.nih.gov/42406655/)，[DOI](https://doi.org/10.1109/TPAMI.2026.3710585)|最终作者列表与旧arXiv版本不同；终版正文未核验，不混用旧综述细节。|
|LASER、KG-ARMM，CIKM2026|[官方议程](https://cikm2026.diag.uniroma1.it/program/)，分别Applied/Full|全文和官方代码未找到；不把摘要数字当完整证据。|
|When Modalities Go Missing: Early Fusion for Multimodal Recommendation，WSDM2026 short|[DOI](https://doi.org/10.1145/3773966.3779385)，1094–1098|全文/官方代码未核验。|
|CaIRec、MLLMRec-R1|[CaIRec预印本](https://arxiv.org/abs/2607.26720)，[MLLMRec-R1源码](https://github.com/wangyu0627/MLLMRec-R1)|未取得正式录用证据，不按顶会已发表收录。|
|MARS|OpenReview所见仍是Submitted to ICLR2026|提交状态不等于录用；没有完成状态链，不计入。|

## 四、排除的年份或任务范围错配

- FUMMER：实际 [IPM 2024 出版社记录](https://www.sciencedirect.com/science/article/pii/S0306457324001365)，不是 TOIS2026。
- Causality-Inspired Fair Representation Learning for Multimodal Recommendation：[作者列表](https://www.comp.hkbu.edu.hk/~lichen/Publications.html)为 TOIS43(6), **2025**。
- IISAN-Versa：[官方仓库](https://github.com/GAIR-Lab/IISAN)标 TKDE2025；2026仓库更新不改论文年份。
- Enhancing Robustness and Generalization Capability ... via Sharpness-Aware Minimization：TKDE2025，[作者列表](https://jinfeng-xu.github.io/)；2026机构入库不等于2026论文。
- PerVRA：[作者页面](https://rlqja1107.github.io/publications/)标 WACV2027，排除出2026正式论文池。
- Modality-Mix Learning 等通用多模态任务，没有直接推荐证据，不收录。
- [A reproducibility study of multimodal embeddings for recommender systems](https://github.com/GAIR-Lab/MKF4MMRec)属于 IJMIR2026 扩展来源，本轮未据其摘要计数；不自行称顶刊。

## 五、未据此增加痛点的“已解决动机”

SG-URInit 的随机用户初始化差异、MLLMRec 的固定 kNN 低相似边、MTS² 的简单共享融合模态受压制、Tlow/MMQ 的原始量化错位等，都有对应处理。除非另有残余证据，不能把论文引言直接变成“当前仍无人解决”的结论。
