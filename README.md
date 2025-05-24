
* hugoインストール

nix 設定ファイルに記述されていれば、下記コマンドでインストールされる。

```
darwin-rebuild switch --flake ~/.config/nix-darwin/#${hostname}
```

* local起動

```
hugo server -D
```


* 記事作成

```
hugo new posts/title.md
```
