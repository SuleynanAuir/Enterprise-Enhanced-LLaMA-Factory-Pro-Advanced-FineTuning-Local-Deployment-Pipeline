
# 🚀 LLaMA / Qwen 高级微调 & 本地部署 Pipeline

![# LLaMA Factory](assets/logo.png)

<p align="center">

<img src="https://img.shields.io/badge/LLM-Fine--Tuning-blue"/>
<img src="https://img.shields.io/badge/Framework-Transformers-yellow"/>
<img src="https://img.shields.io/badge/Training-LoRA%20%7C%20QLoRA-green"/>
<img src="https://img.shields.io/badge/Deployment-Ollama-orange"/>
<img src="https://img.shields.io/badge/GPU-AutoDL%204090-red"/>
<img src="https://img.shields.io/badge/Language-Python-black"/>

</p>

---

# 🌟 项目简介

本项目构建了 **企业级 LLM 全流程训练与部署系统**，覆盖：

1. 数据采集、清洗与增强（Dataset Engineering）
2. 指令微调与参数高效优化（LoRA / QLoRA / DPO）
3. 模型量化与加速（HF → GGUF / CPU 推理优化）
4. 本地部署与服务化（Ollama / llama.cpp）
5. RAG + Agent 扩展（多模态知识检索 + 动态回答）

**项目亮点：**

* 🔥 完整 LLM 工程化 Pipeline
* 🧠 面向招聘，突出 AI / LLM 工程能力
* ⚡ 支持多 GPU / 多显存优化
* 📊 可展示 Benchmark 与训练曲线
* 🤖 可直接扩展 RAG & Agent 应用

---

# 🧩 系统架构

```
数据采集 → 数据清洗 → AI 数据增强 → Dataset 注册
         ↓
    LLM 微调 (LoRA / QLoRA / DPO)
         ↓
    模型导出 (HuggingFace)
         ↓
    模型量化 (GGUF)
         ↓
    本地部署 (Ollama / llama.cpp)
         ↓
    RAG / Agent 扩展 (Optional)
```

💡 **工程实践价值：**
招聘官可直接看到你掌握了**数据工程 + 模型微调 + 优化部署 + AI 产品落地能力**。

---

# 📁 项目结构

```bash
LLM-Factory-Pipeline/
│
├── data/                       # 数据集目录
│   ├── dataset_info.json        # 数据注册信息
│   └── training_dataset.json    # 训练数据
│
├── scripts/                    # 工具脚本
│   └── convert_hf_to_gguf.py    # 模型量化脚本
│
├── models/                     # 模型存放
│
├── notebooks/                  # 数据分析 / 可视化
│
├── benchmark/                  # 训练曲线 & 性能对比
│
└── README.md
```

---

# ☁️ 云端 GPU 环境

**推荐平台：**

| 平台          | 说明             |
| ----------- | -------------- |
| AutoDL      | 国内低延迟 RTX 4090 |
| RunPod      | 国际 GPU 方案      |
| Lambda Labs | 高稳定性 GPU       |
| AWS / GCP   | 企业级 GPU 方案     |

**显卡推荐：** RTX 4090 / A100 / H100

**显存需求示例：**

| 模型  | 显存   |
| --- | ---- |
| 7B  | 24GB |
| 13B | 48GB |
| 30B | 80GB |

> ⚡ 使用 **QLoRA** 可大幅降低显存需求。

---

# 🧠 环境配置

```bash
conda create -n llamafactory python=3.11 -y
conda activate llamafactory
pip install -e ".[torch,metrics]"
```

核心依赖：

* PyTorch
* Transformers
* PEFT
* Accelerate
* Datasets

---

# 📊 数据工程（核心）

* 使用 **EasyDataset** 自动生成训练数据
* 数据增强策略：指令扩展、多答案、多模态上下文
* 支持难度分级：Easy / Medium / Hard
* 数据注册到 `dataset_info.json` 确保 LLaMA Factory 可识别

```json
{
 "weibo_dataset": {
  "file_name": "weibo_dataset.json",
  "formatting": "alpaca"
 }
}
```

---

# 🔥 模型微调

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

# ⚡ 模型量化与优化

```bash
python convert_hf_to_gguf.py \
--model path_to_model \
--outfile model.gguf \
--outtype q8_0
```

* 优化内存占用
* 提升 CPU / GPU 推理速度
* 支持低成本本地部署

---

# 🚀 本地部署（Ollama / llama.cpp）

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

# 📊 Benchmark 示例

| 模型       | 数据集           | Loss | F1   | Notes              |
| -------- | ------------- | ---- | ---- | ------------------ |
| Qwen-7B  | weibo_dataset | 0.12 | 0.97 | Instruction tuning |
| LLaMA-7B | weibo_dataset | 0.15 | 0.95 | LoRA 微调            |

* 📈 提供训练曲线 / 训练日志可视化
* ⚡ 支持多 GPU / Mixed-Precision / Gradient Accumulation

---

# 🤖 RAG + Agent 扩展（可选）

1. 将模型接入 **文档检索 + 知识库**
2. 实现 **Question → Context → Answer** 流程
3. 支持 **多模态知识增强**
4. 结合 LLM 输出构建 **智能 Agent / Chatbot**

---

# 🧠 招聘导向技能展示

| 核心能力                | 说明                                      |
| ------------------- | --------------------------------------- |
| Dataset Engineering | 数据采集 / 清洗 / 增强                          |
| LLM 微调              | LoRA / QLoRA / DPO / Instruction Tuning |
| AI Infrastructure   | GPU / AutoDL / 多显存训练                    |
| Model Optimization  | 模型量化 / GGUF / CPU / 推理优化                |
| Deployment          | Ollama / llama.cpp / RAG / Agent        |
| Benchmark           | Loss / F1 / 可视化训练曲线                     |

---

# 🏷 技术栈

```text
Python, PyTorch, Transformers, PEFT, LLaMA Factory, Ollama, GGUF, AutoDL GPU
```

---

# 🌟 求职亮点说明

* 项目覆盖 **完整 LLM 工程流程**
* 可展示 **工程能力 + AI 算法能力**
* 数据增强 / 多模态 / RAG / Agent 扩展
* 模型量化与低显存训练经验
* 本地部署与服务化能力

> 💎 招聘官可直接看到你掌握了 **企业级 LLM 项目实战能力**

---

# ⭐ 支持 / Star

如果对你有帮助：

```text
Star ⭐
Fork 🍴
```


