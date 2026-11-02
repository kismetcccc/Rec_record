# 2026 多模态推荐：有证据的痛点记录

检索截止：**2026-11-02**；时间窗口：**2026-01-01—2026-11-02**。

## 实际结果与计数口径

首轮记录 **24 项、15 份问题文档**。第二轮在实际读取首轮提交后，新增 **10 项**、补充旧条目证据，当前累计 **34 项、22 份问题文档**。新增明细见[第二轮增量记录](INCREMENT_20261102_02.md)。这些是有条件的问题与实现边界，不是同等数量的全新模型创新点。

- **28 项有核心会议/期刊来源支持**；另 **6 项仅由明确标注的补充来源支持**：P11/P28（SIGIR short）、P17/P25（IJCAI）、P20/P21（CIKM）。同一痛点的补充证据不重复计数。
- 按问题性质看：**27 项模型、数据表示或计算条件问题；1 项评估可比性条件（P14）；1 项诊断不足（P11）；5 项公开实现/复现边界（P15—P18、P34）**。这只是统计说明，不是检索前预设分类。
- IIMRec 只有作者明确录用声明与camera-ready信息，出版方独立核验尚未完成；它只补充 P13 的源码观察，P13 另有已确认 GMI/MMWave 支撑，不靠该待补状态增加数量。
- 待核验台账中的正文不足、正式状态不足、条件性风险或只有已解决动机的内容单列，**不计入确认数量**。

每项写明具体条件、影响、章节/图表、实际查看的源码位置、现有处理与残余、判断类型。没有运行训练，也没有设计模型、推荐模块或制定实验方案。

## 分组结果

以下分组是在收集证据后形成。一个文件可有多个不同子项，也允许单项独立。

|文档|痛点编号|数量|
|---|---|---:|
|[共交互图补全的供体相关性、冷启动支持与污染传播](01_behavior_graph_imputation.md)|P01、P02、P03|3|
|[高比例文本缺失下，补全仍有下游模型相关的恢复差距](02_missing_text_recovery.md)|P04|1|
|[模态额外贡献不足与已观测内容受损后的残余退化](03_contaminated_modality_contribution.md)|P05、P06|2|
|[扩大语义邻域引入偏好无关关系](04_semantic_neighbor_expansion.md)|P07、P08|2|
|[频域平滑深度过大时，有用细节可能随噪声被压掉](05_smoothing_detail_loss.md)|P09|1|
|[对齐强度与排序效用不一致，以及对齐效果的直接诊断不足](06_alignment_strength_and_diagnostics.md)|P10、P11|2|
|[类别错误监督造成模态权重误导](07_category_supervision_errors.md)|P12|1|
|[稀疏图输出与训练免费，不代表预处理没有密集矩阵开销](08_preprocessing_scale_cost.md)|P13|1|
|[删除缺失物品改变目录与评估人群，绝对指标不再同口径](09_catalog_comparison.md)|P14|1|
|[官方发布物的可解析性、输入工件与论文实现对应关系](10_release_reproducibility.md)|P15、P16、P17、P18、P34|5|
|[自适应模态路由增加在线推理复杂度](11_agentic_inference_cost.md)|P19|1|
|[共用户行为校准的证据精度与候选内作用范围](12_local_candidate_calibration.md)|P20、P21|2|
|[图像压缩表示之外，文本独有且推荐相关的细节仍难充分提取](13_text_unique_information.md)|P22|1|
|[目录和用户扩张时，旧模型质量与周期重训成本的取舍](14_catalog_growth_retraining.md)|P23|1|
|[图文渲染为视觉语义单元时，人工版式决定可保留的信息](15_visual_unit_layout_capacity.md)|P24|1|
|[有意图文操纵下的促销防御取舍与训练污染曝光残余](16_adversarial_defense_accuracy.md)|P25、P26|2|
|[时间条件传播依赖正确的交互时间次序](17_temporal_metadata_corruption.md)|P27|1|
|[冷物品曝光均衡，不等于成功命中覆盖充分](18_cold_item_success_coverage.md)|P28|1|
|[小批优化仍重复承担全图或全热目录计算](19_per_step_global_training_work.md)|P29|1|
|[相似用户行为补齐策略依赖交互密度与行为可复用性](20_donor_sequence_completion.md)|P30|1|
|[图文离散表示的token容量与稀疏惩罚：两种不同边界](21_discrete_representation_limits.md)|P31、P32|2|
|[完整特征的离线互补增强，不能保证跨骨干直接受益](22_augmented_feature_transfer.md)|P33|1|

## 全部去重条目

