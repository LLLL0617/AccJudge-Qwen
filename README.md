# AccJudge-VL: 基于多模态大模型的交通事故责任认定系统  

## 项目简介  

 **AccJudge-VL** 是一个开源交通事故责任认定辅助系统。本研究采用 **Qwen2.5-VL-7B-Instruct** 作为基础模型，针对道路交通事故责任认定任务开展系统性微调工作。在数据准备阶段，团队构建了专业化的微调数据集：文本数据方面，系统整合了《中华人民共和国道路交通安全法》及其实施条例，并补充最高人民法院指导性案例和省级实施细则，形成覆盖全国31个省区市的法律知识库；多模态数据方面，通过采集网络公开事故视频和脱敏处理的责任认定文书，构建了包含事故现场图像序列、结构化事故描述和专业责任认定结论的三元组数据集，数据由业内专家评估校验。

模型微调采用**三阶段渐进式**策略：第一阶段进行法律文本法律文本和交通事故责任认定书**单模态监督训练（SFT）**，使用LoRA训练方法在FP16精度下优化模型的法律条文理解和适用能力，保证输出有法律依据且格式规范；第二阶段是继续进行**基于人类反馈的强化学习（RLHF）**，通过专业标注员对模型输出的数千组对比数据进行偏好评分，优化责任划分的准确性和法律依据的完整性。第三阶段是开展**多模态联合训练**，通过交叉注意力机制融合视觉特征与文本语义，使模型能够分析连续图像帧中的时空线索并生成符合法律逻辑的责任认定推理。最终模型在保留通用能力的同时，在交通事故责任认定任务上的准确率显著优于通用基座模型，并能够生成包含责任比例、法条引用和证据链分析的结构化输出。本项目通过系统性微调，使模型具备专业的法律条文理解能力与多模态事故分析能力，能够辅助交通管理部门、保险公司和法律从业者进行高效、准确的责任认定工作。

## 核心特性  

✅ **专业化法律知识库**  
- 整合《道路交通安全法》及实施条例  
- 涵盖最高人民法院指导案例和31个省区市实施细则  
- 结构化法律条文关联体系  

✅ **多模态事故分析**  
- 支持事故现场图像序列分析  
- 时空线索推理能力（车辆轨迹、碰撞点识别等）  
- 文本描述与视觉证据协同推理  

✅ **三阶段优化架构**  
1. **法律文本SFT微调**：LoRA方法优化法律条文适用能力  
2. **RLHF强化学习**：专业标注员优化责任划分准确性  
3. **多模态联合训练**：交叉注意力机制融合视觉与文本特征  

✅ **结构化输出**  
- 责任比例量化  
- 法条自动引用  
- 证据链逻辑分析  
- 规范化法律文书生成  

## 数据集构建  

📚 **文本数据**  
- 法律法规条文（国家级+省级）  
- 5,000+脱敏责任认定书  
- 最高人民法院指导案例库  

🎥 **多模态数据**  
- 3,200+事故视频片段（脱敏处理）  
- 图像序列-描述-结论三元组数据集  
- 专家校验的时空标注（碰撞时序、车辆轨迹等）  

## 性能表现  

在测试集上相比基座模型：  
- 法律条文引用准确率提升 **62%**  
- 责任划分与专家共识匹配度达 **89.3%**  
- 多模态推理一致性提高 **55%**  

## 快速开始  

```bash
git clone https://github.com/yourorg/AccJudge.git
cd AccJudge
pip install -r requirements.txt
```

示例代码见 `demo.ipynb`，支持：  
- 纯文本责任认定  
- 图像序列分析  
- 视频帧级推理  


## 许可协议  

本项目采用 **Apache License 2.0**，模型权重需遵守[Qwen模型许可](https://github.com/QwenLM/Qwen2)。  

## 贡献指南  

欢迎通过Issue或PR提交：  
- 地方性法规补充  
- 测试案例  
- 多模态标注工具改进  

> 注：本项目为研究用途，实际责任认定应以交管部门为准
