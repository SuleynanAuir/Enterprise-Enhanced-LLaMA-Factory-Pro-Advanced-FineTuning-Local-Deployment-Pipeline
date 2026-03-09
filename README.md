# 🚀 Enterprise-Enhanced LLaMA Factory Pro: Advanced Fine-Tuning & Local Deployment Pipeline
![LLaMA Factory](assets/logo.png)

<p align="center">
  <img src="https://img.shields.io/badge/LLM-Fine--Tuning-blue"/>
  <img src="https://img.shields.io/badge/AutoDL-red"/>
  <img src="https://img.shields.io/badge/EasyDataset-Data-Augmentation-yellow"/>
  <img src="https://img.shields.io/badge/Serving-Ollama%20%7C%20llama.cpp-orange"/>
  <img src="https://img.shields.io/badge/Training-QLoRA%20%7C%20QLoRA%20%7C%20DPO-green"/>
  <img src="https://img.shields.io/badge/Serving-Ollama%20%7C%20llama.cpp-orange"/>
</p>

<p align="center">
  <a href="./README_CN.md"><img alt="中文" src="https://img.shields.io/badge/Language-%E4%B8%AD%E6%96%87-red"/></a>
  <a href="./README_EN.md"><img alt="English" src="https://img.shields.io/badge/Language-English-blue"/></a>
</p>

## 😈 1. 项目改进：

- 🔥 完整 `一键部署-LLM工程化` Pipeline (LLaMA Factory Pro++)
  - 增强原有 LLaMa Factory 微调体系的部署效率
  
- 💻 云平台 AutoDL `托管云端数据存储 + 训练` (AutoDL)
  
- 👍 利用 `EasyDataset` 进行数据增强全流程pipeline
  - 支持私有数据 (`private data`) 直接进行加载 + 增强
  - 自动识别多模态文件 + 生成高质量、高相关性【问题+答案】pair + 全文推理逻辑链训练
 
- ⚡️ 支持多 GPU / 多显存优化
  - 单机多卡 / 多卡多机部署
  
- 🤖 可直接扩展 RAG & Agent 应用


---

## 🌟 2. 项目定位

### LLMs 微调全链路
本项目提供一条可落地的 **LLM 全流程工程链路**：

1. 数据采集、清洗、增强与标准化注册
2. 高效微调（LoRA / QLoRA / DPO）
3. 模型导出与量化（HF → GGUF）
4. 本地/边缘部署（Ollama / llama.cpp）
5. 可扩展 RAG + Agent 业务能力

该项目同时强调：
- 可展示从数据到部署的端到端工程负责
- **业务价值**：兼顾效果、时延、成本与可维护性

### 🛣️ 后续增强路线 (on process)

1. 增加自动化评测（任务效果 + 安全 + 回归）
2. 增加 CI 冒烟测试（训练/推理）
3. 增加 API 网关、鉴权与限流
4. 增加监控看板（时延、Token、错误率）


---

## 🧩 3. 典型业务场景

- 客服与工单 Copilot（私有知识问答）
- 企业内部知识助手（制度、SOP、FAQ）
- 垂直行业助手（金融、法务、医疗、电商）
- 合规场景下的私有化本地部署

---

## 🏗️ 4. 系统架构

```text
数据采集 → 清洗 → 增强 → Dataset 注册
      ↓
模型微调（LoRA / QLoRA / DPO）
      ↓
模型导出（HuggingFace）
      ↓
模型量化（GGUF）
      ↓
服务部署（Ollama / llama.cpp）
      ↓
RAG + Agent 编排（可选）
```

---

## 💼 5. 工程亮点

- **数据工程化**：统一字段规范、样本增强、质量过滤
- **训练高效化**：混合精度、梯度累积、多 GPU 适配
- **推理降本化**：量化后降低内存占用并提升 CPU 推理速度
- **部署可复现**：本地服务配置清晰，便于演示与交付
- **评估闭环化**：支持指标记录与实验对比，便于持续迭代

---

## 📈 6. 业务指标展示模板

> example: 
| 指标 | 基线模型 | 微调后 | 改善 |
| --- | --- | --- | --- |
| 任务准确率 | 71% | 86% | +15 pts |
| 平均时延（CPU） | 2200 ms | 980 ms | -55% |
| 单千次请求成本 | 1.00x | 0.42x | -58% |
| 幻觉率 | 18% | 8% | -10 pts |

> 建议替换为你真实实验结果（更有说服力）。

---

## ☁️ 7. 云端 GPU 环境

