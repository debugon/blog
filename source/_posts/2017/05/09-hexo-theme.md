---
title: "Hexoでブログにテーマを設定する話"
date: 2017-05-09 11:42:11
categories:
  - Programming
  - Hexo
tags:
  - Hexo
  - Git
  - GitHub
  - YAML
---

予告通り、Hexoで作成したブログにテーマを設定したいと思います。
Hexoでブログを作った方ならにお気づきになると思いますが、当ブログもデフォルトのテーマから変更しています。

## Hexoで作成したブログにテーマを設定する流れ
全体的な流れとしては・・・

1. Hexoのテーマを見つける
2. テーマのGitレポジトリを`ブログ名\themes\`に適当にcloneする
3. `_config.yml`の`theme:`以下をclone時の名前に変更する

となります。

### 1. Hexoのテーマを見つける
Hexoのテーマは[公式サイト](https://hexo.io/themes/)かGitHubか何かで「Hexo-theme」と検索すれば探せます。
公式サイトはサムネイルが表示されるのでデフォルトテーマからとりあえず変えたいという場合には最適かと思います。

<img src="..\..\..\img\hexo_theme.png" />

今回は[こちら](https://github.com/hexojs/hexo-theme-light)のLightテーマを使います。

<img src="..\..\..\img\hexo_theme_light.png" />

###  2. テーマをcloneする
欲しいテーマを見つけたら、以下のコマンドでローカルの`ブログ名\themes\`にcloneします。

```
$git clone https://github.com/hexojs/hexo-theme-light.git themes\light
```

うまくいけば`ブログ名\themes\`に`light`というディレクトリが生成されているはずです。

### 3. `_config.yml`に設定する
最後に`_config.yml`にテーマを設定して終わりです。
以下のように`_congig.yml`を開いて、該当箇所を変更します。

```YAML:_config.yml
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: light
```

deployする前に`hexo server`で確認して、良ければ`hexo generate -d`でブログを更新してください。

### EX. テーマのデザインが崩れてしまう時
テーマをいろいろ試している際に躓いた部分があります。
テーマにjadeとsassが使われている場合、サイトのデザインが崩れてしまうようです。
専用のプラグインが用意されているので、以下のコマンドでインストールします。

```
$npm install hexo-renderer-jade --save
$npm install hexo-renderer-sass --save
```

こうしたプラグインは各テーマの導入方法の部分に記載されていると思いますので、入れたいテーマに合わせてインストールしてください。

## 最後に
Hexoの導入までされた方ならテーマの変更は容易かと思います。
前回の記事でも触れましたがHexoは利用者が多い分、テーマの種類も豊富なのが売りの一つではないでしょうか。
次回はフィードの設定について取り扱いたいと考えています。
<font color="White">前回まではBracketsでmdの編集してたけど、Atomに移行してみました。</font>
<font color="White">ってプラグインでコマンドライン開けたり、スペルチェックできたり、カラーコード出せたり、最高じゃないですかー</font>
