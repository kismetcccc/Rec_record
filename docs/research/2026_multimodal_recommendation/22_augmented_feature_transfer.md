# 完整特征的离线互补增强，不能保证跨骨干直接受益

## P33 只替换增强特征时，迁移收益仍依赖数据和推荐器

- **条件/影响**：MAGE把离线增强特征交给其他骨干，保持其架构、建图和目标不变；相同增强在部分数据/骨干上没有增益。
- **证据**：Appendix D.1/Table 7，Baby R@20：GUME .1042→.1034，MGCN .0964→.0956，MENTOR .1048→.1030；Sports/Clothing为正。Baby部分R@10反而小增，不能称全指标退化，也不能擅自宣称统计显著。
- **已处理/残余**：MAGE完整双流设计已改善similarity-islands动机；这里仅是作者展示的离线特征迁移边界。作者没有隔离“稀疏/共购噪声”等解释，不把猜测写成原因已证。
- **类型**：实验支持、作者明确指出；未复现。
- **代码**：[官方MAGE](https://github.com/Alex-bupt/mage)，SHA `9a1a16c2734ed1f35f0ea175b3bab8eb21fe3348`；[`AdvancedPaCE.process_vector` L89–127](https://github.com/Alex-bupt/mage/blob/9a1a16c2734ed1f35f0ea175b3bab8eb21fe3348/stage1_process.py#L89-L127)局部SVD/残差；[`main` L212–275](https://github.com/Alex-bupt/mage/blob/9a1a16c2734ed1f35f0ea175b3bab8eb21fe3348/stage1_process.py#L212-L275)分组注入。代码不提供跨骨干收益保证，失败判断来自表格。
- **状态/版本**：[NeurIPS2026官方程序](https://neurips.cc/virtual/2026/poster/155124)，已录用、尚未开会；读[作者v1](https://arxiv.org/html/2610.37409v1)。

**不并入旧条目的原因**：P01是缺失补全的同质性收益；这里已有完整内容。P05改变模态集合，这里集合不变；P07改变邻域范围，这里保持骨干只替换特征。仅“下游依赖”同词不足以强行合并。
