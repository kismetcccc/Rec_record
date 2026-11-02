# 小批优化仍重复承担全图或全热目录计算

## P29 batch 局部化没有消除训练步中的全局表示工作

**共同基础**：损失以mini-batch组织，但每步仍需全图/全目录中间表示。以下两条是同一训练规模问题的不同实现，不分别计数；不能统一写成N²注意力。

- **SRGFormer证据**：§IV-F/Fig.6、§IV-G承认大图训练负担。已简化Transformer组件，仍未免去非局部计算。Clothing输给FREEDOM不证明差距由规模单独造成，不用作因果证据。
- **SRGFormer源码**：[`_train_epoch` L141–146](https://github.com/HubuKG/SRGFormer/blob/c1d8082ceceb37e82bd247e707b67b47254b6476/common/trainer.py#L141-L146)逐batch调用；[`calculate_loss` L174–192](https://github.com/HubuKG/SRGFormer/blob/c1d8082ceceb37e82bd247e707b67b47254b6476/models/srgformer.py#L174-L192)先全forward再索引batch；[forward L111–146](https://github.com/HubuKG/SRGFormer/blob/c1d8082ceceb37e82bd247e707b67b47254b6476/models/srgformer.py#L111-L146)完整超边/全图表示。[GTLayer L24–43](https://github.com/HubuKG/SRGFormer/blob/c1d8082ceceb37e82bd247e707b67b47254b6476/models/GTlayer.py#L24-L43)实际按非零边，不采纳“指数复杂度”或dense attention推断。
- **SEMCo证据**：§3.2.1 Eq.(5–6)避免显式item-item相似矩阵，但§4.2.1末段仍指出全物品集用户构建的规模问题。
- **SEMCo源码**：[`train` L96–105](https://github.com/gmeehan96/SEMCo/blob/0ae1effb23ddac7339666c9af5324711aa909282/models/SEMCo.py#L96-L105)每batch调用；[`SEMCo_Learner.forward` L181–204](https://github.com/gmeehan96/SEMCo/blob/0ae1effb23ddac7339666c9af5324711aa909282/models/SEMCo.py#L181-L204)只截取用户行但仍编码全部warm items；教师[forward L322–345](https://github.com/gmeehan96/SEMCo/blob/0ae1effb23ddac7339666c9af5324711aa909282/models/SEMCo_online.py#L322-L345)也具有该范围。

**判断类型**：作者明确指出、代码观察；作者时间分析不是本轮计时。没有运行模型/压力测试，不声称特定OOM或实测延迟。

**状态/版本**：[SRGFormer官方代码](https://github.com/HubuKG/SRGFormer)、[TMM2026元数据](https://api.crossref.org/works/10.1109/TMM.2026.3673527)、[作者v1](https://arxiv.org/html/2511.00584v1)；SEMCo为SIGIR2026 short补证，正式状态见P28。均未逐字对读出版社终稿。

**为何不并入P13**：P13是离线dense预构图峰值；本项是优化步反复计算。也不同于P19在线agent推理及P23目录变化时重训。只按“规模”二字合并会丢失原因和发生环节。
