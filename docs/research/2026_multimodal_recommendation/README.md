# 2026 多模态推荐：有证据的痛点记录

检索截止：**2026-11-02**；时间窗口：**2026-01-01—2026-11-02**。

## 实际结果与计数口径

本轮得到 **24 个去重后的条件性痛点，归为 15 份问题文档**。这是证据支持的问题与适用边界，不是“24个全新未解决模型创新点”。

- **20 项有核心会议/期刊来源支持**；另 **4 项仅由明确标注的补充来源支持**：P11（SIGIR short）、P17（IJCAI）、P20/P21（CIKM）。同一痛点的补充证据不重复计数。
- 按问题性质看：**18 项模型、数据表示或计算条件问题；1 项评估可比性条件（P14）；1 项诊断不足（P11）；4 项公开实现/复现边界（P15—P18）**。这只是统计说明，不是检索前预设分类。
- IIMRec 只有作者明确录用声明与camera-ready信息，出版方独立核验尚未完成；它只补充 P13 的源码观察，P13 另有已确认 GMI/MMWave 支撑，不靠该待补状态增加数量。
- 待核验台账中的正文不足、正式状态不足、条件性风险或只有已解决动机的内容单列，**不计入24项**。

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
|[官方发布物的可解析性、输入工件与论文实现对应关系](10_release_reproducibility.md)|P15、P16、P17、P18|4|
|[自适应模态路由增加在线推理复杂度](11_agentic_inference_cost.md)|P19|1|
|[共用户行为校准的证据精度与候选内作用范围](12_local_candidate_calibration.md)|P20、P21|2|
|[图像压缩表示之外，文本独有且推荐相关的细节仍难充分提取](13_text_unique_information.md)|P22|1|
|[目录和用户扩张时，旧模型质量与周期重训成本的取舍](14_catalog_growth_retraining.md)|P23|1|
|[图文渲染为视觉语义单元时，人工版式决定可保留的信息](15_visual_unit_layout_capacity.md)|P24|1|

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

## 分组判断的几个关键区别

- 补全的同质性收益、冷启动结构支持、供体污染共享传播路径，但成因不同，同文分项；文本缺失恢复结果不被强行归因于其中某一个。
- 新增模态的边际贡献和原有输入质量下降不是同一比较条件，同文分项；不同污染协议不逐个凑数。
- 邻域范围既可影响虚拟交互，也可影响DPO难度估计，共同基础明确、作用环节不同，同文分项。
- 离线预构图资源、在线agentic推理、目录增长重训的成因和时间环节不同，分别保存。
- 语法错误、输入工件缺失、论文代码差异、依赖版本敏感同属复现发布物，但不是同一个原因，保留四个子项。

## 核验资料与限制

- [方法、范围与判断规则](METHODOLOGY.md)
- [论文正式状态、版本与官方代码账](SOURCES.md)
- [待核验、已解决动机与排除台账](PENDING_AND_EXCLUSIONS.md)

优先提供官方 GitHub 及固定提交代码定位；必要的论文状态/HTML页面用于核验，没有提供PDF下载链接。数字均是论文报告，不冒称本轮复现。未找到可核验官方源码时明确注明；没有以“代码缺某模块”推导模型缺陷。

未声称穷尽领域。公开全文可访问性、官方代码完整性及正式版本对应关系会限制结论范围。未来出版或截止日后的变化不在本次结论内。
