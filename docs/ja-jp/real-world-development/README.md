---
title: "実践的な開発"
slug: ja-jp/real-world-development
authors:
  - geektrainer
lastUpdated: 2026-09-16
---

現実的なシナリオ、完成したアプリケーション、共有バックログを使って、ソフトウェア開発ライフサイクル全体で GitHub Copilot を体験します。変更を計画し、コードを作成し、動作をテストし、プル リクエストをレビューし、エージェントを使って作業を管理する流れを繰り返します。

## シナリオ

架空の会社 Tailspin Toys で新しく働く開発者として、開発者向けテーマのボード ゲーム クラウドファンディング サービスに取り組みます。チームのバックログは GitHub issue としてすでに登録されており、作業を始められます。フィルターやページネーションなどの機能開発に加えて、アクセシビリティやコーディング標準などの品質改善も含まれます。

## 作業環境を選ぶ

GitHub Copilot は、どの環境で作業していても利用できます。希望する開発方法に合った環境を選択してください。各ワークショップは、それぞれ独自のセットアップから始まり、共通の Tailspin Toys シナリオを使います。

### [GitHub Copilot CLI][cli]

ターミナルでエージェント型アシスタントを使います。Plan と Autopilot の各モード、指示、スキル、カスタム エージェント、Playwright MCP、Agent Merge、実用的なスラッシュ コマンドを扱います。

### [GitHub Copilot app][app]

並行するエージェント セッションを実行し、セッション モードを切り替え、Canvas で共同作業を行い、デスクトップ アプリから GitHub issue とプル リクエストを管理します。

### [GitHub Copilot cloud agent][cloud]

GitHub issue を非同期エージェントに割り当て、作業に指示を追加し、進行状況を監視して、作成されたプル リクエストをレビューします。

### [Visual Studio Code][vscode]

Visual Studio Code と GitHub Codespaces で GitHub Copilot を使います。エディターを離れずに、Copilot Chat の agent mode、MCP サーバー、カスタム エージェントを利用します。

[cli]: cli/
[app]: app/
[cloud]: cloud/
[vscode]: vscode/
