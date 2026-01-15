## チェックリスト

> **注意**: このリポジトリはすでに初期化されています。`Challenge`フォルダに移動して、すぐに演習を始められます。

### ステップ 1: 初期セットアップ

- [ ] `git add index.html style.css`でファイルをステージングする
- [ ] `git commit -m "初回コミット: プロジェクトの初期ファイルを追加"`でコミットする
- [ ] `git log --oneline`でコミット履歴を確認する

### ステップ 2: ブランチの作成と切り替え

- [ ] `git branch feature/1-exercise-header`で新しいブランチを作成する
- [ ] `git branch`でブランチ一覧を確認する（現在のブランチに`*`が表示される）
- [ ] `git checkout feature/1-exercise-header`でブランチを切り替える
- [ ] `git status`で現在のブランチを確認する

### ステップ 3: ブランチでの作業

- [ ] `index.html`の`<h1>`タグの内容を「Git 応用ワークショップ」に変更する
- [ ] `style.css`に`.header`クラスのスタイルを追加する（例: `text-align: center; color: #1976d2;`）
- [ ] `git add .`で変更をステージングする
- [ ] `git commit -m "ヘッダーを追加: タイトルとスタイルを更新"`でコミットする
- [ ] `git log --oneline --graph`でブランチの履歴を確認する

### ステップ 4: メインブランチに戻る

- [ ] `git checkout main`（または`git checkout master`）でメインブランチに戻る
- [ ] `index.html`を確認し、変更が反映されていないことを確認する
- [ ] `git branch -a`でブランチ一覧を確認する

### ステップ 5: ブランチのマージ

- [ ] `git merge feature/1-exercise-header`で`feature/1-exercise-header`ブランチをマージする
- [ ] `git log --oneline --graph`でマージ後の履歴を確認する
- [ ] `index.html`と`style.css`を確認し、変更が反映されていることを確認する
- [ ] `git branch -d feature/1-exercise-header`でマージ済みブランチを削除する

### ステップ 6: 新しいブランチで機能追加

- [ ] `git checkout -b feature/advanced-footer`でブランチを作成して切り替える（ショートカット）
- [ ] `index.html`にフッターセクション（`<footer>`タグ）を追加する
- [ ] `style.css`に`.footer`クラスのスタイルを追加する
- [ ] `git add .`で変更をステージングする
- [ ] `git commit -m "フッターを追加"`でコミットする

### ステップ 7: スタッシュの使用

- [ ] `index.html`に未完成の変更を加える（例: コメントを追加）
- [ ] `git stash`で変更を一時保存する
- [ ] `git status`で作業ディレクトリがクリーンなことを確認する
- [ ] `git stash list`でスタッシュ一覧を確認する
- [ ] `git stash pop`でスタッシュを復元する

### ステップ 8: リモートリポジトリの設定（オプション）

- [ ] GitHub などでリモートリポジトリを作成する
- [ ] `git remote add origin <リポジトリURL>`でリモートを追加する
- [ ] `git remote -v`でリモート設定を確認する
- [ ] `git push -u origin main`でリモートにプッシュする（オプション）

### ステップ 9: コミットの修正

- [ ] 小さな変更を加える（例: タイポの修正）
- [ ] `git add .`でステージングする
- [ ] `git commit --amend -m "修正: タイポを修正"`で最後のコミットを修正する
- [ ] `git log --oneline`でコミット履歴を確認する

### ステップ 10: 履歴の確認と比較

- [ ] `git log --oneline --graph --all`ですべてのブランチの履歴を確認する
- [ ] `git diff main feature/advanced-footer`でブランチ間の差分を確認する
- [ ] `git show HEAD`で最新コミットの詳細を確認する

## 完了後

すべてのチェックリストを完了したら、`Answer`フォルダの解説を確認して理解を深めましょう。

## ヒント

- `git checkout -b <ブランチ名>`は`git branch`と`git checkout`を一度に実行するショートカットです
- マージ前に必ず`git status`で状態を確認しましょう
- スタッシュは一時的な変更を保存するのに便利です
- リモートリポジトリは実際のプロジェクトで必須です
