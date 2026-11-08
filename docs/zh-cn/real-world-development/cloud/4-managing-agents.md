---
title: "练习 4 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

前几节练习中，你要求 Copilot 云智能体执行了三项不同任务，帮助改进用户体验并添加功能。云智能体能够异步自主工作，但监控这些任务仍然很重要。

你可以使用多种工具管理分配给云智能体的任务，包括 GitHub.com 上的[智能体页面][agents-page]。在这个任务控制中心，可以查看所有包含未关闭拉取请求 (PR) 的智能体任务，探索执行过的操作，甚至引导正在进行的会话。

本课将介绍如何：

- 浏览智能体页面，监控云智能体任务。
- 引导正在进行的会话，请求添加其他功能。

## 场景

分配高对比度模式任务后，团队意识到也可以同时添加浅色模式。由于智能体已经在更新网站样式并添加切换功能，因此增加浅色模式很合理。你将引导智能体继续工作，确保它在实现高对比度模式的同时也加入浅色模式。

## 审查 Copilot 云智能体任务

查看当前分配给 Copilot 云智能体的所有任务状态。

1. 转到 [Copilot 智能体页面](https://github.com/copilot/agents)。
2. 查看主面板和左侧面板中的任务列表。应能看到你分配给 Copilot 的任务，包括：
   - 为代码库更新文档。
   - 生成用于修改游戏的 API。
   - 为网站添加高对比度模式。
3. 选择一个正在运行的任务，查看 Copilot 已执行的操作，例如：
   - 从存储库检出代码。
   - 创建 Copilot 工作环境。
   - 设置 MCP 服务器。
   - 执行完成分配任务所需的其他步骤。

> [!NOTE]
> 列出的具体步骤会因 Copilot 工作状态及其采用的方法而异。

4. 同时留意右侧的拉取请求 (PR) 面板。可以通过它查看 PR 和更改的文件。

## 引导云智能体

现在已经了解正在运行的任务，接下来要求 Copilot 在实现高对比度模式时加入浅色模式切换功能。

1. 选择与添加高对比度模式相关的会话。确切标题会因 Copilot 使用的名称和当前工作状态而异。

    ![任务控制中心中的无障碍会话](../../../_images/ex6-accessibility-session.png)

2. 观察会话几分钟，等待设置完成并开始执行任务。开始看到类似下方的消息时，就表示已进入这一阶段。
3. 在 **Steer active session while Copilot is working** 对话框中，添加以下提示词：

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![Copilot 智能体页面中的任务截图，其中高亮显示 Steer active session while Copilot is working 对话框](../../../_images/ex6-steer-cloud-agent-task.png)

4. 按 <kbd>Enter</kbd> 发送提示词。
5. 留意 Copilot 如何确认提示词，并将其纳入工作流程。

## 让 Copilot 完成工作

与之前一样，Copilot 会继续处理更新后的任务！发送消息时，Copilot 会先完成当前步骤，再将新请求加入工作流程。

这同样需要几分钟。等待期间，可以暂停一下，回顾目前学到和探索的内容。

## 总结与后续步骤

本课介绍了 Copilot 智能体页面，这是监控和引导 GitHub Copilot 云智能体任务的中心位置。通过任务控制中心，可以跟踪所有活动和已完成的任务、审查正在执行的工作，并重定向进行中的任务以调整范围或提供其他指导。

本课中，你：

- 使用任务控制中心和智能体页面监控了云智能体任务。
- 重定向了正在进行的会话，请求添加其他功能。

Copilot 正在完成无障碍功能。接下来，你将[迭代 Copilot 创建的拉取请求][next-lesson]。

## 资源

- [Copilot 智能体页面][agents-page]
- [关于自定义智能体][custom-agents]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
