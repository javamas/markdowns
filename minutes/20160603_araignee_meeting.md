# じゃばます！議事録

* 2016/06/03
* 参加者:disc99、nayuta、charmikity、ta-chibana、HonMarkHunt

## MQへの送信受信するクラスを共通化するか？

* 共通化する

### 前提

* Channnelオブジェクトを返すクラスを作る
* コネクションの取得などを毎回書くのは面倒だから
* https://www.rabbitmq.com/tutorials/tutorial-one-java.html

### どこまで共通化するか

* 接続
* メーセジのフォーマットに沿って変換する
* 送受信

### どのように共通化するか

* Contrller, Transfer, Loaderのクラス内で高塩作成のMQTemplete(仮)を使用する

## データソース

* host, DB, username, password
* などの接続情報
* 全て環境変数に切り出す -> [heroku12factor](http://12factor.net/ja/config)
* issue

## 実行結果の通知について考える

### 前回まで決まってたこと

* ログレベルの出力ではなくイベントでログを出す

### わからないこと

1. どういうイベントの時にログを出していいかわからない
1. イベントで通知をしようとするとアプリが止まったことを感知できない

### 決まったこと

1. イベントを出す時

		* アプリ起動時
		* アプリ終了時
		* Contrller, Transfer, Loaderのサービス的なメソッドの呼び出し/終了
		* DB保存時
		* main()にcatchされた時

1. 終了のログが来なければ異常終了を感知できる
