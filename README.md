# Usage git & github

目的：Coding で困って行ったことなどを記録

## ローカルリポジトリからリモートリポジトリへのアクセス設定

github に登録したユーザー名とメールアドレスで:
~~~sh
git config --global user.name [username]
git config --global user.email [useremail]
~~~

## リモートリポジトリからクローンして始める場合
~~~sh
git clone https://github.com/[username]/[repository].git
cd [repository]
~~~

`vscode` を使えるなら、`ソース管理` でOK、使えない場合に:

~~~sh
cd [repository]

# 作成もしくは編集 ⇒ 追加 ⇒ コミット
nano README.md
git add README.md
git commit -m "Add file"

# ブランチの作成、変更
git branch -M main

# リモートリポジトリに反映
git push -u origin main

# リモートリポジトリを変更したら
git pull origin main
~~~

## ローカルリポジトリからプッシュして始める場合

`vscode` を使えるなら、`ソース管理` でOK、使えない場合に:

~~~sh
mkdir [repository]
cd [repository]

# あとは、上記と一緒かな？
~~~

## .gitignore を作成

[gitignore.io](https://www.toptal.com/developers/gitignore) にアクセスして簡単に作成

## [git commit 時に自動コードチェックと整形](https://blog.imind.jp/entry/2022/03/11/003534)

`git commit` 時に実行され、`pass` しないとコミットされない。
vscode を使えない時に便利

~~~sh
sudo -H python3 -m pip install -U pre-commit black isort flake8 pyproject-flake8 mypy
# pre-commit ruff で OK かも？

pre-commit sample-config > .pre-commit-config.yaml
# ".pre-commit-config.yaml" を編集
pre-commit autoupdate
# rev にアップデートがあれば、".pre-commit-config.yaml" を編集
pre-commit install
~~~
`pyproject.toml` に設定を記述する。

## 他のリポジトリを含める場合 (submodule)

他のリポジトリを追加

~~~sh
cd [repository]
git submodule add https://github.com/[username]/[submodule].git
git commit -m "add submodule"
git push origin main
~~~

他のリポジトリの更新を反映 
> 自動で更新を取り込むことはない

~~~sh
cd [repository]
git submodule update --remote --recursive
git commit -m "update submodule"
git push origin main
~~~

他のリポジトリを含んだリポジトリをクローンする場合

~~~sh
git clone --recursive https://github.com/[username]/[repository].git
~~~