---
title: "AtCoder Python環境"
date: 2020-05-16T23:16:37+09:00
toc: false
images:
tags:
  - atcoder
  - python
  - env
  - programming
  - competitive_programming 
  - Mac
---

2020年5月段階での自分のAtCoder環境をメモがてら書いておく。
Python環境を想定しているが、AtCoder関連のところは他言語利用者も参考になるかもしれない。
Macを利用している。
質問や分かりにくい点あれば追記するので [@ryo_n_code](https://twitter.com/ryo_n_code) へ。


下記を目指したつもり
* コンテストサイト毎の環境を独立
* 複数マシン(デスクトップとラップトップ等) での利用も容易にする
* シンプルな操作
* サンプルのコピペ操作の排除
* サンプルが通らないコードの提出防止


# ソースコード管理

## github

gitを利用してバージョン管理をしている。
githubはプライベートリポジトリも無料で作成できるので、プライベートリポジトリを作成し、
ソースコードファイル、python環境管理ファイル(下記で記述)などもリポジトリ内に保存している。
ディレクトリ構造は下記のようになっている。
コンテスト毎にディレクトリを作成し、コンテストディレクトリの中に各問題ディレクトリが存在している。
各問題ディレクトリの中にソースコードと、testディレクトリが存在し、testディレクトリ内にサンプルが存在する。

```
$ tree
.
├── abc001
│   ├── a
│   │   ├── main.py
│   │   └── test
│   │       ├── sample-1.in
│   │       ├── sample-1.out
│   │       ├── sample-2.in
│   │       ├── sample-2.out
│   │       ├── sample-3.in
│   │       └── sample-3.out
│   ├── b
│   │   ├── main.py
│   │   └── test
│   │       ├── sample-1.in
│   │       ├── sample-1.out
│   │       ├── sample-2.in
│   │       ├── sample-2.out
│   │       ├── sample-3.in
│   │       └── sample-3.out
```

# Python環境

## pyenv

https://github.com/pyenv/pyenv

環境毎にPythonのバージョンを切り替えるために使用。
AtCoderだと3.8.2だが、Codeforcesだと3.7.2が利用されている。

AtCoder環境のディレクトリで下記コマンドを実行すればPython 3.8.2が利用される
```
# 3.8.2をインストール
$ pyenv install 3.8.2
# 下記コマンドを実行したディレクトリ配下ではPython 3.8.2が使用されるようになる
$ pyenv local 3.8.2
```


## pipenv

https://github.com/pypa/pipenv

環境毎に依存モジュール管理をするために使用。
AtCoderだとnumpy, scipyが利用できるが、Codeforcesだと利用できなかったりする。


AtCoder環境のディレクトリで下記コマンドを実行すればPython 3.8.2環境で各モジュールが利用できるようになる。
```
$ pipenv --python 3.8.2
$ pipenv install numpy scipy online-judge-tools
```

また、pipenvのスクリプト機能を利用し、自前ラッパースクリプトをpipenv環境で実行できるようにしている。

```
$ pipenv run test
$ pipenv run submit
```
下記設定を入れておけば、上記コマンドで自前スクリプトを実行できる。
上記コマンドは各問題ディレクトリで実行されることを想定しているので相対パスでスクリプトを指定している。
(あまりイケてない、、?)

```
$ cat Pipfile
[[source]]
name = "pypi"
url = "https://pypi.org/simple"
verify_ssl = true

[dev-packages]
pylint = "*"

[packages]
numpy = "*"
scipy = "*"
online-judge-tools = "*"

[requires]
python_version = "3.8.2"

[scripts]
test = "../../test.sh"
submit = "../../submit.sh"
```


# AtCoder

## online-judge-tools

https://github.com/online-judge-tools/oj

サンプルのダウンロード、サンプルを利用したテストの実行、ソースコードの提出ができるようになる。

## atcoder-cli

https://github.com/Tatamo/atcoder-cli

コンテストを指定し、コンテスト内の各問題のサンプルのダウンロード、テンプレートを利用したソースコードの準備が可能になる。

## 自前ラッパースクリプト

### 提出用

カレントディレクトリから提出先を判別し、online-judgel-toolsを使って提出を可能にする。
提出前にサンプルのテストを実行し、テスト失敗した場合は警告を出すようにしている。

提出先URLの取得にatcoder-cliが作成したメタデータを利用してるので、jqコマンドを事前にインストールする必要がある。


submit.sh
```bash
#!/bin/bash

path=$(pwd)

task=$(echo "${path}" | rev | cut -d '/' -f 1 | rev)
url=$(< ../contest.acc.json jq -r ".tasks[] | select(.directory.path == \"${task}\") | .url")

oj t -c "python main.py"

case "$?" in
    1) echo "Test is failed. If you want to submit the script. Please type yes." >&2
       read -r answer
       case "$answer" in
           "yes") echo "submit script";;
           *) exit 1
       esac
esac

if [ "$1" = "Python" ]; then
    oj s -y -w 0 "${url}" main.py --language Python
elif [ "$1" = "PyPy" ]; then
    oj s -y -w 0 "${url}" main.py --language 4047
elif [ "$1" = "PyPyOld" ]; then
    oj s -y -w 0 "${url}" main.py --language 3510
else
    oj s -y -w 0 "${url}" main.py --language Python
fi
```
問題ディレクトリ配下で下記のようにスクリプトを呼び出す
```
$ ../../submit.sh
```

### サンプルテスト用

下記はテストを実行するためのスクリプト
test.sh
```bash
#!/bin/bash

oj t -c "python main.py"

```

### コンテスト開始用

下記はコンテストを開始するためのスクリプト
* 各問題URLをブラウザで開く
* atcoder-cliを使って各問題サンプルを取得
* atcoder-cliで作成されたテンプレートファイルをPyCharmで開く

new.sh
```bash
#!/bin/bash

contest=$1

open https://atcoder.jp/contests/${contest}/tasks/${contest}_a
open https://atcoder.jp/contests/${contest}/tasks/${contest}_b
open https://atcoder.jp/contests/${contest}/tasks/${contest}_c
open https://atcoder.jp/contests/${contest}/tasks/${contest}_d
open https://atcoder.jp/contests/${contest}/tasks/${contest}_e
open https://atcoder.jp/contests/${contest}/tasks/${contest}_f

acc new ${contest}

charm ${contest}/*/*.py
```

使い方
```
$ ./new.sh abc123
```



# エディタ

## PyCharm CE

VSCodeでも良いと思うが、PyCharmの方が若干賢い気がするので利用。


* Plugin
  * IdeaVim
    * vim操作を可能にする。
  * Settings Repository
    * PyCharmの設定をgithub上に保存することが可能になる。設定保存先リポジトリはgithubのプライベートリポジトリ。 

# ターミナル関連

## iTerm

Mac用ターミナル
Ctrl + ~ でアクティブにする設定を利用

## ghq

gitリポジトリ管理用ツール。fzfと併用すれば容易にAtCoder環境ディレクトリに到達できる

## fzf

fuzzy-finder。gitリポジトリをfuzzy-finderするためや、過去コマンドをfuzzy-finderするために利用。


# コンテスト時

## コンテスト開始時

下記コマンドで、問題文開く、サンプル取得、各問題ソースコードをPyCharm
で開く、A問題のディレクトリに移動をする
```
 ./new.sh abc167 && cd abc167/a
``` 

## コンテスト中

### PyCharmで問題を解く

PyCharmのLive Templates(スニペット)も適宜利用。

### 適当な入力を試す

* Ctrl + Shift + Rでコード実行。
* Cmd + 4 でRunウィンドウへ移動。
* 適当な入力をする
* 出力の確認
* Escでエディタに戻る

### デバッグをする

* ブレークポイントを指定
* Ctrl + Shift + Dでコード実行。
* Cmd + 5 でDebugウィンドウへ移動。
* 適当な入力をする
* F8押してステップ実行
* 適宜監視したい変数値をWatchに登録などをし監視
* デバッグ、、 


### サンプルテストを実行

ターミナル操作

```
$ pwd
(略)../atcoder/abc167/a

# サンプルが通るかチェック
$ pipenv run test
[*] 3 cases found
time: illegal option -- f
usage: time [-lp] command.
[!] GNU time is not available: time

[*] sample-1
[x] time: 0.039492 sec
[+] AC

[*] sample-2
[x] time: 0.037746 sec
[+] AC

[*] sample-3
[x] time: 0.036085 sec
[+] AC

[x] slowest: 0.039492 sec  (for sample-1)
[+] test success: 3 caseso

```
### コードを提出

ターミナル操作

```
# 提出前に再度サンプルテストが実行される
$ pipenv run submit Python

[*] 3 cases found
time: illegal option -- f
usage: time [-lp] command.
[!] GNU time is not available: time

[*] sample-1
[x] time: 0.036650 sec
[+] AC

[*] sample-2
[x] time: 0.035715 sec
[+] AC

[*] sample-3
[x] time: 0.035876 sec
[+] AC

[x] slowest: 0.036650 sec  (for sample-1)
[+] test success: 3 cases

(略)...

[x] PyPy is available for Python interpreter
[*] you can use `--no-guess` option if you want to do an unusual submission
[*] chosen language: 4006 (Python (3.8.2))
[!] the problem "https://atcoder.jp/contests/abc167/tasks/abc167_a" is specified to submit, but no samples were downloaded in this directory. this may be mis-operation
[x] open the submission page with browser
```

提出ページがブラウザで開かれるのでACするかを確認

### 次の問題へ移動

* ターミナルのディレクトリ移動
```
$ cd ../b
```

* PyCharmで次の問題のソースコードを開く

を繰り返す


