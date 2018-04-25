# メロンのはなし（melonJSで始めるゲーム開発入門）

`JavaScript` `入門` `ゲーム制作` `TiledMapEditor` `melonJS`

## この記事のテーマ

![melonman.png](https://qiita-image-store.s3.amazonaws.com/0/178904/94020aea-4797-1ca5-e3d1-03f8e36e72a4.png)

モダンなJSと日々奮闘しているそこのあなた！！（ほし）
あまいあま〜いメロンの国へいざなっちゃうゾ！！（はーと）

## melonJS

[公式サイト](http://melonjs.github.io/melonJS/docs/index.html)

![melon.png](https://qiita-image-store.s3.amazonaws.com/0/178904/02ada03b-21a1-77ee-4638-70c928c81091.png)

- JavaScript製のゲームエンジン！
- 2Dゲームの開発に適している！
- HTML5が動作するブラウザでゲームが動く！軽い！

### こんなのが作れちゃう！！

ちなみに筆者の手作り（ひどい作り）

<img width="864" alt="mytown.png" src="https://qiita-image-store.s3.amazonaws.com/0/178904/efef97eb-01b5-2da8-f565-df54081d2ccb.png">

github => [mqtsuo02/melonjs-town-sample](https://github.com/mqtsuo02/melonjs-town-sample)

公式には色んなサンプルが公開されてるよ（ほし） => [made-with-melonJS](https://github.com/melonjs/melonJS/wiki/made-with-melonJS)

## いますぐ始めたい！！

その情熱、メロンにぶつけろ！！

### 必要なものは2つだけ！

- nodeの開発環境
- [Tiled Map Editor（無料）](https://www.mapeditor.org/)

## まずは土台を作るよ〜

だまってコマンドを打て！！

```
# grunt入ってない人はインストール
npm install -g grunt-cli

# 公式のBoilerplateをclone
git clone https://github.com/melonjs/boilerplate.git
cd boillerplate

# npm install
npm install

# ローカル環境立ち上げ
grunt serve

```

ブラウザから`http://localhost:8000/`にアクセスして黒い画面が見えればOK！！

ちなみに`http://localhost:8000/#debug`とアクセスすればデバッグモードでみれるよ！！（ほし）

ビルドコマンドその他は`melonjs/boilerplate`のREADMEを参照 => [melonjs/boilerplate](https://github.com/melonjs/boilerplate)

ちなみにBoilerplateにはデフォルトでElectronが入っているので、コマンド一つでWindows/macOS/Linux向けにデスクトップアプリがビルドできる。すごい。

## 画面をつくるよ〜

芸術性がとわれる！！（ははは）

使いたい素材をここに入れておく => `data/img/`（今回は[capsulemonsters/newbark](https://github.com/capsulemonsters/newbark)のassetsを使わせてもらった）

Tiledマップエディタを起動 & 新規マップの作成 => `data/map/`に保存

１マス：32 x 32、800 x 480になるように設定（好きにやって良い）

<img width="450" alt="map_setting.png" src="https://qiita-image-store.s3.amazonaws.com/0/178904/4405fd5e-d452-2118-dd4c-b252aca23534.png">

タイルセットの読み込み => `data/img/`に置いたマップ素材を選択

<img width="570" alt="tileset_setting.png" src="https://qiita-image-store.s3.amazonaws.com/0/178904/9ffd8d9d-ba5b-c701-33cb-e0e4d97efe90.png">

タイルセットを読み込んだら、あとはマップを描くのみ！！（芸術性）

レイヤーを前面と背面分けて作るといい（物が前面、地面/水面が背面）

<img width="1095" alt="draw_down.png" src="https://qiita-image-store.s3.amazonaws.com/0/178904/02fb5028-d938-e641-142b-07f37b9f75a1.png">

左側を描いたら力尽きた図

## ロジックを書くよ〜

コピペだって立派なプログラミングさ！！

`js/game.js` => 画面サイズをマップに合わせる / autoscale追加

`js/screens/play.js` => マップデータの読み込み（`data/map/*.tmx`のファイル名を設定）

ここまでで`grunt serve` => ブラウザにマップが表示されていればOK

<img width="750" alt="browser_map.png" src="https://qiita-image-store.s3.amazonaws.com/0/178904/e3569e0a-91a2-e8d4-ef5f-cedfbb322408.png">


ここまでやると結構満足感がある

## 主人公を召喚するよ〜

TiledMapEditorでmainPlayerっていうオブジェクトレイヤをつくって、そこに長方形ツールで箱を書く

作った箱オブジェクトにカスタムプロパティを追加する => imageは`data/img/`に置いたファイル名を設定する

|<img width="375" alt="object_setting.png" src="https://qiita-image-store.s3.amazonaws.com/0/178904/41b35a22-6d37-e3a6-1335-a93a7dbfac04.png">|
|:-:|

#### `js/game.js`にキーボード設定を書く

こんな感じで上下左右

```
// enable the keyboard
me.input.bindKey(me.input.KEY.LEFT, "left")
me.input.bindKey(me.input.KEY.RIGHT, "right")
me.input.bindKey(me.input.KEY.UP, "up")
me.input.bindKey(me.input.KEY.DOWN, "down")
```

#### `js/entities/entities.js`に主人公の動作を書く

こんな感じでアニメーションを定義

```
// define a basic walking animation (using all frames)
this.renderable.addAnimation("leftWalk", [3, 4])
this.renderable.addAnimation("rightWalk", [1, 2])
this.renderable.addAnimation("upWalk", [8, 9, 8, 10])
this.renderable.addAnimation("downWalk", [5, 6, 5, 7])

// define a standing animation (using the first frame)
this.renderable.addAnimation("stand", [5])
this.renderable.addAnimation("standLeft", [3])
this.renderable.addAnimation("standRight", [1])
this.renderable.addAnimation("standUp", [8])
```

とりあえずif文で動かしてみる

```
if (me.input.isKeyPressed("left")) {
  // update the entity velocity
  this.body.vel.x -= this.body.accel.x * me.timer.tick

  // change to the walking animation
  if (!this.renderable.isCurrentAnimation("leftWalk")) {
    this.renderable.setCurrentAnimation("leftWalk")
  }
} else if (me.input.isKeyPressed("right")) {
  // update the entity velocity
  this.body.vel.x += this.body.accel.x * me.timer.tick

  // change to the walking animation
  if (!this.renderable.isCurrentAnimation("rightWalk")) {
    this.renderable.setCurrentAnimation("rightWalk")
  }
}
```

ちゃんと設計して良いものを作ろう！！（白目）

## 見えない壁をつくる

`collision`って名付けたオブジェクトレイヤを作って、長方形ツールで壁を書く

<img width="1202" alt="collision.png" src="https://qiita-image-store.s3.amazonaws.com/0/178904/60370bb9-fa03-c7c3-a47b-8bff8e17dca2.png">

それだけでOK！！主人公がちゃんとぶつかるか確認しよう！！

<img width="864" alt="datsugoku.png" src="https://qiita-image-store.s3.amazonaws.com/0/178904/ff0782bf-4112-2434-5e48-1cbb32beabaf.png">

......ん？？？

|<img width="530" alt="datsugokugoku.png" src="https://qiita-image-store.s3.amazonaws.com/0/178904/ad5b8f3a-b31b-492b-214a-e2ab0730aa53.png">|
|:-:|

シャバの空気はうめぇ〜！！！！

## できたかな？

今回は公式の[tutorial-platfomer](http://melonjs.github.io/tutorial-platformer/)を参考にして作ったので、分からないところはそっちで解決できるかも

とりあえず筆者が徹夜で作ったものはここ（ひどい作り） => [mqtsuo02/melonjs-town-sample](https://github.com/mqtsuo02/melonjs-town-sample)

以上、ありがとうございました。

## お役立ちリンク

- [melonJS - wiki](https://github.com/melonjs/melonJS/wiki)
- [公式チュートリアル](http://melonjs.github.io/tutorial-platformer/)
- [melonJSで作られたサンプル集](https://github.com/melonjs/melonJS/wiki/made-with-melonJS)
