# Git 応用演習 - 解答と解説

## 演習の完全な実行手順

> **注意**: `Challenge`フォルダはすでに Git リポジトリとして初期化されています。`cd Challenge`で移動して、すぐに演習を始められます。

### ステップ 1: 初期セットアップ

```bash
cd Challenge
git add index.html style.css
git commit -m "初回コミット: プロジェクトの初期ファイルを追加"
git log --oneline
```

**解説:**

- 基本的なコミット操作です。応用演習の基盤となる最初のコミットを作成します。
- `git add`で複数ファイルを一度に指定できます。
- `git log --oneline`で簡潔な履歴を確認できます。

---

### ステップ 2: ブランチの作成と切り替え

```bash
git branch feature/1-exercise-header
git branch
git checkout feature/1-exercise-header
git status
```

**解説:**

- `git branch <ブランチ名>`: 新しいブランチを作成します（現在のブランチから分岐）。
- `git branch`: ブランチ一覧を表示します。現在のブランチには`*`が表示されます。
- `git checkout <ブランチ名>`: 指定したブランチに切り替えます。
- `git switch <ブランチ名>`: Git 2.23 以降では、`git switch`も使用できます（より直感的）。

**ブランチとは:**

- ブランチは独立した開発ラインです
- メインブランチ（`main`または`master`）を壊すことなく、新しい機能を開発できます
- チーム開発では、各機能を別々のブランチで開発し、後で統合します

**重要なポイント:**

- ブランチを作成しても自動的に切り替わりません
- 切り替えるには`git checkout`または`git switch`が必要です
- ブランチ名は意味のある名前にしましょう（例: `feature/login`, `bugfix/header`）

---

### ステップ 3: ブランチでの作業

```bash
# index.htmlの<h1>を変更:
# <h1>Git応用演習ページ</h1> → <h1>Git 応用ワークショップ</h1>

# style.cssに追加:
# .header { text-align: center; color: #1976d2; }

git add .
git commit -m "ヘッダーを追加: タイトルとスタイルを更新"
git log --oneline --graph
```

**解説:**

- ブランチ上で変更を行い、コミットします。
- この変更は`feature/1-exercise-header`ブランチにのみ存在します。
- `git log --oneline --graph`でブランチの分岐を視覚的に確認できます。

**ベストプラクティス:**

- 1 つのブランチには 1 つの機能や修正をまとめます
- コミットメッセージは変更内容を明確に記述します
- 小さなコミットを積み重ねることで、履歴が追いやすくなります

---

### ステップ 4: メインブランチに戻る

```bash
git checkout main
# index.htmlを確認（変更が反映されていない）
git branch -a
```

**解説:**

- `git checkout main`: メインブランチに戻ります。
- メインブランチでは、`feature/1-exercise-header`で行った変更は見えません。
- これがブランチの重要な特徴です：各ブランチは独立した作業環境です。

**ブランチの切り替え時の注意:**

- 未コミットの変更がある場合、Git は切り替えを拒否する場合があります
- その場合は`git stash`で一時保存するか、コミットしてから切り替えます

---

### ステップ 5: ブランチのマージ

```bash
git merge feature/1-exercise-header
git log --oneline --graph
# index.htmlとstyle.cssを確認（変更が反映されている）
git branch -d feature/1-exercise-header
```

**解説:**

- `git merge <ブランチ名>`: 指定したブランチの変更を現在のブランチに統合します。
- マージ後、`feature/1-exercise-header`の変更が`main`に反映されます。
- `git branch -d <ブランチ名>`: マージ済みのブランチを削除します（安全）。

**マージの種類:**

1. **Fast-forward マージ**: 分岐がない場合、単純にポインタを進める
2. **3-way マージ**: 分岐がある場合、マージコミットを作成する

**コンフリクト（競合）が発生した場合:**

```bash
# コンフリクトが発生すると、Git がマーカーを挿入します:
`<<<<<<< HEAD
現在のブランチの内容
=======
マージするブランチの内容
>>>>>>> feature/1-exercise-header`

# エディタで手動で解決し、以下を実行:
git add <解決したファイル>
git commit
```

**重要なポイント:**

