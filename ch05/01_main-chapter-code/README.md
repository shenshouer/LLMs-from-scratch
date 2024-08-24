# 章节 5：在无标签数据上预训练模型

### 主章节代码

- [ch05.ipynb](ch05.ipynb) 包含本章节中出现的所有代码
- [previous_chapters.py](previous_chapters.py) 是一个 Python 模块，其中包含了前一章节中出现的 `MultiHeadAttention` 模块和 `GPTModel` 类，我们在 [ch05.ipynb](ch05.ipynb) 中导入它来预训练 GPT 模型
- [gpt_download.py](gpt_download.py) 包含了下载预训练 GPT 模型权重的实用函数
- [exercise-solutions.ipynb](exercise-solutions.ipynb) 包含本章节练习解答

### 额外代码

- [gpt_train.py](gpt_train.py) 是一个独立的Python脚本文件，包含了我们在 [ch05.ipynb](ch05.ipynb) 中实现的用于训练GPT模型的代码（您可以将其视为总结本章内容的代码文件）
- [gpt_generate.py](gpt_generate.py) 是一个独立的Python脚本文件，包含了我们在 [ch05.ipynb](ch05.ipynb) 中实现的用于加载和使用来自OpenAI的预训练模型权重的代码 

