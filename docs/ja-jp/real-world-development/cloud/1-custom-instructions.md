---
title: "演習 1 - カスタム指示 (Cloud agent)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: Copilot cloud agent →][next-lesson]

生成 AI を利用する際は、コンテキストが重要です。タスクを特定の方法で実行する必要がある場合や、Copilot に知っておいてほしい背景情報がある場合は、そのコンテキストを参照できるようにします。[指示ファイル][instruction-files]を使うと、Copilot に「何を」してほしいかだけでなく、「どのように」実行してほしいかも伝えられます。

この演習では、次の操作を行います。

- リポジトリのカスタム指示とパス指定の指示ファイルを使って、プロジェクト固有のコンテキスト、コーディング ガイドライン、ドキュメント標準を Copilot に伝える方法を確認します。
- `.github/copilot-instructions.md` に新しいリポジトリ全体の標準を追加します。

> [!NOTE]
> VS Code や CLI のハーネスとは異なり、この演習では変更前後のプロンプトを比較しません。Copilot cloud agent は GitHub issue に対して非同期で動作するため、リアルタイムで並べて効果を示すのが難しいためです。後の演習で cloud agent が作成したプル リクエストを確認する際に、指示ファイルの影響を確認します。

## 指示ファイル

### シナリオ

優れた開発会社と同様に、Tailspin Toys には開発プラクティスに関するガイドラインと要件があります。たとえば、次のとおりです。

- データ レイヤーには必ずユニット テストを用意します。
- UI はダーク モードにし、現代的な印象にします。
- TSDoc doc コメントを使ってコードにドキュメントを追加します。
- 各ファイルの先頭に、ファイルの内容を説明するコメント ブロックを追加します。

指示ファイルを使って Copilot に適切な情報を提供し、これらのプラクティスに沿ってタスクを実行できるようにします。

### カスタム指示

カスタム指示を使うと、Copilot がコーディング スタイルや要件を理解できるように、コンテキストや好みを伝えられます。コーディング規約、ライブラリ、コメントの形式などを指定することで、より適切な提案やコード スニペットを得られます。リポジトリ全体、または特定のタスクやファイルの種類に指示を設定できます。

指示ファイルには 2 種類あります。

- `.github/copilot-instructions.md` は、リポジトリに対する**すべての**要求で Copilot に送信される単一の指示ファイルです。技術スタック、開発中の内容の概要、ベスト プラクティスなど、Copilot Chat や CLI でのほとんどの要求に関係するプロジェクト レベルの情報を記載します。
- `.github/instructions/*.instructions.md` は、特定のタスクやファイルの種類に対して作成できます。TypeScript や Astro などの言語、UI コンポーネントの作成やユニット テストの追加などのタスクに関する指示を記載できます。

> [!NOTE]
> IDE では、指示ファイルは Copilot Chat のコード生成にのみ使われ、コード補完や次の編集候補には使われません。
>
> Copilot Chat、Copilot CLI、Copilot cloud agent は、リポジトリ レベルの指示と `applyTo` frontmatter を持つ `*.instructions.md` ファイルの両方を使います。
>
> Copilot は AGENTS.md や CLAUDE.md など、ほかの標準に基づく指示ファイルにも対応しています。[詳細はこちら][custom-instructions-support]。

### 指示ファイルを管理するためのベスト プラクティス

指示ファイルの作成について詳しく説明することはこの演習の範囲外ですが、サンプル プロジェクトには代表的な方法が示されています。概要は次のとおりです。

- `copilot-instructions.md` には、開発内容、プロジェクト構造、全体的なコーディング標準など、プロジェクト レベルのガイダンスを記載します。
- `*.instructions.md` には、ユニット テスト、Astro コンポーネント、データ レイヤーなどのファイルの種類や、特定のタスクに関する指示を記載します。
- 自然な言葉を使い、明確なガイダンスと例を示します。

指示ファイルの作成方法は 1 つではありません。AI の他の利用と同様に、実際に試しながらプロジェクトに合う方法を見つけてください。

> [!TIP]
> GitHub Copilot を使う各プロジェクトには、十分な指示ファイルを用意してください。このプロジェクトの指示ファイルには、[UI の更新][ui-instructions]や [Astro][astro-instructions] など、さまざまなタスク向けのものがあります。
>
> Copilot に指示ファイルを生成してもらうこともできます。各環境で方法は異なります (たとえば VS Code の **Configure Chat → Generate Agent Instructions**、Copilot CLI の `/init`)。必要な場合は、対象環境のレッスンで説明します。
>
> テンプレートやひな形を探している場合は、指示ファイル、カスタム エージェントなどを集めたリポジトリ [awesome-copilot][awesome-copilot] を確認してください。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## このプロジェクトのカスタム指示ファイルを確認する

