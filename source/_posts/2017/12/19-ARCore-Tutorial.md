---
title: "Google版ARKit、ARCoreに手を出してみる"
date: 2017-12-19 01:13:02
categories:
  - Programming
  - Android
  - Unity
tags:
  - Android
  - Unity
  - ARCore
---

久しぶりの更新になります！
少し時間を空けるつもりが、思った以上の時間になってしまうなんてことなってしまいました・・・

つい先日、Googleより<a href="https://twitter.com/projecttango/status/941730801791549440" target="_blank">Tangoサービスの終了</a>が発表されました。

<blockquote class="twitter-tweet" data-lang="ja"><p lang="en" dir="ltr">We’re turning down support for Tango on March 1, 2018. Thank you to our incredible community of developers who made such progress with Tango over the last three years. We look forward to continuing the journey with you on ARCore. <a href="https://t.co/aYiSUkgyie">https://t.co/aYiSUkgyie</a></p>&mdash; Tango (@projecttango) <a href="https://twitter.com/projecttango/status/941730801791549440?ref_src=twsrc%5Etfw">2017年12月15日</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

正確には前々から終了の告知はなされていたのですが、今回の発表では2018年3月と具体的な日程を提示してきました。
今後の開発は`ARCore`に一本化していくとのことです。

今回はTangoの終了のお知らせに合わせて発表された、ARCoreのDevelopersPreview2を実機に入れてみたいと思います。（本当はTangoの終了がPreview2の発表に合わせて行われたのですが・・・）

## ARCoreとは
<img src="..\..\..\img\arcore-logo.jpg" />
ARCoreはApple社のARkitの対抗馬としてGoogleが発表したものであり、スマートフォンの背面カメラ`1つ`のみを使用してAR体験を提供するSDKです。
Tangoと違い`3つのカメラ`や`特殊なセンサー`といったハードウェアが不要で、現行のどのスマートフォンでも利用可能というメリットがあります。
その半面Tangoよりも空間の認識能力が低く、赤外線による空間深度を取得できないといったデメリットもありますが、ついにTango自体がサポートを終了してしまうこととなります。

### 対応端末
<img src="..\..\..\img\arcore-device.png" />

ARCoreは現在開発者向けのSDKがリリースされていますが、対応機種はGoogleが販売をしているGoogle Pixelシリーズと、Samsungが販売しているGalaxy S8のみとなっています。
日本国内でPixelシリーズは一般販売されていないのでGalaxy S8を使うか、Pixelを個人輸入するほかありません。

### 言語
<img src="..\..\..\img\arcore-lang.png" />

ARCoreはJava, Unity, UnrealEnginで使用でき、Tangoの導入と同じようなガイドが設けられています。
今回のアプリも`Unity`で作っていきます。

## ARCoreを試してみる
長々とARCoreについて書いたので、そろそろARCoreを動かしてみたいと思います。
ちなみにAndroidの設定もろもろは本筋から外れるので省略します。

### 開発環境
* Google Pixel Android8.1
* Unity 2017.3
* ARCore Developers Preview 2

### SDKの入手
まずはARCoreの<a href="https://developers.google.com/ar/" target="_blank">公式サイト</a>よりUnity向けのARCoreSDKを手に入れましょう。
Unityの下にある`GET STARTED`からガイドページに行くことができます。
この記事の執筆時にはUnity 2017.3以上のバージョンが推奨されていました。

<img src="..\..\..\img\arcore-sdk.png" />

`SDK for Unity`をクリックし`.unitypackage`形式でダウンロードします。
次にこのSDKをUnityで作成したプロジェクトにインポートしましょう。

### プロジェクトの作成
まずは適当にUnity3Dでプロジェクトを作成します。
今回はARCoreDevelopersPreview2という名前にしました。
作成後、先ほどダウンロードしたパッケージを`Assets > Import Package > Custom Package`からインポートしましょう。
選択後、何をインポートするか聞かれますが、問題はないと思いますので`Import`をクリックします。

