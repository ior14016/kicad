# はじめに

この文章は[KiCAD 公式ドキュメント Ver8.0](https://docs.kicad.org/8.0/en/getting_started_in_kicad/getting_started_in_kicad.html)を翻訳し，実習用に編集したものです．<br>
一部簡略されている部分があるため，深く知識を得たい場合は，[公式ドキュメント](https://docs.KiCAD.org/)に目を通すことをおすすめします．<br>

公式ドキュメントは日本語も存在しますが，<font color="red">**翻訳が不完全**</font>です．<br>
本文書は KiCAD(Ver8.0)で使用されている UI を元に`日本語`で説明を行いますが，今後文章が変化することが予想されます．<br>
Google 翻訳や DeepL 翻訳などを使用して読み進めることをおすすめしますが，画像内の言語は翻訳できないため，普段から<font color="red">**英語**</font>で使用することを強く推奨します．<br>

本文書は，<font color="green">Windows11</font>での操作方法を説明します．<br>
それ以外の OS などについては異なる外見や動作を行うことが予想されますが，読み替えるなどして自己対応をお願いいたします．<br>

また，本文書は**教育目的のみ**に使用することを前提としています．<br>
著作権や営利目的などの権利等については，[KiCAD 公式ドキュメント](https://www.KiCAD.org/about/licenses/)に記載されていることに従ってください．<br>

基本的に，文字を入力する際は<font color="red">**半角英数字のみ**</font>を使用します．<br>
全角文字や絵文字などを使用すると文字化けなどが発生し，最悪の場合は製作したデータが破損・読み込めないことが予想されます．<br>
必ず，`半角英数字`を使用してください．<br>
**それ以外は動作を保証できません!**<br>

KiCAD は開発段階のソフトウェアですので，突発的な動作停止(フリーズ)もありえます．<br>
フリーズを抑える方法はおまけに記載しますが，せっかくの作業データを失わないよう，こまめにデータを保存することをおすすめします．<br>

> `Ctrl`+`S`で保存．<br>

# 目次

- [はじめに](#はじめに)
- [目次](#目次)
- [本日行うこと](#本日行うこと)
- [KiCAD に使いたい部品が存在しない!?](#kicad-に使いたい部品が存在しない)
- [ライブラリについて](#ライブラリについて)
- [シンボルを自作する](#シンボルを自作する)
  - [シンボルピン](#シンボルピン)
  - [シンボルを描く](#シンボルを描く)
  - [シンボルのプロパティ](#シンボルのプロパティ)
- [フットプリントを自作する](#フットプリントを自作する)
  - [フットプリントのパッド](#フットプリントのパッド)
  - [フットプリントのアウトライン](#フットプリントのアウトライン)
- [シンボルとフットプリントの同期](#シンボルとフットプリントの同期)
- [digikey を使って効率化](#digikey-を使って効率化)
  - [シンボルのインポート](#シンボルのインポート)
  - [フットプリントのインポート](#フットプリントのインポート)
  - [シンボルとフットプリントの同期](#シンボルとフットプリントの同期-1)
  - [3D モデルの同期](#3d-モデルの同期)
- [乾電池型モバイルバッテリーの製作](#乾電池型モバイルバッテリーの製作)
- [おわりに](#おわりに)
- [協力・謝辞](#協力謝辞)

# 本日行うこと

1. カスタムシンボルの作り方
2. カスタムフットプリントの作り方
3. `digikey`を使った，時短レシピ
4. 乾電池型モバイルバッテリーの製作

# KiCAD に使いたい部品が存在しない!?

KiCAD には様々なシンボルやフットプリントのライブラリが存在しますが，すべての部品が存在するわけではありません．<br>
残念ながら，既定のライブラリに存在しないものは`諦める`か`自作`するしかありません．<br>

諦めるのは簡単ですが，折角の機会です．一緒に自作してみましょう．<br>

`プロジェクトマネージャー`を開いて，乾電池型モバイルバッテリー用のプロジェクトを，新規に作成してください．<br>

> 私は，`document`フォルダに移動して，新規プロジェクト名を`5V-charger`とします．<br>
> 先日作った`KiCAD-project`フォルダと同じ階層になると思います．<br>
> 自分で名前を付ける場合は，以下を読み替えてください．

# ライブラリについて

KiCAD では`シンボル`と`フットプリント`をそれぞれ別のライブラリに保管しています．<br>
つまり，シンボルは`シンボルライブラリ`に，フットプリントは`フットプリントライブラリ`にまとめて保管されています．<br>
まずはシンボルを製作し，その後にフットプリントを製作するのが基本の流れです．<br>

# シンボルを自作する

プロジェクトマネージャーからシンボルエディタを選ぶと，`シンボルエディタ`ウィンドウが開きます．<br>
シンボルを自作する際はこの`シンボルエディタ`を活用しましょう<br>

左の一覧には KiCAD が既定で持っているライブラリの一覧を表示しています．<br>
本日，乾電池型モバイルバッテリーに使うスライドスイッチの型番は[`OS102011MS2QN1`](https://www.digikey.jp/ja/products/detail/c-k/OS102011MS2QN1/411602)です．<br>
フィルター機能を使用して探してみますが存在しません．<br>
というわけで，このスイッチのシンボルを自作してみます．<br>

`ファイル` -> `新規ライブラリ` -> `プロジェクト` -> `OK` を選択<br>
`5V-charger`フォルダ直下に`5V-charger_Library.kicad_sym`と名前を付けて，保存します．

> `プロジェクト`ではなく，`グローバル`を選ぶと，このプロジェクト以外でも自作したシンボルを使い回すことができます．<br>
> デメリットとして，仲間(別の PC)に回路図を共有する際に，自作したシンボルが共有されません．

左のアイテム欄に`5V-charger_Library`が追加されました．<br>
このアイテムを選択した状態で，`新しいシンボルを作成`を選択します．

> ショートカットキーは`Ctrl`+`N`

`新しいシンボル`ウィンドウが開きますので，以下の表のように記入しましょう．
|記入欄|記入内容|説明|
|-|-|-|
|シンボル名|OS102011MS2QN1|型番名を記入|
|デフォルトのリファレンス端子|SW|スイッチなので SW を記入|

## シンボルピン

次に，ピンの設定をしていきます．<br>
`ピンの追加`を選択しましょう．<br>

> ショートカットキーは`P`

`ピンのプロパティ`ウィンドウが開きますので，以下の表のように記入しましょう．<br>
|記入欄|記入内容|説明|
|-|-|-|
|ピン名|A|ピンの名前を入力|
|ピン番号|1|ピン番号を入力|
|エレクトリカルタイプ|パッシブ|ここで設定を間違えると ERC エラーが発生します|
|向き|右|接続方向を選択|

> 右側にプレビューが表示されます．色々試してみよう．

`OK`を選択すると設定したピンがマウスカーソルに追従するので，適当なところでクリックして配置します．

> UI が日本語なので`パッシブ`と表示されています．~~カッコ悪い~~

スイッチには接続端子が 3 本あるので，同様にして，2 番ピンと 3 番ピンを作成しましょう．<br>
||2 番ピン|3 番ピン|
|-|-|-|
|ピン名|B|C|
|ピン番号|2|3|
|エレクトリカルタイプ|パッシブ|パッシブ|
|向き|右|右|

以下の図のように，配置してください．

## シンボルを描く

ピンを配置した状態で，`円を描画`と`つながった図形ラインを追加`などを使って，シンボルを図のようにスイッチと一目でわかるように描きましょう．<br>
ここではより細かい描画を行うために，グリッドを切り替えると便利です．<br>
キャンバスを右クリックし、`グリッド` -> `10.00 mils`を選択すると，グリッドが小さくなり，細かい描画が行えます．

> 注意!<br>
> 図形を描き終えたら，`50.00 mils`のグリッドに戻すのを忘れずに!<br>
> シンボルピンは動かす際は，必ず`50.00 mils`のグリッドで行うこと!<br>
> 後にピンが接続できないトラブルが発生します!

## シンボルのプロパティ

検索しやすいようにシンボルにプロパティを設定します．<br>
`ファイル` -> `シンボルのプロパティ`を選択して，ライブラリシンボルのプロパティウィンドウを開きます．<br>
`キーワード`欄に`SPDT`や`switch`,`toggle`等といった，部品の特徴などを記入します．<br>
こうすることで，フィルターで検索した際に候補として引っかかりやすくなります．<br>
`OK`を選択して，保存しましょう．<br>
これで，シンボルは完成です．

# フットプリントを自作する

`プロジェクトマネージャー`から`フットプリントエディター`を開きます．<br>
`ファイル` -> `新規ライブラリ` -> `プロジェクト` -> `OK` を選択<br>
`5V-charger`フォルダ直下に`5V-charger_Library.pretty`と名前を付けて，保存します．<br>
左のアイテム欄に`5V-charger_Library`が追加されました．<br>
このアイテムを選択した状態で，`新規に空のフットプリントを作成します`を選択します．<br>
フットプリント名を`OS102011MS2QN1`，フットプリントタイプを`スルーホール`とします．

> 表面実装部品の場合は`SMD`を選択しましょう．

## フットプリントのパッド

今回使うスイッチ(OS102011MS2QN1)には足が 3 本(正確には 5 本)あり，データーシートを見るとそれぞれの間隔は`2.00mm`となっています．~~インチじゃないんかい!~~<br>
配置を容易にするために，パッドの間隔に合わせてグリットを調節します．<br>
`設定` -> `設定` -> `フットプリントエディター` -> `グリッド`から`2mm`...は無いので，下部の`+`ボタンを選択し，新しいグリッドの X サイズを`2.00000`とします．<br>
フットプリントエディターに戻って，上部ツールボックスでグリッドの間隔が`2.0000mm`になっていれば OK です．<br>

基本的には，スルーホールのフットプリントは`1番ピンが座標(0,0)に配置`され，`1番ピンが最も左上`に来るように配置しますが，今回は無視して 2 番ピンが座標(0,0)に来るようにしちゃいましょう．<br>

> つまり，パッドの座標は以下の表のようになるはずです．<br>
> ||X 座標|Y 座標|
> |-|-|-|
> |1 番ピン|-2.0|0.0|
> |2 番ピン|0.0|0.0|
> |3 番ピン|2.0|0.0|

右ツールバーから`パッドを追加`を選択し，左から右に 3 つ配置しましょう．<br>

> 注意!<br>
> データーシートと同じように，左から`1,2,3`と並べてください!<br>
> パッドに記載している番号と，さきほど自作したシンボルのピン番号が同期されます．<br>
> ショートや誤配線の元となるので，データシートをしっかり読むことを強く推奨します!<br>

データシートを読むと，パッドの直経が`0.80mm`と指定されています．<br>
1 番のパッドをダブルクリックして，プロパティを確認して，問題がないか確かめます．<br>
デフォルトでは`0.762`と記載されています．<br>
誤差程度ですが，ほんの少し足りないので，修正します．<br>
同様にして，2 番ピンと 3 番ピンも修正しましょう．<br>

> パッドの大きさもこのプロパティで変更することができます．<br>
> しかし，あまりにも大きすぎると隣のピンと一体化したりなどと，色々と不都合が起こってしまうので，程々にしておきましょう．<br>
> データーシートによっては最適なパッドの大きさを記載しているものもあります．

## フットプリントのアウトライン

`F.Fab`レイヤーを選択した後，`短形を描画`を選び，パッドを囲むようにアウトラインを書きます．<br>
このアウトラインをデータシートに記載されているスイッチの寸法と正確に合わせることで，3D 表示した際の干渉をチェックすることができます．<br>
今回使用するスイッチの幅は`8.60mm`，奥行きは`4.30mm`です．<br>
描画した短形をダブルクリックして，プロパティから矩形の大きさと座標を指定することができます．<br>

> 難しい場合はグリッドを`0.10mm`に設定した後に，アウトラインを引くとうまくいくかも?

`表示` -> `3Dビューアー`を選択してみると，なんだかいい感じです．

> 本当ならば，`F.Fab`レイヤーに正確なパーツのアウトラインを描き．<br> `F.Silkscreen`レイヤーに少し大きめのアウトラインを描き．<br>
> 他のフットプリントと重ならないように`F.Courtyard`レイヤーに，フットプリント全体を囲むアウトラインを記載します．<br>
> が，面倒なので今回はやりません．

これでフットプリントは完成です．忘れず保存しましょう．

# シンボルとフットプリントの同期

完成した自作のシンボルとフットプリントを紐づけます．
`プロジェクトマネージャー`から`シンボルエディター`を開き，自作したシンボルを選びます．<br>
`ファイル` -> `シンボルのプロパティ`から`ライブラリシンボルのプロパティ`ウィンドウを開きます．<br>
`フットプリント`の`値`項目を選択すると，入力モードとなりますが，欄の右側に`書庫マーク`が表示されるのでクリックします．<br>
`フットプリントライブラリ`が開きますので，先ほど作成したフットプリントを選んで，紐づけましょう．<br>

> キーワード欄に検索に引っかかりやすいキーワードを入れておくと，フィルタ検索で引っかかりやすくなります．<br>
> 保存を忘れずに!

これでシンボルとフットプリントを紐づけることができました．<br>
試しに，`回路図エディター`から自作したシンボルを選び，`PCBエディター`から自作したフットプリントが呼び出され，`3Dビューアー`で問題なく表示されるか確かめてみましょう．<br>

これでデーターシートさえあれば，どんな回路部品でも自作できるようになりました．

# digikey を使って効率化

結構時間がかかりましたね…．一つ作るだけでも大仕事です．<br>
ここで，今回使用する部品一覧を見てみましょう．<br>

| Reference   | Value             | Footprint                        | Qty |
| ----------- | ----------------- | -------------------------------- | --- |
| BT1,BT2,BT3 | BCAAAPC           | 5V-charger:BAT_BCAAAPC           | 3   |
| C1          | 120pF             | Capacitor_SMD:C_0603_1608Metric  | 1   |
| C2          | 2.2uF             | Capacitor_SMD:C_0603_1608Metric  | 1   |
| C3,C4,C5    | 10uF              | Capacitor_SMD:C_0603_1608Metric  | 3   |
| D1          | D_Schottky        | Diode_SMD:D_SOD-123              | 1   |
| D2          | LED               | LED_SMD:LED_0603_1608Metric      | 1   |
| J1          | USB1130-15-A_REVA | 5V-charger:GCT_USB1130-15-A_REVA | 1   |
| L1          | 2.2uH             | Inductor_SMD:L_1008_2520Metric   | 1   |
| R1          | 5ohm              | Resistor_SMD:R_0603_1608Metric   | 1   |
| R2,R3       | 200ohm            | Resistor_SMD:R_0603_1608Metric   | 2   |
| SW1         | OS102011MS2QN1    | 5V-charger:SPDT_OS102011_CNK     | 1   |
| U1          | TPS613222ADBV     | Package_TO_SOT_SMD:SOT-23-5      | 1   |

どうやら，電池 BOX と USB-TypeA(メス)を作成する必要がありそうです．<br>
[電池 box](https://www.digikey.jp/ja/products/detail/mpd-memory-protection-devices/BCAAAPC/560754)<br>
[USB-TypeA](https://www.digikey.jp/ja/products/detail/gct/USB1130-15-A/13545899)<br>

じゃぁ，頑張って書いてね．~~頑張れ ♡ 頑張れ ♡~~<br>
…なんて鬼なことは言いません．<br>
もっと効率の良い方法があります．<br>
その方法は回路部品を販売している企業 HP からシンボルとフットプリントをダウンロードして，KiCAD に適用させる方法です．<br>

電子部品を販売している[`digikey`](https://www.digikey.jp/)や[`Mouser`](https://www.mouser.jp/)，[`RSコンポーネンツ`](https://jp.rs-online.com/web/)，[`秋月電子`](https://akizukidenshi.com/catalog/default.aspx)，[`共立エレショップ`](https://eleshop.jp/shop/)，[`マルツオンライン`](https://www.marutsu.co.jp/)等など，<br>
様々な回路部品を専門として取り扱っている企業はありますが，その中でも今回は`digikey`という企業の HP を使って自作ライブラリを簡単に作る方法をご紹介します．<br>

そもそも前提として，digikey で購入した部品に`データシート`と`EDA/CADモデル`が存在していることが前提条件です．<br>
試しに[digikey の公式 HP](https://www.digikey.jp/)から`スライドスイッチ`と検索しただけでも，4000 品目以上がヒットします．(2022/04 時点)<br>
これを 1 つ 1 つ確認していくのは絶望的な作業となります．<br>
絞り込むために，`在庫状況`で`在庫あり`と`通常商品`にチェックを付け，`メディア`で`データシート`と`EDA/CADモデル`にチェックを入れて，`フィルタの適用`を選択してみましょう．<br>
おそらく，500 弱まで絞り込めます．(2022/04 時点)<br>

> 在庫が少ないと当然，売り切れることが多くなります．<br>
> 値段や性能以外で絞り込むための指標として活用しましょう．<br>
> また，使い方や寸法などの大きさなどの重要なデータが詰まった`データーシート`が存在することで，安心して使用することができます．<br>
> 間違っても，生産終了品や，データーシートが存在しないものは設計難易度が跳ね上がるため，購入しないことを心がけましょう．~~ぶっちゃけありえない~~<br>
> あとはお財布と相談して購入してください．

さて，効率化のためには`EDA/CADモデル`が重要となってきます．<br>
使用する部品を決めたら部品のページから`EDA/CADモデル`のリンクをクリックすると，その部品に対応したシンボルとフットプリント，おまけに 3D モデルが配布されている場所にたどり着きます．<br>

> 3D モデルが無いのは仕方がないとして，シンボルとフットプリントがあれば自作する必要がなくなり，設計時間はぐんと早くなります．

`ダウンロード形式を選択`して，`KiCAD v6+`を選び，適当なところにダウンロードしてください．<br>

> `KiCAD v5`でも問題はありません．<br>
> 3DCAD モデルがあれば，ついでにダウンロードしましょう．

すべてダウンロードできましたら，.zip フォルダを解凍して，使いやすいようにフォルダ分けして整理しましょう．

> 以下の図のように，プロジェクトフォルダ直下に`libフォルダ`を作成し，その中に`sym(シンボル)`フォルダ，`pretty(フットプリント)`フォルダ，`3dmodel`フォルダを作成して，整理すると楽です．

![fig.050](/pictures/050.png)<br>
![fig.051](/pictures/051.png)<br>
![fig.052](/pictures/052.png)<br>
![fig.053](/pictures/053.png)<br>
![fig.054](/pictures/054.png)<br>

## シンボルのインポート

まずは，digikey からダウンロードしたシンボルファイルをインポートします．<br>
`プロジェクトマネージャー`から`設定`-> `シンボルライブラリを管理`を選択すると`シンボルライブラリ`ウィンドウが開きます．<br>
`プロジェクト固有ライブラリ`タブに切り替え，`テーブルに既存ライブラリを追加`アイコンを選択します．<br>
先ほど整理した，`lib`フォルダ内部にある，`sym`フォルダ内の 3 つのファイルをすべて選択して，`開く`を選択すると，digikey からダウンロードしたシンボルファイルが KiCAD にインポートされます．<br>
`OK`を選択して，適用しましょう．

> 先程作った自作ライブラリと今回インポートしたスイッチは見分けがつくようにしてください．<br>
> 紛らわしい場合は，どちらかを削除しましょう．

## フットプリントのインポート

次に，フットプリントをインポートします．<br>
`プロジェクトマネージャー`から`設定`-> `フットプリントライブラリを管理`を選択すると`フットプリントライブラリ`ウィンドウが開きます．<br>
`プロジェクト固有ライブラリ`タブに切り替え，`既存を追加`アイコンを選択します．<br>
先ほど整理した，`lib`フォルダ内部にある，`pretty`フォルダを選択して，`フォルダーの選択`を選択すると，digikey からダウンロードしたシンボルファイルが KiCAD にインポートされます．<br>

> 注意!<br>
> シンボルをインポートする際は`ファイル`を選択しましたが，フットプリントをインポートする際は`フォルダ`を選択してください．

`OK`を選択して，適用しましょう．

## シンボルとフットプリントの同期

先ほど自作のシンボルとフットプリントを同期させたときと手順は同じです．<br>

`プロジェクトマネージャー`から`シンボルエディター`を開き，インポートしたシンボルを選びます．<br>
`ファイル` -> `シンボルのプロパティ`から`ライブラリシンボルのプロパティ`ウィンドウを開きます．<br>
`フットプリント`の`値`項目を選択すると，入力モードとなりますが，欄の右側に`書庫マーク`が表示されるのでクリックします．<br>
`フットプリントライブラリ`が開きますので，先ほど作成したフットプリントを選んで，紐づけましょう．<br>

> キーワード欄に検索に引っかかりやすいキーワードを入れておくと，フィルタ検索で引っかかりやすくなります．<br>
> 保存を忘れずに!

これで digikey からインポートしてきた，シンボルとフットプリントを紐づけることができました．<br>
試しに，`回路図エディター`から自作したシンボルを選び，`PCBエディター`から自作したフットプリントが呼び出され，`3Dビューアー`で問題なく表示されるか確かめてみましょう．<br>

これで EDA/CAD モデルさえあれば，どんな回路部品でもインポートできるようになりました．

## 3D モデルの同期

オマケ要素です．<br>
同期もできましたので，先ほどインポートしたシンボルとフットプリントを問題なく使用する事ができますが，3D ビューアーで表示した際に，3D モデルは存在しない状態で描画されます．<br>
せっかく 3D モデルもダウンロードしたので，これもシンボルとフットプリントに同期させてみましょう．<br>

`プロジェクトマネージャー`から`フットプリントエディター`を開き，先ほどインポートしたフットプリントを選択します．<br>
選択した状態で，上部ツールバーの`フットプリントのプロパティを編集`を選択しましょう．<br>
`フットプリントのプロパティ`ウィンドウが開きますので，`3Dモデル`タブを選択します．<br>
`フォルダマーク`を選択し，先ほど整理した，`lib`フォルダ内部にある，`3dmodel`フォルダ内の対応する 3D モデルを選択して，`OK`を選択すると，digikey からダウンロードした 3D モデルが KiCAD にインポートされます．<br>
この時，プレビューを見ると，配置が間違っている場合がありますので，左側欄の`スケール`，`回転`，`オフセット`を調節して，正しく配置し直しましょう．<br>

> 基本的には`回転`を調節するだけで，正しい位置に収まることが多いです．<br>

`OK`を選択して，適用しましょう．<br>

> 保存を忘れずに!

これで 3D モデルが表示されるようになりました．

# 乾電池型モバイルバッテリーの製作

長い説明も終わり，いよいよ本題です．<br>
先に提示してしまいましたが，もう一度，本日使用する回路部品一覧を以下に記述します．<br>

| Reference   | Value             | Footprint                        | Qty |
| ----------- | ----------------- | -------------------------------- | --- |
| BT1,BT2,BT3 | BCAAAPC           | 5V-charger:BAT_BCAAAPC           | 3   |
| C1          | 120pF             | Capacitor_SMD:C_0603_1608Metric  | 1   |
| C2          | 2.2uF             | Capacitor_SMD:C_0603_1608Metric  | 1   |
| C3,C4,C5    | 10uF              | Capacitor_SMD:C_0603_1608Metric  | 3   |
| D1          | D_Schottky        | Diode_SMD:D_SOD-123              | 1   |
| D2          | LED               | LED_SMD:LED_0603_1608Metric      | 1   |
| J1          | USB1130-15-A_REVA | 5V-charger:GCT_USB1130-15-A_REVA | 1   |
| L1          | 2.2uH             | Inductor_SMD:L_1008_2520Metric   | 1   |
| R1          | 5ohm              | Resistor_SMD:R_0603_1608Metric   | 1   |
| R2,R3       | 200ohm            | Resistor_SMD:R_0603_1608Metric   | 2   |
| SW1         | OS102011MS2QN1    | 5V-charger:SPDT_OS102011_CNK     | 1   |
| U1          | TPS613222ADBV     | Package_TO_SOT_SMD:SOT-23-5      | 1   |

また，回路図も以下に表示します．<br>
![fig.201](/pictures/201.png)

配線図と配置図，3D ビューアーや事前に製作した実物も以下に表示します．<br>

配置例<br>
![fig.202](/pictures/202.png)

表面実装部品側<br>
![fig.301](/pictures/301.png)

スルーホール部品側<br>
![fig.302](/pictures/302.png)

表面実装部品側(実物)<br>
![fig.401](/pictures/401.jpg)

スルーホール部品側(実物)<br>
![fig.402](/pictures/402.jpg)

スルーホール部品側(実物，ケース付き)<br>
![fig.403](/pictures/403.jpg)

残り時間すべてを使い，今までに得た知識を総動員して，これらを完成させましょう!<br>

# おわりに

今回説明したこと以外にも便利な機能はたくさんあります．<br>
興味があればぜひ，公式のドキュメントを覗いてみてください．<br>

KiCAD はオープンソースのフリーソフトウェアであるため，日々改良がなされており，Ver が上がるにつれて様々な機能が追加され，修正され，アップデートされていきます．<br>
もしかしたら次の Ver では，大きなアップデートが入り，この`KiCAD ver8.0`ドキュメントと大きく異なるかもしれません．<br>
それでも，公式のドキュメントやコミュニティサイト，SNS などで情報発信をしている有志の方たちから情報を得て，使いこなせようになってほしいと願っています．<br>
忘れてしまったときや，久しぶりに使うときに，このドキュメントを見返して活用してみてください．<br>

# 協力・謝辞

本企画の運営・広報・プロデュース担当である，中津先生<br>
講義資料などを提供していただいた，安藤先生<br>
その他学校関係者と，このドキュメントを読んでくれた皆さまに多大なる感謝を．<br>
<br>
ドキュメント作成者　乾 伊織
