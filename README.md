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

### 見出し、もしくはヘッダ
先頭に#記号をつける形式をATX形式のヘッダと呼びます。1〜6個の#記号および1行のテキストを記述します。Pandocには「ヘッダの前に空行を入れる」という制約があります。

~~~

\## レベル2のヘッダ

\### レベル3のヘッダ

~~~
### 改行

### リンク

### コード

### 引用文

### 表
4種類の表(テーブル)が使用できます。最初の3種類はCourierのような等幅フォントの使用を前提とします。4種類目はプロポーショナルフォントの使用が可能で、列を左右・中央に寄せるために列のテキストを左右に移動する必要もありません。

* シンプルテーブル
* マルチラインテーブル
* グリッドテーブル
* パイプテーブル

#### シンプルテーブル

~~~
 Right Left   Center  Default
------ ----- -------- -------
    12 12     12          12
   123 123    123        123
     1 1       1           1

Table: シンプルテーブルのデモ
~~~

 Right Left   Center  Default
------ ----- -------- -------
    12 12     12          12
   123 123    123        123
     1 1       1           1

Table: シンプルテーブルのデモ

#### マルチラインテーブル

~~~
---------------------------------------------------------
 Centered  Default         Right Left
  Header   Aligned       Aligned Aligned
---------- ------- ------------- ------------------------
 First     row              12.0 Example of a row that
                                 spans multiple lines.

 Second    row               5.0 Here's another one. Note
                                 the blank line between
                                 rows.
---------------------------------------------------------

Table: 表題がここに入ります。
複数の行です。
~~~

---------------------------------------------------------
 Centered  Default         Right Left
  Header   Aligned       Aligned Aligned
---------- ------- ------------- ------------------------
 First     row              12.0 Example of a row that
                                 spans multiple lines.

 Second    row               5.0 Here's another one. Note
                                 the blank line between
                                 rows.
---------------------------------------------------------

Table: 表題がここに入ります。
複数の行です。

#### グリッドテーブル

~~~
~~~

#### パイプテーブル

~~~
~~~


## pandocでpdfに変換する

### pandocの実行

~~~
pandoc README.md -o README.pdf -V documentclass=ltjarticle --latex-engine=lualatex --toc -N
~~~

