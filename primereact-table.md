# PrimeReactのテーブルコンポーネントが多機能で結構使える

`PrimeFaces` `React` `PrimeReact`

PrimeReactっていうReactのUIライブラリがある。OSS

- [公式サイト](https://www.primefaces.org/primereact/#/)
- [GitHubページ](https://github.com/primefaces/primereact)

元々はPrimeFacesっていうJava系のUIライブラリがあって、それのReact版 (Angular版のPrimeNGもある)
公式サイトのガイドやサポートがしっかりしていて、それなりの安心感がある

名前とかアイコンはトランスフォーマーのコンボイからとってるっぽい
[Optimus Prime - Wikipedia](https://en.wikipedia.org/wiki/Optimus_Prime)

2017/03にα版が公開されて、徐々に機能追加されていき2017/09にバージョン1.0.0がリリースされた
現在もアップデートがされていて、この記事を書いている時(2018/02/09)のLatest releaseは1.4.0
スタイルはBootstrapライクで親しみやすいが、余白が少なめな印象はある

今回はPrimeReactのテーブルコンポーネントを触って見たので、その感想
Data > DataTable (https://www.primefaces.org/primereact/#/datatable)


## 特徴

### 多機能なテーブルが作れる

自前で実装するにはそれなりに工数がかかる機能が標準で使える
各機能のデモが公式ページで見れるので、実装前に吟味もしやすい

- ページング
- ソート
- フィルタ
- 編集機能
- 行選択
- 行折りたたみ
- 列幅調整
- 列入れ替え
- 列表示/非表示
- CSV出力
- データの非同期読み込み

### ヘッダー部分に自前のコンポーネントが入れられる

テーブル系のライブラリによっては機能を増やすあまり、実装上の制約があるものもある
(ヘッダーに文字列しか挿入できなかったり、ライブラリ標準のボタンしか設置できなかったり...)
PrimeReactのテーブルはヘッダー内も自由にコンポーネントが書けるので、ライブラリによる制約がなく使える

ヘッダーに制約があることでライブラリを採用できなかったりするので、そこは安心


## 導入

実際にコンポーネントをimportして使うまでにはざっと以下の手順

1. npmパッケージのインストール
  `npm install primereact --save`

2. 各CSSのimport
  - 共通CSS：`primereact.min.css`
  - 使用テーマ：`themes/omega/theme.css`
  - FontAwesome：`font-awesome.css` (デフォルトのアイコンとして使用されている)

3. あとは使いたい場所で使いたいコンポーネントをimport
  `import { DataTable } from "primereact/components/datatable/DataTable"`

特にハードルは感じなかった


## 締めの感想
- スタイルの癖があまりないので、基本は他のUIライブラリを使って一部分だけPrimeReactを使用するとかでもうまく馴染みそう
- テーブル以外にも割と凝ったコンポーネントがあるので、要件にマッチすれば使えるところには使えそう
