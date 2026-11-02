# 删除缺失物品改变目录与评估人群，绝对指标不再同口径

## P14 删除与补全协议的样本空间不同
- **问题、条件、影响**：删除缺图/缺文物品同时改变交互、物品目录与评估对象；绝对 Recall 的变化不能直接解释为补全效果。
- **证据**：GMI Introduction/Fig.1、VI-A/Table II 明确将 dropped 与 imputed 视为不同数据集。
- **已处理/剩余**：GMI 在各自协议内比较多模态相对协同模型的增益，已经意识到并处理比较问题；不同目录的绝对分数仍不能因此直接横比。本项不是指控作者评价不公平。
- **类型**：作者明确指出、实验支持。
- **代码**：[官方仓库](https://github.com/danielemalitesta/Graph-Missing-Modalities-TKDE)，[`run_dropped.py`](https://github.com/danielemalitesta/Graph-Missing-Modalities-TKDE/blob/1d7607027f6b52ca48281aec67fb542f96a6978e/run_dropped.py)、[`run_multimodal.py`](https://github.com/danielemalitesta/Graph-Missing-Modalities-TKDE/blob/1d7607027f6b52ca48281aec67fb542f96a6978e/run_multimodal.py) 定位两协议入口；实质判断来自正文，不凭文件名下结论。[作者论文状态页](https://arxiv.org/abs/2602.17354)。

这是数据与比较对象问题，与补全的表示误差不同，单独保存。
