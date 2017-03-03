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

### vimにVOoMを導入する

VOoM(Vim Outliner of Markups)はマークアップされたテキストのアウトライナーです。
最新版のダウンロードは [VOoM : Vim two-pane outliner](http://www.vim.org/scripts/script.php?script_id=2657) から行いました。
バージョンは5.2以上が必要です。5.1以下だとPython3がサポートされていないからです。Ubuntuのターミナルで`apt install vim-voom`でインストールされるバージョンは5.1です。

VOoM-5.2.zipを解凍してできるVOoMディレクトリの下のautoload、doc、pluginを~/.vim/の下にコピーします。

### vim-markdownの設定

## pandocでpdfに変換

### pandocの
