# Part3 review

[PullRequestURL](https://github.com/ta-chibana/ghostmethod_rb/pull/3)

---
## Productクラス(両方)にproduct~~~という名前を付ける必要はない

### 問題

* Productクラス内の変数やメソッドはProductクラスのものであるから、  
「Productクラスの~」という意味で名前に付与する必要はない。

### 対応

* "product_name"等の名前から"product"を削除

---
## method_missingでやるべきでない処理がある

### 問題

* `method_missing`は、定義されていないメソッドが呼び出された場合に呼び出されるが、  
`method_missing`内でProductクラスの肝となる処理が行われてしまっている。
* 一つのメソッドが複数の役割を持ってはいけないという原則から外れている。

### 対応

* `method_missing`の役割を処理の受け渡しのみにする。
* 肝となる処理は別のメソッドとして切り出す。

---
## DataSourceの役割が多い

### 問題

* DB接続、各種テーブルからのデータの取得といった、複数の役割を持ってしまっている。

### 対応

* DataSourceクラスの役割をDB接続のみにし、それ以外の機能は別のクラスに任せる。

---
## メソッドを細かく分け過ぎている

### 問題

* `is_present?`、`return_data`は、大した処理をしていないにもかかわらず、メソッドに切り出されており、  
逆に処理を追いづらくなってしまう。
* 一箇所からしか呼び出されておらず、コードの行数も短いため、分ける必要性がない。

### 対応

* 呼び出し元の役割に影響を与えないので、メソッドにしないように修正する。

### その他

* とにかく分ければ良いというものではない。
* 分け過ぎて処理の流れが把握しづらくなることもあるため、注意する。

---
## 変数名、メソッド名が不適切

### 問題

* dataは抽象的すぎるため、どんな値を参照するのかがわかりにくい。
* `is_present?`は、すべての属性に値が入っているか確認するメソッドであるが、  
名前からは本来の機能が伝わらない。

### 対応

* dataはもう少し具体的でわかりやすい変数名に修正する。  
* `is_present?`は１箇所からしか呼び出されておらず、行数も短い。  
よって呼び出し元にそのまま書いても問題ないため、削除する。

### その他

* Rubyにおいてbooleanを返すメソッドには「**?**」をつけて表現する慣例があるため、  
booleanを返すメソッド名に「is」等のprefixをつけることはあまりない。  
(例) Array#include?, Object#nil?  
そのため、「is」等のprefixはつけずに慣例通り末尾に「**?**」をつけて表現すべき。

---
## 唐突に未知の単語が登場する

### 問題

* "product_type"という単語が突然出てきた。
* 多く登場する単語ではなく、さらに定義が曖昧なため、読み手からは何を表しているのか把握しづらい。

### 対応

* コード外で**用語集**を作成し、そこでプロジェクトに関する単語の定義を行ってチーム内で共有する。

### その他

* 用語集を作成することで、メンバー間での命名のブレを減らすことができる。
* 用語がある程度決まると命名に悩まなくて済む。

---
## 関数化が読みづらい

### 問題

* 無意味な関数化がされている。
* 条件判定の結果によって文字列を生成したくないのであれば、素直にif文書けば良い。

### 対応

* 三項演算子をif文に修正し、関数オブジェクトを削除する。

