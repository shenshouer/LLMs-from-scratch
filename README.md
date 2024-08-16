# 构建一个大型语言模型（从零开始）

这个仓库包含了开发、预训练和微调一个类似GPT的大型语言模型的代码，是《从零开始构建大型语言模型》的官方代码仓库。

<br>
<br>

<a href="http://mng.bz/orYv"><img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/cover.jpg?123" width="250px"></a>

<br>

在这本书中，你将学习到如何从零开始构建一个大型语言模型（LLM），通过逐步编码的方式，从模型的内部构造中理解其工作原理。本书将带领你构建自己的LLM，用清晰的文字、图表和示例来解释每一个阶段。

以教育为目的，本书所描述的训练和开发你自己的小型但功能齐全的模型的方法，与创建支撑大型模型的基础模型ChatGPT所采用的方法类似。此外，本书还包含了加载预训练模型权重进行微调的代码。

- 官方代码仓库：[https://github.com/rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch)
- [本书在Manning上的链接](http://mng.bz/orYv)
- [本书在Amazon上的链接](https://www.amazon.com/gp/product/1633437167)
- ISBN 9781633437166

<a href="http://mng.bz/orYv#reviews"><img src="https://sebastianraschka.com//images/LLMs-from-scratch-images/other/reviews.png" width="220px"></a>


<br>
<br>

下载本仓库的压缩包，点击[Download ZIP](https://github.com/rasbt/LLMs-from-scratch/archive/refs/heads/main.zip)按钮，或者在终端中执行以下命令：

```bash
git clone --depth 1 https://github.com/rasbt/LLMs-from-scratch.git
```

(如果您从Manning网站下载了代码包，请考虑访问GitHub上的官方代码仓库：[https://github.com/rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) 以获取最新更新。)
<br>
<br>


# 目录

请注意，本`README.md`文件是Markdown（`.md`）文件。如果您从Manning网站下载了代码包并在本地计算机上查看，我建议您使用Markdown编辑器或预览器来获得更好的阅读体验。如果您还没有安装Markdown编辑器，[MarkText](https://www.marktext.cc)是一个不错的免费选择。

你或者也可以在浏览器中通过访问[https://github.com/rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch)来查看本仓库的其他文件，这些文件都自动渲染为Markdown格式。

<br>
<br>
<!--  -->

> [!提示]

> 如果你需要安装Python和Python包并设置代码环境的指导，建议阅读[setup](setup)目录下的[README.md](setup/README.md)文件。
> 
<br>

[![Code tests (Linux)](https://github.com/rasbt/LLMs-from-scratch/actions/workflows/basic-tests-linux.yml/badge.svg)](https://github.com/rasbt/LLMs-from-scratch/actions/workflows/basic-tests-linux.yml)
[![Code tests (Windows)](https://github.com/rasbt/LLMs-from-scratch/actions/workflows/basic-tests-windows.yml/badge.svg)](https://github.com/rasbt/LLMs-from-scratch/actions/workflows/basic-tests-windows.yml)
[![Code tests (macOS)](https://github.com/rasbt/LLMs-from-scratch/actions/workflows/basic-tests-macos.yml/badge.svg)](https://github.com/rasbt/LLMs-from-scratch/actions/workflows/basic-tests-macos.yml)



<br>

| 章节标题                         | 主要代码 (快速访问)                                                                                                                                                                                                                                                                                                             | All 代码 + 补充              |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------- |
| [设置建议](setup)                | -                                                                                                                                                                                                                                                                                                                               | -                            |
| Ch 1: 理解大型语言模型           | 无代码                                                                                                                                                                                                                                                                                                                          | -                            |
| Ch 2: 使用文本数据               | - [ch02.ipynb](ch02/01_main-chapter-code/ch02.ipynb)<br/>- [dataloader.ipynb](ch02/01_main-chapter-code/dataloader.ipynb) (总结)<br/>- [exercise-solutions.ipynb](ch02/01_main-chapter-code/exercise-solutions.ipynb)                                                                                                           | [./ch02](./ch02)             |
| Ch 3: 编码注意机制               | - [ch03.ipynb](ch03/01_main-chapter-code/ch03.ipynb)<br/>- [multihead-attention.ipynb](ch03/01_main-chapter-code/multihead-attention.ipynb) (总结) <br/>- [exercise-solutions.ipynb](ch03/01_main-chapter-code/exercise-solutions.ipynb)                                                                                        | [./ch03](./ch03)             |
| Ch 4: 从0开始实现一个GPT模型     | - [ch04.ipynb](ch04/01_main-chapter-code/ch04.ipynb)<br/>- [gpt.py](ch04/01_main-chapter-code/gpt.py) (总结)<br/>- [exercise-solutions.ipynb](ch04/01_main-chapter-code/exercise-solutions.ipynb)                                                                                                                               | [./ch04](./ch04)             |
| Ch 5: 对未标记数据的预训练       | - [ch05.ipynb](ch05/01_main-chapter-code/ch05.ipynb)<br/>- [gpt_train.py](ch05/01_main-chapter-code/gpt_train.py) (总结) <br/>- [gpt_generate.py](ch05/01_main-chapter-code/gpt_generate.py) (总结) <br/>- [exercise-solutions.ipynb](ch05/01_main-chapter-code/exercise-solutions.ipynb)                                       | [./ch05](./ch05)             |
| Ch 6: 文本分类的微调             | - [ch06.ipynb](ch06/01_main-chapter-code/ch06.ipynb)  <br/>- [gpt_class_finetune.py](ch06/01_main-chapter-code/gpt_class_finetune.py)  <br/>- [exercise-solutions.ipynb](ch06/01_main-chapter-code/exercise-solutions.ipynb)                                                                                                    | [./ch06](./ch06)             |
| Ch 7: 按照指令进行微调           | - [ch07.ipynb](ch07/01_main-chapter-code/ch07.ipynb)<br/>- [gpt_instruction_finetuning.py](ch07/01_main-chapter-code/gpt_instruction_finetuning.py) (总结)<br/>- [ollama_evaluate.py](ch07/01_main-chapter-code/ollama_evaluate.py) (总结)<br/>- [exercise-solutions.ipynb](ch07/01_main-chapter-code/exercise-solutions.ipynb) | [./ch07](./ch07)             |
| 附录 A: 介绍 PyTorch             | - [code-part1.ipynb](appendix-A/01_main-chapter-code/code-part1.ipynb)<br/>- [code-part2.ipynb](appendix-A/01_main-chapter-code/code-part2.ipynb)<br/>- [DDP-script.py](appendix-A/01_main-chapter-code/DDP-script.py)<br/>- [exercise-solutions.ipynb](appendix-A/01_main-chapter-code/exercise-solutions.ipynb)               | [./appendix-A](./appendix-A) |
| 附录 B: 参考和进一步阅读         | 无代码                                                                                                                                                                                                                                                                                                                          | -                            |
| 附录 C: 练习解答                 | No code                                                                                                                                                                                                                                                                                                                         | -                            |
| 附录 D: 为训练循环添加装饰特性   | - [appendix-D.ipynb](appendix-D/01_main-chapter-code/appendix-D.ipynb)                                                                                                                                                                                                                                                          | [./appendix-D](./appendix-D) |
| 附录 E: 使用LoRA进行参数高效调优 | - [appendix-E.ipynb](appendix-E/01_main-chapter-code/appendix-E.ipynb)                                                                                                                                                                                                                                                          | [./appendix-E](./appendix-E) |


<br>
&nbsp

下面的思维模型总结了本书中覆盖的内容。

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/mental-model.jpg" width="650px">

<br>
&nbsp

## 硬件需求

本书主要章节的代码都可以运行在普通的笔记本电脑上，并且不需要特定的硬件支持。这种方法可以让广大的读者参与到本书的学习中来。此外，代码会自动利用可用的GPU资源。（请参阅[setup](https://github.com/rasbt/LLMs-from-scratch/blob/main/setup/README.md)文档以获取更多的推荐。）

&nbsp;

## 附属资料

几个文件夹包含了额外的材料，供感兴趣的读者参考。

- **设置**
  - [Python 设置技巧](setup/01_optional-python-setup-preferences)
  - [安装本书中使用的 Python 包和库](setup/02_installing-python-libraries)
  - [Docker环境设置向导](setup/03_optional-docker-environment)
- **章节 2:**
  - [比较各种字节对编码 (BPE) 实现](ch02/02_bonus_bytepair-encoder)
  - [Understanding the Difference Between Embedding Layers and Linear Layers](ch02/03_bonus_embedding-vs-matmul)
  - [使用简单数字理解数据加载器](ch02/04_bonus_dataloader-intuition)
- **章节 3:**
  - [比较高效的多头注意力实现](ch03/02_bonus_efficient-multihead-attention/mha-implementations.ipynb)
  - [理解 PyTorch 缓冲区](ch03/03_understanding-buffers/understanding-buffers.ipynb)
- **章节 4:**
  - [FLOPS 分析](ch04/02_performance-analysis/flops-analysis.ipynb)
- **章节 5:**
  - [使用 Transformers 从 Hugging Face 模型库进行替代权重加载](ch05/02_alternative_weight_loading/weight-loading-hf-transformers.ipynb)
  - [在古腾堡计划数据集(Project Gutenberg Dataset)上预训练 GPT](ch05/03_bonus_pretraining_on_gutenberg)
  - [为训练循环添加装饰特性](ch05/04_learning_rate_schedulers)
  - [优化预训练的超参数(Hyperparameters)](ch05/05_bonus_hparam_tuning)
- **章节 6:**
  - [额外实验微调不同层级和使用更大模型](ch06/02_bonus_additional-experiments)
  - [在 50k IMDB 电影评论数据集上微调不同模型](ch06/03_bonus_imdb-classification)
- **章节 7:**
  - [用于查找近似重复项和创建被动语态条目的数据集工具](ch07/02_dataset-utilities)
  - [使用 OpenAI API 和 Ollama 评估指令响应](ch07/03_model-evaluation)
  - [生成指令微调的数据集](ch07/05_dataset-generation)
  - [使用 Llama 3.1 70B 和 Ollama 生成偏好数据集](ch07/04_preference-tuning-with-dpo/create-preference-data-ollama.ipynb)
  - [大模型对齐的直接偏好优化 (DPO)](ch07/04_preference-tuning-with-dpo/dpo-from-scratch.ipynb)

<br>
&nbsp

## 本仓库的问题、反馈和贡献

我欢迎所有类型的反馈，最好通过[讨论](https://github.com/rasbt/LLMs-from-scratch/discussions)论坛进行分享。同样的，如果您有任何疑问或只是想和其他人分享想法，请不要犹豫发布在论坛上。

如果您发现任何问题或错误，请不要犹豫发布[Issue](https://github.com/rasbt/LLMs-from-scratch/issues)。

然而，由于本仓库包含了本书的主要章节的代码，因此目前无法接受扩充主要章节代码内容的贡献，因为这会导致与实体书的偏离。保持一致的风格有助于确保所有读者都能获得愉快的阅读体验。


&nbsp;
## 引语

如果您发现本书或代码对您的研究有用，请考虑引用它。

芝加哥式引用:

> 拉施卡，瑟斯坦。《从零开始构建大型语言模型》。Manning出版社，2024。ISBN：978-1633437166。

BibTeX 条目:

```
@book{build-llms-from-scratch-book,
  author       = {Sebastian Raschka},
  title        = {Build A Large Language Model (From Scratch)},
  publisher    = {Manning},
  year         = {2024},
  isbn         = {978-1633437166},
  url          = {https://www.manning.com/books/build-a-large-language-model-from-scratch},
  github       = {https://github.com/rasbt/LLMs-from-scratch}
}
```
