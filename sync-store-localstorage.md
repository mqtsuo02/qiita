# StoreとLocalStorageを部分的に同期させる（備忘録）

`JavaScript` `redux`

同期は[redux-localstorage](https://github.com/elgerlambert/redux-localstorage)を使用して実現する
デフォルトだとStoreのState全て同期するため、設定用の関数(slicer)を定義する

本記事は本家READMEの実装サンプル的な位置づけ


## 実装ルール

- persistState関数に設定値を渡したものをcomposeする
- keyに設定した値がLacalStorage上のKeyとなる
- ValueはJSON形式で一括して保存される

Stateがこのような構造で定義されているとして、user: {id, name}だけ同期したいものとする

```js

const state = {
  user: {
    id: 1,
    name: "foo",
    address: "bar",
  },
  data: {
    /* ... */
  },
}
```

Storeの定義を以下のように書く

```js

import {compose, createStore} from 'redux'
import persistState from 'redux-localstorage'

const store = createStore(
  reducer,
  initialState,
  compose(
    middlewares,
    persistState("", {
      key: "hoge",
      slicer,
    })
  )
)


// slicerで以下のようにStateから必要な部分を切り出す

const slicer = () => (state) => ({
  user: {
    id: state.user.id,
    name: state.user.name,
  },
})
```

ブラウザ上では以下のように保存される

|Key|Value|
|:-------|:-------|
|hoge|{"user":{"id":1,"name":"foo"}}|

## 締めの感想

勝手に変換して同期してくれるので非常に楽だった


## 参考
https://github.com/elgerlambert/redux-localstorage
