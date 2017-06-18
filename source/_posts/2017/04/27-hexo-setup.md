---
title: "GitHub PagesとHexoで作る静的サイトブログ"
date: 2017-04-27 19:39:12
categories:
  - Programming
  - Hexo
tags:
  - Hexo
  - Git
  - GitHub
  - Markdown
  - YAML
---

今回は本ブログを立ち上げるためにGitとHexoについて学びましたので忘れないうちに書いておこうと思います。
GitHub PagesとHexoを用いてブログを作るところまで行こうと考えていますが、長くなりそうであれば別の記事に分けると思います。

## Hexoとは
Hexoとは前回の記事でも触れましたが、**静的サイトジェネレータ**の一つです。
静的サイトジェネレータを用いることで静的ファイル(html、css、javascript)で叩き出してくれる代物で、その中でもHexoはブログに特化していると言われています。
私は**ヘキオ**と呼んでますが**ヘクソ**や**ヘキソ**とも呼ばれているようです。
使うには**node.js**でインストールし、コマンドラインで記事の作成やGitを使ってブログをサーバーにデプロイすることになります。

## Hexoを使ってみる
- 必須環境  
    - Node.js
    - Git

上記を使用しますのでインストールしておいてください。

まずHexoをインストールするので、**コマンドライン**(コマンドプロンプトやgit bashなど)上で

```
$npm install hexo-cli -g
```

と入力し実行してください。  
間違ってなければパッケージがグローバル領域にインストールされますので、Hexoのコマンドが使用できるようになります。
次に下記のコマンドを実行し、ベースとなるサイトを作成して動かします。

```
$hexo init ブログ名
$cd ブログ名
$npm install
$hexo server
```

実行してみるとlocalhost:4000に作成したブログを見ることができます。
ただし現段階ではまだテーマを導入していないので、宇宙を背景にブログ名が表示されているだけだと思います。
このままでは寂しいので新しい記事を追加してみましょう。

```
$hexo new 記事名
```

こちらのコマンドで記事が`ブログ名\source\_post\記事名.md`といった形で生成されます。
しかしファイル名に日本語を用いるのはいろいろとアウトなのでできれば**英語で生成する**のが望ましいです。(本記事は`hexo-setup.md`で作っています)
生成されたファイルを開くと・・・

```markdown:記事名.md
---
title: 記事名
date: YYYY-MM-DD HH:mm:ss
tags:
---
```

となっていますので、`title`を適宜編集してください。
また、本文は下の空欄部分(- - -、以下)に**マークダウン**で記入していくことになります。
書き終わったら保存して`hexo server`で先ほど同様、localhost:4000で確認できます。
書き始める前に実行しておけば、プレビューしながら編集することもできるのでオススメです。

それでは最後に**GitHub Pages**で公開する手順を説明します。

## GitHub Pagesで公開する
Github Pagesで公開するにはまずGitHubに専用のレポジトリを作成。
そのレポジトリにHexoでデプロイするといった流れになります。

さくっと`ユーザー名.github.io`という名前のレポジトリをGitHubに作ります。
この時に**README.mdを追加しない**ほうが、すぐに**https**か**ssh**をコピーできますのでオススメです。(作ってしまった場合は`clone or download`から見ることができます)
作成できたら`ブログ名\_config.yml`を開いて、対象の部分を以下のように修正・追加します。
ソースまるまる載せるわけにもいかないので、**変更部分のみ抜粋**しています。

```yml:_config.yml
# Site
title: ブログ名
language: en
timezone: Asia/Tokyo

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://ユーザー名.git.io
root: /

# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: git@github.com:ユーザー名/ユーザー名.github.io.git
  branch: master
```

`language: en`にしているのはHexoのテーマの大体が日本語に対応していないからです。
デフォルトで中国語に設定されているテーマですとブログが漢字だらけになってしまうので、英語を選択しています。
`repo: `以下は先ほど作ったレポジトリの**https**か**ssh**を入力してください。
Hexo 3.x系からは`type: `で**github**ではなく**git**を選択しているので注意してください。
変更が終わったら上書き保存して、コマンドラインに戻ってください。

次にHexoにサービスにGitをデプロイするためのプラグインをインストールして、実際にGitHub上に作ったサイトを公開します。

```
$npm install hexo-deployer-git --save
$git init
$git remote add origin {https or ssh}
$hexo generate
$hexo deploy
```

うまくいけば、これで`ユーザー名.github.io`上でブログを見ることができるようになっています。
ここで躓きやすいのが**`$git init`していない**、**PCでsshを設定していない**などが挙げられます。(実際にsshを設定していなくてhttpsで公開する羽目に・・・)
またHexoのコマンドは大体は以下のように**省略**でき、ブログの更新する際は一行で済ませることができます。

```
$hexo g -d
```

この一行で`$hexo generate`と`$hexo deploy`をしています。
他にもローカルで建てる時の`hexo server`が`hexo s`に略せたりできたので、気になる方は公式のドキュメントを覗いてみると良いかもしれません。

## 最後に
次の更新は**テーマの変更**についてやりたいと考えています。
また`_config.yml`についても触れられたらいいかと思っていますので、よろしくお願いします。
<font color="White">ブログ名もしっくりこないし、Hexoを弄りきれていないから当分はHexoの話題になりますね。</font>
<font color="White">というか記事書いていたら零時すぎてしまったんじゃが・・・</font>
