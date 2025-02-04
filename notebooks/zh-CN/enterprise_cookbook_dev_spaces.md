# 在 HF 空间中的互动开发

_作者：[Moritz Laurer](https://huggingface.co/MoritzLaurer)_

像 Google Colab 或 Kaggle Notebooks 这样的服务使得人们可以在浏览器中的 Jupyter notebooks 里轻松地访问计算资源。然而，这些服务也存在一些局限性：
- GPU 不稳定，训练任务可能在完成前被取消。
- GPU 选择仅限于几个单一 GPU。
- 没有原生支持通过本地 IDE（如 VS Code）连接到云端 GPU。

HF JupyterLab Spaces 克服了这些限制。使用 HF JupyterLab Space，你可以：
- 在浏览器中使用 JupyterLab 完成所有开发工作。
- 动态切换 CPU 和各种 GPU，除非你希望它们停止，否则硬件不会停止。
- 通过 SSH 将你的本地 IDE（如 VS Code）连接到云计算资源，进行完整的远程开发。

本教程将引导你完成设置自己的 JupyterLab Space 的步骤。

## 在 HF JupyterLab Spaces 中进行互动开发

### 创建你的 JupyterLab Space
要创建自己的 HF JupyterLab Space，请访问 [空间创建页面](https://huggingface.co/new-space?template=SpacesExamples%2Fjupyterlab)，然后点击 `Docker` > `JupyterLab`。HF JupyterLab Space 本质上是一个 Docker 容器，内含预配置的 JupyterLab 复制品，运行在 Hugging Face 的云基础设施上。以下是配置 JupyterLab Space 的一些建议：

- **选择正确的所有者**：如果你将 JupyterLab Space 用作企业组织的工作一部分，请在 `Owner` 下拉菜单中选择该组织的名称（例如，下面图像中的虚拟“enterprise-explorers”）。任何计算费用将会计入该企业组织的账户。
- **访问控制**：如果你只想让团队中的某些成员访问 JupyterLab Space，可以点击 `Everyone` 并限制对 JupyterLab Space 的访问，仅限于预定义的资源组。资源组是企业 Hub 的功能，它允许你将对特定仓库（如模型、数据集、Spaces）的访问限制给更小的团队成员群体。请参阅[文档](https://huggingface.co/docs/hub/en/security-resource-groups)了解如何创建你的第一个资源组。

<div style="flex justify-center">
    <img src="https://huggingface.co/datasets/huggingface/cookbook-images/resolve/main/enterprise-jupyterlab-creation-1.png" width="450">  
</div>

- **选择硬件**：你可以选择从免费的 CPU 到 A100 GPU 等各种硬件。设置 Space 时，我们建议选择免费的基础 CPU。等到你需要更强硬件时，可以切换到付费硬件（可查看可用硬件和价格 [这里](https://huggingface.co/pricing)）。
- **持久存储**：将持久存储附加到 Space 上非常重要，这样你创建的所有文件（代码、模型、数据）在 Space 暂停或重置时也能被保存。以后你也可以在设置中增加磁盘空间。所有持久数据都存储在 `/data` 目录中（[文档](https://huggingface.co/docs/hub/en/spaces-storage)）。
- **设置密码**：创建 Space 后，登录 JupyterLab 时需要密码。该密码通过 `JUPYTER_TOKEN` Space 密钥来定义。如果没有设置密码，默认密码是“huggingface”。建议设置一个强密码。
- **开发模式**：开发模式是为企业 Hub 用户提供的一项功能，它允许你通过 SSH 连接到任何 HF Space。启用此功能后，你可以通过 VS Code 进行远程开发，使用 Space 的云硬件（该功能也可以在后续启用/禁用）。有关预览文档，请参见[此处](https://huggingface.co/dev-mode-explorers)。
- **私有 Space**：作为额外的安全措施，建议将 Space 设置为私有，这样只有企业组织的成员（以及特定资源组成员）才能看到它。

<div style="flex justify-center">
    <img src="https://huggingface.co/datasets/huggingface/cookbook-images/resolve/main/enterprise-jupyterlab-creation-2.png" width="450">
</div>

设置好 JupyterLab Space 后，你可以点击 `Create Space`。Space 会开始构建，几秒钟后，你会看到 JupyterLab 的登录界面。此时，你可以使用之前定义的密码登录。

<div style="flex justify-center">
    <img src="https://huggingface.co/datasets/huggingface/cookbook-images/resolve/main/enterprise-jupyterlab-login.png">
</div>

### 使用你的 JupyterLab Space

现在，你可以在浏览器中使用自己的 JupyterLab Space 进行工作！你可以在左侧的文件浏览器中创建自己的目录结构，存放 .ipynb 笔记本或其他文件和数据集。如果你启用了持久存储，所有文件都会永久保存在 Space 的默认 `/data` 目录中。

<div style="flex justify-center">
    <img src="https://huggingface.co/datasets/huggingface/cookbook-images/resolve/main/enterprise-jupyterlab-first-notebook.png">
</div>

### 动态切换 CPU 和 GPU

与 Google Colab 等服务类似，你可以动态更改 Space 的硬件配置。我们建议先在免费或升级的 CPU 上进行初步工作，如数据清洗、设置终端或测试 API。一旦代码配置完成，你只需点击 Space 右上角的 `Settings`，即可切换到适合计算密集型推理或训练任务的硬件。更改硬件时，Space 会自动重启，所有环境变量会丢失（类似于 Google Colab），几秒钟后，你将在新硬件上获得一个全新的清洁环境。你的存储和保存的文件（如代码、数据等）当然也会随之迁移到新硬件上。下图显示了当前（2024 年 6 月）的可用硬件，未来会进行更新。

图像左下角显示的是 `Sleep time settings`，你可以设置在空闲时硬件运行多长时间。这是相较于 Google Colab 的一大优势。如果你想节省费用，可以设置 Space 在空闲 15 分钟后进入休眠模式；但如果你需要长达 48 小时或更长的训练运行，你可以防止 Space 进入休眠模式，任由它持续运行。你还可以手动暂停 Space，这样就不再为硬件付费。

<div style="flex justify-center">
    <img src="https://huggingface.co/datasets/huggingface/cookbook-images/resolve/main/enterprise-jupyterlab-hardware-options.png">
</div>

在设置下方，你会看到其他选项，如扩展存储、重置 Space 等。如果在创建 Space 时没有设置密码，你也可以在这里创建一个名为 `JUPYTER_TOKEN` 的密钥，替换默认的“huggingface”密码。

> [!TIP]
> 如果你在多日或多周的使用过程中，存储缓存积累了文件，当你收到持久存储已满的警告时，可能会认为存储配额还未达到，重新设置 Space 为出厂设置可以清空缓存，有时会有帮助。

### 自定义你的 JupyterLab Space

记住，你的 JupyterLab Space 本质上是一个预配置的 Docker 容器，因此，如果你熟悉 Docker，也可以根据自己的需求进行自定义。例如，你可以进入 Space 的 `Files` 部分，向 `requirements.txt` 文件中添加新依赖，或者你可以将默认的容器镜像更换为另一个镜像（例如，如果你需要预安装特定版本的 CUDA 和 PyTorch）。

<div style="flex justify-center">
    <img src="https://huggingface.co/datasets/huggingface/cookbook-images/resolve/main/enterprise-jupyterlab-files.png">
</div>

## 开发模式：通过本地 VS Code 在 HF Spaces 上开发

如果你不喜欢在浏览器中使用 JupyterLab，尝试使用 `开发模式`。`开发模式` 允许你通过 SSH 将本地 IDE（如 VS Code）连接到任何 Space 的硬件上。[HF Pro/Enterprise](https://huggingface.co/pricing) 订阅用户可以为任何 Space 启用 `开发模式`。

启用 `开发模式` 后，你会在 JupyterLab Space 窗口的左下角看到一个弹出窗口。要通过 SSH 连接到本地 VS Code，首先需要在本地安装 [VS Code Remote - SSH 插件](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh)，并将你的 SSH 密钥添加到 [HF 个人资料](https://huggingface.co/settings/keys) 中。点击 `Connect with VS Code`，应该会打开你的本地 VS Code 窗口，并与 Space 建立远程连接。任何支持通过 SSH 进行远程开发的 IDE 都可以使用类似的过程。

<div style="flex justify-center">
    <img src="https://huggingface.co/datasets/huggingface/cookbook-images/resolve/main/enterprise-jupyterlab-devmode-popup.png" width="450">
</div>

当你通过 SSH 连接到 Space 时，默认目录是空的 `/app` 目录。你需要切换到 `/data` 目录，这里保存了所有持久化的文件（代码、数据、模型等）。`/data` 目录是唯一一个保证在会话间持久存储文件的目录。如果你希望修改基础 Docker 容器，也可以访问 `/HOME/user/app` 目录。

> [!TIP]
> `/data` 目录中的持久化文件目前不会自动备份，因此建议定期备份重要文件，以避免数据丢失。




就这样，你可以在浏览器中运行 JupyterLab Space，动态切换多个强大的 GPU，并从本地 IDE 连接到硬件。

整个教程就是在一个免费的 CPU 空间中编写的，我们邀请你在自己的 JupyterLab Space 中跟随其他 Enterprise Hub Cookbook 的教程一起操作。