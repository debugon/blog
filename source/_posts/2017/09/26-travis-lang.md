---
title: "TravisCIを利用するお話-言語編-"
date: 2017-09-26 00:57:49
categories:
  - Programming
  - TravisCI
tags:
  - TravisCI
  - YAML
---

前回はTravisCIを導入するための話でしたが、今回はそこから掘り下げて`lang`部について取り上げたいと思います。

## TravisCIの`lang`部
TravisCIでは`.yml`ファイルに記述する際、検査に使用する言語を`lang`部に書き記す必要があります。
前回はNode.jsを例に進めましたが、そのほかにも様々な言語をサポートしているので気になった方は一度見るといいかもしれません。
<img src="..\..\..\img\travis_lang_list.png" />

今回お話ししたいのは、一つの検査に複数の言語を使用する場合です。
「RedPenでバリバリ、検査するゾ～」なんて豪語しておきながら、躓いてしまった時のお話になります。

## TravisCIによる複数言語での検査
ご存知の通り当ブログはHexoによって生成したファイルをGitHub.ioにアップロードして、公開しているという形式を採っています。
その生成元ファイルをTravisCIとRedPenでチェックし、OKであれば生成してGitHub.ioにコミットするということをしたかったのです。
しかしながら、Hexoはjavascriptで書かれており、RedPenはというとJAVAアプリケーションなのです。
当然`lang`部に`lang: node_js`と書けば「RedPenはJAVAアプリケーションだぞゴルァ！」を怒られ、`lang: java`と書けば「Node.jsってなんすかー？」とエラーを連発してしまいます。
その時は日本語で記載されたTipsがなかったものですこし悩みましたが、海外のフォーラムで似た環境の方がいたので参考になりました。
解決策としては...

```YAML:.travis.yml
lang: node_js, java
node_js:
  - "node"

jdk:
  - oraclejdk8
```

`lang`部に複数の言語をカンマで区切って記すだけでいいんですね！
すごい簡単でした！
あ！
使うNode.jsとJDKのバージョンの指定もお忘れなく！
<img src="..\..\..\img\travis_lang_working.png" />
...
画像ですと見づらいですが、236行目で`npm install`と511行目で`redpen...`が走っているところを見ると、ちゃんと動いていると思います。

## 最後に
長い前置きの割にあっさり終わったじゃねぇーか！という方、いるかもしれません。
実際に私も結構躓いていた割に答えがあっさりしていて複雑な気持ちになりました。
もしかしたらHexoでブログ作ってみたけどRedPenで検査してみてぇっていう物好きがいるかもしれませんので、困ったときにお力になれば嬉しかったりします。

<!--
><div style="text-align: right;">
引用元：[name](https://)
</div>
<img src="..\..\..\img\" />
<font color="White"></font>
-->
