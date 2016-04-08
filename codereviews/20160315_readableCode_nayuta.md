# Part2 review

[PullRequestURL](https://github.com/nayuta28/LineAnalyzer/pull/2)

---
## JavaDocにそのままファイルフォーマットを記載している

### 問題

* JavaDocはhtmlで表示されるので整形されて表示されないことがある

### 対応

* htmlタグを使用する
* そのまま表示したければpreタグを使用する

---
## 不要なコメントが記載されている

### 問題

* コードからすぐに分かることをコメントに書くべきでない

```java
// ファイルから全行を取得
List<String> allLinesList = readFile(filePath);
```

### 対応

* コメントを削除
* メソッド名を`readAllLinesByFile()`に変更

---
## 横に長過ぎるコードは見辛い

### 問題

* 横にツラツラと長くなってしまうとコードが一目で追えなくなってしまう

### 対応

* 横幅の制限をコーディングルールに追加する
* 昔は80行、長い人で120行まで
* 100行を制限とする
* メソッドチェーンでコードが長くなる場合はメソッドごとに改行する

### その他

* 前回同じ内容の指摘があったのに出来ていなかったのでIDEで必ず設定するようにする

---
## マジックナンバーはやめよう

### 問題

* コード上に **1**, **0** 以外の変数が出てくると読み手はなぜ数が急に出てきたか分からない

### 対応

* **1**, **0** 以外の数はコード上に突然出さない
* 変数、定数に格納する
* 設定ファイルに書き出す

### その他

* これも前回出た指摘事項。コーディング時に意識するようにする。

---
## mapのソートと集計を１メソッド内で行っている

### 問題

* 複数の処理を行うメソッドは理解しにくく追いづらい

### 対応

* 処理を適切に切り分けて１メソッド１処理にする

---
## +演算子はあまり使うべきじゃない

### 問題

* String同士を + で結合するとパフォーマンスが低下するのでやめたほうがいい

### 対応

* 1.8から追加されたString#join() を使用する

### その他

* 第１回でも上がっていた指摘事項だが、対策方法は複数ありそうなので有効法を検討していきたい

---
## 変数の宣言の型がインターフェイスじゃない

### 問題

* 実装を切り替えたくなった場合に修正箇所が増えてしまうリスクがある

### 対応

* ListやMapはインターフェイスで宣言する

### その他

* [調べていて分かりやすかった記事](http://qiita.com/Mura-Mi/items/e52c28ab7cb5db140d53)

---
## java.util.stream#foreach内の一時変数が分かり辛い

### 問題

* 変数名が(key, value)では中身が分からない

### 対応

* 一時変数であっても分かりやすい変数名にする

### その他

* 意識しすぎて変数名が長くなり過ぎると今度はコードが読みづらくなるので注意する

---
## 変数のスコープが大きい

### 問題

* スコープの有効範囲が広過ぎると意図しないところで値が変わってしまいその後の処理にも影響が出るリスクがある

### 対応

* 後から変更をされたくないクラス変数はprivate static final にする