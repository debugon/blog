---
title: "Hexoで作成したブログにサイトマップを設定する話"
date: 2017-05-24 12:27:11
categories:
  - Programming
  - Hexo
tags:
  - Hexo
  - YAML
---

今回はHexoで作成したブログに**サイトマップ**を実装する方法を紹介します。
とは言えHexoでフィードの設定をする方法を調べた方なら、既にご存知かと思われます。
私もフィードの設定の次いでに設定した人の一人です。が、サイトマップがどういうものなのか分らないで導入したこともあり、これを機に調べてみることにしました。

## サイトマップとはなにか
とりあえずｇｇってWikipediaを開いてみると・・・

>Sitemaps（サイトマップ）標準は、ウェブマスターがサーチエンジンに、サイト内でクロールすべきURLを教えるための方式を規定するものである。サイトマップは、当該サイトにおけるURL全てをリストした、XMLファイルとして提供し、ウェブサイト運営者は各URLに付加的情報として、最終更新日時や更新頻度、他のURLとの相対的な重要度を加えたりできる。Sitemapsに対応したサーチエンジンでは、この情報を使って、サイトのクロールをより効率的に行えるようになる。サイトマップはサーチエンジンへのURL追加規約であり、URL排除規約であるrobots.txtを補完するものである。
><div style="text-align: right;">
引用元：[Sitemaps - Wikipedia](https://ja.wikipedia.org/wiki/Sitemaps)
</div>

などなど書いてあり正直に言うと

<img src="..\..\..\img\idk.png" />
<font color="White">クロールのリンクなんて、水泳ですよこれー！</font>

***なんてことはありませんでした。***
よく読んだらある程度は理解できた。（と思います、たぶん）

1. ファイル形式はXML
2. URLとその他情報が記載される
3. Google等の検索エンジンがこれをもとに、クロールを効率的に行う

### クロールとはなにか
やっぱり気になるのでクロールについても調べてみました。
さっと引用すると

>クロールとは、検索エンジン内のシステムであるクローラ(ロボット)が一つ一つのサイトを巡回し、サイトの情報を収集することを指します
><div style="text-align: right;">
引用元：[クロールとは - Webマーケティング用語｜ferret [フェレット]](https://ferret-plus.com/1061)
</div>

クルーラーというのがインターネット上のサイトを巡回することで、検索結果に基づいた情報が表示されるようにしているということかしら。
サイトマップが設定されることで、検索エンジン側がそのサイトの情報を効率よく収集できるようになるという認識でいいっぽいです。

検索結果に表示されるにはとりあえず**一度はクロールされなければいけない**ということなので、ブログをやってく上では非常に重要な作業ということですね。

## Hexoにサイトマップを設定していく
今回もまたHexoのプラグインでサクッと済ませていくのですが、ここで一つ問題が。
サイトマップ用のプラグインが**公式**の出しているものと、有志が**作成**したものがあるのでどちらか選ばなければいけません。

1. 公式：`hexo-generator-sitemap`
2. 有志：`hexo-generator-seo-friendly-sitemap`

公式のものは置いておいて、有志の`hexo-generator-seo-friendly-sitemap`はなんなのでしょう。

npmを覗いてみます。
>Generate SEO-friendly sitemap.
Inspired by XML Sitemap in Yoast Wordpress SEO Plugin (https://yoast.com).
It will generate separated sitemap files for pages, posts, categories, tags and a XSL stylesheet.
><div style="text-align: right;">
引用元：[hexo-generator-seo-friendly-sitemap](https://www.npmjs.com/package/hexo-generator-seo-friendly-sitemap)
</div>

### SEOとはなにか
分からないことは調べる！
<font color="White">とにかく引用！サクッと行数稼げて楽だ！</font>

>SEOとは、”Search Engine Optimization” の略であり、検索エンジン最適化を意味する言葉です。検索結果でWebサイトがより多く露出されるために行う一連の取り組みのことを指します。
><div style="text-align: right;">
引用元：[SEO（検索エンジン最適化）とは | SEO基礎知識 [SEO HACKS]](https://www.seohacks.net/basic/knowledge/seo/)
</div>

検索エンジンの最適化とあるが、おそらくここでは「クルーラーが効率的に情報収集できるようなサイトマップ構成をするよ！」っていうプラグインかと。
ということでSEOにフレンドリーな`hexo-generator-seo-friendly-sitemap`をつかっていきます。


ではやっていきます。
npmコマンドで`hexo-generator-seo-friendly-sitemap`をインストールしましょう。

```
$npm install hexo-generator-seo-friendly-sitemap --save
```

うまくインストールされたのであれば、次に`_config.yml`を開いてサイトマップを設定します。
一番下あたりに以下のソースを追加して、サイトマップのXMLを指定してあげます。
ちなみにフィードと同じで、一度**deployしないと生成されない**かもしれません。

```YAML:_config.yml
sitemap:
  path: sitemap.xml
```

これで作業は終了。
***ね、簡単でしょ？***
あとはいつも通り、`hexo g -d`でdeployすれば`public`ディレクトリに`sitemap.xml`かそれっぽいのが生成されていると思われます。

## 最後に
結構前にサイトマップを設定したけれど、今だGoogle検索に引っかからないです（切実
実際にブログをHexoで初めてみて常々感じますが、世界（特に中国）で人気なだけあってプラグインが豊富で助かっています。
正直、サイトマップまで設定したので次回は何を書こうか考え中です。
それでは！
<font color="White">ChinaPostでオーダーしたイヤホンが発送されているということなんで、時期的にレビュー記事でもいいかなと思ってたり。</font>

<!--
<img src="..\..\..\img\" />
<font color="White"></font>
-->
