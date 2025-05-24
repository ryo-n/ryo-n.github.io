---
title: "開発環境 2025"
date: 2025-05-24T09:14:03+09:00
draft: false
---

# OS

macOS


# エディタ

Neovim, VSCode

* テキストファイルを編集するときにはNeovimを使います。このファイルもNeovimで編集しています。
* コーディングをするときにはVSCodeを使います。簡単なスクリプト程度ならNeovimを使います
* Neovimはプラグイン管理に疲れたので、Lazyvimを利用


# ターミナルエミュレータ

Ghostty

* アイコン可愛く、設定シンプルなので良いです。自分の設定はこれくらいです。

```
font-family = "Monaco"
font-family-bold = "Monaco"
font-family-italic = "Monaco"
font-family-bold-italic = "Monaco"
font-family = "HackGen Console NF"
font-size = 12

background-opacity = 0.85

macos-titlebar-style = tabs
macos-option-as-alt = true

keybind = ctrl+i=text:\x09
keybind = ctrl+m=text:\x0d
keybind = ctrl+[=text:\x1b

mouse-hide-while-typing = true
```

# ターミナルマルチプレクサ

tmux

* 以前はscreen使っていて、今はtmux。zellijも触ったが、乗り換えませんでした。
* エスケープキーはCtrl + j にしています。
* ウィンドウ切り替えに Shift + 左右矢印キーを使っています。 

# シェル

zsh

* zshrcをいつか整理したいです。

# フォント

Monaco + Hack Nerd Font Mono

* 英数字はMonacoで日本語などはHack Nerd Fontにしています。

# ブラウザ

Edge

* Google Chrome でも良いのですが、なんとなくEdgeを使っています。

# 開発環境のセットアップ

nix, homebrew

* nix でCUIを管理しています。
* homebrew でGUIを管理しています。
* mas を使っていてApp Storeのアプリも管理しています。
* homemanager, nix-darwinを使っていて、そこからhomebrewなどを呼び出しています。

# dotfiles

chezmoi

* ドットファイル管理はnixは利用せず、chezmoiを利用しています。

# キーボード

https://system76.com/keyboards/
Launch keyboard + Kailh Deep Sea Silent Pro Box Islet

* Apple純正のMagicKeyboardを使っていましたが、最近Launch keyboardにしました。
* スペースキーの左に4キーあるのが好みです。
* スペースキーの左右を英数、かなに割り当てて、英数の左のキーをCmd、Alt としていてずらしています。
* また、かなの右のキーはHyperKeyに割り当てていて、グローバルショートカットキー呼び出しに利用しています。


# その他コマンドラインツール

## git 関連

tig, lazygit

* 基本tigを利用しています。
* neovimからの呼び出しはlazygitをにしています。

## コマンド履歴管理

atuin

* サーバーにコマンド履歴を保存していて、どの端末からもコマンド履歴を参照できるようになっています。
* 自前でサーバーを立てることもできますが、atuinのサーバーを利用しています。


## ディレクトリ移動

zoxide

* ディレクトリ移動しやすくなります。
* zi 使ってインタラクティブサーチしつつ、移動先を選ぶことが多いです。

## リポジトリ移動

ghq

* Ctrl + g でリポジトリ一覧をfzfでインタラクティブサーチし、移動できるようにしています。