<img src="..\..\..\img\arcore-import.png" />
(キャプチャし忘れちゃって、追加された後になってたりします・・・)

これでUnityのプロジェクトにARCoreのSDKを入れることができました。

### プロジェクトのビルド設定
忘れないうちにビルド設定を済ませてしまいましょう。
`File>Build Settings...`からビルド設定画面を開きます。
まずはプラットフォームをAndroidに変更します。
Androidを選択し`Switch Platform`をクリックし、ビルド対象をAndroidに設定します。

<img src="..\..\..\img\arcore-platform.png" />

次に`Player Settings...`をクリックし、設定画面を開きます。
ARCoreを動作させるために以下のような設定をします。
`Other Settings`タブから
  * `Multithreaded Rendering`のチェックを外す
  * Minimum API LevelはAndroid 7.0以上を選択
  * ~~Target API LevelはAndroid 7.0 か 7.1を選択~~
  * <font color="Red">Target API Levelは実機のバージョンのSDKをインストールし`Automatic`に設定</font>

`XR Settings`タブから
  * `ARCore Supported`にチェック

このときAndroid 7.0以上を選択できない場合は、Android SDKからAPI Level 24以上をダウンロードしていないと思いますので一度確認してみてください。

最後にARCoreのサンプルシーンを読み込むように設定します。
`Assets > GoogleARCore > Examples > HelloAR > Scenes`を開き、`HelloAR.unity`を`Scenes In Build`にドラッグアンドドロップします。

<img src="..\..\..\img\arcore-examples.png" />

これにてUnity側のプロジェクトの作成・設定は終了となります。
実機にインストール・・・と行きたいところですが、端末側にも準備が必要なのでまだ行いません。


## ARCoreシステムアプリをインストールする
ARCoreを動かす端末側にもARCoreのアプリケーションを導入する必要があります。
ARCoreシステムアプリは実機のブラウザからダウンロードしインストールするか、adbコマンドを用いて実機にインストールするかして導入しましょう。

<img src="..\..\..\img\arcore-apk.png" />

今回は前者の方法ででさくっとインストールしました。
特に権限の要求とかはなかったと思います。

これでようやく動作させる環境が整いました。
最後にUnityに戻り、ビルドしましょう！


## いざビルド
`Build Settings`から`Build And Run`をクリックし、任意の名前の`.apk`で保存します。
うまくいけばビルドが通るはずです。

<img src="..\..\..\img\arcore-error.png" />
(しまった、PixelってAndrodi 8.1だった・・・)
急いでダウンロードします・・・

<img src="..\..\..\img\android-update.png" />

Target API Levelに7.1以上が表示されないので`Automatic`に変更してビルドします。

<img src="..\..\..\img\arcore-success.png" />

無事にインストールできたようです。

## ARCoreを動かす
インストールが終わると勝手に起動すると思いますが、起動しなかった場合はインストールアプリの一覧から起動してみてください。
私は起動時にカメラの権限だけ求められましたので、許可しています。

<img src="..\..\..\img\arcore-test.png" />
(適当に手元で動かしたものをスクショしてみました)

起動すると青い点が点々と現れ平面のスキャンが始まり、平面だと認識すると画面のような線が表示されます。
ドロイド君はタップすることでその位置に表示することができました。


## 最後に
お疲れさまでした！
ARKitに対抗してARCoreを出したと一時期は騒がれていましたが、Tangoでできていたことが従来のスマートフォンでもできるようになるというのはすごいと感じます。
ARKitはiPhoneの開発環境を持ち合わせていないので試すのは難しいのですが、噂だとARKitよりも平面の検出スピードは速いと聞きます。
ARCoreはそろそろ正式リリースされるとのことなので、とても期待が高まりますね！


<!--
<a href="url-hogehoge" target="_blank">URL名</a>
<div style="text-align: right;">
引用元：[name](https://)
</div>
<img src="..\..\..\img\" />
<font color="White"></font>
-->
