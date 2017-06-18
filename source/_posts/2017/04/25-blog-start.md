---
title: "GitHub + Hexo でブログを立ててみたお話"
date: 2017-04-25 03:41:14
categories:
  - Blog
tags:
  - Blog
  - Hexo
---

# Github PagesとHexoを使ってブログを立ててみた
初めまして、でぶごんです。  
マークダウンによる記述はちょっと慣れていないので、今回は挨拶程度で勘弁してください。

ブログを立てることになったのですが、**はてなブログ**や**Qiita**、**WordPress**等、色々あると思ます。  
正直立てた今でもはてなブログで妥協しておけばよかったのではと思っていますが、Hexoで作ったページをGitHub Pages（以下GitHub）で公開するという形にしました。  

GitHubにデータ管理出来たらSlackで通知やらなんやらできるんじゃね？という考えで調べてみたところ、
**静的サイトジェネレータ**なるものでGitHubに公開できるということが分かったのがきっかけでした。  
この静的サイトジェネレータを用いることで静的ファイル（html, js, css）として叩き出すことができ、GitHubで公開できるということです。  
将来的にはSlcakで記事の更新（デプロイ）を通知として受けれたり、文章チェッカーなんかもあるようなので使えたらいいなと考えてます。  
詳しい話は後日、ちゃんとした記事でまとめたいと考えています。  
（一応テストも兼ねているからそんなに多い量のテキストは書きたくないのじゃ）  

最後だけそれっぽいことを書くと
```
hexo init {blogName}
cd {blogName}/public
git init
git add --all
git commit -m "first commit"
git remote add origin {ssh}
git push origin master
```
上記は生成された{blogName}ディレクトリ内のpublicをcommitしてmasterにpushしてるので、完全に```hexo deploy```が死んでますねー・・・

おわり
