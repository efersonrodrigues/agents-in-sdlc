---
title: "演習 4 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

これまでの演習では、ユーザー エクスペリエンスの改善と機能追加を目的として、Copilot cloud agent に 3 つのタスクを依頼しました。cloud agent は非同期かつ自律的に動作するよう設計されていますが、タスクの進行状況を監視することも重要です。

cloud agent に割り当てたタスクを管理する方法はいくつかあります。たとえば、GitHub.com の[agents ページ][agents-page]では、オープンなプル リクエスト (PR) があるすべてのエージェント タスクを確認できます。実行内容を調べたり、進行中のセッションに方向を示したりできます。

このレッスンでは、次の操作を行います。

- agents ページで cloud agent のタスクを監視します。
- 実行中のセッションに指示を追加して、機能を依頼します。

## シナリオ

チームはエージェントにハイ コントラスト モードの作成を依頼した後、ライト モードも追加する良い機会だと考えました。サイトのスタイル更新と切り替え機能の実装を進めているため、ライト モードも含めるのが適切です。エージェントに方向を示し、ハイ コントラストに加えてライト モードも追加するよう依頼します。

## Copilot cloud agent のタスクを確認する

Copilot cloud agent に割り当てたタスクの現在の状態を確認しましょう。

1. [Copilot agents ページ](https://github.com/copilot/agents)に移動します。
2. メイン ペインと左ペインの両方でタスクの一覧を確認します。次のような Copilot に割り当てたタスクが表示されます。
    - コードベースのドキュメントの更新。
    - ゲーム変更用 API の生成。
    - Web サイトへのハイ コントラスト モードの追加。
3. 実行中のタスクを 1 つ選択し、Copilot が実行した作業を確認します。たとえば、次の内容が表示されます。
    - リポジトリのチェックアウト。
    - Copilot が作業する環境の作成。
    - MCP サーバーの設定。
    - 割り当てられたタスクを完了するための各種手順。

> [!NOTE]
> 表示される手順は、Copilot の作業状況や採用した方法によって異なります。

4. 右側に表示されるプル リクエスト (PR) ペインも確認します。ここから PR と変更されたファイルを確認し、作業を監視できます。

## cloud agent に方向を示す

実行中のタスクを確認できたので、ハイ コントラスト モードに取り組んでいる Copilot に、ライト モードの切り替えも追加するよう依頼します。

1. ハイ コントラスト モードを追加するセッションを選択します。Copilot が付けたタイトルや作業状況によって、表示される名前は異なります。

    ![mission control のアクセシビリティ セッション](../../../_images/ex6-accessibility-session.png)

2. セットアップが完了し、作業を開始したことが表示されるまで、数分間セッションを確認します。次のようなメッセージが表示されたら作業開始です。
3. **Steer active session while Copilot is working** ダイアログに、次のプロンプトを入力します。

    ```plaintext
    ハイ コントラスト モードの作業と合わせて、ライト モードも追加してください。このモードにも切り替えを用意し、ユーザーが希望する表示モードを選べるようにしてください。
    ```

    ![agents ページの cloud agent タスクで、Copilot の作業中にアクティブなセッションを誘導するダイアログが強調表示されています](../../../_images/ex6-steer-cloud-agent-task.png)

4. <kbd>Enter</kbd> を押してプロンプトを送信します。
5. Copilot がプロンプトを確認し、作業に取り込むことを確認します。

## Copilot に作業を進めてもらう

前回と同様に、Copilot は更新されたタスクに取り組みます。メッセージを送信した時点で作業中の手順が終わると、新しい依頼を作業の流れに取り込みます。

今回も完了まで数分かかります。その間に休憩し、これまでに学んだことを振り返りましょう。

## まとめと次のステップ

このレッスンでは、Copilot cloud agent のタスクを監視して指示するための中心的な場所である Copilot agents ページを確認しました。mission control では、進行中および完了したタスクを追跡し、実行内容を確認し、進行中のタスクの範囲を変更したり追加のガイダンスを与えたりできます。

次の内容を学びました。

- mission control と agents ページを使って cloud agent のタスクを監視する方法。
- 実行中のセッションに追加の機能を依頼する方法。

Copilot がアクセシビリティ機能を実装している間に、Copilot が作成したプル リクエストを[反復改善する][next-lesson]方法を確認しましょう。

## リソース

- [Copilot agents ページ][agents-page]
- [カスタム エージェントについて][custom-agents]

---

| [← 前のレッスン: カスタム エージェント][previous-lesson] | [次のレッスン: Copilot の作業を反復改善する →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
