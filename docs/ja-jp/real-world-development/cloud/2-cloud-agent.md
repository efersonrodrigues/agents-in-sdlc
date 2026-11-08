---
title: "演習 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: カスタム指示][previous-lesson] |
|:--|

技術的負債に悩んでいない組織は、ほとんどないでしょう。未解決のセキュリティ問題、更新が必要なレガシー コード、実装する時間がなくバックログに残った機能リクエストなどがあります。GitHub Copilot の cloud agent は、コードの更新や機能追加などのタスクを自律的に実行できます。作業が完了すると、人間の開発者が確認できるドラフト PR を作成します。面倒な作業を任せて開発プロセスを加速し、より重要な作業に集中できます。

Copilot cloud agent を使って、次の内容を学びます。

- コード生成環境のカスタマイズ。
- 操作を安全に行う方法。
- 範囲を明確に定めた issue の重要性。
- issue を Copilot に割り当てる方法。

## シナリオ

Tailspin Toys には対処したい技術的負債があります。最初のサイトを開発した委託先がドキュメントを適切に整備しておらず、コードにドキュメントがほとんどありません。まず、アプリケーションのエクスポートされたすべての関数に TSDoc doc コメントを追加したいと考えています。

また、デザイン チームはゲームを見つけやすくしたいと考えています。各ゲームの詳細ページに、同じカテゴリに属する他のタイトルを関連ゲームとして表示します。受け入れテストで UX を試せるよう、完成度の高い実装はまだ必要ありません。現在はブロッカーですが、優先度の高い issue がほかにあります。

どちらも優先順位が下がりやすいタスクであり、Copilot cloud agent に適しています。Copilot cloud agent に非同期で処理させて別の作業に集中し、後から作業を確認して期待どおりかを判断できます。

## GitHub Copilot cloud agent の紹介

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) は、人間の開発者と同じようにバックグラウンドでタスクを実行します。人間の開発者と同様に、[GitHub issue を Copilot に割り当てる](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions)など、複数の方法で作業を依頼できます。割り当てると Copilot は進行状況を追跡するドラフト プル リクエストを作成し、環境を設定してタスクを開始します。作業中または完了後に Copilot のセッションを確認できます。提案された解決策のレビュー準備ができると、プル リクエストで通知されます。

## 範囲を明確にした指示の重要性

GitHub Copilot は魔法ではありません。考える手間を省けるわけではありません。一見簡単な操作でも、詳しく調べると複雑な場合があります。[Copilot cloud agent のタスク範囲を定める際は注意してください][cloud-agent-best-practices]。AI ペア プログラマーとして扱い、段階的に作業し、学び、試し、適応させます。生成 AI を利用しても、ソフトウェア開発の基本は変わりません。

## このリポジトリのカスタム指示

これまでの演習では、カスタム指示と Copilot のガイド方法を確認しました。カスタム指示を実際に試した場合は `.github/copilot-instructions.md` が機能することを確認済みです。まだの場合は、cloud agent に作業を割り当てる前に、このリポジトリに含まれる指示ファイルを読み取り専用で確認して、後でその影響を確認できるようにしましょう。

リポジトリの GitHub Web UI、または起動済みの codespace で次のファイルを開きます。

- `.github/copilot-instructions.md` — **Code standards** セクション、特に TypeScript の規約と TSDoc doc コメントの要件を確認します。
- `.github/instructions/unit-tests.instructions.md` — `applyTo` frontmatter を確認します。この指示は `**/*.test.ts` ファイルに適用されます。

次のセクションで **Code lacks documentation** issue を cloud agent に割り当てたら、結果のプル リクエストで TSDoc doc コメント、TypeScript の規約、コメント ヘッダーを確認します。後の演習で PR をレビューする際にも取り上げます。

## Copilot cloud agent の開発環境を設定する

担当者にかかわらず、コード作成には通常、特定の環境とセットアップが必要です。Copilot にタスクを割り当てるときも同様で、Copilot はソフトウェア エンジニアのように作業します。

cloud agent は GitHub Actions を使って作業環境を用意します。作業開始前に実行する特別なセットアップ ワークフローを `.github/workflows/copilot-setup-steps.yml` に作成して、[環境をカスタマイズ][setup-workflow]できます。必要な開発ツールと依存関係を利用できるようになります。学習しやすいように、このラボではあらかじめ設定済みです。単一の Astro アプリ用に、Node.js、プロジェクトの依存関係、エンドツーエンド テスト用のブラウザー バイナリ、移行とシードが済んだ SQLite データベースを利用できます。

```yaml
name: "Copilot Setup Steps"

# Allows you to test the setup steps from your repository's "Actions" tab
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Set the permissions to the lowest permissions possible needed for *your steps*. Copilot will be given its own token for its operations.
    permissions:
      # If you want to clone the repository as part of your setup steps, for example to install dependencies, you'll need the `contents: read` permission. If you don't clone the repository in your setup steps, Copilot will do this for you automatically after the steps complete.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Frontend / app setup - Node.js (the whole app is now Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migrate + seed the local SQLite database so builds and tests have data.
      - name: Set up the database
        run: npm run db:setup
```

一般的な GitHub ワークフローに見えますが、次の点に注目してください。

- `copilot-setup-steps` という 1 つのジョブが含まれます。このジョブは Copilot がプル リクエストの作業を始める前に GitHub Actions で実行されます。
- `workflow_dispatch` トリガーを使うと、リポジトリの **Actions** タブからワークフローを手動実行できます。Copilot の実行を待たずにワークフローの動作を確認できます。

