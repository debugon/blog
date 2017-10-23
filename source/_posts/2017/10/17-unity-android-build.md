---
title: Windows Subsystem for Linuxを入れてみる
date: 2017-10-17 09:16:04
categories:
  - Linux
tags:
  - WSL
  - Linux
---

ついにWindows 10 Fall Creators Updateが正式リリースされ、Windows Subsystem for Linuxが提供されました。
InsiderPreview版では既にベータ版を利用できたのですが、リリースの時期も近かったということもあって見送ることにしていました。
今回はそのWindows Subsystem for Linux（以下、WSL）を実際にインストールしてみようと思います。

## まずは、Windows10のアップデートを
早速WSLを入れたいところですが、まずはWindows10のアップデートをしなければいけません。
使っているPCのバージョン（ビルド）を確認しましょう。

`Windowsの設定＞更新とセキュリティ＞Windows Update＞OSビルド情報`と進むことで現在使用しているPCのバージョンを確認することができます。

<img src="..\..\..\img\windows_build.png" />

この`OSビルド`とい番号が`16299`以上になっていることを確認してください。
もしそうでなければ古いバージョンが入っていますので、Winodws Updateに戻って更新しましょう。


## WSLの有効化
現在WSLはコマンドプロンプトとストア版から利用することができます。
しかし、それらを利用する前に`Windowsの機能の有効化`からWSLの機能を有効化し追加してあげる必要があります。

`Windowsの設定＞アプリ＞アプリと機能＞プログラムと機能`から従来のプログラムの追加と削除の画面を開くことができます。

<img src="..\..\..\img\program_list.png" />

ここからさらに`Windowsの機能の有効化または無効化`を開いて、WSLを有効化します。

<img src="..\..\..\img\windows_apps.png" />

OKをクリックすると、必要なツールのインストールが始まりますので気長に待ちましょう。
私はそのままWSLを起動しましたが、終わったら念のために再起動を掛けたほうがいいかもしれません。

## ストア版Ubuntuの入手
当初bashコマンドでのインストールを知らなかったため、ストア経由でWSLをインストールしました。
Windowsストアを開き`Ubuntu`で検索するとカノニカル社が提供しているUbutuアプリがあると思いますので、こちらをインストールすることでUbuntu版のWSLを使用することができるようになります。
もしインストールできないようであれば、Windowsのバージョンが古いと思いますのでアップデートを確認してみてください。

<img src="..\..\..\img\wsl_ubuntu.png" />


## Windows Subsystem for Linuxの起動
早速、インストールされたアプリを起動してみましょう。
設定が済んでいれば、Ubuntuのインストールを促されるはずです。
もしエラーメッセージが出ているようであれば、WSLの有効化が済んでいないと思われますのでもう一度見直してみてください。

Ubuntuのインストールの際に

* ユーザ名
* パスワード

を要求されますが、これは使用中のWindowsのパスワードではなく新たにUbuntuに設定するものなので同一にする必要はありません。

<img src="..\..\..\img\wsl_install.png" />

インストールが完了すればWSLの導入は終了となります。


## 少し弄ってみた
`sudo apt update`でアップデートをやってみます。
結構アップデート対象が多くてびっくりしました。

<img src="..\..\..\img\apt_update.png" />

終わると`apt list --upgradable`を実行しろと言われたんで、実行して更新されたものを確認してみました。

<img src="..\..\..\img\apt_list.png" />

リストを見てみると最初からgccやgitなどが突っ込まれていましたが、気づかないで普通にアップデートしちゃいました・・・


## 最後に
WSLはLinuxやUNIXのようにターミナルをよく使ってる方なら非常に魅力的なのではないでしょうか。
私はどちらかというとUbuntu自体に興味があったところからインストールしてみようとなった口なので何とも言えませんが、いまだ勉強不足なところがありますので当分はGit Bashかなと思っています。
<font color="White">ついにUbuntuがWindowsに入ったぜえええええええええええええええええ！！！！</font>
<font color="White">といっても、UbuntuのロゴがだいしゅきマンなのでいつかサブPCにUbuntuを突っ込んで弄りまくりたいですねー（ぶぃ</font>


<!--
><div style="text-align: right;">
引用元：[name](https://)
</div>
<img src="..\..\..\img\" />
<font color="White"></font>
-->
