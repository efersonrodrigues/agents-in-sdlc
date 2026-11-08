---
title: "练习 5 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Copilot 处于智能体模式时，会自主探索代码库、提出更改、编辑文件并运行命令。由于这些工作会在本机实时执行，VS Code 中的 Copilot Chat 会持续显示每次工具调用和文件编辑。你可以直接在聊天中审查每项差异、接受或拒绝单项更改，并通过后续提示词引导对话、改进或扩展工作，全程无需离开编辑器。

本练习将介绍如何：

- 实时监控无障碍智能体的工作。
- 审查并接受建议的文件编辑。
- 在会话进行中引导智能体，在高对比度模式之外添加浅色模式切换。

## 场景

你在[练习 4][previous-lesson]中使用的无障碍自定义智能体正在实现高对比度模式。工作进行期间，设计团队又提出了浅色模式切换请求，供觉得默认主题太暗的用户使用。无需从头开始新对话，你可以引导当前会话扩展工作范围。

## 监控 Copilot 进度

Copilot Chat 视图会显示智能体执行的每个步骤，包括探索的文件、运行的命令和提出的编辑。每次文件编辑都会在聊天中显示差异和 **Keep** / **Undo** 控件。

1. 返回练习 4 中的 Copilot Chat 视图。
2. 智能体工作时，滚动聊天窗口，查看工具调用。你会看到文件读取、文件编辑，以及它请求运行的终端命令。
3. 智能体提出文件编辑时，聊天中会显示差异：
   - 选择 **Keep** 接受更改。
   - 选择 **Undo** 撤销更改，让智能体重新尝试。
4. 也可以打开聊天顶部的 **Files changed** 指示器，查看智能体在本次会话中修改的全部文件。

> [!NOTE]
> 如果工具调用请求权限（例如运行终端命令），智能体会暂停并显示 **Allow** 提示。只批准你认可的命令。

5. 等待智能体完成高对比度模式。它会发送一条总结所做更改的最终消息。

## 引导智能体添加浅色模式

现在高对比度模式已就绪，可以在同一对话中扩展工作，添加浅色模式切换。由于继续使用同一聊天会话，智能体会保留先前工作的上下文，包括修改的组件、使用的样式方案和本地存储模式。

1. 在 Copilot Chat 输入框中发送以下后续提示词：

    ```plaintext
    Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
    ```

2. 智能体会查看现有更改，并在此基础上提出浅色模式相关修改。
3. 新编辑出现时，像处理高对比度模式一样逐项审查，并对每项差异选择 **Keep** 或 **Undo**。
4. 如果智能体的处理方向不符合预期，例如试图重构切换 UI，可以选择聊天输入框旁的 **Stop** 按钮停止任务，然后发送更明确的后续消息。

> [!TIP]
> 引导正在进行的会话比从头开始更快。可以使用后续提示词提出调整（例如“简化 CSS，使用 CSS 变量而不是重复选择器”）、纠正方向（例如“不要添加第三个切换项，把浅色模式放入现有设置面板”），或扩展范围（例如“为这两个切换项添加键盘快捷键”）。

## 审查工作集

提交工作前，快速检查智能体修改的所有内容。

1. 在 VS Code 中打开 **Source Control** 视图。
2. 审查已更改文件列表。应能看到 Astro 组件、样式和相关测试的更新。
3. 打开几个已更改文件查看差异。确认其中体现了自定义智能体的无障碍实践，例如 ARIA 属性、键盘导航、语义化 HTML 和本地存储持久化。
4. 确认满意后，在 Source Control 面板中暂存并提交更改。下一课会发布这些更改。

## 总结与后续步骤

你使用 Copilot Chat 智能体模式监控并引导了正在进行的会话：逐项审查文件编辑、接受或拒绝更改，并发送后续提示词扩展工作，同时保留上下文。

本课中，你了解了：

- 实时监控智能体工作。
- 接受或拒绝单项文件编辑。
- 使用后续提示词引导会话。

下一课将介绍如何[将无障碍工作作为拉取请求发布][next-lesson]，并审查本实验中本地自定义智能体生成的更改。

## 资源

- [VS Code 中的 Copilot Chat][copilot-chat-vscode]
- [使用智能体模式][agent-mode]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
