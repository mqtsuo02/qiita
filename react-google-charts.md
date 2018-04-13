# Reactでチャート出すならreact-google-charts

`React`

react-google-chartsっていうReact用のチャートライブラリがある
- [公式サイト](https://rakannimer.github.io/react-google-charts/)
- [GitHubページ](https://github.com/RakanNimer/react-google-charts)

[Google Charts](https://developers.google.com/chart/)っていうGoogle製のチャートライブラリ (以下本家と表現する) があり、react-google-chartsはこれのReact用ラッパー。コンポーネントをimportしてJSXで利用できるようになる

本家がGoogle製だということもあり、結構無理なデータの入れ方をしてもそれなりにいい感じで調整してくれる。チャート系のライブラリはUIが崩れやすかったりするが、このライブラリは比較的強いと思う


## 導入

ライブラリをインストール (`npm install react-google-charts`) して下記な感じでコンポーネント書けばOK

```HogeChart.jsx
// @flow
import React from "react"
import { Chart } from "react-google-charts"

type Props = {
  data: *,
  graphId: string,
  height: string,
  options: *,
  width: string,
}

export default ({ data, graphId, height, options, width }: Props) =>
  <div>
    <Chart
      chartType="PieChart"
      data={data}
      graph_id={graphId}
      height={height}
      options={options}
      width={width}
    />
  </div>
```

実装したいチャート別にoptions等を固定値にして、別々の名前でexportしておけば使いやすいと思う

型定義もコンポーネント別に詳細化すれば安全なものができると思う


## カスタマイズ

基本的な使い方としては、本家のstyleで設定している部分 (heightやwidth) やdrawChart関数内で設定している値 (ラベルやデータ) を、react-google-chartsではコンポーネントのpropsとして渡すようなイメージ

propsに設定できるパラメータと型は[ここ](https://github.com/RakanNimer/react-google-charts/blob/master/docs/Chart.md)で確認できる

公式サイトにStoryBook的な感じで触れる[デモページ](https://rakannimer.github.io/react-google-charts/#/examples/DonutChart?_k=33gr2y)があり、JSON形式でpropsの値を変えながら挙動を確認することができる

例えば本家PieChartsでの[Exploding a Slice](https://developers.google.com/chart/interactive/docs/gallery/piechart#exploding-a-slice)を実装したければ、本家のdataとoptionsで定義されている部分をデモにコピペしてあげれば確認できる (JSをJSON形式にするので若干手間ではあるが)

<img width="700" alt="exploding_chart.png" src="https://qiita-image-store.s3.amazonaws.com/0/178904/6071c7bd-cf95-b537-013b-e604f00264b9.png">

入れたJSONはこんな感じ

```json
{"chartType":"PieChart","width":"100%","data":[["Language","Speakers (in millions)"],["Assamese",13],["Bengali",83],["Bodo",1.4],["Dogri",2.3],["Gujarati",46],["Hindi",300],["Kannada",38],["Kashmiri",5.5],["Konkani",5],["Maithili",20],["Malayalam",33],["Manipuri",1.5],["Marathi",72],["Nepali",2.9],["Oriya",33],["Punjabi",29],["Sanskrit",0.01],["Santhali",6.5],["Sindhi",2.5],["Tamil",61],["Telugu",74],["Urdu",52]],"options":{"title":"Indian Language Use","legend":"none","pieSliceText":"label","slices":{"4":{"offset":0.2},"12":{"offset":0.3},"14":{"offset":0.4},"15":{"offset":0.5}}}}
```


## デモページにないチャートを出せるのか

本家サンプルにあるChart Typesとreact-google-chartsのデモページを比較すると、デモの方が若干サンプルが少ないように見えたので、デモにないものも実装できるのか気になった

例えば[Organization Chart](https://developers.google.com/chart/interactive/docs/gallery/orgchart)とか、本家のdata内にstyle指定のhtmlとかが入ってて、そこがうまくいくか否か

実際にやってみたが、style部分がうまくいかなかった。dataを端折ってシンプルにしたら一応使えるものではあった

試したJSON (うまくいかず)

```json
{"chartType":"OrgChart","width":"100%","data":[[{"v":"Mike","f":"Mike<div style=\"color:red; font-style:italic\">President</div>"},"","The President"],[{"v":"Jim","f":"Jim<div style=\"color:red; font-style:italic\">Vice President</div>"},"Mike","VP"],["Alice","Mike",""],["Bob","Jim","Bob Sponge"],["Carol","Bob",""]]}
```

<img width="767" alt="org_chart_ng.png" src="https://qiita-image-store.s3.amazonaws.com/0/178904/6953a9b3-d27a-f67a-148b-bd2fbd3caa67.png">

シンプルにしたJSON

```json
{"chartType":"OrgChart","width":"100%","data":[["Mike","","The President"],["Jim","Mike","VP"],["Alice","Mike",""],["Bob","Jim","Bob Sponge"],["Carol","Bob",""]]}
```

<img width="734" alt="org_chart.png" src="https://qiita-image-store.s3.amazonaws.com/0/178904/1223480c-60b6-34ab-2d93-3770d22a4ee8.png">


dataの中をうまくすればいけるのかもしれないが、単純にJSON形式にするだけじゃいけないっぽい

issueあげてる人もいるみたい
( https://github.com/RakanNimer/react-google-charts/issues/92 )

結論としては、デモページにサンプルがないチャートについては、導入前に検証した方が良さそうということ


## 締めの感想

- 使いやすくて好き
- Google LOVE
- ライブラリ作成者の[Rakan Nimerさん](https://github.com/RakanNimer) LOVE
