# Gitコマンド早見表

## 最初に見るコマンド

### 今どこにいるか確認する

```powershell
git status
```

見るポイント:

- 今のブランチ名
- 変更されたファイル
- コミット待ちのファイル

### ブランチ一覧を見る

```powershell
git branch
```

リモートブランチも見る場合:

```powershell
git branch -a
```

## ブランチ操作

### mainへ移動する

```powershell
git switch main
```

### mainを最新化する

```powershell
git pull
```

### 新しいブランチを作って移動する

```powershell
git switch -c docs/example
```

### 既存ブランチへ移動する

```powershell
git switch docs/example
```

## 変更確認

### 変更されたファイルを見る

```powershell
git status
```

### 具体的な差分を見る

```powershell
git diff
```

### コミット予定の差分を見る

```powershell
git diff --cached
```

## コミット

### 全部ステージする

```powershell
git add .
```

### コミットする

```powershell
git commit -m "Update study schedule"
```

### 直近のコミットを見る

```powershell
git log --oneline -5
```

## push

### 初回push

```powershell
git push -u origin docs/example
```

### 2回目以降のpush

```powershell
git push
```


## PRマージ後のブランチ整理

### GitHub側

Pull Requestをマージしたら、画面に表示される`Delete branch`を押す。

### ローカル側

```powershell
git switch main
git pull --ff-only
git fetch --prune
git branch -d docs/example
```

### コマンドの意味

| コマンド | 意味 |
| --- | --- |
| `git switch main` | 安定版ブランチへ戻る |
| `git pull --ff-only` | GitHubのmainをローカルへ取り込む |
| `git fetch --prune` | GitHubで削除済みのブランチ情報をローカルにも反映する |
| `git branch -d docs/example` | マージ済みのローカル作業ブランチを削除する |

`-d`は安全削除なので、未マージなら削除されない。

### 今回の例

```powershell
git switch main
git pull --ff-only
git fetch --prune
git branch -d docs/git-workflow
```

## よくある場面

### 作業前の定番

```powershell
git switch main
git pull
git switch -c study/chapter-01-ai-basic
```

### 作業後の定番

```powershell
git status
git diff
git add .
git commit -m "Add chapter 1 study log"
git push -u origin study/chapter-01-ai-basic
```

### ブランチを間違えたかもと思ったら

```powershell
git status
```

まず状態を見る。慌てて削除やリセットをしない。

### mainに直接変更してしまったら

まだコミットしていなければ、作業ブランチを作ってそのまま移動できる。

```powershell
git switch -c docs/my-work
```

その後、通常どおりコミットする。

## このPJでよく使うブランチ名

| やりたいこと | ブランチ名例 |
| --- | --- |
| 学習ログを書く | `study/chapter-01-ai-basic` |
| 週次レビューを書く | `study/weekly-review-2026-07-05` |
| 社内ガイドを直す | `docs/ai-guide-v1` |
| Git運用を直す | `docs/git-workflow` |
| プロンプトを追加する | `practice/prompt-library` |
| 誤字を直す | `fix/typo` |

## やらない方がよい操作

初心者のうちは、以下は一人で実行しない。

```powershell
git reset --hard
git clean -fd
git push --force
```

必要になったら、目的と影響を確認してから実行する。