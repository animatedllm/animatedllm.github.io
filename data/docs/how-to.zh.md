# 如何使用此应用

您是老师、学生，还是好奇的访客？

欢迎！在这个简短的概览中，您将了解到此应用的功能以及如何充分利用它。

## 此应用的作用是什么？

**首先，让我们来看看 AnimatedLLM 不是什么**。

AnimatedLLM（至少目前！）不是一个完整的教育应用，无法带您从头到尾全面了解大型语言模型的工作原理。

要深入理解这一主题，您还需要参考其他资料。

首先，可以尝试观看 [3Blue1Brown](https://www.youtube.com/@3blue1brown/videos) 频道的这段短视频（英文，提供多国语言字幕）：

<iframe width="560" height="315" src="https://www.youtube.com/embed/LPZh9BOjkQs?si=Nogb8BgfP9kL1DIa" title="YouTube video player" frameborder="0" allow="clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

互联网上还有许多其他资源。其中的优质资源包括 Jay Alammar 的这些带插图的博文：

- **[Illustrated GPT-2](https://jalammar.github.io/illustrated-gpt2/)**
- **[Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/)**

对于捷克的学生，这里有直接关注大型语言模型的大学课程：

- **MFF UK:** [Large Language Models (NPFL140)](https://ufal.mff.cuni.cz/courses/npfl140)
- **FIT ČVUT:** [Neural Language Models (NI-NLM)](https://bilakniha.cvut.cz/en/predmet8241006.html)
 
 
（注：此应用的作者参与了第一门课程的教学并负责领导第二门课程 😇）

**那么，AnimatedLLM 的作用是什么呢？**

AnimatedLLM 中的动画主要作为一种教学辅助工具。它们有助于解释语言模型的工作原理，否则这些原理可能需要费力地“空口描述”或在白板上绘图才能讲清楚。

例如：
- 模型生成的文本是从哪里来的？
- 模型“在文档上进行训练”是什么意思？
- 下一个 token 的概率具体是从哪里来的？
- 等等。


至于我们为什么要研究这些过程、语言模型是如何诞生的，以及它们在 ChatGPT、Gemini 或 Claude 等复杂服务中的角色——这些内容您需要去别处学习。


**还有一个警告...**

AnimatedLLM 中的某些语言模型原理经过了简化。程度并不严重，但为了清晰起见，省略了一些技术细节。

如果您对这些具体的技术细节感兴趣，以下动画更深入地探讨了模型架构：
- [llm-viz](https://bbycroft.net/llm)
- [Transformer Explainer](https://poloclub.github.io/transformer-explainer/)

## 应用是如何运作的？

AnimatedLLM 中的动画是**与真实语言模型交互的记录**。

这意味着两点：
- 动画展示了真实语言模型的真实行为。
- 在播放动画期间，实际上并没有运行语言模型；浏览器只是在播放记录。

### 记录是如何创建的？
这些记录是使用来自 [Hugging Face](https://huggingface.co/models) 仓库的小型开源语言模型生成的。

模型在大学计算集群上使用 [vLLM](https://github.com/vllm-project/vllm) 框架运行。该框架允许收集精细的细节，例如下一个 token 的概率。

选择了特定的 prompt 和文档来演示各种有趣的现象（例如，“为什么模型不太会数字母？”）。

提供以下不同维度的数据：
- 模型 (models)
- 解码温度 (decoding temperature)
- 语言 (languages)

您可以在 [项目仓库](https://github.com/kasnerz/animated-llm/tree/main/scripts/data-generation) 中找到用于生成记录的脚本。

还有一个脚本可以用来 [下载并探索](https://github.com/kasnerz/animated-llm/blob/main/scripts/download_data.py) 所有当前的 JSON 格式记录。

### 记录中包含哪些数据？

⚠ 注意：这些信息自编写以来可能已发生部分变化。

#### 模型
此应用包含以下模型的输出：
- [CohereForAI/aya-expanse-8b](https://huggingface.co/CohereForAI/aya-expanse-8b)
- [meta-llama/Llama-3.2-1B-Instruct](https://huggingface.co/meta-llama/Llama-3.2-1B-Instruct)
- [Qwen/Qwen3-4B-Instruct-2507](https://huggingface.co/Qwen/Qwen3-4B-Instruct-2507)
- [allenai/Olmo-3-7B-Think](https://huggingface.co/allenai/Olmo-3-7B-Think)
- [openai-community/gpt2-xl](https://huggingface.co/openai-community/gpt2-xl)

为了教学目的，还提供了一个来自“vanilla Transformer”的记录——即一个权重随机初始化的模型（它基于 `Llama-3.2-1B-Instruct` 架构，但这只是一个技术细节）。

#### 解码温度
解码温度是一个介于 0 到 ∞ 之间的数值，简单来说，它决定了选择下一个 token 的随机程度。

当温度接近零时，几乎总是选择最可能的 token；而在极高温度下，模型预测的影响微乎其微，token 是随机选择的。

应用中提供了以下温度值的记录：
- 🧊 **0.0**：始终选择概率最高的 token，
- 🌡 **1.0**：根据模型的概率随机选择 token，
- 🔥 **5.0**：随机选择 token，模型的概率仅起次要作用。

#### 语言

我们提供应用支持的所有语言的记录。目前包括：

- 🇬🇧 英语
- 🇨🇿 捷克语
- 🇫🇷 法语
- 🇺🇦 乌克兰语
- 🇨🇳 中文

选择这些语言是为了涵盖广泛的语系和文字系统。

有兴趣添加更多语言或修复错误？请跳转到“如何提供反馈？”部分。

⚠ 注意：除英语和捷克语外，网站翻译均是使用大型语言模型自动生成的。


## 如何操作应用
### 如何选择特定的记录？

1. 在主屏幕上，选择您感兴趣的语言模型方面。
2. 在设置中选择 **模型 (model) 和 温度 (temperature)**。在某些动画中，这些设置是直接可见的；在其他动画中，它们隐藏在图标下：

![settings](img/settings.png)

3. 通过国旗图标选择 **语言**。（目前，更改记录语言会同步切换整个应用的语言）：

![language](img/languages.png)

4. 点击“Play”按钮开始动画。

### 高级技巧

动画也可以使用键盘快捷键进行控制。

除了“Play”按钮外，您还可以使用右箭头键单步执行动画，或使用左箭头键返回上一步。

而且还有更多快捷键！

您可以在键盘图标下找到所有快捷键：

![keyboard](img/keyboard.png)


## 如何提供反馈？

请将问题和改进建议发送至 **[GitHub 讨论区](https://github.com/kasnerz/animated-llm/discussions)**。

如果您没有 GitHub 账号，也可以直接写信给应用的主要作者（[Zdeněk Kasner](https://kasnerz.github.io)；您可以在 [这里](https://ufal.mff.cuni.cz/zdenek-kasner) 找到他的电子邮箱）。