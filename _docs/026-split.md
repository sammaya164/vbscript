---
title: "Split関数、Join関数"
permalink: /split/
last_modified_at: 2021-11-01T00:00:00-02:00
toc: false
---

Split関数は文字列から配列を作成する。

{% highlight vb %}
Dim tmp
Dim fruit

tmp = "みかん,りんご,メロン"
fruit = Split(tmp, ",")

MsgBox fruit(0) 'みかんと表示される
MsgBox fruit(1) 'りんごと表示される
MsgBox fruit(2) 'メロンと表示される
{% endhighlight %}

Split関数の引数と戻り値：

|引数|説明|必須/省略可|
|---|---|---|
|第1引数|文字列|必須|
|第2引数|区切り文字(デフォルトはスペース(" "))|省略可|
|第3引数|配列の要素数の上限(デフォルトは-1(無制限))|省略可|
|第4引数|区切り文字の比較方法(0:バイナリモード,1:テキストモード)|省略可|
|戻り値|配列|-|

バイナリモードはアルファベットの大文字と小文字を区別し、テキストモードは区別しない。

Join関数は配列から文字列を作成する。

{% highlight vb %}
Dim fruit

fruit = Array("みかん", "りんご", "メロン")
MsgBox Join(fruit, ",") 'みかん,りんご,メロンと表示される
{% endhighlight %}

Join関数の引数と戻り値：

|引数|説明|必須/省略可|
|---|---|---|
|第1引数|配列|必須|
|第2引数|区切り文字(デフォルトはスペース(" "))|省略可|
|戻り値|文字列|-|

Split関数で作成した配列の要素は文字列として扱われる。

以下はArray関数とSplit関数で作成した配列について、各要素の総和を求める例。

{% highlight vb %}
Dim a
Dim s

a = Array(1,2,3)    '1,2,3の配列(数値)
s = Split("1,2,3", ",") '1,2,3の配列(文字列)

MsgBox TypeName(a(0)) 'Integerと表示される
MsgBox TypeName(s(0)) 'Stringと表示される

MsgBox a(0) + a(1) + a(2) '6と表示される
MsgBox s(0) + s(1) + s(2) '123と表示される
{% endhighlight %}

配列sの総和(1+2+3=6)を求めたつもりが、文字列の結合(123)になってしまった。
`CInt(s(0)) + CInt(s(1)) + CInt(s(2))`など型変換が必要。
