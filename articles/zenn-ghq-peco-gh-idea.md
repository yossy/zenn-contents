---
title: "ghq + peco + GitHub CLIでターミナルの生産性を上げたい！"
emoji: "🦁"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["ghq", "peco", "GitHubCLI"]
published: false
---

## はじめに

何番煎じかはわかりませんが、有名なghq・pecoの組み合わせが汎用性ありすぎてとても便利だったので一例を記事にしてみました。

## 目的

今更ですがghq,peco,GitHubCLIが超便利だったので紹介します。
一例としてこんな感じでターミナルからブラウザでリポジトリを開けるようにします。
![](https://storage.googleapis.com/zenn-user-upload/0laslgz702xlv48ao94wiqzzowkf)

### [ghq](https://github.com/x-motemen/ghq)とは

リポジトリ管理ツールです。
`ghq get <リポジトリのURL>`でghqで設定したディレクトリにgit cloneしてくれます。
さらに`ghq list`でghqで管理しているリポジトリ一覧を一覧で出力してくれます。
詳細は[作者の方のブログ](https://motemen.hatenablog.com/entry/2014/06/01/introducing-ghq)や[公式のリポジトリ](https://github.com/x-motemen/ghq)を参照してください。

- インストール例（Mac OS）
```bash
$ brew install ghq
```

- 設定例
```bash:.gitconfig
[ghq]
  root = ~/projects # gitで開発を行っているディレクトリ
  root = ~/go/src # goのリポジトリは別で管理しているという人用（一例です）
```

### [peco](https://github.com/peco/peco)とは

標準入力で渡された一覧を表示しつつ、インクリメンタルサーチでテキストを絞っていけるツールです。
もともと`ctrl + r`でインクリメンタルサーチできると思いますが、pecoだとコマンド履歴を表示した上で絞っていけるので超便利です。
いつもありがとうございます。
詳細は公式や[こちらの記事](https://qiita.com/vintersnow/items/08852df841e8d5faa7c2)とか色んな方が紹介してくださっているのでそちらを参照してください。

- インストール例（Mac OS）
```bash
$ brew install peco
```

### [Github CLI](https://github.com/cli/cli)とは

GitHubが[2020年9月に正式版を公開](https://github.blog/jp/2020-09-18-github-cli-1-0-is-now-available/)した、コマンドライン上でGitHubの操作を行えるツールです。
[マニュアル](https://cli.github.com/manual/)が用意されているので使い方は[こちら](https://cli.github.com/manual/)に載っています。

- インストール例（Mac OS）
```bash
$ brew install gh
```

- インストール後の認証
```bash
$ gh auth login
```

認証まで完了したら`gh repo view <リポジトリ名>`とかでリポジトリの内容を閲覧してみましょう。
ターミナルにREADMEの内容が出力されると思います。

## 実用例

ghq,peco,GitHubCLIがインストールできて準備ができたら実際に使ってみます。
エイリアスは設定しなくてもコマンド打てますが、設定しておくのがおすすめです！

### 対象リポジトリをブラウザでターミナルから開く

- 以下を.zshrc(or .bashrcなど)に記載

```bash:.zshrc
# aliasはお好きなのを設定してください。
alias ghw='gh repo view -w $(ghq list | peco)
```

- 設定を反映する
```bash
$ source ~/.zshrc
```

- Demo
こんな感じでターミナルからブラウザでリポジトリを開くことができました！
![](https://storage.googleapis.com/zenn-user-upload/0laslgz702xlv48ao94wiqzzowkf)

### 番外編

以下でこんなのもあるよというのも記載しています！

```bash:.zshrc

# ghqで管理しているリポジトリにpecoで絞って移動する。
alias cdp='cd $(ghq list -p | peco)'

# ghqで管理しているリポジトリをpecoで絞ってVSCodeで開く。
alias vs='code $(ghq list -p | peco)'

# カレントディレクトリのOpenになっているPRをブラウザで開く。
alias pr='gh pr view --web'
```

## 終わりに

ghqとかpecoなどを使った組み合わせは他にもたくさん探したらでてくると思いますが、
今回はGithubCLIとの組み合わせを載せてみました。
こんな便利なものを公開してくれている方々に本当に感謝ですね。
「これもええで！」みたいなのがあればぜひ教えて下さい！

## 参考

ありがとうございます！
- https://cli.github.com/manual/gh_pr_view
- [GitHub CLIで始める快適GitHub生活](https://qiita.com/ryo2132/items/2a29dd7b1627af064d7b)
- [ghq: リモートリポジトリのローカルクローンをシンプルに管理する](https://motemen.hatenablog.com/entry/2014/06/01/introducing-ghq)
- [え、まだpecoを使ってないの？？？](https://qiita.com/vintersnow/items/08852df841e8d5faa7c2)
