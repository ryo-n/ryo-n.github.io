---
title: "第一回マスターズ選手権 -決勝- 参加記"
date: 2024-04-22T17:09:41+09:00
---

第一回マスターズ選手権 -決勝- に参加しました。
チーム名は、BABA_IS_AC で、メンバーは ryo_n, sasayu, Taiyoの3人です。
結果は34位でした。


# コンテスト開始前

* 会場
    * [ソラシティカンファレンスセンター](https://www.soracity-cc.jp/)
    * ファミマ!!、スターバックスが近くにあります
        * お菓子にもコーヒーにも困らない、良い環境
* 受付
    * 10時-11時が受付時間
    * 10時過ぎには20人くらいの列が既にできていました
    * kaede2020さんが受付をしてくれました
* 会場
    * 3部屋に分かれている
        * 大きな1部屋で開催するとネットワークの設定が別途必要になり、コストが高くなる という話を懇親会でchokudaiさんが教えてくれました
    * 1チーム4席分のスペース
    * 8口くらいの電源を2チームで共有
        * 長い充電ケーブルがあると便利そうでした
    * WiFiは会場に用意されているもの。扉にSSIDとパスワードが貼ってありました
* ノベルティ等
    * サンドイッチ
    * inゼリー
    * クリアファイル
    * AtCoderステッカー
* その他
    * ネットワークトラブルに備え、暗号化zipを事前に配布するという試みがありました
    * トラブルがあった場合はパスワードを会場で公開し、問題はローカルで閲覧する運用です
        * 結果トラブルは発生しなかったので、暗号化zipは使わなかったです

# コンテスト中

* 自分はビジュアライザーの実装から開始しました
* テンプレートには、yunixさんの [visualizer-template](https://github.com/yunix-kyopro/visualizer-template-public) を利用しました
* 問題もろくに見ずにローカルテスターのコードを見て、ビジュアライザーを実装していました
    * x, yの入力がいつもと逆という情報もsasayuに教えてもらい助かりました
    * その情報を聞いていたのにも関わらず、終盤までバグが残っていました、、
* ビジュアライザーの実装は下記の通り
```
11:42 ドローンを描画
11:49 壁を描画
11:50 目的地を描画
12:39 ドローンの移動を描画
13:02 到着した目的地の色を変更
14:29 ドローン半径修正、キャンバスのサイズを大きく修正
14:58 壁の座標を修正
```

* 12時40分頃にはTaiyoが初提出をしました。提出チームが少なかったのもありますが、その時点で4位でチーム内で盛り上がりました
* 13時頃から自分も問題を解こうとし、問題を読み始めました。理解が曖昧なところはチーム名に聞いたりし、理解を深めました
* ドローン位置を仮定した、単純な貪欲を書いてA問題を試しましたが、目的地の横をかすめるような動きで全然得点には繋がらず
* 風の影響が少ないB問題ならいけるかなと思いましたが、こちらも横をかすめるような動きでで全然得点には繋がらず
    * 今思うと、ベクトルの計算か何かにバグがあった可能性が高いです
* 自分が得点に繋がらない間、sasayuがB問題を提出し、順調にスコアを伸ばしていました。ただ、周りの伸びも早く、順位は下がり30位くらいでした
* あとは、Taiyoのローカル環境テスター サポートをしたり、上記のビジュアライザーの壁の修正をしたりして、コンテストを終えました


# 懇親会

* 2Fの大きな会場で懇親会が開催
* 立食形式
    * 軽食
        * 寿司、サンドイッチ、 ローストビーフ等
    * アルコール
        * ビール、ワイン、ウィスキー等
    * ソフトドリンク
        * お茶、オレンジジュース等
* スタンプラリーゲーム
    * アルコールは、スポンサーブースを3つ回るともらえるという仕組み
    * 全スポンサーを回ると、AtCoderグッズがもらえる
    * 自分は全部まわりました
* スポンサーブース
    * 事業の説明やノベルティの配布がありました
    * スポンサー一覧
        * Monxer
        * THIRD
        * いい生活
        * ALGO ARTIS
        * RECRUIT
        * TOYOTA
* 何人かとお話したり、chokudaiさんと写真を撮ってもらったりしました
* 最後表彰式があって解散

# 二次会

* shindannin さん主催の二次会 (反省会)に参加
* 会場は Ottotto BREWERY 淡路町店
* ビール美味しく、二次会に丁度良い軽食がでて大満足でした
* 他のチームの方々と話したり、ネット越しにしか話したことのない方々とお話できて楽しかったです