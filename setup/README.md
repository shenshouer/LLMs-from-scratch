# 可选设置说明


当前文档列出了设置机器和使用本仓库代码的不同方法。我推荐从上到下浏览不同的章节，然后决定最适合您的需要的方法。

&nbsp;

## 快速入门

如果您已经在您的机器上安装了 Python，那么最快的方法是从本代码仓库的根目录下通过[../requirements.txt](../requirements.txt)文件按如下方式执行pip安装命令来安装依赖项：


```bash
pip install -r requirements.txt
```

&nbsp;

# 本地设置


这里提供了在本地运行本书代码的建议。注意，本书的主要章节中的代码旨在在合理的时间范围内运行于传统笔记本电脑上，不需要特殊的硬件。我在M3 MacBook Air笔记本电脑上测试了所有主要章节。此外，如果您的笔记本电脑或台式机具有NVIDIA GPU，则代码将自动利用它。

&nbsp;

## 设置Python


如果您还没有安装Python，我已经在以下目录中写过关于我的个人Python设置偏好：

- [01_可选Python偏好设置](./01_optional-python-setup-preferences)
- [02_安装Python库](./02_installing-python-libraries)

*使用DevContainers* 部分提供了另一种安装项目依赖项的方法。
&nbsp;

## 使用Docker DevContainers

作为*设置Python*替代方案，如果您更喜欢使用Docker开发环境隔离项目依赖项和配置，则可以使用Docker。这种方法消除了手动安装软件包和库的需求，并确保一致的开发环境。您可以在[03_optional-docker-environment](./03_optional-docker-environment)中找到有关设置Docker和DevContainer的更多说明。

- [03_可选Docker开发环境设置](03_optional-docker-environment)

&nbsp;

## Visual Studio Code 编辑器

当前有许多优秀的代码编辑器可供选择。我最喜欢的开源编辑器是[Visual Studio Code (VSCode)](https://code.visualstudio.com)，它可以轻松地通过许多有用的插件和扩展进行增强（有关更多信息，请参阅*VSCode扩展*部分）。macOS、Linux和Windows的下载说明可以在[VSCode主页](https://code.visualstudio.com)上找到。

&nbsp;

## VSCode 扩展(Extensions)

如果您使用Visual Studio Code作为主要代码编辑器，则可以在`.vscode`子文件夹中找到推荐的扩展。要安装这些扩展，请在VSCode中打开`extensions.json`文件，然后在右下角弹出菜单中单击“安装”按钮。

&nbsp;

# 云资源

这些部分描述了云替代方案，用于运行本书中所述的代码。

虽然代码可以在没有专用GPU的传统笔记本电脑和台式电脑上运行，但具有NVIDIA GPU的云平台可以显着提高代码的运行时间，特别是在第5到第7章。

&nbsp;

## 使用 Lightning Studio

为了在云中获得顺畅的开发体验，我推荐[Lightning AI Studio](https://lightning.ai/)平台，它允许用户设置持久环境并在云CPU和GPU上使用VSCode和Jupyter Lab。


一旦你启动一个新的Studio，你可以打开终端并执行以下设置步骤来克隆仓库并安装依赖项：

```bash
git clone https://github.com/rasbt/LLMs-from-scratch.git
cd LLMs-from-scratch
pip install -r requirements.txt
```

(在Google Colab中，只需执行一次设置步骤，因为Lightning AI Studio环境是持久的，即使在CPU和GPU机器之间切换也是如此。)

然后，导航到要运行的Python脚本或Jupyter笔记本。如果您想在第5章或第6、7章中加速代码的运行时间，则可以轻松地将GPU连接到环境，例如，在第5章中预训练LLM或在第6、7章中微调LLM。

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/README/studio.webp" alt="1" width="700">

&nbsp;


## 使用 Google Colab

为了在云中使用Google Colab环境，请转到[https://colab.research.google.com/](https://colab.research.google.com/)，然后从GitHub菜单中打开相应的章节笔记本，或者将笔记本拖动到*上传*字段中，如图所示。

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/README/colab_1.webp" alt="1" width="700">


还要确保将相关文件(数据集文件和笔记本要从其中导入的.py文件)上传到Colab环境，如下所示。

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/README/colab_2.webp" alt="2" width="700">


你还可以选择在GPU上运行代码，方法是将*Runtime*更改为如下所示。

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/README/colab_3.webp" alt="3" width="700">


&nbsp;

# Questions?
# 疑问？

如果你有任何问题，请不要犹豫，通过本GitHub仓库的[Discussions](https://github.com/rasbt/LLMs-from-scratch/discussions)论坛与我联系。