- マージ前に`git status`で状態を確認しましょう
- コンフリクトは恐れる必要はありません。落ち着いて解決できます
- `git branch -D <ブランチ名>`（大文字の D）は、マージしていないブランチも強制削除します

---

### ステップ 6: 新しいブランチで機能追加

```bash
git checkout -b feature/advanced-footer
# index.htmlに<footer>タグを追加
# style.cssに.footerクラスを追加
git add .
git commit -m "フッターを追加"
```

**解説:**

- `git checkout -b <ブランチ名>`: ブランチを作成して同時に切り替えるショートカットです。
- これは`git branch <ブランチ名>`と`git checkout <ブランチ名>`を一度に実行するのと同じです。

**ブランチ命名規則:**

- `feature/`: 新機能
- `bugfix/` または `fix/`: バグ修正
- `hotfix/`: 緊急修正
- `refactor/`: リファクタリング
- `docs/`: ドキュメント

---

### ステップ 7: スタッシュの使用

```bash
# index.htmlに未完成の変更を加える
git stash
git status
git stash list
git stash pop
```

**解説:**

- `git stash`: ワーキングディレクトリの変更を一時的に保存します。
- ブランチを切り替える前に、未完成の変更を保存するのに便利です。
- `git stash pop`: 最新のスタッシュを復元して削除します。

**スタッシュのその他のコマンド:**

- `git stash list`: スタッシュ一覧を表示
- `git stash apply`: スタッシュを復元するが削除しない
- `git stash drop`: スタッシュを削除
- `git stash clear`: すべてのスタッシュを削除

**使用例:**

```bash
# 緊急のバグ修正ブランチに切り替える必要があるが、現在の作業は未完成
git stash
git checkout hotfix/critical-bug
# バグ修正を完了
git checkout feature/my-feature
git stash pop  # 元の作業を再開
```

---

### ステップ 8: リモートリポジトリの設定

```bash
# GitHubでリポジトリを作成後:
git remote add origin https://github.com/username/repository.git
git remote -v
git push -u origin main
```

**解説:**

- `git remote add <名前> <URL>`: リモートリポジトリを追加します。
- 通常、メインのリモートは`origin`という名前を使います。
- `git remote -v`: リモート設定を確認します。
- `git push -u origin main`: ローカルの`main`ブランチをリモートの`origin/main`にプッシュします。
- `-u`オプションで、今後は`git push`だけでプッシュできます。

**リモートの主要コマンド:**

- `git push`: ローカルの変更をリモートに送信
- `git pull`: リモートの変更をローカルに取得してマージ
- `git fetch`: リモートの変更を取得するがマージしない
- `git clone <URL>`: リモートリポジトリをクローン

**プッシュとプルの流れ:**

```
ローカル → git push → リモート
リモート → git pull → ローカル
```

---

### ステップ 9: コミットの修正

```bash
# 小さな変更を加える（例: タイポの修正）
git add .
git commit --amend -m "修正: タイポを修正"
git log --oneline
```

**解説:**

- `git commit --amend`: 最後のコミットを修正します。
- コミットメッセージを変更したり、変更を追加できます。
- **注意**: すでにプッシュしたコミットを修正する場合は注意が必要です。

**使用例:**

```bash
# コミットメッセージを修正
git commit --amend -m "新しいメッセージ"

# 変更を追加してコミットを修正
git add forgotten-file.txt
git commit --amend --no-edit  # メッセージは変更しない
```

**重要な注意点:**

- すでにプッシュしたコミットを`--amend`すると、履歴が書き換わります
- チーム開発では、共有されたコミットの修正は避けるべきです
- 必要に応じて`git push --force`を使いますが、慎重に使用してください

---

### ステップ 10: 履歴の確認と比較

```bash
git log --oneline --graph --all
git diff main feature/advanced-footer
git show HEAD
```

**解説:**

- `git log --oneline --graph --all`: すべてのブランチの履歴をグラフで表示します。
- `git diff <ブランチ1> <ブランチ2>`: 2 つのブランチ間の差分を表示します。
- `git show HEAD`: 最新コミットの詳細（変更内容）を表示します。

**その他の便利な履歴コマンド:**

- `git log --oneline -10`: 最新 10 件のコミット
- `git log --author="名前"`: 特定の作成者のコミット
- `git log --since="2024-01-01"`: 特定の日付以降
- `git log --grep="キーワード"`: コミットメッセージで検索
- `git diff HEAD~1`: 1 つ前のコミットとの差分