少し時間を取って、このリポジトリに含まれる指示ファイルを確認します。中心となる `copilot-instructions.md` と、さまざまなタスク向けの `*.instructions.md` ファイルがあります。エディターまたは GitHub Web UI で開いてください。

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの簡単な説明と、**Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** の下には、**GitHub Actions Workflows** の追加ガイダンスもあります。これらは Copilot とのすべてのやりとりに適用されます。
3. `.github/instructions` フォルダーを開いて内容を確認します。Astro ファイル、Drizzle データ レイヤー、テストなどの指示があります。
4. `.github/instructions/unit-tests.instructions.md` を開きます。先頭の `applyTo` フィールドは、リポジトリのルートを基準とする glob を設定します。ここでは、`**/*.test.ts` に一致するファイルなど、TypeScript のテスト ファイルに適用されます。
5. このプロジェクトでユニット テストを作成するための指示を確認します。
6. 最後に `.github/instructions/drizzle.instructions.md` を開き、末尾までスクロールします。`unit-tests.instructions.md` などの他の指示ファイルや、プロジェクト内の既存ファイルへのリンクがあります。大きな指示を再利用可能な小さなファイルに分け、Copilot が参照できる例を示せます (ここにあるパスはリポジトリのルートではなく、指示ファイルからの相対パスです)。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションではプロジェクトのコーディング標準を説明していますが、コード内のドキュメント作成はまだ必須ではありません。次の手順で、TSDoc doc コメントとファイル コメント ヘッダーのルールを追加します。

## 新しいブランチを作成する

ここではベスト プラクティスに従い、変更用のブランチを作成します。

1. 前の演習で使った codespace に戻ります。
2. 新しいターミナルを開きます。
3. 新しいブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions-cloud
   ```

## 新しい標準を追加する

前に説明したように、`.github/copilot-instructions.md` は Copilot にプロジェクト レベルの情報を伝えるためのファイルです。コード提案の質を高めるため、リポジトリのコーディング標準を記載しましょう。

1. `.github/copilot-instructions.md` を開き直します。
2. 27 行目付近にある **Code formatting requirements** セクションを探します。プロジェクトのコーディング標準が記載されていますが、コード内のドキュメント作成に関するルールがありません。
3. 既存の標準の直後に、次の Markdown 行を追加し、ファイル コメント ヘッダーと TSDoc doc コメントを追加するよう Copilot に指示します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md` を保存します。

> [!TIP]
> 前のレッスンで確認したように、リポジトリ レベルの `.github/copilot-instructions.md` には全体的な指示を、特定の言語、ファイルの種類、タスク向けの `*.instructions.md` ファイルには詳細な指示を記載できます。プロジェクト全体の標準である doc コメントのルールは、リポジトリ レベルのファイルに適しています。

## 指示の変更をコミット、プッシュ、マージする

cloud agent は issue の対象ブランチから作業用ブランチを作成します。次の演習で割り当てる issue は `main` から分岐するため、cloud agent が指示を使えるように、この変更を `main` に反映します。

1. ステージングしてコミットします。

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. ブランチをプッシュします。

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. github.com で `custom-instructions-cloud` から `main` へのプル リクエストを作成し、マージします。次の演習で Copilot に issue を割り当てると、cloud agent はこの指示を読み取ります。

> [!TIP]
> このワークショップで `main` に直接変更を加える場合は、ブランチを作成する手順を省略して、`main` にコミットしてもかまいません。実際のプロジェクトでの手順を体験できるように、ここではブランチを使っています。

## まとめと次のステップ

このプロジェクトの指示ファイルから Copilot がコンテキストを取得する方法を確認し、`.github/copilot-instructions.md` にリポジトリ全体の標準を追加しました。次の演習から、このハーネスで cloud agent が作成するプル リクエストに標準が適用されます。

次は [Copilot cloud agent に最初の issue を割り当てます][next-lesson]。

## リソース

- [GitHub Copilot のカスタマイズに使用する指示ファイル][instruction-files]
- [カスタム指示を作成するためのベスト プラクティス][instructions-best-practices]
- [Copilot 向けのより良いカスタム指示を書く 5 つのヒント][copilot-instructions-five-tips]
- [指示ファイルなどを集めた Awesome Copilot][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
