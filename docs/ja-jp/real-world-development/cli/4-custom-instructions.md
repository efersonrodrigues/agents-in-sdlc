---
title: "レッスン 4 - カスタム指示で Copilot を導く"
description: "リポジトリの指示を確認し、ドキュメント標準を追加して、絞り込み機能のコードに適用します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

生成 AI を利用する際は、コンテキストが重要です。タスクを特定の方法で実行する必要がある場合は、Copilot がそのガイダンスを参照できるようにします。[指示ファイル][instruction-files]では、必要なコードだけでなく、その構成方法も説明できます。絞り込み機能を実装できたので、Copilot が使った指示を確認し、ドキュメント標準を追加してコードに適用します。

このレッスンでは、次の操作を行います。

- リポジトリの指示とパス指定の指示ファイルがエージェントに適用される方法を確認します。
- コーディング標準に従うよう指示ファイルを更新します。
- 指示ファイルがコードに与える影響を確認します。

## シナリオ

優れた開発会社と同様に、Tailspin Toys には開発プラクティスに関するガイドラインと要件があります。たとえば、次のとおりです。

- コメントでは、コードの内容を言い換えるのではなく、意図や自明でない決定を説明します。
- `db/` と `src/lib/` のエクスポートされた関数には、目的、パラメーター、戻り値を TSDoc/JSDoc で記載します。`db` 引数を注入する場合は、その説明も含めます。
- 再利用可能な Astro コンポーネントには `Props` の契約を記載し、関連コードが変更された際にコメントも最新の状態にします。
- 既存の書式設定と lint のガイダンスを維持します。

指示ファイルを使って Copilot に適切な情報を提供し、これらのプラクティスに沿ってタスクを実行できるようにします。

## 指示ファイル

カスタム指示を使うと、Copilot がコーディング スタイルや要件を理解できるように、コンテキストや好みを伝えられます。コーディング規約、ライブラリ、コメントの形式などを指定することで、より適切な提案やコード スニペットを得られます。リポジトリ全体、または特定のタスクやファイルの種類に指示を設定できます。

指示ファイルには 2 種類あります。

- `.github/copilot-instructions.md` は、リポジトリに対する**すべての**要求で Copilot に送信される単一の指示ファイルです。ほとんどの要求に関係するプロジェクト レベルの情報を記載します。
- `.github/instructions/*.instructions.md` は、特定の言語、ファイルの種類、タスクに関する指示を記載します。

> [!NOTE]
> 指示の形式とサポートは環境によって異なります。特定の形式に依存する前に、[カスタム指示のサポート リファレンス][custom-instructions-support]を確認してください。

## このプロジェクトのカスタム指示ファイルを確認する

スターター プロジェクトには、作業を始めるための指示ファイルが含まれています。変更を加える前に、既存のファイルを確認し、変更後の影響と比較しましょう。

1. Codespace に戻ります。
2. Codespaces エディターで (ターミナルではなく) `.github/copilot-instructions.md` を開きます。
3. プロジェクトの簡単な説明とコーディング ガイダンスを確認します。このリポジトリで Copilot とやりとりするすべての場面に適用されます。
4. `.github/instructions` フォルダーを開き、ファイルを確認します。Astro ファイル、Drizzle データ レイヤー、テストなどの指示があります。
5. `.github/instructions/unit-tests.instructions.md` を開きます。先頭の `applyTo` フィールドが、適用対象を決める glob を設定しています。
6. `.github/instructions/drizzle.instructions.md` を開き、他の指示ファイルやプロジェクト ファイルへのリンクを確認します。大きな指示を小さく再利用可能なファイルに分け、Copilot が参照できる例を示せます。

## チームのガイダンスに合わせて指示ファイルを更新する

既存のファイルは良い出発点ですが、まだ不十分な点があります。`copilot-instructions.md` を編集し、新しく生成される TypeScript に TSDoc コメントを追加するよう指示します。

1. `.github/copilot-instructions.md` で、35 行目付近にある **Code formatting guidance** セクションを探します。
2. 最後の箇条書きとして、次の行を追加します。

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

ファイルは自動的に保存されます。

## 更新したガイダンスを使う

Copilot CLI は会話の開始時にリポジトリの指示を読み込みます。更新した指示を保存したら、会話を終了して絞り込みの会話を再開します。これで機能のコンテキストを失わずに、新しいガイダンスを読み込めます。

1. 絞り込みの会話が開いている場合は、`/exit` を入力して閉じます。Copilot CLI は会話を自動的に保存します。
2. `game-filters-cli` ブランチのリポジトリ ルートで、保存した会話を再開します。

   ```bash
   copilot --resume
   ```

   選択画面が表示された場合は絞り込みの会話を選び、`game-filters-cli` ブランチがチェックアウトされていることを確認します。
3. 次のように Copilot に依頼して、更新したガイダンスを適用します。

   ```plaintext
   指示とコードのガイダンスを更新しました。生成したコードをガイダンスに合わせて更新してください。
   ```

4. `/diff` を入力し、変更された TypeScript ファイルを確認します。新しい TSDoc コメントが追加され、その説明がコードの内容と合っていることを確認します。

## まとめと次のステップ

Copilot CLI が指示ファイルからコンテキストを取得する方法を確認し、新しい標準を機能に適用しました。具体的には、次の作業を行いました。

- リポジトリの指示とパス指定の指示ファイルがエージェントに適用される方法を確認しました。
- コーディング標準に従うよう指示ファイルを更新しました。
- 指示ファイルがコードに与える影響を確認しました。

次は、再利用可能な `quality-checks` スキルを[カスタマイズして実行し][next-lesson]、lint とテストを一貫して実行します。

## リソース

- [Copilot CLI 用のカスタム指示を追加する][instruction-files]
- [カスタム指示のサポート][custom-instructions-support]
- [カスタム指示を作成するためのベスト プラクティス][instructions-best-practices]
- [指示ファイルなどを集めた Awesome Copilot][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
