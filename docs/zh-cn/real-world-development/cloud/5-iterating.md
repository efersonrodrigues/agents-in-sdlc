---
title: "练习 5：迭代 GitHub Copilot 的工作"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

## 审查工作

在整个实验中，你与 GitHub Copilot 协作完成了多项任务，以改进用户体验并添加功能。你要求 Copilot 为代码添加文档、实现供设计团队迭代的相关游戏功能，以及实现高对比度和浅色模式切换等无障碍功能。现在来检查代码更改；必要时向 Copilot 提供反馈，进一步改进结果。

### 场景

正如前面多次提到的，加入生成式 AI 并不会改变软件设计和 DevOps 的基本原则。仍然要审查生成的代码，并遵循常规 DevOps 流程。接下来，先审查 GitHub Copilot 创建的文档、相关游戏功能和无障碍功能，再为团队其他成员启用审查。

## GitHub Copilot 云智能体的安全性

Copilot 云智能体会在后台无人监督地执行任务，因此受到一些安全限制：

- Copilot 只能读取存储库，并且只能写入它用于处理任务的分支。
- 云智能体在 GitHub Actions 中运行，并在独立的临时环境中工作。
- 任何 GitHub Actions 工作流在运行前都需要人工批准。
- [默认情况下，外部资源访问受限](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall)，包括 MCP 服务器。

## 审查生成的文档

先查看 GitHub Copilot 云智能体创建的第一个 PR：为代码添加文档。此处使用 GitHub.com 上的标准 PR 界面。

> [!NOTE]
> 查看 PR 时，可能会看到 GitHub Copilot 被防火墙阻止的警告。这是**预期行为**，因为 Copilot 默认无法访问许多外部资源，包括外部 MCP 服务器。你可以[自定义或禁用 Copilot 云智能体防火墙][agent-firewall]。

1. 在新标签页中返回 github.com 上的存储库。
2. 选择 **Pull Requests**，打开 PR 列表。
3. 打开标题类似于 **Add missing documentation** 或更完整标题的 PR。

> [!NOTE]
> 如果 Copilot 仍在处理任务，PR 标题会带有 **[WIP]** 标记。请等待 Copilot 完成。可能需要几分钟，可以稍作休息或回顾目前学到的内容。

4. PR 准备好后，选择 **Files changed** 选项卡并审查更改。

    ![Files changed 选项卡](../../../_images/shared-pr-files-changed.png)

5. 查看新添加的 TSDoc 文档注释和其他文档。具体更改可能有所不同。检查 TSDoc 文档注释、TypeScript 规范和文件注释头；它们来自练习 2 开始时查看的自定义指令文件。
6. 审查更新并确认符合预期后，返回 **Conversation** 选项卡并向下滚动。
7. 查看是否有等待批准的工作流提示。
8. 如果有等待批准的工作流，请选择 **Approve and run workflows**。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. 你应能在 PR 的检查区域看到工作流已排队。如果一切正常，单体 Astro 应用的项目检查就会通过。检查可能需要几分钟。

## 向 GitHub Copilot 请求更改

与 Copilot 协作处理 PR 并非单向过程。你可以像提及团队成员一样在 PR 评论或代码行内评论中提及 Copilot。Copilot 会读取评论，并启动另一个会话来处理请求。由于结果具有非确定性，无法提供适用于所有情况的固定提示词。可以要求 Copilot：

- 在每个代码文件开头添加简短说明文件用途的注释头。
- 为 TypeScript 和 Astro 文件添加 TSDoc 文档注释。
- 创建 README，介绍 Astro 应用结构。

1. 添加评论并提及 **@copilot**，请求对生成的文档进行更改。可以使用上面的建议，也可以提出其他文档改进要求。
2. 选择 **View Session**，观察 Copilot 如何处理任务。你会看到它启动新会话进行更新。
3. 选择 **Back to pull request** 返回 PR。

    ![Back to pull request](../../../_images/ex7-back-to-pr.png)

4. Copilot 完成更改后，PR 中会出现新提交。
5. 选择 **Files changed** 选项卡，审查更改。

可以继续迭代，直到满意为止。完成后，可以将 PR 从草稿转换为准备审查状态，再合并到 main 分支。

![Convert PR to ready](../../../_images/ex7-ready-for-review.png)

## 审查相关游戏功能

返回 Copilot 为解决游戏详情页显示相关游戏议题创建的 PR。

1. 返回 GitHub.com 上的存储库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似于 **Show related games on the game details page** 或更完整标题的 PR。
4. 选择 **Files changed** 选项卡，审查生成的代码。
5. 审查更新并确认符合预期后，返回 **Conversation** 选项卡并向下滚动。
6. 查看是否有等待批准的工作流提示。
7. 如果有等待批准的工作流，请选择 **Approve and run workflows**。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

