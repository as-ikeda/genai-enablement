# Git運用方針

## 目的

このプロジェクトでは、生成AIパスポートの資格学習と社内向けAI活用ガイド作成を進めながら、Gitの基本的な使い方も学べる運用にする。

難しいGit Flowではなく、個人・小規模PJで使いやすい「main + 作業ブランチ」のシンプルな運用を採用する。

## 基本方針

- `main` は安定版として扱う
- 作業は必ず目的別ブランチで行う
- 1ブランチ = 1つの目的にする
- 変更がまとまったらコミットする
- `main` に戻す前に差分を確認する
- Git操作そのものも学習ログ・社内展開ネタとして扱う

## ブランチ構成

| ブランチ | 用途 | 例 |
| --- | --- | --- |
| `main` | 安定版。社内共有してよい状態 | 初期整理済み資料、完成したガイド |
| `docs/*` | ドキュメント追加・整理 | `docs/git-workflow`, `docs/ai-guide-v1` |
| `study/*` | 学習ログ・試験対策の更新 | `study/chapter-01-ai-basic` |
| `practice/*` | 実務活用例・検証ログの追加 | `practice/codex-study-plan` |
| `fix/*` | 誤字修正・リンク修正など小さな修正 | `fix/reference-link` |

## ブランチ命名ルール

```text
種別/内容
```

### 種別

| 種別 | 使う場面 |
| --- | --- |
| `docs` | ガイド、手順書、成果物計画を整備する |
| `study` | 学習ログ、試験対策、弱点管理を更新する |
| `practice` | AI活用事例、検証ログ、プロンプト例を追加する |
| `fix` | 誤字、リンク、表記ゆれなどを直す |

### 例

```text
docs/git-workflow
study/chapter-01-ai-basic
practice/codex-study-plan
fix/exam-date-note
```

## 日常の流れ

### 1. mainを最新にする

```powershell
git switch main
git pull
```

### 2. 作業ブランチを作る

```powershell
git switch -c docs/git-workflow
```

### 3. ファイルを編集する

Markdownを更新する。Codexに作成・整理してもらってもよい。

### 4. 差分を確認する

```powershell
git status
git diff
```

### 5. コミットする

```powershell
git add .
git commit -m "Add Git workflow guide"
```

### 6. リモートへpushする

```powershell
git push -u origin docs/git-workflow
```

### 7. mainへ反映する

GitHub上でPull Requestを作成して確認する。個人運用で急ぎの場合はローカルでmergeしてもよい。

推奨はPull Requestを使うこと。Gitの流れを学びやすく、差分確認の練習にもなる。

## Pull Requestで確認すること

- 目的に合った変更だけが入っているか
- 社内共有してよい表現になっているか
- 公式情報のURLと確認日があるか
- 個人情報、顧客情報、機密情報が含まれていないか
- READMEやINDEXからたどれるか

## コミットメッセージ方針

英語でも日本語でもよいが、何をしたかが一目で分かるようにする。

| 種類 | 例 |
| --- | --- |
| 追加 | `Add study schedule for August exam` |
| 更新 | `Update exam plan with study hours` |
| 修正 | `Fix reference links` |
| 整理 | `Organize AI guide outline` |

## このPJでの推奨運用

| 作業 | ブランチ例 | コミット粒度 |
| --- | --- | --- |
| 第1章の学習ログ追加 | `study/chapter-01-ai-basic` | 学習ログ1件で1コミット |
| 週次レビュー更新 | `study/weekly-review-2026-07-05` | 週次レビュー単位 |
| AI活用ガイド更新 | `docs/ai-guide-v1` | 見出し・章単位 |
| プロンプト集追加 | `practice/prompt-library` | テーマ単位 |
| 誤字修正 | `fix/typo-2026-07` | まとめて1コミット |

## 運用の軽量ルール

- 完璧なブランチ名にこだわりすぎない
- 迷ったら `docs/`, `study/`, `practice/`, `fix/` のどれかにする
- 1日の作業終わりに `git status` を見る
- mainへ直接コミットしない練習をする
- 途中でもpushしてよい。バックアップにもなる

## 社内メンバーへの伝え方

このPJでは、資格取得だけでなく、Gitの基本操作も一緒に学ぶ。

- ブランチを切る: 作業場所を分ける
- コミットする: 作業の区切りを記録する
- pushする: GitHubへバックアップ・共有する
- Pull Requestを作る: 変更内容を見直す
- mergeする: 安定版に反映する

Gitを「開発者だけのもの」として扱わず、学習記録・資料作成・社内ナレッジ整理にも使えるものとして体験する。