---

## Git のブランチ戦略

### Git Flow

```
main (本番環境)
  └── develop (開発環境)
      ├── feature/新機能1
      ├── feature/新機能2
      └── hotfix/緊急修正
```

### GitHub Flow（シンプル）

```
main (常にデプロイ可能)
  ├── feature/新機能1
  ├── feature/新機能2
  └── feature/新機能3
```

---

## よく使う Git コマンドまとめ（応用編）

| コマンド                           | 説明                         |
| ---------------------------------- | ---------------------------- |
| `git branch`                       | ブランチ一覧を表示           |
| `git branch <ブランチ名>`          | ブランチを作成               |
| `git checkout <ブランチ名>`        | ブランチを切り替え           |
| `git checkout -b <ブランチ名>`     | ブランチを作成して切り替え   |
| `git switch <ブランチ名>`          | ブランチを切り替え（新）     |
| `git merge <ブランチ名>`           | ブランチをマージ             |
| `git branch -d <ブランチ名>`       | ブランチを削除               |
| `git stash`                        | 変更を一時保存               |
| `git stash pop`                    | スタッシュを復元             |
| `git remote add <名前> <URL>`      | リモートを追加               |
| `git push`                         | リモートにプッシュ           |
| `git pull`                         | リモートから取得してマージ   |
| `git commit --amend`               | 最後のコミットを修正         |
| `git log --graph --oneline --all`  | すべてのブランチの履歴を表示 |
| `git diff <ブランチ1> <ブランチ2>` | ブランチ間の差分を表示       |

---

## コンフリクトの解決方法

### 1. コンフリクトの確認

```bash
git merge feature/other
# CONFLICT メッセージが表示される
```

### 2. コンフリクトファイルを開く

```html
<<<<<<< HEAD
<div class="container">
  <h1>メインブランチの内容</h1>
  =======
  <div class="container">
    <h1>feature/otherブランチの内容</h1>
    >>>>>>> feature/other
  </div>
</div>
```

### 3. 手動で解決

```html
<div class="container">
  <h1>統合された内容</h1>
</div>
```

### 4. 解決を完了

```bash
git add <解決したファイル>
git commit
```

---

## トラブルシューティング

### Q: ブランチを切り替えられない

A: 未コミットの変更がある可能性があります。`git stash`で保存するか、コミットしてから切り替えましょう。

### Q: マージでコンフリクトが発生した

A: エディタでマーカー（`<<<<<<<`, `=======`, `>>>>>>>`）を探し、手動で解決してから`git add`と`git commit`を実行します。

### Q: 間違えたブランチにコミットしてしまった

A: `git reset HEAD~1`でコミットを取り消し、正しいブランチに切り替えてから`git cherry-pick`でコミットを移動できます。

### Q: リモートにプッシュできない

A: リモートに新しいコミットがある可能性があります。`git pull`で取得してから再度`git push`を試してください。

### Q: ブランチを削除したいが、マージしていない

A: `git branch -D <ブランチ名>`（大文字の D）で強制削除できますが、データが失われる可能性があるので注意してください。

---

## 次のステップ

この演習を完了したら、以下のトピックに進むことをお勧めします:

1. **Git Rebase**: コミット履歴を整理する
2. **Git Cherry-pick**: 特定のコミットを別のブランチに適用
3. **Git Tag**: リリースバージョンを管理
4. **Git Hooks**: 自動化スクリプト
5. **Git Submodules**: サブプロジェクトの管理
6. **Git Worktree**: 複数の作業ディレクトリ

---

## 参考リソース

- [Pro Git Book（日本語版）](https://git-scm.com/book/ja/v2)
- [Learn Git Branching（インタラクティブチュートリアル）](https://learngitbranching.js.org/?locale=ja)
- [GitHub Flow](https://guides.github.com/introduction/flow/)
- [Git Flow](https://nvie.com/posts/a-successful-git-branching-model/)

---

お疲れ様でした！この演習を通じて、Git の応用的な機能を理解できたはずです。
ブランチとマージはチーム開発の基盤となる重要な概念です。
実際のプロジェクトでも積極的に活用してください。
