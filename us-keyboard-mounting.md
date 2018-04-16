# US配列のキーボードをJIS配列のMacBookにマウンティングした思い出

`Mac` `Keyboard` `MacBook`

これを実現するためにやったことのまとめ

|![mounting_keyboard.jpg](https://qiita-image-store.s3.amazonaws.com/0/178904/a4a8ec87-047b-9e6a-5d0b-ebd2b3d1315b.jpeg)|
|:-:|

US配列主義者だけど、現場に入ったらJIS配列のMacが用意されていた。そんなとき。

自分の場合、本体付属のトラックパッドをよく触るので、外部接続のキーボードをMacBookの前に置いて作業するのも効率が落ちる。

だから本体のキーボードがある位置に、US配列のキーボードをいい感じにマウンティングさせたかった。


## Apple純正のMagic Keyboardがジャストサイズ

Appleのサイトでキーボードを調べてみると、MacBook付属のキーボードと同じスケール感のものがあった => [Magic Keyboard - 英語（US)](https://www.apple.com/jp/shop/product/MLA22LL/A/magic-keyboard-%E8%8B%B1%E8%AA%9Eus)

|![magic_keyboard.jpg](https://qiita-image-store.s3.amazonaws.com/0/178904/aa5d82d4-69fa-c30c-51f7-d9c3488bcb79.jpeg)|
|:-:|

もしかするといけるかもな...と思い、JIS配列のMacBookを持って電気屋に行った。

実際に売り場で現物をマウンティングさせてみると、これがビックリ。ジャストサイズではないか。

上に乗せるぶん若干の高低差はあるが、そんなに違和感がなかった。すぐに購入した。

## Karabiner Elementsで本体のキーボードを無効化する

[Karabiner Elements](https://pqrs.org/osx/karabiner/)というソフトを使えば、外部キーボードを接続したときに本体キーボードを無効化する設定ができる。

設定は簡単で、外部キーボードを接続した後に`Preferences > Devices`の`Disable the built-in keyboard while ...`をONにするだけ。

これで、Magic KeyboardをONにすると、本体付属のキーボードが無効化されるようになった。

マウンティングさせても大丈夫。


## 注意点等

### 電源ボタンは反応してしまう

上の設定を行っても、本体の電源ボタンだけは反応してしまうので注意が必要。

ただ、マウンティングしているキーボードが下手にずれない限りは特に押すことはない。

自分の場合、10ヶ月くらい使って2回くらいスリープしたような。それくらいの頻度。

### Early 2016のMacBookじゃないといい感じにならない

キーが薄くなったEarly 2016のMacBookじゃないといい感じにならないようだ。

試しに一世代前のEarly 2015のMacBookにマウンティングさせてみたが、キーに厚みがあるぶんフワフワァして安定しなかった。フワフワァして安定しなかった。

## 以上

ありがとうございました。
