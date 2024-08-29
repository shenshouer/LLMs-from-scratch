# 章节7 遵循指令进行微调

本文件夹包含用于模型评估的实用代码。



&nbsp;
## 使用OpenAI API评估指令响应

- [llm-instruction-eval-openai.ipynb](llm-instruction-eval-openai.ipynb) notebook使用OpenAI的GPT-4评估由指令微调模型生成的响应。它适用于以下格式的JSON文件：


```python
{
    "instruction": "What is the atomic number of helium?",
    "input": "",
    "output": "The atomic number of helium is 2.",               # <-- The target given in the test set
    "model 1 response": "\nThe atomic number of helium is 2.0.", # <-- Response by an LLM
    "model 2 response": "\nThe atomic number of helium is 3."    # <-- Response by a 2nd LLM
},
```

&nbsp;
## 使用Ollama在本地评估指令响应

- [llm-instruction-eval-ollama.ipynb](llm-instruction-eval-ollama.ipynb) notebook提供了一种替代上述方法，利用Ollama下载的本地Llama 3模型。