推荐 GPU：`RTX 4090` / `A100` / `H100`  
推荐 Python：`3.11`

```bash
conda create -n llamafactory python=3.11 -y
conda activate llamafactory
pip install -e .
pip install -r requirements/metrics.txt
```

可选一行安装：

```bash
pip install -e ".[torch,metrics]"
```

- 核心依赖：

* PyTorch
* Transformers
* PEFT
* Accelerate
* Datasets


---

## 📁 8. 建议目录结构

```bash
LLaMa-Factory-Fine-Tuning/
├── data/
│   ├── dataset_info.json
│   └── *.json
├── scripts/
├── src/
├── saves/
├── docs/
├── mm_cn.md
└── mm_en.md
```

---


## 📊 9. 数据工程（核心）

> (1) 使用 **EasyDataset** 自动生成训练数据\
> (2) 数据增强策略：指令扩展、多答案、多模态上下文 \
> (3) 支持难度分级：Easy / Medium / Hard
> (4) 数据注册到 `dataset_info.json` 确保 LLaMA Factory 可识别

- `exe文件`下载 easydataset 
- 配置 `AI 供应商 + AI模型`（注意模型过期弃用问题，要看一下官方文档）
- ⚠️：AI工具的选择，要看一下分别 `“多模态” / “文本” / “视频” / “音频” / “推理” 各方面的能力`
- 组合AI工具，来进行数据增强
- ‼️：配置过程，详细参数解释
- 🥬：输出：输出到某一个位置的 json 文件，然后额外复制到自己手动复制到自己存放数据的位置（命名），**`⚠️一定要一定要！！！在 /“xxx/LLaMa Factory Fine-Tuning/data/dataset_info.json” 目录下，增加一个 <命名> 的配置`**

```json
{
 "weibo_dataset": {
  "file_name": "weibo_dataset.json",
  "formatting": "alpaca"
 }
}
```

---

## 🚀 10. 本地部署示例（Ollama）

创建 `Modelfile`：

```text
FROM model.gguf
PARAMETER temperature 0.7
```

构建并运行：

```bash
ollama create my-model -f Modelfile
ollama run my-model
```

---

## 🧠 11. 能力映射细节

| 能力维度 | 项目内容 |
| --- | --- |
| 数据工程 | 采集、清洗、增强、注册规范 |
| LLM 微调 | LoRA / QLoRA / DPO 全流程实践 |
| AI 基础设施 | 显存优化、GPU 训练、可扩展配置 |
| MLOps 思维 | 可复现环境、指标追踪、交付规范 |
| 产品化能力 | 本地部署、API 扩展路径、RAG 集成 |
| AI Infrastructure   | GPU / AutoDL / 多显存训练                    |
| Model Optimization  | 模型量化 / GGUF / CPU / 推理优化                |
| Deployment          | Ollama / llama.cpp / RAG / Agent        |
| Benchmark           | Loss / F1 / 可视化训练曲线                     |

---


### 🔥 11.1 模型微调

基础模型：LLaMA / Qwen / Mistral / DeepSeek

微调方式：

| 方法      | 描述       |
| ------- | -------- |
| Full FT | 全参数微调    |
| LoRA    | 参数高效微调   |
| QLoRA   | 量化微调，低显存 |
| DPO     | 偏好优化     |

示例参数：

```python
learning_rate = 2e-4
batch_size = 4
gradient_accumulation = 8
epochs = 3
```

---


### ⚡ 11.2 微调模型量化与优化

```bash
python convert_hf_to_gguf.py \
--model path_to_model \
--outfile model.gguf \
--outtype q8_0
```

* 优化内存占用
* 提升 CPU / GPU 推理速度
* 支持低成本本地部署

* 📈 提供训练曲线 / 训练日志可视化
* ⚡ 支持多 GPU / Mixed-Precision / Gradient Accumulation

---

### 🚀 11.3 应用模型本地部署（Ollama / llama.cpp）

创建 `Modelfile`:

```text
FROM model.gguf
PARAMETER temperature 0.7
```

构建模型并运行：

```bash
ollama create my-model -f Modelfile
ollama run my-model
```

可实现 **即时本地 LLM 推理服务**。

---

---

### 🤖 11.4 RAG + Agent 扩展（可选）

1. 将模型接入 **文档检索 + 知识库**
2. 实现 **Question → Context → Answer** 流程
3. 支持 **多模态知识增强**
4. 结合 LLM 输出构建 **智能 Agent / Chatbot**

---


# ⭐ 支持 / Star

如果对你有帮助：

```text
Star ⭐
Fork 🍴
```


