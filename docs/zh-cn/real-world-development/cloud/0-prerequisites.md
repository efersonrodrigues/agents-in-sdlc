---
title: "练习 0：先决条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

开始 Copilot 云智能体练习前，需要先完成环境准备。你将创建 Tailspin Toys 存储库的个人副本，并启动一个 [codespace][codespaces]，用于编辑指令文件并审查云智能体的工作成果。

## 设置实验存储库

通过[模板][template-repository]创建存储库副本，以便编写实验代码。新存储库包含实验所需的全部文件，后续练习都会使用它。

1. 在新的浏览器窗口中，转到 [Tailspin Toys 模板][tailspin-template]。
2. 在实验存储库页面选择 **Use this template**，再选择 **Create a new repository**，创建自己的存储库副本。

    ![Use this template 按钮](../../../_images/ex0-use-template.png)

3. 如果在 GitHub 或 Microsoft 主办的活动中参加本研讨会，请遵循导师提供的说明。否则，可在有权使用 GitHub Copilot 的组织中创建新存储库。

    ![输入存储库模板设置](../../../_images/ex0-repository-settings.png)

4. 记下所创建的存储库路径（**organization-or-user-name/repository-name**），后续实验会用到该路径。

## 创建 codespace

接下来，将使用 codespace 完成实验。

[GitHub Codespaces][codespaces] 是基于云的开发环境，可直接在浏览器中编写、运行和调试代码。它提供功能完整的 IDE，并支持多种编程语言、扩展和工具。

1. 打开刚创建的存储库。
2. 选择绿色的 **Code** 按钮。

    ![选择 Code 按钮](../../../_images/ex0-code-button.png)

3. 选择 **Codespaces** 选项卡，再选择 **+** 按钮创建新的 Codespace。

    ![创建新的 codespace](../../../_images/ex0-create-codespace.png)

创建 codespace 需要几分钟，但仍然比手动安装所有服务快得多。等待期间，可以了解 GitHub Copilot 的其他功能，接下来就会用到。

> [!CAUTION]
> 后续练习还会回到此 codespace。现在先将它保留在浏览器标签页中。

> [!NOTE]
> 本研讨会设计为在 codespace 或本地 [dev container][dev-containers] 中运行。这两种方式都能确保环境已安装顺畅体验所需的全部先决条件。如果更希望在本地运行，请在 VS Code 中打开克隆后的存储库，并在出现提示时选择 **Reopen in Container**。VS Code 会构建与 codespace 相同的 dev container。

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## 总结

恭喜，你已创建实验存储库的副本，并开始创建 codespace。后续将与 Copilot 云智能体协作时会用到它。

## 下一步

接下来为云智能体添加自定义指令。继续学习[练习 1 - 自定义指令][next-lesson]。

## 资源

- [GitHub Codespaces 概览][codespaces]
- [通过模板创建存储库][template-repository]
- [Codespaces 入门][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