## ドキュメントを追加する

ドキュメントの重要性は広く理解されていますが、情報が古い、またはドキュメントがないプロジェクトは少なくありません。こうした技術的負債が放置されると、生産性が下がり、コードベースの保守や新しい開発者の受け入れが難しくなります。Copilot はドキュメントの作成を得意としているため、cloud agent に割り当てるのに適した issue です。バックグラウンドで必要なドキュメントを生成し、後の演習で作業を確認します。

1. 新しいブラウザー タブで github.com のリポジトリに移動します。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しい issue ダイアログを開きます。
4. **Blank issue** を選択します。
5. **Title** に `Code lacks documentation` と入力します。
6. **Description** に次の内容を入力します。

    ```plaintext
    関数やメソッドには、必要に応じて TSDoc doc コメントを含めることが組織の要件です。しかし、最近の更新ではこの標準が守られていません。動作を明確にする doc コメントが含まれるよう、既存のコードを更新してください。
    ```

7. **Create** を選択して issue を作成します。
8. 右側で **Assign to Copilot** を選択し、割り当てダイアログを開きます。

  ![Copilot を issue に割り当てる画面](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。
10. **Pull Requests** タブを選択します。
11. 新しく生成されたプル リクエスト (PR) を開きます。タイトルは `[WIP]: Code lacks documentation` のようなものです。一覧に新しい PR が表示されない場合は、少し待ってからブラウザーを更新します。
12. 数分後、Copilot が todo リストを作成していることを確認します。

> [!NOTE]
> Copilot の todo リストが PR に表示されるまで数分かかることがあります。Copilot は先ほど説明したワークフローを実行して環境を作成し、プロジェクトを分析して、最適な方法を検討しています。

13. todo リストと、実行予定のタスクを確認します。
14. プル リクエストのタイムラインを下にスクロールし、Copilot が issue の作業を開始したことを確認します。
15. **View session** ボタンを選択します。

  ![Copilot のセッション画面](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 表示を更新するために、ブラウザーを再読み込みする必要がある場合があります。

16. ライブ セッションを確認し、Copilot がどのように問題を解決しているかを見ます。コードの調査、プロジェクトの状況の把握、計画を考えるための一時停止、コードの作成などを確認できます。

作業には数分かかります。Copilot cloud agent の主な目的は、非同期にタスクを処理して別の作業に集中できるようにすることです。この機能を活用するため、もう 1 つのタスクを cloud agent に割り当てた後、アプリケーションに機能を追加するコードを作成します。

## ゲーム詳細ページに関連ゲームのセクションを追加する

GitHub Copilot cloud agent の利点の 1 つは、作業を分担できることです。デザイン チーム向けに関連ゲームのセクションを追加する作業自体は長くかからないかもしれませんが、その時間を別の作業に使えます。cloud agent に割り当ててみましょう。

1. github.com のリポジトリに戻ります。
2. **Issues** タブを選択します。
3. **New issue** を選択します。
4. **Blank issue** を選択します。
5. **Title** に `Show related games on the game details page` と入力します。
6. **Description** に次の内容を入力します。

    ```markdown
    各ゲームの詳細ページに関連ゲームを表示し、より多くのゲームを見つけられるようにします。デザイン チームは UX を試し、受け入れテストを行いたいと考えています。要件は次のとおりです。

   - `src/lib/` に、指定されたゲームと同じカテゴリに属し、そのゲーム自体を除外した他のゲームを返すデータ アクセス ヘルパーを追加する
   - ヘルパーを使って、ゲーム詳細ページに「Related games」セクションを表示する
   - 関連ゲームがない場合に対応する
   - 新しいヘルパーのユニット テストを作成する
   - PR の作成前に、すべてのテストが合格することを確認する
    ```

7. **Create** を選択して issue を作成します。
8. 右側で **Assign to Copilot** を選択し、割り当てダイアログを開きます。

  ![Copilot を issue に割り当てる画面](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。

まもなく、Copilot が作業を開始したことを示す 👀 が issue の最初のコメントに表示されます。

![Copilot が issue に取り組んでいることを示す目の絵文字](../../../_images/ex4-issue-eyes-emoji.png)

Copilot は 2 つ目の依頼に取り組み始めました。Copilot cloud agent はソフトウェア エンジニアと同じように動作するため、常に監視する必要はありません。作業が完了したら確認します。次に、カスタム エージェントの作成と使用を学びましょう。

## まとめと次のステップ

このレッスンでは [GitHub Copilot cloud agent][copilot-agents]について学びました。cloud agent に issue を割り当てると、非同期で作業を依頼できます。技術的負債への対処、新機能の作成、別のフレームワークからのコード移行などに Copilot を利用できます。

次の内容を学びました。

- コード生成環境のカスタマイズ。
- 操作を安全に行う方法。
- 範囲を明確に定めた issue の重要性。
- issue を Copilot に割り当てる方法。

cloud agent がバックグラウンドで作業している間に、カスタム エージェントの作成と使用に取り組みます。[Copilot cloud agent は MCP サーバーも利用でき][cloud-agent-mcp]、前のモジュールで確認したカスタム指示も使えます。

## リソース

- [Copilot cloud agent について][copilot-agents]
- [GitHub issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップ ワークフローのベスト プラクティス][cloud-agent-best-practices]

| [次のレッスン: カスタム エージェント →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
