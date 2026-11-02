# 论文、正式状态与官方源码证据账

核验日：2026-11-02。下表是实际进入确认条目或其补证的论文。**正式录用证据不等于已经取得出版社终稿**；所读版本和受限情况明确区分。代码文件定位见对应问题文档，均未训练复现。

## 确认条目使用的来源

|简称及完整标题|正式状态证据与所读版本|官方仓库/核验范围|
|---|---|---|
|GMI：Training-Free Graph-Based Imputation of Missing Modalities in Multimodal Recommendation|TKDE 2026, 38(5):3250–3263，[DOI](https://doi.org/10.1109/TKDE.2026.3667005)。[作者状态页](https://arxiv.org/abs/2602.17354)明确 accepted，[卷期记录](https://dblp.org/rec/journals/tkde/MalitestaRPNM26)交叉核验。读作者 final version；IEEE详情页本次失败，不冒称已读取。|[官方代码](https://github.com/danielemalitesta/Graph-Missing-Modalities-TKDE)，已读 impute/mask/运行入口。|
|GRE-MC：Robust Multimodal Recommendation via Graph Retrieval-Enhanced Modality Completion|SIGIR 2026，946–957，[DOI](https://doi.org/10.1145/3805712.3809607)；[作者全文](https://arxiv.org/html/2605.00670v1)有会议信息，书目交叉核验；ACM详情访问受限。|未找到可核验官方实现；第三方 morel 不作为官方。|
|VI-MMRec：Similarity-Aware Training Cost-free Virtual User-Item Interactions for Multimodal Recommendation|KDD 2026，[大会名单](https://kdd2026.kdd.org/papers/)、[DOI](https://doi.org/10.1145/3770854.3780200)；读[作者稿](https://arxiv.org/abs/2512.08702)，2025预印本首发不改变2026正式归属。|[官方代码](https://github.com/Jinfeng-Xu/Vi-MMRec)，模型文件已读、仅静态解析。|
|MMWave：Tackling the Modality Inhibitance Effect with Wavelet-based Modality Integration in Multi-modal Recommendation|TKDE 2026，[DOI](https://doi.org/10.1109/TKDE.2026.3737154)；[出版社登记元数据](https://api.crossref.org/works/10.1109/TKDE.2026.3737154)确认年份，[作者全文](https://arxiv.org/html/2610.16229v1)已读。元数据创建日不当上线日期。|[官方代码](https://github.com/kennethorq/MMWave)，特征分解、建图、forward、loss已读。|
|OrthoRec：Beyond Modality Harmony: Orthogonal Purification and Topology-Guided MoE for Conflict-Aware Multimodal Recommendation|ACM MM 2026 已录用/in press；[大学正式记录](https://scholars.cityu.edu.hk/en/publications/beyond-modality-harmony-orthogonal-purification-and-topology-guid/)、[DOI](https://doi.org/10.1145/3767308.3836499)。读作者全文。会议尚未举行。|[官方代码](https://github.com/Camilla-jl/Orthorec)，净化、路由及SSL已读。|
|IIMRec：One Graph, Multiple Gains: Single High-Quality Item-Item Graph for Multimodal Recommendation|[作者声明](https://arxiv.org/abs/2607.24607)明确 Accepted by ACM MM 2026，camera-ready 有 [DOI](https://doi.org/10.1145/3767308.3836382)。**出版方/大会独立核验未完成**；仅作为预处理问题的作者确认来源补证，不单独据此增加确认数量。|[官方代码](https://github.com/Jinfeng-Xu/IIMRec)，建图/NCER已读，并独立复核条件分支。|
|CAMMSR：Category-Guided Attentive Mixture of Experts for Multimodal Sequential Recommendation|ICDE 2026 Research，[官方名单](https://icde2026.github.io/accepted-papers)第159项；读[作者全文 v1](https://arxiv.org/html/2603.04320v1)，未逐字核对出版社终稿。|未找到可核验官方代码；不猜文件定位。|
|HSD：Hierarchy-Aware Multimodal Distillation for Recommendation|TMM 2026, 28:2279–2290，[DOI](https://doi.org/10.1109/TMM.2026.3651049)，[出版社元数据](https://api.crossref.org/works/10.1109/TMM.2026.3651049)确认。全文未得，**仅使用可直接核验的发布工件问题**，不从摘要提出模型缺陷。|[官方代码](https://github.com/Tuo97/HSD)，README、数据占位、加载器已读。|
|MTS²-4MM：Three Minds, One Student: Online Multi-Teacher Knowledge Distillation for Multimodal Recommenders|IJCAI 2026 Main Track 3133–3141，[官方全文入口](https://ijcai.org/proceedings/2026/348)、[DOI](https://doi.org/10.24963/ijcai.2026/348)。作为扩展来源单列。|[官方代码](https://github.com/MICLab-Rec/MTS4MM)，损失及implementation notes已读。|
|SDA：Structural and Disentangled Adaptation of Large Vision Language Models for Multimodal Recommendation|SIGIR 2026 **short**，[官方名单](https://sigir2026.org/en-AU/pages/program/accepted-papers)、[DOI](https://doi.org/10.1145/3805712.3809977)、[大学记录](https://opus.lib.uts.edu.au/handle/10453/197181)。读[作者v2](https://arxiv.org/abs/2512.06883)；短文单列。|[官方代码](https://github.com/RaoZhongtao/SDA)，对比损失/梯度分析/适配器已读。|
|AdaM-Rec：Adaptive Modality Routing for Multimodal Recommendation|NeurIPS 2026 **已录用**，[官方目录](https://neurips.cc/Downloads/2026)，[作者论文入口](https://arxiv.org/abs/2609.38455)。会议尚未举行。|[官方代码](https://github.com/RomGai/AdaM-Rec)，调度及自适应融合已读。|
|I-LLMRec：Token-Efficient Item Representation via Images for LLM Recommender Systems|ICLR 2026，[官方目录](https://iclr.cc/Downloads/2026)、[作者发表列表](https://rlqja1107.github.io/publications/)。所读[作者版本](https://arxiv.org/abs/2503.06238)标Published as a conference paper at ICLR2026；预印本2025首发。|[官方代码](https://github.com/rlqja1107/torch-I-LLMRec)，表示/评分/训练恢复入口已读。|
|SynGR：Unleashing the Potential of Cross-Modal Synergy for Generative Recommendation|ICML 2026，[官方目录](https://icml.cc/Downloads/2026)指向poster/63723，[作者论文](https://arxiv.org/abs/2605.18920)已读。|[官方代码](https://github.com/gxingyu/SynGR)，使用作者README依赖警告，不声称重跑过。|
|HaNoRec：Multimodal Large Language Models with Adaptive Preference Optimization for Sequential Recommendation|SIGIR 2026 **full**，1903–1913，[官方名单](https://sigir2026.org/en-AU/pages/program/accepted-papers)、[DOI](https://doi.org/10.1145/3805712.3809590)。读[作者稿](https://arxiv.org/abs/2511.18740)，含正式页眉。|[官方代码](https://github.com/wangyu0627/HaNoRec)，难度计算/邻居选择已读。|
|CARD：Non-Uniform Quantization of Visual Semantic Unit for Generative Recommendation|SIGIR 2026 **full**，[官方名单](https://sigir2026.org/en-AU/pages/program/accepted-papers)、[DOI](https://doi.org/10.1145/3805712.3809538)；读[作者稿](https://arxiv.org/abs/2604.26427)含正式会议信息。|[官方代码](https://github.com/HAI-UESTC/CARD)，卡片渲染容量已读。|
|AMUR：Information-Guided Selective Modality-Interest Alignment for Multimodal Recommendation|CIKM 2026 **Full Research 已录用**，[官方议程](https://cikm2026.diag.uniroma1.it/program/)题名略缩，作者对应；[DOI](https://doi.org/10.1145/3799682.3840808)。读[作者v1](https://arxiv.org/html/2608.27950v1)。|[官方代码](https://github.com/Wenze1/AMUR)，共享选择及loss已读。扩展来源，不额外重复计同一对齐痛点。|
|BRIDGE：Behavior-Guided Residual Integration with Dual-Frequency Graph Evidence|CIKM 2026 **Full Research 已录用**，[官方议程](https://cikm2026.diag.uniroma1.it/program/)、[DOI](https://doi.org/10.1145/3799682.3840961)；读[作者v2](https://arxiv.org/html/2605.22073v2)，不用旧标题v1。|[官方代码](https://github.com/LIZESHENG13/bridge)，共用户证据与full_sort_predict已读。扩展来源。|
|TGQ-Former：Text-Guided Visual Representation Learning for Robust Multimodal E-Commerce Recommendation|KDD 2026 Research Track，[官方名单](https://kdd2026.kdd.org/papers/)、[DOI](https://doi.org/10.1145/3770855.3818176)。读[作者稿](https://arxiv.org/abs/2605.17366)，有旧模板页眉，未逐字对应终稿。|未找到官方源码；用户加购共现导出的I2I召回，非最终用户排序，作范围明确的补证。|

CIKM 2026、ACM MM 2026、NeurIPS 2026 均不因“2026”标签写成截至本次已举办。未找到仓库不等于仓库不存在；未获取全文不等于论文没有对应分析。

## 截止日前的代码快照

各问题页的代码链接固定 SHA，而非随时变化的 main。已核验的快照包括：GMI `1d760702…`、VI-MMRec `b793b907…`、MMWave `51e761d6…`、OrthoRec `63113803…`、IIMRec `b22a3691…`、HSD `9c0b2647…`、MTS4MM `4157dbb7…`、SDA `524cf2ab…`、AdaM-Rec `8ceb7f13…`、I-LLMRec `a778ec75…`、SynGR `60c76cb4…`、HaNoRec `587face7…`、CARD `b8ce0976…`、AMUR `d6d5f862…`、BRIDGE `4ee976f5…`。

示例已核验提交日期：IIMRec 2026-08-05、MTS4MM 2026-10-25、AdaM-Rec 2026-10-14、I-LLMRec 2026-05-20、SynGR 2026-08-12、OrthoRec 2026-09-03。快照日期只界定检查对象，不能代替论文出版年份。

## 检索覆盖及完整性边界

使用官方会议程序/论文集、出版元数据、作者主页、作者正文和官方 GitHub 交叉核验；多模态推荐综述/论文清单只作发现入口。全文访问受限者保留在 [待核验台账](PENDING_AND_EXCLUSIONS.md)，未用摘要或第三方总结代替实验。

已搜索的会议包含 SIGIR/WWW/KDD/AAAI/ICDE/ACM MM/ICLR/ICML/NeurIPS/RecSys，并扩展 CIKM/WSDM/IJCAI；期刊包含 TKDE/TOIS/TMM/TPAMI/TNNLS 与明确标注的 TORS/Information Fusion 等相邻来源。该覆盖是检索记录，不表示每个 venue 都找到可纳入痛点的全文，更不表示没有遗漏。


## 第二轮增量来源（2026-11-02，基于首轮621b529）

新增章节/实验层面检查与仅状态/源码检查严格分开，数量以[本轮记录](INCREMENT_20261102_02.md)为准。没有把重克隆算成新仓库，也没有把摘要检索算全文深读。

|工作|正式状态、读取版本|官方仓库与本次范围|
|---|---|---|
|UAT-MC：Band Together: Untargeted Adversarial Training with Multimodal Coordination Against Evasion-Based Promotion Attacks|[IJCAI2026官方全文](https://ijcai.org/proceedings/2026/347)，Main Track 3124–3132；新深读|[gmXian/UAT-MC](https://github.com/gmXian/UAT-MC)，8694273…，仅README占位，无可核验实现。|
|VENOMREC：Cross-Modal Interactive Poisoning for Targeted Promotion in Multimodal LLM Recommender Systems|[ICML2026正式PMLR306](https://proceedings.mlr.press/v306/guan26b.html)，37417–37433；读该页正式论文，不使用旧摘要代替|[GuoweiGuan666/VenomRec](https://github.com/GuoweiGuan666/VenomRec)，076ce68…，特征层接口及AE过滤实际静态检查。|
|TimeMM：Time-as-Operator Spectral Filtering for Dynamic Multimodal Recommendation|SIGIR2026 full，[DOI](https://doi.org/10.1145/3805712.3809616)及官方名单；读[作者v1](https://arxiv.org/html/2604.26247v1)|[llm-ml/TimeMM](https://github.com/llm-ml/TimeMM)，628a923…，时间构图、TRAIN选择及传播已读。|
|SEMCo：Sparse Contrastive Learning for Content-Based Cold Item Recommendation|SIGIR2026 short，[DOI](https://doi.org/10.1145/3805712.3809975)，读[作者v1](https://arxiv.org/html/2604.12990v1)；Electronics图文，Clothing仅文本不作本轮多模态依据|[gmeehan96/SEMCo](https://github.com/gmeehan96/SEMCo)，0ae1eff…，多模态编码/批训练/教师与用户聚合已读。|
|SRGFormer：Structurally Refined Graph Transformer for Multimodal Recommendation|[IEEE登记元数据](https://api.crossref.org/works/10.1109/TMM.2026.3673527)确认TMM28:7516–7528（2026）；[作者v1](https://arxiv.org/abs/2511.00584)称2025录用。**录用2025/正式卷期2026分别保留**，没有把元数据created当上线日；IEEE详情受验证限制|[HubuKG/SRGFormer](https://github.com/HubuKG/SRGFormer)，c1d8082…，训练循环、forward、边注意力及loss已读。|
|MARS：Modality-Aligned Retrieval for Sequence Augmented CTR Prediction|[IEEE正式Early Access](https://ieeexplore.ieee.org/abstract/document/11699087/)，2026-09-22，DOI10.1109/TKDE.2026.3735698；读[作者v2](https://arxiv.org/html/2509.01184v2)，未逐字对终稿。旧清单同缩写ICLR条目身份仍待核，不静默替换|[wangshukuan/MARS](https://github.com/wangshukuan/MARS)，4522c56…，多种PaddingStrategy已读；快照早于v2，不称即论文全部实验版。|
|MoToRec：Sparse-Regularized Multimodal Tokenization for Cold-Start Recommendation|[AAAI2026条目](https://ojs.aaai.org/index.php/AAAI/article/view/38558)、[大学正式记录](https://scholars.cityu.edu.hk/en/publications/motorec-sparse-regularized-multimodal-tokenization-for-cold-start/)；推进旧候选，读[作者v2](https://arxiv.org/abs/2602.11062v2)|未找到可核验可读取官方实现，候选仓库404不算已检官方代码。|
|MACRec：Multi-Aspect Cross-modal Quantization for Generative Recommendation|[AAAI2026条目](https://ojs.aaai.org/index.php/AAAI/article/view/38664)，[作者v2](https://arxiv.org/abs/2511.15122v2)；保守记全文重查，不冒称本轮首次发现/首次深读|[zhangfw123/MACRec](https://github.com/zhangfw123/MACRec)，7a48e74…，本轮补读RQ层、量化及对齐；仓库重查不计新仓库。|
|MAGE：Can Complementary Signals Bridge Similarity Islands? Manifold-Augmented Graph Embedding for Multimodal Recommendation|[NeurIPS2026官方程序](https://neurips.cc/virtual/2026/poster/155124)，已录用未举行；读[作者v1](https://arxiv.org/html/2610.37409v1)|[Alex-bupt/mage](https://github.com/Alex-bupt/mage)，9a1a16c…，增强、邻域及建图实际检查。|
|VBF++：Variational Bayesian Fusion with Context-Aware Priors and Recommendation-Guided Adversarial Refinement for Multimodal Video Recommendation|[AAAI2026条目](https://ojs.aaai.org/index.php/AAAI/article/view/38469)，40(17):14520–14528；官方首页关联仓库，**正文未完整取得，非全文深读**|[muhhpu/VBF](https://github.com/muhhpu/VBF)，852dfe6…，默认训练入口和辅助损失数据流实际检查；只作P34实现观察。|
|TMMSRec：Time-interval-aware Multi-Modal Sequential Recommender（TOIS2026）|[出版社元数据](https://api.crossref.org/works/10.1145/3827608)print2026-07-31、online2026-08-11；正文403，**只状态+代码检查**|[wangpp0602/TMMSRec](https://github.com/wangpp0602/TMMSRec)，f75f18f…，README/main/model/utils已读；仅补P16与待核验接口观察。|
|UniRec|第三方ICLR标签不采用；[正式OpenReview入口](https://openreview.net/forum?id=WXE255GWhQ)索引为TMLR04/2026。读作者arXiv2601.19423v2，正式稿逐字对应未核；**不进入核心新增痛点计数**|[ulab-uiuc/UniRec](https://github.com/ulab-uiuc/UniRec)，2fa0ad2…，item QFormer及user encoder已读。|

额外状态核验：CAMMSR新增[IEEE正式论文记录](https://ieeexplore.ieee.org/abstract/document/11629195)，DOI10.1109/ICDE65706.2026.00166，Date Added 2026-08-12；这是旧论文出版证据补充，不算新痛点或新深读。IIMRec原待补独立状态仍保留；本轮DOI/Crossref未成功返回，不据此声称其未录用。
