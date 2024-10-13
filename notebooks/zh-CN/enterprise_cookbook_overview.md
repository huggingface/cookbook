# 企业级 Hub 操作指南

企业级 Hub 操作指南专为高级用户和企业设计，旨在帮助他们超越 Hugging Face Hub 的标准免费功能，将机器学习更深入地集成到生产工作流程中。本指南通过一系列可复制粘贴代码的 Jupyter Notebook 来帮助你开始使用 Hub 的高级功能。

<Youtube id="CPQGBn-yXJQ"/>


## 在 HF Spaces 中进行交互式开发
使用 JupyterLab Spaces，你可以像在 Google Colab 中一样启动个人 Jupyter Notebook，也可以选择更多可靠的 CPU 和 GPU（例如 H100 或 4xA10G），并可以随时切换。此外，通过激活 Spaces 开发模式，你还可以从本地 IDE（如 VSCode）使用这些云端硬件。阅读此指南以了解如何启动 GPU 并通过本地 IDE 连接到它。

更多详情，请参阅 [JupyterLab Spaces](https://huggingface.co/docs/hub/spaces-sdks-docker-jupyter) 和 [开发模式](https://huggingface.co/dev-mode-explorers) 文档。


## 推理 API（无服务器）
使用我们的无服务器推理 API，你可以通过简单的 API 调用测试各种开源模型（例如生成式 LLM、高效嵌入模型或图像生成器）。无服务器推理 API 有速率限制，主要用于初始测试或低容量使用。阅读此指南以了解如何查询无服务器推理 API。

更多详情，请参阅 [无服务器 API](https://huggingface.co/docs/api-inference/index) 文档。


## 推理端点（专用）

使用我们的专用推理端点，你可以轻松地在各种硬件上部署任何模型，本质上是通过几次点击就创建了你的个人生产就绪 API。阅读此指南以了解如何创建和配置你自己的专用端点。

更多详情，请参阅 [专用端点](https://huggingface.co/docs/inference-endpoints/index) 文档。 


## 使用 Argilla Spaces 进行数据标注

无论你是在进行 LLM 的零样本测试还是训练自己的模型，在机器学习之旅开始时，创建优质的测试或训练数据可能是最有价值的投资。Argilla 是一个免费、开源的数据标注工具，使你能够为文本、图像或音频任务创建高质量数据。阅读此指南以了解如何在浏览器中创建数据标注工作流程（单独或在更大的团队中）。

更多详情，请参阅 [Argilla](https://docs.argilla.io/en/latest/) 文档和 [HF Argilla Spaces](https://huggingface.co/docs/hub/spaces-sdks-docker-argilla) 集成。


## AutoTrain Spaces（即将推出）
使用 AutoTrain Spaces，你可以在简单的界面中训练自己的机器学习模型，无需任何代码。阅读此指南以了解如何在 Hub 上的 AutoTrain Space 中使用各种 GPU 微调你自己的 LLM。 

更多信息，请参阅 [AutoTrain](https://huggingface.co/docs/autotrain/index) 文档。


## 使用 Spaces 和 Gradio 创建私有演示

视觉演示比言语更有说服力。如果你想说服利益相关者认可机器学习最小可行产品（MVP），演示尤其重要。阅读此指南以了解如何使用 Gradio 在 Spaces 上创建私有机器学习演示。

更多信息，请参阅 [Spaces](https://huggingface.co/docs/hub/spaces-overview) 和 [Gradio Spaces](https://huggingface.co/docs/hub/spaces-sdks-gradio) 文档。


## Hub 上的高级协作（即将推出）

随着你的团队和用例的增长，管理数据集、模型和团队成员变得更加复杂。阅读此指南以了解高级协作功能，如特定资源组的私有数据集、基于 git 的版本控制以及模型卡片中的 YAML 标签。 

更多信息，请查看 [Hub](https://huggingface.co/docs/hub/index) 和 [Hub Python 库](https://huggingface.co/docs/huggingface_hub/index) 文档。