# Markdown形式のファイルをpdfに変換する

## パソコンの環境

OSのバージョンの確認

~~~
$ cat /etc/lsb-release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=16.10
DISTRIB_CODENAME=yakkety
DISTRIB_DESCRIPTION="Ubuntu 16.10"
~~~
アーキテクチャの確認
~~~
$ arch
x86_64
~~~
`vim --version`
~~~
$ vim --version
VIM - Vi IMproved 7.4 (2013 Aug 10, compiled Nov 24 2016 22:32:42)
適用済パッチ: 1-1829
追加拡張パッチ: 8.0.0056
~~~

## Markdown編集環境

### vimの設定

### vimにVOoMをインストールする

VOoM(Vim Outliner of Markups)はマークアップされたテキスト用のアウトライナーです。
最新版のダウンロードは [VOoM : Vim two-pane outliner](http://www.vim.org/scripts/script.php?script_id=2657) から行いました。
バージョンは5.2以上が必要です。5.1以下だとPython3がサポートされていないからです。Ubuntuのターミナルで`apt install vim-voom`でインストールされるバージョンは5.1です。

VOoM-5.2.zipを解凍してできるVOoMディレクトリの下のautoload、doc、pluginを~/.vim/の下にコピーします。

### VOoMを使ってみる
Markdown形式のファイルをvimで開いている状態で`:Voom markdown`とコマンドを入力します。他のコマンドには`:Voomhelp`、`:Voomexec`、`Voomlog`があるようですがまだ使ったことはありせん。VOoMはtwo-pane outlinerと説明されていますので左側に表示される部分をペインと呼ぶことにします。その左側のペインにはMarkdownで見出しとして記述されたものがツリーとして表示されています。

左側のペインと右側のペインを移動するには<tab>キーを

### vim-markdownの設定

## pandocでpdfに変換

### pandocをインストールする
Ubuntuでは
~~~
sudo apt install pandoc
~~~
でインストールします。実行結果は以下になります。
~~~
$ sudo apt install pandoc
[省略]
以下の追加パッケージがインストールされます:
  libluajit-5.1-2 libluajit-5.1-common pandoc-data
提案パッケージ:
  texlive-latex-recommended texlive-xetex texlive-luatex pandoc-citeproc
  texlive-latex-extra wkhtmltopdf
以下のパッケージが新たにインストールされます:
  libluajit-5.1-2 libluajit-5.1-common pandoc pandoc-data
アップグレード: 0 個、新規インストール: 4 個、削除: 0 個、保留: 0 個。
[省略]
~~~

