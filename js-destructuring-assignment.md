# オブジェクトを分割代入する際に、変数に別名をつける（備忘録）

`JavaScript`

オブジェクトを分割代入する際に、プロパティ名とは別の名前にできたら便利だなと思い調べた。
意外な書き方でちょっと驚いた。


## こんな感じ

```hoge.js
const itemObject = {
  id: 1,
  name: "foo",
}

const { id: itemId, name: itemName } = itemObject

console.log(itemId) // 出力される
console.log(itemName) // 出力される

console.log(id) // エラーになる
console.log(name) // エラーになる

```

## 有効な場面

様々な場面で使えると思うが、APIを複数回叩く場面で使ってみた。
APIのレスポンスをオブジェクトで受け取る際に、名前の重複を回避して分解できる。

```fuga.js
// APIレスポンスの共通オブジェクト{response, error}があるとして

const { response: res1, error: err1 } = yield apiFunction1()
const { response: res2, error: err2 } = yield apiFunction2()

if (!(err1 || err2)) {
  /* ... */
}


// 別名をつけないと、冗長でちょっと気持ち悪いと感じる時もある
const object1 = yield apiFunction1()
const object2 = yield apiFunction2()

if (!(object1.error || object2.error)) {
  /* ... */
}

```


## 締めの感想

どうしてこんな書き方なのかはよく分からないが、できる。
モチベーションが余ったら調べたい。


## 参考

https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment

ページの真ん中あたりに記述あり
