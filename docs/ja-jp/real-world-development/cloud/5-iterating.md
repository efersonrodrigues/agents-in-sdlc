---
title: "演習 5: GitHub Copilot の作業を反復改善する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

## 作業を確認する

このラボでは、ユーザー エクスペリエンスの改善と機能追加を目的に、GitHub Copilot といくつかのタスクに取り組みました。コードへのドキュメント追加、デザイン チームが改善できる関連ゲーム機能の作成、ハイ コントラストとライト モードの切り替えを含むアクセシビリティ機能の実装を依頼しました。コードの変更を確認し、必要に応じて Copilot にフィードバックを伝え、作業を改善しましょう。

### シナリオ

これまでに何度も確認したとおり、生成 AI を利用しても、ソフトウェア設計や DevOps の基本は変わりません。生成されたコードを確認し、通常の DevOps プロセスに沿って作業します。まず、チームの残りのメンバーにレビューを有効にする前に、ドキュメント、関連ゲーム機能、アクセシビリティ機能に関する GitHub Copilot の提案を確認しましょう。

## GitHub Copilot cloud agent のセキュリティ

Copilot cloud agent は非同期かつ監督なしでタスクを実行するため、安全性を保つためのセキュリティ制約が設けられています。次のような制約があります。

- Copilot はリポジトリへの読み取りアクセスのみを持ち、書き込みアクセスはコード用のブランチに限られます。
- cloud agent は GitHub Actions 内で動作し、作業用の独立した一時環境を作成します。
- GitHub Actions ワークフローの実行には、人による承認が必要です。
- MCP サーバーを含む[外部リソースへのアクセスは、既定で制限されています](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall)。

## 生成されたドキュメントを確認する

まず、コードにドキュメントを追加するために GitHub Copilot cloud agent が作成した最初のプル リクエスト (PR) を確認します。GitHub.com の標準的な PR インターフェイスを使います。

> [!NOTE]
> PR を確認すると、GitHub Copilot がファイアウォールでブロックされているという警告が表示される場合があります。Copilot は、外部 MCP サーバーへの呼び出しなど、既定では外部リソースへのアクセスが制限されているため、これは**想定どおり**です。必要であれば、[Copilot cloud agent のファイアウォールをカスタマイズまたは無効化][agent-firewall]できます。

1. 新しいブラウザー タブで github.com のリポジトリに戻ります。
2. **Pull Requests** を選択して、プル リクエストの一覧を開きます。
3. **Add missing documentation** など、同様のタイトルが付いたプル リクエストを開きます。

> [!NOTE]
> Copilot がまだ作業中の場合、プル リクエストには **[WIP]** が付いています。その場合は、Copilot が作業を完了するまで待ちます。数分かかることがあるため、休憩したり、これまでに学んだことを振り返ったりしてください。

4. プル リクエストの準備ができたら、**Files changed** タブを選択して変更を確認します。

    ![Files changed タブ](../../../_images/shared-pr-files-changed.png)

5. TSDoc doc コメントなど、更新されたコードを確認します。変更内容は状況によって異なります。

    変更を確認しながら、TSDoc doc コメント、TypeScript の規約、コメント ヘッダーを探します。これらは演習 2 の最初に確認したカスタム指示ファイルで指定されています。

6. 更新内容に問題がなければ、**Conversation** タブに戻り、下にスクロールします。
7. 一部のワークフローが承認待ちになっていることを示す表示を探します。
8. ワークフローが承認待ちの場合は、**Approve and run workflows** を選択します。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)
9. プル リクエストのチェック欄にワークフローが登録されます。問題がなければ、単一の Astro アプリのプロジェクト チェックが成功します。完了まで数分かかることがあります。

## GitHub Copilot に変更を依頼する

プル リクエストで Copilot と作業することは、一方通行ではありません。チーム メンバーに依頼するのと同じように、プル リクエストのコメントやコードへのインライン コメントで Copilot にメンションできます。Copilot はコメントを確認し、対応するための新しいセッションを開始します。結果は非決定的なため、必ずこう依頼すべきという文面はありません。次のような変更を Copilot に依頼できます。

- 各コード ファイルの先頭に、内容を簡潔に説明するコメント ヘッダーを追加する。
- TypeScript と Astro のファイルに TSDoc doc コメントを追加する。
- Astro アプリの構造を説明する README を作成する。

1. 上記の例などを使い、コードベースに追加したいドキュメントについて、**@copilot** をメンションして生成されたドキュメントの変更を依頼するコメントを追加します。
2. **View Session** を選択し、Copilot が作業する様子を確認します。Copilot が更新用の新しいセッションを開始します。
3. **Back to pull request** を選択して、プル リクエストに戻れます。

    ![Back to pull request](../../../_images/ex7-back-to-pr.png)

4. Copilot が変更を完了すると、プル リクエストに新しいコミットが表示されます。
5. **Files changed** タブを選択して変更を確認します。

納得できるまで反復改善を続けてください。完了したら、PR をドラフトからレビュー可能な状態に変更し、`main` ブランチにマージできます。

![Convert PR to ready](../../../_images/ex7-ready-for-review.png)

## 関連ゲーム機能を確認する

ゲーム詳細ページに関連ゲームを表示する issue に対して Copilot が作成した PR を確認します。

