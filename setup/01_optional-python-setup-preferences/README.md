# Python设置技巧



有几种不同的方法可以安装Python并设置计算环境。在这里，我将说明我的个人偏好。

 (我使用的是运行macOS的电脑，但这个工作流程适用于Linux机器，也可能适用于其他操作系统。)


<br>
<br>


## 1. 下载并安装Miniforge

从GitHub存储库下载miniforge [这里](https://github.com/conda-forge/miniforge).

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/01_optional-python-setup-preferences/download.png" alt="download" width="600px">

根据您的操作系统，这应该下载一个`.sh` (macOS, Linux)或`.exe`文件(Windows)。

对于`.sh`文件，打开命令行终端并执行以下命令

```bash
sh ~/Desktop/Miniforge3-MacOSX-arm64.sh
```

`Desktop/`是下载Miniforge安装程序的文件夹。在你的电脑上，你可能要用`Downloads/`替换。

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/01_optional-python-setup-preferences/miniforge-install.png" alt="miniforge-install" width="600px">

Next, step through the download instructions, confirming with "Enter".
接下来，按照下载说明进行操作，按"Enter"确认。

如果你需要使用很多包，Conda可能很慢，因为它复杂而繁琐的依赖解析过程以及处理大型软件包索引和元数据的处理。为了加快Conda的速度，你可以使用以下设置，它切换到一种更有效的Rust重新实现来解决依赖关系：

```
conda config --set solver libmamba
```

<br>
<br>


## 2. 创建一个新的虚拟环境

在安装成功完成后，我建议创建一个名为`LLMs`的新虚拟环境，你可以通过执行以下命令来实现：

```bash
conda create -n LLMs python=3.10
```

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/01_optional-python-setup-preferences/new-env.png" alt="new-env" width="600px">

> 许多科学计算库并不立即支持最新版本的Python。因此，在安装PyTorch时，建议使用Python版本稍旧一点的版本。例如，如果最新版本的Python是3.13，建议使用Python 3.10或3.11。

下一步，激活你的新虚拟环境（每次打开新的终端窗口或标签时都要这样做）：

```bash
conda activate LLMs
```

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/01_optional-python-setup-preferences/activate-env.png" alt="activate-env" width="600px">

<br>
<br>

## 可选：自定义终端样式

如果你想让你的终端看起来像我的，可以安装[Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh)项目。

<br>
<br>

## 3. 安装新的Python库

为了安装新的Python库，你可以使用`conda`包管理器。例如，你可以安装[JupyterLab](https://jupyter.org/install)和[watermark](https://github.com/rasbt/watermark)如下：

```bash
conda install jupyterlab watermark
```

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/01_optional-python-setup-preferences/conda-install.png" alt="conda-install" width="600px">



你也可以使用`pip`来安装库。默认情况下，`pip`应该链接到你的新`LLms` conda环境：

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/01_optional-python-setup-preferences/check-pip.png" alt="check-pip" width="600px">

<br>
<br>

## 4. 安装PyTorch

可以像安装其他Python库或包一样安装PyTorch。例如：

```bash
pip install torch==2.0.1
```

However, since PyTorch is a comprehensive library featuring CPU- and GPU-compatible codes, the installation may require additional settings and explanation (see the *A.1.3 Installing PyTorch in the book for more information*).
然而，由于PyTorch是一个包含CPU和GPU兼容代码的全面库，因此安装可能需要额外的设置和说明（请参阅本书的第A.1.3节获取更多信息）。

也强烈建议参考官方PyTorch网站上的安装指南[https://pytorch.org](https://pytorch.org)。
<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/01_optional-python-setup-preferences/pytorch-installer.jpg" width="600px">



---




其他问题？请随时在[讨论区](https://github.com/rasbt/LLMs-from-scratch/discussions)中联系。