# MiniMax-M2.5模型简介

MiniMax-M2.5模型采用GQA + MoE结构，总参数量为229B，推理时激活的参数为10B。从M1到M2，MiniMax重新采用了Full Attention机制，M2.5的架构则与M2保持一致。

效果：在 SWE-Bench Verified、Multi-SWE-Bench和BrowseComp（含上下文管理）等评测中分别取得了80.2%、51.3%和76.3%的高分。

性能：SWE-Bench Verified评测的速度比M2.1快37%，与Claude Opus 4.6的速度相当。

架构特点：
- Attention模块：
  - 采用partial rope计算位置编码
  - 使用QK RMSNorm
  - GQA模式
- MoE模块:
  - 均采用独立专家，单token仅8个专家计算
  - router计算训练时引入jitter噪声，采用sigmoid以及routing bias计算（类似于Deepseek V3）
- 输出接MTP模块
- 支持序列长度200k

## 整体架构

<p align="center">
  <img src="minimax_m_2_5_architecture.jpg" alt="MiniMax-M2.5架构图" />
</p>

## 相关资料：

- [整体介绍（官方博客）](https://github.com/MiniMax-AI/MiniMax-M2.5)
- [模型配置文件](https://huggingface.co/MiniMaxAI/MiniMax-M2.5/blob/main/config.json)
- [Transformer模型定义](https://github.com/huggingface/transformers/blob/main/src/transformers/models/minimax_m2/modeling_minimax_m2.py)
