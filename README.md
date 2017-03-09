% Markdown形式のファイルをpdfに変換する
 pandoc
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

左側のペインと右側のペインを移動するには\<tab>キーを使います。

### vim-markdownの設定

## pandocの設定

### pandocとは

pandocのホームページは[Pandoc a universal document conver](http://pandoc.org)です。

マークアップされたテキストを他の形式に変換するためのツールです。

### LaTeXの環境をインストールする

日本語を扱うためにはLuaLaTexが必要になります。インストールは下記のコマンドで行います。

~~~
sudo apt install texlive-luatex texlive-lang-cjk lmodern texlive-xetex
~~~

### pandocをインストールする
[Pandoc a universal document conver](http://pandoc.org/installing.html)のダウンロードページからダウンロードします。
Ubuntu用にdebファイルをダウンロードします。pandoc-1.19.2.1-1-amd64.debです。
インストールは以下のコマンドで行います。

~~~
sudo dpkg -i pandoc-1.19.2.1-1-amd64.deb
~~~

## Markdownの構文
Markdownにはいくつかの拡張があります。このドキュメントはhtmlへの変換とpandocによるpdfへの変換がうまくいく構文に限定して説明します。

### 文字エンティティを使用する特殊文字
&amp;と&lt;は文字エンティティで記述する必要があります。
&amp;は
```
&amp;
```

&lt;は
```
&lt;
```
と記述します。

著作権記号&copy;を記述するときは
```
&copy;
```
と記述します。

## ブロック要素の構文

### 段落と改行



### 見出し、もしくはヘッダ
ヘッダは日本語だと見出しですね。

先頭に#記号をつける形式をATX形式のヘッダと呼びます。1〜6個の#記号および1行のテキストを記述します。Pandocには「ヘッダの前に空行を入れる」という制約があります。

    ## レベル2のヘッダ

    ### レベル3のヘッダ

アンダーラインでヘッダを記述するSetex形式も使用できますが#のほうが簡単と思います。

### 引用

### リスト

### コードブロック

### 水平線

## インライン要素の構文

### リンク

### 強調

### コード

### イメージ

## その他

### 自動リンク

### バックシュラッシュエスケープ

## 拡張の構文

### 表
pandocでは4種類の表が使用できます。以下の4つです。

* シンプルテーブル
* マルチラインテーブル
* グリッドテープル
* パイプテーブル

パイプテーブルで試してみます。

|右寄せ | 左寄せ|デフォルト|中央寄せ|
|------:|:------|----------|:------:|
| 12   | 12   | 12       | 12     |
| 123  | 123  | 123      | 123    |
| 1    | 1    | 1        | 1      |


### タイトルブロック
タイトルブロックはpandocの拡張です。
pdfの先頭にタイトルをつけたい場合はファイルの先頭に%で始まるタイトルブロックを記述します。

~~~
% タイトル
% 著者(複数の場合はセミコロンで区切る)
% 日付
~~~

タイトルを複数行にしたい場合は2行目以降の先頭にスペースを入れます。

~~~
% タイトル
 副タイトル
~~~

## pandocでpdfに変換する

### pandocの実行

~~~
pandoc README.md -o README.pdf -V documentclass=ltjarticle --latex-engine=lualatex --toc -N
~~~