8. 你应能在 PR 的检查区域看到工作流已排队。如果一切正常，单体 Astro 应用的项目检查就会通过。检查可能需要几分钟。
9. **可选：**也可以在 Codespace 中检出此分支，手动测试相关游戏功能。打开 Codespace 终端并运行以下命令（将 `<branch-name>` 替换为 Copilot 创建的分支名，例如 **copilot/fix-8**）：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

Copilot 已创建相关游戏功能！与之前一样，可以迭代并要求 Copilot 更新。例如，可以调整显示的相关游戏数量，也可以要求添加文件注释头和 TSDoc 文档注释（请记住，分配此任务时，你尚未更新自定义指令）。与之前一样，在 **Conversation** 选项卡中发表评论即可提出请求，Copilot 会据此启动新会话。

## 审查无障碍功能

最后，审查使用无障碍自定义智能体实现的功能。此 PR 应同时包含练习 3 中分配的高对比度模式，以及练习 4 在任务控制中心请求的浅色模式。

1. 返回 GitHub.com 上的存储库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似于 **Add high contrast mode to website** 或更完整标题的 PR。

> [!NOTE]
> 如果 Copilot 仍在处理任务，PR 标题会带有 **[WIP]** 标记。请等待 Copilot 完成，可能需要几分钟。

4. 选择 **Files changed** 选项卡，审查生成的代码。
5. 审查实现时，重点检查：
   - 用于切换模式的 UI 组件。
   - 用于保存用户偏好的本地存储。
   - 高对比度和浅色模式的 CSS 或样式更改。
   - 无障碍属性（ARIA 标签、键盘导航等）。
   - 管理模式切换的 JavaScript/TypeScript 代码。
6. 审查更新并确认符合预期后，返回 **Conversation** 选项卡并向下滚动。
7. 查看是否有等待批准的工作流提示。
8. 如果有等待批准的工作流，请选择 **Approve and run workflows**。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. 你应能在 PR 的检查区域看到工作流已排队。如果一切正常，项目检查就会通过。检查可能需要几分钟。
10. **可选：**可以在 Codespace 中检出此分支，手动测试无障碍功能。打开 Codespace 终端并运行以下命令（将 `<branch-name>` 替换为 Copilot 创建的分支名）：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    然后启动应用，在浏览器中测试高对比度和浅色模式切换，并确认页面重新加载后仍保留设置。

请注意，无障碍自定义智能体帮助 Copilot 根据无障碍最佳实践实现这些功能。如果发现无障碍问题或改进点，可以像处理之前的 PR 一样，在评论中提及 **@copilot** 请求更新。

## 可选练习——继续委派工作

云智能体适合处理待办事项，让你能先专注其他工作。可以在自己的存储库中创建更多议题并分配给 Copilot，例如：

- 在游戏详情页创建支持者兴趣表单。
- 为游戏列表实现分页。
- 为数据访问辅助函数添加输入验证和错误处理。

## 总结

你已完成云智能体工作流。本系列课程中，你：

- **检查了存储库自带的自定义指令文件**，以便了解它们之后如何影响云智能体的输出。
- **将议题分配给 Copilot 云智能体**，观察它设置环境、制定计划并异步执行任务。
- **创建并使用自定义智能体**，为无障碍访问添加高对比度和浅色模式切换。
- **使用 Copilot 智能体页面作为任务控制中心**，监控并引导无障碍会话。
- **审查并迭代云智能体的拉取请求**，提及 `@copilot` 请求更改并批准工作流。

## 回顾与后续步骤

你已完成云智能体工作流。如果想继续探索，其他工作流可以从不同产品界面补充相关练习：

- 🖥️ **[VS Code 工作流](../../vscode/)** — 直接在 IDE 中探索 Copilot Chat 智能体模式和 MCP 集成。
- 💻 **[CLI 工作流](../../cli/)** — 在终端中交付两项经过审查的更改，并学习 Plan 和 Autopilot 模式、智能体技能、自定义 QA 智能体、Playwright MCP、Agent Merge，以及可选的 `/delegate` 云智能体桥接。

在自己的存储库中，还可以尝试：

- 将重构或测试覆盖率议题分配给云智能体。
- 为其他领域创建自定义智能体。
- 为不同技术栈设置 `copilot-setup-steps.yml`。

## 资源

- [GitHub Copilot][github-copilot]
- [关于 Copilot 智能体][copilot-agents]
- [将 GitHub 议题分配给 Copilot][assign-issue]
- [Copilot 云智能体设置工作流最佳实践][cloud-agent-best-practices]
- [配置 Copilot 云智能体防火墙][agent-firewall]

---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall
[previous-lesson]: ../4-managing-agents/
