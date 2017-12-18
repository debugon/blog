---
title: Unityで話題のTangoを動かしてみる
date: 2017-10-31 03:41:37
categories:
  - Programming
  - Android
tags:
  - Android
  - Unity
  - Tango
---
<img src="..\..\..\img\tango-home.png" />

つい最近CEATECのお話を聞く機会があり、ARやMR（MixedReality）に力を入れている企業が多いという話をされていました。
特にGoogleとMicrosoftが結構プッシュしているようで、GoogleはTangoというAR技術を開発し、MicrosoftはOSレベルでMRの開発キットを機能として盛り込むなどといった動きを見せています。

私もGoogleTango対応の端末をお借りする機会があったので、試しにUnityでサンプルを動かしてみたいと思います。

## Tangoについて
Googleの公開しているTangoは3つのカメラと赤外線を用いることで非常に高精度な空間認識を持ち味としているようで、既存の技術とは大きく違って空間の深度というものを採れるようです。
赤外線でレイキャストをしているみたいなんですが、詳しくはGoogleが公開しているTangoのPVをご覧になってください。


### 対応機種について
<img src="..\..\..\img\tango-device.png" />

現在GoogleTangoに対応している端末は２種のみですが、CEATECを終えた今はTangoの知名度も上がったと思いますので今後に期待しましょう。

1. Lenovo Phab 2 Pro
2. ASUS ZenFone AR

どちらも大型のスマートフォン、もといファブレットに近いサイズですね・・・
カメラを３つも積んでいるので仕方がないですが、持ち運びや日常利用には結構大きいのではないでしょうか。


## Tangoの導入
ここからはTangoをUnity環境に導入する手順について説明したいと思います。
UnityとAndroidビルドの設定は終わっているとして話を進めます。
（近いうちにAndroidのビルド環境の記事を書こうと考えていますので、合わせて読んでいただけると幸いです。）

手順としては以下の通りになります。
1. Tangoの入手
2. Tangoのインポート
3. Tangoのビルド設定

### 1. Tangoの入手
まず初めにTangoのパッケージを入手しなければいけません。
公式サイト右上の`デベロッパー`から各言語のSDKを選択できます。
今回はUnityで作りますのでUnitySDKの詳細から取得しましょう。

<img src="..\..\..\img\tango-unity.jpg" />

詳細から進んでもUnity専用のページではなく似たような画面が出ますので、`使ってみる`をクリックしてドキュメントに移動します。

<img src="..\..\..\img\tango-howto.png" />

進むと上記のようなページに移動しますが、ここではTangoを動かす際のUnityの設定と必須環境が記載されています。
* API Levelが17以上のAndroid SDK
* Unity5.2.1以降のUnity
* Unity向けのTango SDK
* Google USB Driver

`API Lebel...`と`Tango Unity SDK`を除けば、大体はUnityでAndroidアプリをビルドするときに環境が整っていると思います。
ページの`Tango Unity SDK`からダウンロードページに行くことで、ようやくTangoSDKをダウンロードすることができます。

<img src="..\..\..\img\tango-sdk.jpg" />

`Tango SDK for Unity`をクリックして最新のSDKを落としましょう。
`.unitypackage`形式でダウンロードされるので、Unityを開いていると自動的に開いているプロジェクトにインポートされます。
「このプロジェクトはダメ！」という場合はあらかじめUnityを閉じでおくか、キャンセルしてください。

### 2. Tangoのインポート
TangoSDKを落としましたら、Unityで3Dプロジェクトを新規作成してください。
今回はUnity2017.2で作ってみます。（Unityの導入記事もそれで書いていましたので）
プロジェクト名は`hoge`で作成しました。
開発画面に来ましたら、さっそく先ほどダウンロードしたパッケージをインポートします。
`Assets > Import Package > Custom Package...`から`.unitypackage`形式のパッケージをインポートできます。

<img src="..\..\..\img\unity-import.jpg" />

パッケージを開くとインポートされるリストが表示されますので、問題がないようでしたら`Import`をクリックしてインポートしてしまいましょう。
インポートが終わると画面下部のAssets以下にいろいろ追加されますので、一度確認しましょう。

<img src="..\..\..\img\unity-tango-files.png" />
このようになっているはずです。

### 3. Tangoのビルド設定
Tangoのアプリケーションは要件としてAndroid4.2以降でなければいけないので、Androidのビルド設定を変更する必要があります。
`File>Build Settings...`からビルド対象の設定をします。
まずはPlatformの箇所で`Android`をダブルクリックか選択してください。（ダブルクリックするとその時点でビルド対象がAndroidに変更されます。）
次に`Player Settings...`をクリックし、ビルドの設定を変更します。
`Other Settings`を選択し、`Minimum API Level`の箇所を`Android 4.2 'Jelly Bean' (APK level 17)`を選びましょう。

<img src="..\..\..\img\unity-android-setting.jpg"/>

またここで`Multithread Rendering`のチェックを外しておきます。
ここにチェックが入っていると、アプリケーションでカメラの映像を正しく表示できなくなるからです。
ついでに`Package Name`の設定も済ませていきましょう。

<img src="..\..\..\img\unity-tango-setting.jpg"/>

最後にプラットフォームの変更をしていない場合は`Switch Platform`をクリックして、ビルド対象をAndroidに変更します。
以上で設定は終了ですが、Build Settingsの画面はそのまま開いておいてください。

## Tangoのサンプルを動かす
実際にTangoのサンプルを動かしてみます。
`Assets > TangoSDK > Examples > Scenes`を開き、サンプルのシーンファイルを`Build Settings > Scenes In Build`に突っ込みます。
そのあと`DetectTangoCore`というシーンを一番上に持っていき、初めにビルドされるようにします。
この`DetectTangoCore`シーンが他のシーンとの切り替えを行っています。

<img src="..\..\..\img\tango-sample-build.jpg" />

この状態で`Build & Run`しましょう。
動くはずです。

## 最後に
<font size="5" color="Red">Unity2017.2では動きませんでした！！！</font>
どうやらUnityのバージョンが新しすぎるのもよくないようです・・・
Unity5.5.5でビルドしましたら動きました。
このあたりの情報があまり見受けられないので、親切とは言い難いかもしれません。

<img src="..\..\..\img\tango-menu.png" />
<img src="..\..\..\img\tango-tracking.png" />

<!--
><div style="text-align: right;">
引用元：[name](https://)
</div>
<img src="..\..\..\img\" />
<font color="White"></font>
-->
