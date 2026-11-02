# 自适应模态路由增加在线推理复杂度

## P19 质量提升伴随尚未消除的 agentic 推理成本
- **问题与条件**：按用户/query 生成代理任务、判断模态可靠性并路由，增加在线处理复杂度；与离线建图资源不是同一环节。
- **证据**：AdaM-Rec §4.4 Discussion/Limitations 明确承认额外计算成本和推理效率问题；Fig.3 的候选预算影响质量，但不是实际延迟测量。
- **已处理/剩余**：已按 query 自适应分配文本/多模态召回预算；尚未消除 agentic 工作流开销。不能写成已测量的生产 SLA 失败。
- **类型**：作者明确指出。源码静态观察不用于推测实际延迟或调用次数。
- **官方来源**：[AdaM-Rec 仓库](https://github.com/RomGai/AdaM-Rec)、[作者主页](https://romgai.github.io/)、[NeurIPS 2026 官方名单](https://neurips.cc/Downloads/2026)。截至 11 月 2 日为已录用，不声称会议已举办。

**已读代码**：[`run_pipe.py::_adaptive_embedding_fusion` L584–602](https://github.com/RomGai/AdaM-Rec/blob/8ceb7f13f1e192af4e8dda3fb814b1a8b9067baf/run_pipe.py#L584-L602)，同文件 `run` L1097 起调度；L1351 融合，L1408/1434 构建历史与候选 profile，L1453 调用排序。证明多阶段路径存在，不测算线上耗时。[作者论文入口](https://arxiv.org/abs/2609.38455)。
