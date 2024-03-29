---
title: "Filter関数"
permalink: /filter/
last_modified_at: 2021-11-01T00:00:00-02:00
toc: false
---

Filter関数を使って、検索文字列を含む要素からなる配列を取得できる。

{% highlight vb %}
Dim fruit
fruit = Array("みかん", "りんご", "メロン")

Dim tmp
tmp = Filter(fruit, "ん") '「ん」を含む要素を抽出

MsgBox Join(tmp, ",") 'みかん,りんごと表示される
{% endhighlight %}

Filter関数の引数と戻り値：

|引数|説明|必須/省略可|
|---|---|---|
|第1引数|配列|必須|
|第2引数|検索文字列|必須|
|第3引数|検索文字列が(True:含まれる,False:含まれない)要素を探す|省略可|
|第4引数|検索文字列の比較方法(0:バイナリモード,1:テキストモード)|省略可|
|戻り値|配列|-|

バイナリモードはアルファベットの大文字と小文字を区別し、テキストモードは区別しない。
