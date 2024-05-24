---
marp: true
# dark theme
class: invert
---
<!-- headingDivider: 1 -->

#  Rubyでは全てがオブジェクトについて理解する

# Author

3akurur

![height:200](profile.jpg)
github

![height:200](qr_github.png)

# License

CC BY-NC-SA 4.0

[![CC BY-NC-SA 4.0](https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-nc-sa/4.0/)

Copyright (C) 2024 3akurur

# About this contents

GitHub Pages: [https://3akurur.github.io/20240524-ruby_is_all_about_OBJECT/](https://3akurur.github.io/20240524-ruby_is_all_about_OBJECT)

Repository: [https://github.com/3akurur/20240524-ruby_is_all_about_OBJECT - GitHub](https://github.com/3akurur/20240524-ruby_is_all_about_OBJECT)

![height:200](qr_github_pages.png)

# こんな書き方出来るの知ってますか？_1

```rb
1.+(2)
```

# こんな書き方出来るの知ってますか？_2

```rb
1.+(2)
```

想像通りですが、上記のコードは以下のコードと同義です。

```rb
1 + 2
```

なぜ```1.+(2)``` この様な書き方が出来るのかを```Rubyでは全てがオブジェクト``` という内容を深掘りしながら説明していきたいと思います。

# Javascriptとの比較_1

Rubyでは全てがオブジェクトである事について同じオブジェクト指向言語であるJavaScriptと比較してみていきます。

# Javascriptとの比較_2

## Javascript
- JavaScriptにはプリミティブ値と呼ばれるデータ型があります(プリミティブ型)
  - number・string・boolean・null・undefined・symbol
  - プリミティブ型とはプロパティとメソッドを持たない単純なデータです。

```js
// 1はプリミティブ型の数値
let num = 1;
console.log(typeof num); // => "number"

// なのでクラスは存在しない
console.log(num instanceof Number); // => false
```

つまりメソッドを持たないのでRubyのように```1.+(2)```こういう事は出来ないです。

# Javascriptとの比較_3

## ruby

それに対してRubyではJavascriptでのプリミティブ型も**全てがオブジェクト**です。
※ プリミティブ型 number・string・boolean・null・undefined・symbol

```rb
# 1はIntegerクラスのインスタンス
num = 1
puts num.class # => Integer

# なので数値にもメソッドを呼び出せる
puts num.+(2)  # => "3"
```

# Javascriptとの比較_4

という訳で```1 + 2```は内部的にはIntegerクラスの```+```メソッドを呼び出しています。
つまり```1.+(2)```のシンタックスシュガーであると言えます。
```1 + 2```は数値を足し算する為の組み込みの機能のようですが，この様な理屈があるということを理解しておくと、一段階Rubyへの理解度が上がると思います。

# これを理解しておくとこの様なコードが書けます_1

```rb
array = [1, 2]
array.[](1) # => 2

# 以下と同義
array[1] # => 2
```

# これを理解しておくとこの様なコードが書けます_2

今まで説明した内容を学ぶきっかけとなったのが以下のコードです。

```rb
options = { ids: [1, 2, 3, 4 , 5] }
ids = options&.[](:ids) || []
```

optionsがnilになる可能性があった為、以下のようなイメージのコードが書きたいのですが、当然以下のようなコードは書けないのでメソッド呼び出しをしています。

```rb
ids = options&[:ids]
```