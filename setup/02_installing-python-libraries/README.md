# 安装本书所用Python库和包


当前文档提供有关检查已安装的Python版本和包的更多信息。（请参阅[../01_可选Python偏好设置](../01_optional-python-setup-preferences)文件夹中的更多信息，以了解有关安装Python和Python包的详细信息。）

我们使用了[这里](https://github.com/rasbt/LLMs-from-scratch/blob/main/requirements.txt)列出的库来编写本书。这些库的较新版本也可能兼容。但是，如果您遇到代码问题，则可以尝试这些库版本作为备用方案。

为了更方便地安装这些依赖，您可以从本代码库的根目录使用`requirements.txt`文件并执行以下命令：

```bash
pip install -r requirements.txt
```

或者，您也可以通过GitHub URL安装：

```bash
pip install -r https://raw.githubusercontent.com/rasbt/LLMs-from-scratch/main/requirements.txt
```


然后，完成安装后，请检查所有包是否已安装且是最新版本。您可以使用以下命令：

```bash
python python_environment_check.py
```

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/02_installing-python-libraries/check_1.jpg" width="600px">


这里也建议在JupyterLab中检查版本，方法是运行本目录中的`python_environment_check.ipynb`，理想情况下应该与上述结果相同。

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/02_installing-python-libraries/check_2.jpg" width="500px">


如果您看到以下问题，则可能是JupyterLab实例连接到错误的conda环境：

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/02_installing-python-libraries/jupyter-issues.jpg" width="450px">


在这种情况下，您可能需要使用`watermark`来检查您是否在正确的conda环境中打开了JupyterLab实例，方法是使用`--conda`选项：

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/02_installing-python-libraries/watermark.jpg" width="350px">


<br>
<br>


## 安装PyTorch

PyTorch可以像其他Python库或包一样使用pip进行安装。例如：

```bash
pip install torch==2.0.1
```

不过，由于PyTorch是一个包含CPU和GPU兼容代码的综合库，因此安装可能需要其他设置和说明（请参阅本书的*A.1.3 Installing PyTorch*部分以获取更多信息）。


这里也强烈建议阅读PyTorch官方网站上的安装指南：[https://pytorch.org](https://pytorch.org)。

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/02_installing-python-libraries/pytorch-installer.jpg" width="600px">



---




任何问题？请随时在[讨论论坛](https://github.com/rasbt/LLMs-from-scratch/discussions)中联系我们。
