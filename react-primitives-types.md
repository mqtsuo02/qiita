# react-primitivesのTypeScript型定義ファイルをつくる

`TypeScript` `React` `reactnative` `react-primitives`

TypeScriptを採用しているプロジェクトでreact-primitivesを使ってみた。

react-primitivesの型ファイルをinstallしようとしたが、ないと怒られた。

```
(๑•﹏•) < npm install --save-dev @types/react-primitives
npm ERR! code E404
npm ERR! 404 Not Found: @types/react-primitives@latest

npm ERR! A complete log of this run can be found in:
npm ERR!     ごちゃごちゃ
(#°﹏°) <
```

ちなみに@なしでやってもダメって言われた。

```
(๑•﹏•) < npm install --save-dev types/react-primitives
npm ERR! Error while executing:
npm ERR! /usr/bin/git ls-remote -h -t ssh://git@github.com/types/react-primitives.git
npm ERR!
npm ERR! ERROR: Repository not found.
npm ERR! fatal: Could not read from remote repository.
npm ERR!
npm ERR! Please make sure you have the correct access rights
npm ERR! and the repository exists.
npm ERR!
npm ERR! exited with error code: 128

npm ERR! A complete log of this run can be found in:
npm ERR!     ごちゃごちゃ
(#°﹏°) <
```

## ここから本題

ナイスなissueがあったので、それに従ってみた。 => https://github.com/lelandrichardson/react-primitives/issues/82

`src`配下に以下のようにディレクトリをきって、`index.d.ts`ファイルを作成する

`src/@types/react-primitives/index.d.ts`

```index.d.ts
declare module 'react-primitives' {
  export {
    StyleSheet,
    View,
    Text,
    Image,
    Touchable,
    Animated,
  } from 'react-native'
}
```

ファイル置いておけば自動で認識して解決してくれる。


## 所感

今回はreact-nativeから流用できたから楽だった。

こういうケースは他のライブラリでも多いと思うが、`tsconfig.json`で`"skipLibCheck": true`して無視してしまうのが一般的なんだろうか。どうなんでしょう。


以上、ありがとうございました。
