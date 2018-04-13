# ReduxでネストしているStateの一部分だけを更新する（備忘録）

`JavaScript` `redux`

Stateを小さい単位で更新したい時の、Reducerのreturn内の書き方

Reducerを分割するほどではない時にやる

いっつも忘れるので備忘


## Example

レストランの注文管理システムだとして...

Stateの構造。各要素に個数を持ってるイメージ

- foods
  - beef
  - chicken
- drinks
  - coffee
  - tea
  - water

```js
// @flow

type State = {
  foods: Foods,
  drinks: Drinks,
}

type Foods = {
  beef: number,
  chicken: number,
}

type Drinks = {
  coffee: number,
  tea: number,
  water: number,
}

```

注文情報をセットする`SET_ORDER`と、コーヒーの個数だけセットする`SET_COFFEE`があるとする


```js
// @flow

const setOrder = (order: State): Action => ({
  payload: order,
  type: "SET_ORDER",
})

const setCoffee = (count: number): Action => ({
  payload: count,
  type: "SET_COFFEE",
})

```

## こんな感じ

`SET_COFFEE`のreturn内

```js
// @flow

const orderReducer = (state: State = initialState, action: Action): State => {
  switch (action.type) {
    case "SET_ORDER":
      return action.payload
    case "SET_COFFEE":
      return {
        ...state,
        drinks: {
          ...state.drinks,
          coffee: action.payload,
        },
      }
    default:
      return state
  }
}

```

以上