|编号|具体问题|文档|
|---|---|---|
|P01|图同质性不能作为跨下游模型通用的补全收益保证|[01](01_behavior_graph_imputation.md)|
|P02|冷启动或极少交互使补全缺乏结构支持|[01](01_behavior_graph_imputation.md)|
|P03|已观测供体受污染时，补全可传播错误内容|[01](01_behavior_graph_imputation.md)|
|P04|缺失文本的信息不能稳定恢复到完整输入水平|[02](02_missing_text_recovery.md)|
|P05|新增模态不保证带来稳定的额外收益|[03](03_contaminated_modality_contribution.md)|
|P06|输入质量下降后，已有处理仍保留排序退化|[03](03_contaminated_modality_contribution.md)|
|P07|更多相似物品不一定提供更多有效推荐信号|[04](04_semantic_neighbor_expansion.md)|
|P08|相似邻居规模失衡会扭曲偏好优化的难度估计|[04](04_semantic_neighbor_expansion.md)|
|P09|平滑收益依赖数据，深分解并非单调更好|[05](05_smoothing_detail_loss.md)|
|P10|增强一致性不保证增强推荐质量|[06](06_alignment_strength_and_diagnostics.md)|
|P11|推荐效果和梯度协调不能替代直接的表示对齐量化|[06](06_alignment_strength_and_diagnostics.md)|
|P12|用于分配模态权重的错误类别监督，比缺失类别更易误导推荐|[07](07_category_supervision_errors.md)|
|P13|大目录的密集预构图资源需求与规模相关退化路径|[08](08_preprocessing_scale_cost.md)|
|P14|删除与补全协议的样本空间不同|[09](09_catalog_comparison.md)|
|P15|官方模型文件存在静态解析阻断|[10](10_release_reproducibility.md)|
|P16|公开代码依赖的实际数据划分/映射未随快照提供|[10](10_release_reproducibility.md)|
|P17|论文蒸馏目标与当前实现的定义不等价|[10](10_release_reproducibility.md)|
|P18|生成式推荐器对上游依赖版本敏感，跨版本结果不直接可比|[10](10_release_reproducibility.md)|
|P19|质量提升伴随尚未消除的 agentic 推理成本|[11](11_agentic_inference_cost.md)|
|P20|稀少重叠或突发局部交互削弱行为校准证据|[12](12_local_candidate_calibration.md)|
|P21|基础候选未覆盖的物品不能获得直接残差校准|[12](12_local_candidate_calibration.md)|
|P22|视觉重叠内容掩盖了文本真正有用的补充|[13](13_text_unique_information.md)|
|P23|已有推荐器能用于新目录，但质量保持仍有训练成本|[14](14_catalog_growth_retraining.md)|
|P24|结构化卡片的字段容量会截断超长内容|[15](15_visual_unit_layout_capacity.md)|
|P25|协调式对抗训练降低攻击收益，但未消除残余促销与准确率代价|[16](16_adversarial_defense_accuracy.md)|
|P26|跨模态训练污染可在常规过滤后保留定向曝光|[16](16_adversarial_defense_accuracy.md)|
|P27|时间戳顺序失真后，已自适应的传播仍退化|[17](17_temporal_metadata_corruption.md)|
|P28|已改善曝光分布的模型仍有大量冷物品零成功命中|[18](18_cold_item_success_coverage.md)|
|P29|batch 局部化没有消除训练步中的全局表示工作|[19](19_per_step_global_training_work.md)|
|P30|更多供体或更精细子序列选择，并非跨数据稳定增益|[20](20_donor_sequence_completion.md)|
|P31|码本或语义ID变大后，可学性未随容量单调增加|[21](21_discrete_representation_limits.md)|
|P32|固定码本下增强稀疏惩罚，对低交互物品更敏感|[21](21_discrete_representation_limits.md)|
|P33|只替换增强特征时，迁移收益仍依赖数据和推荐器|[22](22_augmented_feature_transfer.md)|
|P34|辅助损失被标量化，数值加入总损失但直接梯度路径已断开|[10](10_release_reproducibility.md)|

## 分组判断的几个关键区别

- 补全的同质性收益、冷启动结构支持、供体污染共享传播路径，但成因不同，同文分项；文本缺失恢复结果不被强行归因于其中某一个。
- 新增模态的边际贡献和原有输入质量下降不是同一比较条件，同文分项；不同污染协议不逐个凑数。
- 邻域范围既可影响虚拟交互，也可影响DPO难度估计，共同基础明确、作用环节不同，同文分项。
- 离线预构图资源、在线agentic推理、目录增长重训的成因和时间环节不同，分别保存。
- 语法错误、输入工件缺失、论文代码差异、依赖版本敏感、辅助损失梯度路径同属复现发布物，但不是同一个原因，保留五个子项。

## 核验资料与限制

- [方法、范围与判断规则](METHODOLOGY.md)
- [论文正式状态、版本与官方代码账](SOURCES.md)
- [待核验、已解决动机与排除台账](PENDING_AND_EXCLUSIONS.md)

优先提供官方 GitHub 及固定提交代码定位；必要的论文状态/HTML页面用于核验，没有提供PDF下载链接。数字均是论文报告，不冒称本轮复现。未找到可核验官方源码时明确注明；没有以“代码缺某模块”推导模型缺陷。

未声称穷尽领域。公开全文可访问性、官方代码完整性及正式版本对应关系会限制结论范围。未来出版或截止日后的变化不在本次结论内。
