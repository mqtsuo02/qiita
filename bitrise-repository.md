# bitrise.ymlをリポジトリ内で管理するための手引き

`Android` `iOS` `CI` `reactnative` `Bitrise`

Bitriseはモバイル開発向けのCIサービス => [bitrise.io](https://www.bitrise.io/)

|<img width="430" alt="build_for.png" src="https://qiita-image-store.s3.amazonaws.com/0/178904/8f3e5cb1-eb1f-f0d0-22fa-661542561b17.png">|
|:-:|

無料の範囲でiOSビルドを行うことができるので、個人プロジェクトにはありがたい。今回はReactNativeプロジェクトのリポジトリを設定して動かして見た。

## bitrise.ymlでワークフローを設定する

Bitriseにリポジトリを設定した初期段階では、bitrise.ymlはサービス側（bitrise.io）で管理されているが、それをプロジェクトのリポジトリ内で管理したい。そんなとき。

当然ながら公式には手引きがある => [Use bitrise.yml from repository](https://devcenter.bitrise.io/tips-and-tricks/use-bitrise-yml-from-repository/)

英語が分かる人なら何事もなく実現できるのだが、自分は公式の手引きが100%理解できていなかったために若干はまってしまった。上の手引きの概要をまとめつつ、はまったポイントを残しておきたい。

## トリガーマップはbitrise.ioで持つ、それ以降はリポジトリ内で持つ

公式の手引きによると、bitrise.ymlのトリガーマップはbitrise.ioで持った方が良いとのこと。その理由は、リポジトリ内でトリガーマップを持つと、クローンした後でないとトリガーのパターンを判定できなくなるから。

bitrise.ioでトリガーマップの設定をすれば、下図のワークフローが始まる前にトリガーのパターンに応じて処理をしないというフローも作れるのだが、全てをリポジトリ内で持つと必ずクローンしなければならなくなる。

|![bitrise_flow01.png](https://qiita-image-store.s3.amazonaws.com/0/178904/00965864-17cb-e654-91a6-78cb591e6ddc.png)|
|:-:|

なので公式ではbitrise.ymlを分けて持つことが推奨されている。

上図の`Git Clone Repository`までをbitrise.ioで設定し、それ以降のワークフローをリポジトリ内で設定する感じ。


## 作業手順

- bitrise.io上のbitrise.ymlをダウンロード
- リポジトリ直下にbitrise.ymlを置く
- リポジトリ内のbitrise.ymlの`steps`にある`activate-ssh-key`と`git-clone`の設定を削除する
- bitrise.ioのbitrise.ymlの内容を公式記載の設定で上書きする
- あとはpushすれば動きます（ということだ）

作業をした後のbitrise.io上のWorkFlowsは下のような感じになる。

|![bitrise_flow02.png](https://qiita-image-store.s3.amazonaws.com/0/178904/d71036ec-5fe3-e4bf-d405-9cd084bafaa6.png)|
|:-:|


## はまった点

上の手順をやって動かしてみたが、`continue from repo`でエラーになってしまった。エラー内容は『`ci`っていうworkflowは定義されていない』みたいな感じだった。

自分はこの時点でBitriseのドキュメントをあんまり読んでなかったので、ちゃんと勉強してから戻ってきたら、おそらくbitrise.ioのbitrise.ymlで設定している`bitrise run "${BITRISE_TRIGGERED_WORKFLOW_ID}"`で引っかかってるんだろうなと当たりがついた。

直前に`printenv`を入れて確認してみると、この変数に`ci`っていう値が入っていた。

この変数はbitrise.ioの`trigger_map`で設定している`workflow`の値が入るらしい。

公式の手引きにもちゃんと書いてあった（初見で理解できなかった自分にエールを）

> The trick is bitrise run "\${BITRISE_TRIGGERED_WORKFLOW_ID}". The BITRISE_TRIGGERED_WORKFLOW_ID environment variable is set to the "entry" workflow, the one which started the build. So, by running the ci workflow, the bitrise run "${BITRISE_TRIGGERED_WORKFLOW_ID}" command will be the same as bitrise run "ci".


故に解法としては、bitrise.ioの`trigger_map`の`workflow`に設定している値と、リポジトリ内の`workflows`に設定している値を対応させてあげればよい。


## 以上

![bitrise_logo.png](https://qiita-image-store.s3.amazonaws.com/0/178904/d9abd1e4-d4cf-d833-1f13-942a20b125d5.png)

- Bitriseのアイコン可愛い。癒される〜
- Bitriseのアイコン可愛い。癒される〜
- Bitriseのアイコン可愛い。癒される〜
