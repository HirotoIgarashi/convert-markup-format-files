% Markdown形式のファイルをpdfに変換する
% 五十嵐 浩人
% 2017年3月5日

# Markdown形式のファイルをpdfに変換する

## パソコンの環境を確認する

以下のコマンドでOSのバージョンを確認します。

~~~
$ cat /etc/lsb-release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=16.10
DISTRIB_CODENAME=yakkety
DISTRIB_DESCRIPTION="Ubuntu 16.10"
~~~

同じようにアーキテクチャを確認します。

~~~
$ arch
x86_64
~~~

vimのバージョンも確認しておきます。

~~~
$ vim --version
VIM - Vi IMproved 7.4 (2013 Aug 10, compiled Nov 24 2016 22:32:42)
適用済パッチ: 1-1829
追加拡張パッチ: 8.0.0056
~~~

## Markdownの編集環境を設定する

### vimの設定

### vimにVOoMをインストールする

VOoM(Vim Outliner of Markups)はマークアップされたテキスト用のアウトライナーです。
最新版のダウンロードは [VOoM : Vim two-pane outliner](http://www.vim.org/scripts/script.php?script_id=2657) から行いました。
バージョンは5.2以上が必要です。5.1以下だとPython3がサポートされていないからです。Ubuntuのターミナルで`apt install vim-voom`でインストールされるバージョンは5.1です。

VOoM-5.2.zipを解凍してできるVOoMディレクトリの下のautoload、doc、pluginを~/.vimの下にコピーします。

### VOoMを使ってみる

Markdown形式のファイルをvimで開いている状態で`:Voom markdown`とコマンドを入力します。他のコマンドには`:Voomhelp`、`:Voomexec`、`Voomlog`があるようですがまだ使ったことはありせん。VOoMはtwo-pane outlinerと説明されていますので左側に表示される部分をペインと呼ぶことにします。その左側のペインにはMarkdownで見出しとして記述されたものがツリーとして表示されています。

左側のペインと右側のペインを移動するには<tab>キーを使います。

### vim-markdownの設定

## pandocの設定

### pandocとは

pandocのホームページは[Pandoc a universal document conver](http://pandoc.org)です。

マークアップされたテキストを他の形式に変換するためのツールと理解しています。

### LaTeXの環境をインストールする

日本語を扱うためにLuaLaTexが必要になります。

~~~
sudo apt install texlive-luatex texlive-lang-cjk lmodern texlive-xetex
~~~

### pandocをインストールする
[Pandoc a universal document conver](http://pandoc.org/installing.html)のダウンロードページからダウンロードします。
Ubuntu用にdebファイルをダウンロードします。pandoc-1.19.2.1-1-amd64.debです。
Require skylighting >= 0.1.1.4.
インストールは

~~~
sudo dpkg -i pandoc-1.19.2.1-1-amd64.deb
~~~
でインストールします。

## pandoc用にMarkdownを記述する

### タイトルブロック
ファイルの最初に行頭が%で始まるブロックを書くとタイトルして扱われます。

### 見出し

### 改行

### リンク

### コード

### 引用文

### 引用文

## pandocでpdfに変換する

### pandocの実行

~~~
pandoc README.md -o README.pdf -V documentclass=ltjarticle --latex-engine=lualatex --toc -N
~~~