1. GitHub.com のリポジトリに戻ります。
2. **Pull Requests** タブを選択します。
3. **Show related games on the game details page** など、同様のタイトルが付いた PR を選択します。
4. **Files changed** タブを選択し、生成されたコードを確認します。
5. 更新内容に問題がなければ、**Conversation** タブに戻り、下にスクロールします。
6. 一部のワークフローが承認待ちになっていることを示す表示を探します。
7. ワークフローが承認待ちの場合は、**Approve and run workflows** を選択します。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)
8. プル リクエストのチェック欄にワークフローが登録されます。問題がなければ、単一の Astro アプリのプロジェクト チェックが成功します。完了まで数分かかることがあります。
9. **省略可能:** Codespace でこのブランチに切り替え、関連ゲーム機能を手動でテストすることもできます。Codespace に移動してターミナルを開き、次のコマンドを実行します (`<branch-name>` は Copilot が作成したブランチ名、たとえば **copilot/fix-8** に置き換えます)。

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

Copilot が関連ゲーム機能を作成しました。前の作業と同様に、Copilot cloud agent に更新を依頼して、反復的に改善できます。たとえば、表示する関連ゲームの数を調整するよう依頼したり、コメント ヘッダーや TSDoc doc コメントを追加するよう依頼したりできます (この作業はカスタム指示を更新する**前**に割り当てたことを思い出してください)。**Conversation** タブに新しいコメントを追加すると、Copilot が確認して新しいセッションを開始します。

## アクセシビリティ機能を確認する

最後に、アクセシビリティ カスタム エージェントを使って実装した機能を確認します。この PR には、演習 3 で依頼したハイ コントラスト モードと、演習 4 の mission control で依頼したライト モードの両方が含まれているはずです。

1. GitHub.com のリポジトリに戻ります。
2. **Pull Requests** タブを選択します。
3. **Add high contrast mode to website** など、同様のタイトルが付いた PR を選択します。

> [!NOTE]
> Copilot がまだ作業中の場合、プル リクエストには **[WIP]** が付いています。その場合は、Copilot が作業を完了するまで待ちます。数分かかることがあります。

4. **Files changed** タブを選択し、生成されたコードを確認します。
5. 実装を確認し、特に次の点を確認します。
   - モードを切り替える UI コンポーネント。
   - ユーザー設定を保持するための local storage の使用。
   - ハイ コントラスト モードとライト モードの CSS またはスタイルの変更。
   - アクセシビリティ属性 (ARIA ラベル、キーボード操作など)。
   - モード切り替えを管理する JavaScript/TypeScript コード。

6. 更新内容に問題がなければ、**Conversation** タブに戻り、下にスクロールします。
7. 一部のワークフローが承認待ちになっていることを示す表示を探します。
8. ワークフローが承認待ちの場合は、**Approve and run workflows** を選択します。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)
9. プル リクエストのチェック欄にワークフローが登録されます。問題がなければ、単一の Astro アプリのプロジェクト チェックが成功します。完了まで数分かかることがあります。
10. **省略可能:** Codespace でこのブランチに切り替え、アクセシビリティ機能を手動でテストできます。Codespace に移動してターミナルを開き、次のコマンドを実行します (`<branch-name>` は Copilot が作成したブランチ名に置き換えます)。

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    次にアプリケーションを起動し、ブラウザーでハイ コントラストとライト モードの切り替えをテストして、ページを再読み込みしても設定が保持されることを確認します。

アクセシビリティ カスタム エージェントが、アクセシビリティのベスト プラクティスに従って機能を実装するよう Copilot を導いたことを確認してください。アクセシビリティ上の問題や改善点があれば、前の PR と同様にコメントで **@copilot** に更新を依頼できます。

## 省略可能な演習 — 委任を続ける

cloud agent は、バックログの実際の項目を割り当てて別の作業に集中できるときに効果を発揮します。習慣を身につけるため、リポジトリに issue をいくつか作成し、Copilot に割り当ててみてください。たとえば、次のような内容があります。

- ゲーム詳細ページに支援者向けの関心フォームを作成する。
- ゲーム一覧ページにページネーションを実装する。
- データ アクセス ヘルパーに入力検証とエラー処理を追加する。

## まとめ

Cloud agent ハーネスを完了しました。各レッスンを通じて、次のことを行いました。

- **このリポジトリに含まれるカスタム指示ファイルを確認**し、後で cloud agent の出力にどのように反映されるかを確認しました。
- **Copilot cloud agent に issue を割り当て**、環境のセットアップ、計画、非同期の実行を確認しました。
- **カスタム エージェントを作成して使用**し、ハイ コントラストとライト モードの切り替えを追加しました。
- **Copilot agents ページを mission control として利用**し、アクセシビリティ セッションを監視して途中で指示を追加しました。
- **cloud agent のプル リクエストを確認して改善**し、`@copilot` に変更を依頼してワークフローを承認しました。

## レビューと次のステップ

Cloud agent ハーネスを完了しました。ほかのハーネスでは、今回学んだ内容をさらに実践できます。

- 🖥️ **[VS Code ハーネス](../../vscode/)** — IDE から Copilot Chat の agent mode と MCP 統合を体験します。
- 💻 **[CLI ハーネス](../../cli/)** — Plan、Autopilot、エージェント スキル、カスタム QA エージェント、Playwright MCP、Agent Merge、および cloud agent に戻る省略可能な `/delegate` ブリッジを使い、ターミナルからレビュー済みの変更を 2 つ届けます。

自分のリポジトリで、次のアイデアを試してください。

- リファクタリングやテスト カバレッジの issue を cloud agent に割り当てる。
- 別の分野のカスタム エージェントを作成する。
- 別のスタック向けに `copilot-setup-steps.yml` を設定する。

## リソース

- [GitHub Copilot][github-copilot]
- [Copilot エージェントについて][copilot-agents]
- [GitHub issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップ ワークフローのベスト プラクティス][cloud-agent-best-practices]
- [Copilot cloud agent ファイアウォールの設定][agent-firewall]

---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
