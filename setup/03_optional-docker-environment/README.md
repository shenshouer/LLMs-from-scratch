# Docker环境设置指南

如果你更喜欢使用Docker作为开发环境来隔离项目的依赖项和配置，那么使用Docker是一个非常有效的解决方案。这种方法消除了手动安装软件包和库的需求，并确保了开发环境的一致性。

如果你更喜欢使用conda环境，这一篇指南将引导您完成使用Docker作为开发环境的设置，请参阅[../01_可选Python偏好设置](../01_optional-python-setup-preferences)和[../02_安装Python库](../02_installing-python-libraries)。

<br>

## 下载并安装Docker


安装和使用Docker最简单的方法是安装适合你平台的[Docker Desktop](https://docs.docker.com/desktop/)。


Linux (Ubuntu) 用户可能更喜欢安装 [Docker Engine](https://docs.docker.com/engine/install/ubuntu/) 而不是 Docker Desktop，并遵循 [后期安装](https://docs.docker.com/engine/install/linux-postinstall/) 步骤。
<br>

## 使用Visual Studio Code中的Docker DevContainer

一个Docker DevContainer，或开发容器，是一个允许开发人员使用Docker容器作为一个完整的开发环境的工具。不管他们的本地机器配置如何，这种方法确保用户可以快速地获得一个一致的开发环境。

当然，DevContainers也可以与其他IDE一起使用，但最常见的IDE/编辑器是Visual Studio Code（VS Code）。下面的指南将展示如何在VS Code中使用DevContainer来完成本书的开发，但同样的过程也适用于PyCharm。如果您还没有安装VS Code，请[下载](https://code.visualstudio.com/download)它。

1. 克隆本GitHub仓库并进入项目根目录。

```bash
git clone https://github.com/rasbt/LLMs-from-scratch.git
cd LLMs-from-scratch
```

2. 将`.devcontainer`文件夹从`setup/03_optional-docker-environment/`文件夹移动到当前目录（项目根目录）。

```bash
mv setup/03_optional-docker-environment/.devcontainer ./
```

3. 在Docker Desktop中，确保 **_desktop-linux_ builder** 正在运行且将用于构建Docker容器（请参阅 _Docker Desktop_ -> _Change settings_ -> _Builders_ -> _desktop-linux_ -> _..._ -> _Use_）。


4. 如果你有[支持CUDA的GPU](https://developer.nvidia.com/cuda-gpus)，你可以加速训练和推理：



   4.1 安装 **NVIDIA Container Toolkit** 如下所述[这里](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html#installing-with-apt)。NVIDIA Container Toolkit 受到[这里](https://docs.nvidia.com/cuda/wsl-user-guide/index.html#nvidia-compute-software-support-on-wsl-2)所述的支持。

   4.2 添加 _nvidia_ 作为运行时选项（见 _Docker Desktop_ -> _Change settings_ -> _Docker Engine_）。在配置文件中添加以下行：

   ```json
   "runtimes": {
       "nvidia": {
       "path": "nvidia-container-runtime",
       "runtimeArgs": []
   ```

   例如，完整的Docker Engine守护程序配置文件应如下所示：

   ```json
   {
     "builder": {
       "gc": {
         "defaultKeepStorage": "20GB",
         "enabled": true
       }
     },
     "experimental": false,
     "runtimes": {
       "nvidia": {
         "path": "nvidia-container-runtime",
         "runtimeArgs": []
       }
     }
   }
   ```

   再重启Docker Desktop。

5. 在终端中输入`code .`以在VS Code中打开项目。或者，你可以从UI中选择要打开的项目来启动VS Code。

6. 从VS Code的左侧_Extensions_菜单中选择安装 **Remote-Containers** 扩展

7. 打开DevContainer

由于`.devcontainer`文件夹位于`LLMs-from-scratch`主目录中（根据你的设置，某些文件夹可能无法在你的操作系统中显示），VS Code应该会自动检测到它并询问你是否要在DevContainer中打开项目。如果它没有，只需按`Ctrl + Shift + P`打开命令面板并开始输入`dev containers`以查看所有DevContainer特定选项的列表。

8. 选择 **Reopen in Container**

如果镜像还没有被构建过，Docker 将开始构建`.devcontainer`配置文件中指定的Docker映像，或者从一个可用的registry中拉取。

整个过程是自动化的，可能需要几分钟，具体取决于你的系统和互联网速度。你可以在VS Code的右下角点击“Starting Dev Container (show log)”来查看当前的构建进度。

一旦完成，VS Code将在新创建的Docker开发环境中自动连接到容器并重新打开项目，就像在本地机器上运行一样。你将能够像在本地机器上一样编写、执行和调试代码，但有了Docker的隔离和一致性的好处。

> [!警告]
> 如果你在构建过程中遇到错误，这可能是因为你的机器不支持NVIDIA容器工具集，你的机器没有兼容的GPU。在这种情况下，编辑`devcontainer.json`文件并删除` "runArgs": ["--runtime=nvidia", "--gpus=all"],`行，然后重新运行“重新打开Dev Container”过程。

9. 完成。

一旦镜像被拉取并构建完成，你应该能够在容器中看到你的项目，并且已经安装了所有需要的依赖项，可以开始开发了。

<br>

## 卸载Docker镜像


如果不再需要使用它，以下是卸载或删除Docker容器和镜像的说明。这个过程不会从你的系统中卸载Docker本身，而是清理了项目特定的Docker工件。


1. 根据你的DevContainer，列出所有Docker镜像：

```bash
docker image ls
```

2. 使用镜像ID或名称删除Docker镜像：

```bash
docker image rm [IMAGE_ID_OR_NAME]
```

<br>

## 卸载Docker

如果决定不使用Docker，你可以参考官方文档[这里](https://docs.docker.com/desktop/uninstall/)，了解卸载Docker的具体步骤。
