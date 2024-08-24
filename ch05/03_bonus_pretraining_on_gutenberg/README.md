# 在 Project Gutenberg 数据集上预训练 GPT

这个目录中包含了在Project Gutenberg提供的免费图书上训练一个小型GPT模型的代码。

正如Project Gutenberg网站所述，“绝大多数Project Gutenberg的电子书在美国属于公共领域”。


请阅读 [Project Gutenberg Permissions, Licensing and other Common Requests](https://www.gutenberg.org/policy/permission.html) 页面，了解如何使用 Project Gutenberg 提供的资源的更多信息

&nbsp;
## 怎么使用这个代码

&nbsp;

### 1）下载数据集


在这个部分，我们使用[`pgcorpus/gutenberg`](https://github.com/pgcorpus/gutenberg) GitHub仓库中的代码从Project Gutenberg下载图书。


根据目前的情况，这将需要大约 50GB 的磁盘空间，大约需要 10-15 小时的时间，但具体时间可能会更长，这取决于 Project Gutenberg 自那时以来的增长情况。

&nbsp;
#### 为Linux 和 macOS 用户下载说明


Linux 和 macOS 用户可以按照以下步骤下载数据集（如果您是 Windows 用户，请参阅下面的注释）：

1. 将文件夹设置`03_bonus_pretraining_on_gutenberg`为工作目录，以便在此本地文件夹中克隆`gutenberg`仓库（这对于运行提供的脚本`prepare_dataset.py`和`pretraining_simple.py`是必要的）。例如，当在`LLMs-from-scratch`仓库的文件夹中时，通过以下方式进入到`03_bonus_pretraining_on_gutenberg`文件夹：
```bash
cd ch05/03_bonus_pretraining_on_gutenberg
```

1. 在此克隆`gutenberg`仓库 :
```bash
git clone https://github.com/pgcorpus/gutenberg.git
```

1. 进入到 `gutenberg` 仓库文件夹:
```bash
cd gutenberg
```

1. 安装`gutenberg`仓库中的`requirements.txt`文件中定义的所需的包：
```bash
pip install -r requirements.txt
```

2. 下载数据
```bash
python get_data.py
```

1. 返回到`03_bonus_pretraining_on_gutenberg`文件夹：
```bash
cd ..
```

&nbsp;
#### Windows用户特别说明


该[`pgcorpus/gutenberg`](https://github.com/pgcorpus/gutenberg)代码兼容 Linux 和 macOS。但是，Windows 用户必须进行一些小调整，例如添加`shell=True`调用`subprocess`并替换`rsync`

另外，在 Windows 上运行此代码的更简单的方法是使用"Windows Subsystem for Linux"（WSL）功能，该功能允许用户在 Windows 中使用 Ubuntu 运行 Linux 环境。有关更多信息，请阅读[Microsoft 的官方安装说明](https://learn.microsoft.com/en-us/windows/wsl/install)和[教程](https://learn.microsoft.com/en-us/training/modules/wsl-introduction/)。

使用 WSL 时，请确保已安装 Python 3（通过 检查`python3 --version`，或者例如使用`sudo apt-get install -y python3.10` 安装Python 3.10 ）并在那里安装以下软件包：

```bash
sudo apt-get update && \
sudo apt-get upgrade -y && \
sudo apt-get install -y python3-pip && \
sudo apt-get install -y python-is-python3 && \
sudo apt-get install -y rsync
```

> [!NOTE]
>关于如何设置 Python 和安装包的说明可以在[可选的 Python 设置首选项](../../setup/01_optional-python-setup-preferences/README.md)和[安装 Python 库](../../setup/02_installing-python-libraries/README.md)中找到
> 
> 可选地，此仓库提供了运行 Ubuntu 的 Docker 映像。有关如何使用提供的 Docker 映像运行容器的说明，请参阅[可选 Docker 环境](../../setup/03_optional-docker-environment/README.md)

&nbsp;
### 2) 准备数据集

接下来，运行`prepare_dataset.py`脚本，将（截至撰写本文时，共有 60,173 个）文本文件连接成更少的较大文件，以便更有效地传输和访问它们：

```bash
python prepare_dataset.py \
  --data_dir gutenberg/data/raw \
  --max_size_mb 500 \
  --output_dir gutenberg_preprocessed
```

```
...
Skipping gutenberg/data/raw/PG29836_raw.txt as it does not contain primarily English text.                                     Skipping gutenberg/data/raw/PG16527_raw.txt as it does not contain primarily English text.                                     100%|██████████████████████████████████████████████████████████| 57250/57250 [25:04<00:00, 38.05it/s]
42 file(s) saved in /Users/sebastian/Developer/LLMs-from-scratch/ch05/03_bonus_pretraining_on_gutenberg/gutenberg_preprocessed
```


> [!TIP] 
> 请注意，生成的文件以纯文本格式存储，并且为了简单起见未预先标记。但是，如果您计划更频繁地使用数据集或进行多个时期的训练，您可能需要更新代码以将数据集存储在预先标记的形式中，以节省计算时间。有关更多信息，请参阅本页底部的 *设计决策和改进* 部分

> [!TIP]
> 您可以选择较小的文件大小，例如 50 MB。这将产生更多文件，但对于在少量文件上进行更快的预训练运行（用于测试目的）可能很有用


&nbsp;
### 3) 允许预训练脚本

您可以按如下方式运行预训练脚本。请注意，为了便于说明，附加命令行参数以默认值显示：

```bash
python pretraining_simple.py \
  --data_dir "gutenberg_preprocessed" \
  --n_epochs 1 \
  --batch_size 4 \
  --output_dir model_checkpoints
```

输出将采用以下格式：

> Total files: 3  
> Tokenizing file 1 of 3: data_small/combined_1.txt  
> Training ...  
> Ep 1 (Step 0): Train loss 9.694, Val loss 9.724  
> Ep 1 (Step 100): Train loss 6.672, Val loss 6.683  
> Ep 1 (Step 200): Train loss 6.543, Val loss 6.434  
> Ep 1 (Step 300): Train loss 5.772, Val loss 6.313  
> Ep 1 (Step 400): Train loss 5.547, Val loss 6.249  
> Ep 1 (Step 500): Train loss 6.182, Val loss 6.155  
> Ep 1 (Step 600): Train loss 5.742, Val loss 6.122  
> Ep 1 (Step 700): Train loss 6.309, Val loss 5.984  
> Ep 1 (Step 800): Train loss 5.435, Val loss 5.975  
> Ep 1 (Step 900): Train loss 5.582, Val loss 5.935  
> ...  
> Ep 1 (Step 31900): Train loss 3.664, Val loss 3.946  
> Ep 1 (Step 32000): Train loss 3.493, Val loss 3.939  
> Ep 1 (Step 32100): Train loss 3.940, Val loss 3.961  
> Saved model_checkpoints/model_pg_32188.pth  
> Book processed 3h 46m 55s   
> Total time elapsed 3h 46m 55s   
> ETA for remaining books: 7h 33m 50s  
> Tokenizing file 2 of 3: data_small/combined_2.txt  
> Training ...  
> Ep 1 (Step 32200): Train loss 2.982, Val loss 4.094  
> Ep 1 (Step 32300): Train loss 3.920, Val loss 4.097  
> ...


&nbsp;
> [!TIP] 
> 实际上，如果您使用的是 macOS 或 Linux，我建议使用该`tee`命令将日志输出保存到文件中`log.txt`，而不是在终端上打印它们：

```bash
python -u pretraining_simple.py | tee log.txt
```

&nbsp;
> [!WARNING]  
> 请注意，在 V100 GPU 上对文件夹中约 500 Mb 的文本文件之一进行训练`gutenberg_preprocessed`大约需要 4 个小时。
> 该文件夹包含 47 个文件，大约需要 200 小时（超过 1 周）才能完成。您可能希望在较少的文件上运行它


&nbsp;
## 设计决策和改进

请注意，出于教学目的，此代码着重于保持简单和最小化。可以通过以下方式改进代码，以提高建模性能和训练效率：

1. 修改`prepare_dataset.py`脚本以从每个书籍文件中删除 Gutenberg 样板文本
2. 更新数据准备和加载实用程序以预先标记数据集并以标记形式保存它，以便在每次调用预训练脚本时不必重新标记它
3. 如[附录 D：为训练循环扩展更多功能](../../appendix-D/01_main-chapter-code/appendix-D.ipynb)中介绍的，更新`train_model_simple`脚本添加一些特性，如余弦衰减、线性预热和梯度剪裁
4. 更新预训练脚本以保存优化器状态（参见第 5 章中的 5.4 节在 PyTorch 中加载和保存权重；[ch05.ipynb](../../ch05/01_main-chapter-code/ch05.ipynb)），并添加加载现有模型和优化器检查点的选项，并在训练运行中断时继续训练
5. 添加更高级的记录器（例如，权重和偏差）以实时查看损失和验证曲线
6. 添加分布式数据并行（DDP）并在多个 GPU 上训练模型（参见附录 A 中的A.9.3 使用多 GPU 进行训练节；[DDP-script.py](../../appendix-A/01_main-chapter-code/DDP-script.py)）
7. 使用在[高效的多头注意力机制实现](../../ch03/02_bonus_efficient-multihead-attention/mha-implementations.ipynb) 激励章节中实现的 更高效的 `MHAPyTorchScaledDotProduct` 类替换 `previous_chapter.py` 中的 `MultiheadAttention` 类，以提高效率。这个类通过PyTorch的 `nn.functional.scaled_dot_product_attention`函数使用Flash Attention。
8. 通过[torch.compile](https://pytorch.org/tutorials/intermediate/torch_compile_tutorial.html) (`model = torch.compile`) 和 [thunder](https://github.com/Lightning-AI/lightning-thunder) (`model = thunder.jit(model)`) 优化模型以加速训练。
9.  实现梯度低秩投影（GaLore）来进一步加快预训练过程。这可以通过将`AdamW`优化器替换为提供的`GaLoreAdamW`来实现，该优化器包含在[GaLore Python库](https://github.com/jiaweizzhao/GaLore)中。
