# Part2_2 review

[PullRequestURL](https://github.com/char-miki-tty/RandStrGenerator/pull/1)

---
## javadocの１文目の終わりにはピリオド（.）または句点（。）を書く

### 問題点

* ピリオドまたは句点までがクラスの概要になる
* そもそもjavadocの仕様を理解していない

### 対応

* 1文目の終わりにピリオド追加

---
## クラスのjavadocにどういう３文字なのかを書くこと

### 問題点

* クラスの説明が中途半端
* 3文字のランダムな文字列がどんな文字列か分からない

### 対応

* 文字列の説明をクラスのjavadocに追加

---
## char[] CHAR_LISTの変数名はListではなくArray

### 問題点

* ListではないのにListという変数名はおかしい

### 対応

* その変数の用途や型にあった名前をつける

---
## 数字と英小文字ならば、変数名はstrではなくalphaNumericの方が良い

### 問題点

* strでは抽象的
* 数字と英小文字で限定しているのであれば変数名からもそれが分かるようにするべき

### 対応

* strをalphaNumericに変更

---
## private final staticではなくprivate static finalのほうが一般的

### 問題点

* 修飾子の並びが一般的ではない
* 一人だけ違う書き方をするな！

### 対応

* privete static finalに変更

---
## propertiesファイルの場所の変数名はURLではなくPATHではないか

### 問題点

* どう見てもURLではない。PATHです！

### 対応

* PATHに変更

---
## 定数のcharの配列はStringの配列でよかった

### 問題点

* わざわざcharをStringにするぐらいなら最初からStringを使った方が良い
* charをfor文で回して配列に入れるのが分かりにくい
* 他の人が見て理解し難いものは避ける
* 自分もすぐに思い出せないような処理を書かない
* Stringのアルファベット、数値をそのまま配列に入れた方が分かりやすい

### 対応

* Stringに変更してそのまま配列入れる

---
## 今使われている数字ならusedじゃない

### 問題点

* 英語頑張ろう

### 対応

* usingに変更

---
## マジックナンバーはやめる

### 問題点

* 数値が何を表しているか分からない
* 今後変更になる可能性がある

### 対応

* 絶対に固定であれば変数にする
* 文字列の長さ等、可変する可能性があればlengthを使う

---
## 否定から始まる条件はやめる

### 問題点

* 条件が分かりにくい
* 肯定より否定の方が理解に時間がかかる

### 対応

* 否定じゃないif文に変更
* if文の条件式は単純な条件を書こう！

---
## ifとelseでやってることが対応してない

### 問題点

* if elseは対応している処理を書くべき

### 対応

* 対応していない処理があるならifだけにしてtrueだったら関数から抜けるような処理にする

---
## ハードコーディングはやめる

### 問題点

* 他の人が見たら急に謎の数値や文字列が出てきてビックリする
* 仕様変更した時などに後から変更するのが大変

### 対応

* 変数か定数にしてコメントをつける

---
## Stringの再代入はやめる

### 問題点

* Stringは不変オブジェクト！
* さらにStringは+演算子を使うと元の文字列とは別に新しく文字列が出来るので無駄なオブジェクトが生成される

### 対応

* StringBuilderまたはStringBufferに変更
* 今回はスレッドセーフにする必要がないのでStringBuilderにする

### その他

* StringBuilder → 処理速度が速いがスレッドセーフではない
* StringBuffer → 処理速度が遅いがスレッドセーフ

---
## getKeyメソッドの中で文字列のチェックを行なっている

### 問題点

* getKeyという名前も問題、Keyって何だ！
* メソッド内でget以外の処理を行なっている

### 対応

* 重複チェックは別のメソッドに分ける
* isDuplicate()でbooleanを返す

---
## かっこやばい、Arraysの中からRandomにとれなかったっけ？

### 問題点

* 非常に読みづらい
* charをStringに変換するなら初めからStringで良い
* 既存APIの仕様の理解が足りない
* わざわざMath.randomを使用する必要がない

### 対応

* charではなくStringのListに変更
* 既存APIで使えるものを使う
* ArraysにRandomで取れるメソッドはなかったので、Collectionsのshuffleメソッドを使用

### その他

* ありものは利用しましょう！
