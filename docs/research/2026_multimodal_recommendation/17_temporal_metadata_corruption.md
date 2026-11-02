# 时间条件传播依赖正确的交互时间次序

## P27 时间戳顺序失真后，已自适应的传播仍退化

- **问题/条件**：保持交互身份，改变其时间次序或抹去时间差，TimeMM 的近期性边权不再含原有信息，排序质量下降。对象是交互时间元数据，不是 P06 图文内容污染。
- **证据**：TimeMM §5.4/Table 3，CD R@20 原始 .1049、用户内打乱 .0869、常数时间 .0961、轻度 jitter .1018；Game .0986→.0806（打乱）。不能把模拟破坏当真实日志错误率。
- **已处理/残余**：时间核、尺度混合和模态路由已处理静态时间假设，仍依赖有意义的时间顺序；不重新提出“方法没有时间建模”。
- **类型**：实验支持、作者解释；代码观察定位传导路径，未复现表格，未核验扰动脚本。
- **代码**：[官方 TimeMM](https://github.com/llm-ml/TimeMM)，SHA `628a923d27ac3228abf4f3207ba17012a581b66d`。[`build_edge_time_vars_from_train_df` L55–92](https://github.com/llm-ml/TimeMM/blob/628a923d27ac3228abf4f3207ba17012a581b66d/src/models/time_edge_weight_builder_multiscale.py#L55-L92)取训练时间anchor和age；[边权 L115–153](https://github.com/llm-ml/TimeMM/blob/628a923d27ac3228abf4f3207ba17012a581b66d/src/models/time_edge_weight_builder_multiscale.py#L115-L153)构造多尺度权重；[`TIMEMM.__init__` L130–163](https://github.com/llm-ml/TimeMM/blob/628a923d27ac3228abf4f3207ba17012a581b66d/src/models/timemm.py#L130-L163)有split标签时仅取TRAIN，不误报全分割构图。
- **正式状态**：SIGIR 2026 full，[官方名单](https://sigir2026.org/en-AU/pages/program/accepted-papers)、[DOI](https://doi.org/10.1145/3805712.3809616)；读[作者v1](https://arxiv.org/html/2604.26247v1)，未逐字比较终稿。

独立于滤波深度 P09：这里改变时间信息的可信度，不是增加平滑深度。
