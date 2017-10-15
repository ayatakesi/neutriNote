## ユーザーガイド

<sup>[[日本語バージョン](https://github.com/ayatakesi/neutriNote/blob/master/index.md)]</sup>

1. [始めましょう](#started)
1. [バックアップとリストア](#backup)
1. [検索ツール](#search)
1. [高度な機能](#advanced)
    * [メタデータ](#metadata)
    * [マークダウン](#md)
    * [オートメーション(自動化)](#automation)
    * [テキスト展開](#textexpansion)
    * [バッチ選択](#batchselect)
    * [ボイスメモ](#voicememo)
    * [外部フォント](#externalfonts)
    * [アンビエントグロー](#ambientglow)
    * [キーボード](#keyboard)
    * [ジェスチャー](#gestures)
    * [ハック](#hacks)
    * [ビルトイン変数](#variables)
    * [ストレージセーバー](#storage)
    * [API](#api)
    * [スヌーズ](#snooze)
    * [その他](#misc)
    * [例](#examples) 
1. [パフォーマンス](#performance)
1. [既知の問題](#issues)
1. [FAQ](#faq)
1. [個人情報保護](#privacy)
1. [TODO](#todo)
1. [About](#about)

### <a name="started">始めましょう</a>
**neutriNote**を選んでいただき、ありがとうございます。

インストールが終わったら、画面上の指示にしたがって、**Local Repository**の場所を選択してください。

リポジトリーが空なら、すぐにノートを追加できます。

以前に**neutriNote**をインストールしていた場合には、すでにデバイス上にあるリポジトリーを選択すればよいでしょう。

以前のインストールで設定をバックアップしていた場合には、[Restore App
Data](https://www.dropbox.com/s/nveejx2dn1pdbqi/navigation_drawer.png?dl=0,
"Backup/Restore App Data")を選択して設定をリストアすればよいでしょう。

同期(sync)を有効にするのは簡単です。[Syncthing](https://play.google.com/store/apps/details?id=com.nutomic.syncthingandroid&hl=en)のようなサードパーティーアプリをインストールして、それにリポジトリーを登録するか、**neutriNote**専用にデザインされたDropbox用アダプターの[neutriNote
Connector](https://play.google.com/store/apps/details?id=com.appmindlab.connector)を入手してください。

アドオンなしでも、**neutriNote**をすぐに使うことができます。多くの機能を発見するために、あちこち触ってみてください。それが**neutriNote**をあなたのノート体験の高度に統合された一部とするでしょう(たとえばメタデータラベルをロングタップすれば[同じような](https://www.dropbox.com/s/tqa3h774xrn49zd/metadata_long_click.png?dl=0)ラベルをもつノートを取得できるし、編集画面でローカル検索アイコンをタップすれば次のマッチにジャンプすることができます)。これを個人情報管理ツールに拡張するのは、以降のセクションまで待ってください。新しいユーザーはデータを守るための、同期メカニズム以上の手段として[バックアップとリストア](#backup)も調べてみるとよいでしょう。

**重要** v1.3.1より、**neutriNote**はAndroid Marshmallowデバイスの**実行時権限**をサポートしています。外部ストレージの**Local Repository**が正しく機能するために、**neutriNote**に外部ストレージへのアクセス権限を付与するのを忘れないでください。以前に拒否された権限を有効にするには、Androidの**アプリ情報**から権限を有効にしてからアプリを再起動してください。

#### <a name="backup">バックアップとリストア</a>
すでに**Local
Repository**をアクティブにしていれば、ノートはリポジトリーにたいしてシームレスに同期されるでしょう。[Syncthing](https://play.google.com/store/apps/details?id=com.nutomic.syncthingandroid&hl=en)のようなサードパーティー製アプリでフォルダーを共有することにより、ノートをリモートに複製できます。**重要**
同期できない可能性があるので、古いリポジトリーは使用しないでください。常に[始めましょう](#started)セクションの、上記の箇所からリポジトリーの初期化と割り当てで説明している方法を使用してください。
    
**Incremental Backup**とは、煩わしくないやり方でノートをコピーする別の方法です。有効にするには、Settingでそれを単に有効にするだけです。そうすれば、あなたのノートとアプリのセッティングは、少なくとも1日1回は内部ストレージの _neutrinote_export_ というフォルダーにインクリメンタルにバックアップされます。注意: エクスポートされたアプリのセッティングデータは、通常のノートにプレフィクス _.neutrinote_ をつけて保存されるので、他のノートと同じように同期させることができます。

より複雑なシナリオについては、[neutriNote
Backup+](https://play.google.com/store/apps/details?id=com.appmindlab.backupplus)を調べてみてください。

#### <a name="search">検索ツール</a>
修正日時、アクセス日時、ユーザーインターフェースにより提供されるロケーション(location:
場所)にもとづくノート検索に加えて、**neutriNote**は高精度のテキストベース検索と正規表現([regular
expression](http://en.m.wikipedia.org/wiki/Glob_(programming)))をサポートします。以下の構文も、(セッティングなる)事前定義されたフィルターの一部に含めると、再利用性が高くなります。

**Search by Fields** (フィールド検索)により、指定したフィールドに検索を限定できます。たとえば、ノート一覧の上にあるメイン検索バーでは、プレフィクスに`title:`を使用することにより、検索をタイトルに限定できます。`title:log`のような検索文字列の場合は、タイトルの一部に`log`という文字列が含まれるすべてのノートがリターンされます。

検索文字列内でプレフィクスに _meta:_ を使用することにより、検索をメタデータに限定することもできます。 _meta:personal_
のような検索文字列では、メタデータ内の一部に _personal_ という文字列を含むすべてのノートがリターンされます(同様に、 _meta:_
という検索文字列ではメタデータのないすべてのノートがリターンされます)。検索文字列内で単にプレフィクス _metareg:_
を使うことにより、[正規表現](http://en.m.wikipedia.org/wiki/Glob_(programming))も使用可能です。

複数単語の検索でメタデータのマッチを確実にするためには、メイン検索バーで以下の構文を使用するとよいでしょう。
`join:term1,term2,term3`,...:
これは検索がヒットしたメタデータ内で、少なくとも1つの単語がマッチしたことを意味します。このような構文は、metadata/tags内で検索をシミュレートするのに使用できます。

複数単語検索を行う一番簡単なのは、**Advanced
Search**を使う方法です。ブーリアン検索を指定することもできます。`and:term1,term2,term3,...,termN`のような構文は、すべての単語を含むノートを検索し、`or:term1,term2,term3,..,termN`は、これらのうち1つを含む単語を検索します。

**Custom Filters** 上記構文の威力は、それを事前定義された検索フィルターに含めることにより、ユーザーが簡単に抽出できることです。カスタムフィルターは、[Settings](https://www.dropbox.com/s/cfve8rfp4yysro8/custom_filters.png?dl=0)でセミコロンで区切って指定することができます。カスタムフィルターのデフォルトは:

``` all;starred;A;B;C;D;E;F;G;H;I;J;K;L;M;N;O;P;Q;R;S;T;U;V;W;X;Y;Z ```

**all**はすべてのノートを取得するために予約されており、**starred**はスター付きのノートを取得するために予約されています。アルファベット1文字は、タイトルがそのアルファベットで始まるノートを取得するために予約されています。

ノート検索では、**neutriNote**は[Perl](http://www.erudil.com/preqr.pdf)スタイルの基本的なパターン(`\d`は数字、`\s`は空白文字、など)を認識します。
 

### <a name="advanced">高度な機能</a>

### <a name="metadata">メタデータ</a>
メタデータとは、ノートの外部に存在する、一般的な用途のためのテキスト文字列です。メタデータは検索することができ、タグとして使用できます。
        
### <a name="md">マークダウン</a>
**neutriNote**は[PHP Markdown Extra](
http://michelf.ca/projects/php-markdown/extra/)と、Latexスタイルの数式表現をサポートします。数式表現を入力する一番簡単な方法は、数式を`$$`で囲むことです。インラインで数式を記述するには、次の例のように`\\(...\\)`を使用します:
```
This expression \\(\sqrt{3x-1}+(1+x)^2\\) is an example of an inline
equation.
```

インドキュメントのアンカーやフットノートを作成するには、以下の例のようにPHPマークダウンのリンク構文を使用します:

``` # heading 1 {#header1}

## heading 2

* item 1:
    + sub item *1.1*
    + sub item *1.2*
* item 2
    + sub item *2.1*
    + sub item *2.2*
    + sub item 
    + [Link back to header 1](#header1)
```

自動的に目次を作成するには、プレースホルダーとして`<span id='toc'
/>`を追加し、`{#id}`のようなPHPマークダウンの特殊属性の規約にしたがった一意なIDで各パラグラフのヘッダーをタグとして付けします。以下の例を試してみてください:

```
Table of Contents
=================

<span id='toc' />

## Header 1 {#header1}
    * Your paragraph here...
    
## Header 2 {#header2}
    * Your paragraph here...
    
## Header 3 {#header3}
    * Your paragraph here...
```

ノート間のリンクを作成するには、単に以下の構文の1つを使用します(`%20`はスペースを表します):

```
[My File](file:///sdcard/neutriNote/my_file.txt)

[My File](./my_file.txt)

[My File](my_file.txt)

[GTD](get%20things%20done.txt)
```

ローカルリポジトリー配下のイメージにリンクするには、以下のようにします:

```
![My Image](my_image.jpg)
```

単にノート名にプレフィクスを`http://neutriNote.io`をつけるだけで、ハイパーリンクをサポートする他のアプリからノートにリンクすることができます。たとえば:

```
http://neutriNote.io/my_diary

http://neutriNote.io/my_diary?search=first%20headquarter%20visit

```

* マークダウンのイタリックシンボルと、Latexの下付きシンボルは、表記が競合します。この問題を回避するには、下付きシンボルをエスケープするか、式をスクリプトブロックで囲みます。たとえば、

    `$$k_{n+1} = n^2 + k_n^2 - k_{n-1}$$`

のかわりに
    
    `$$k\_{n+1} = n^2 + k\_n^2 - k\_{n-1}$$`

のように記述するか、以下のように希望するタイプのスクリプトブロックを使用します:
    
```
<script type="math/tex">k_{n+1} = n^2 + k_n^2 - k_{n-1}</script>
```

ポピュラーなインラインCSSで、マークダウンのスタイルを簡単にカスタマイズできます。より高度なスタイルが必要な場合は、`~neutrinote_styles.txt`にあなたのCSSを定義して、ビルトインのスタイルを、"swap
out"
することができます。あなたのスタイルが既存のマークダウンテーマにもとづいたものである場合、このプロセスはとても容易でしょう。たとえば、あなたのマークダウンを**solarize**するには、以下の2行をコピーして、`~neutrinote_styles.txt`に貼り付けてください。

```
<link href="http://thomasf.github.io/solarized-css/solarized-light.min.css"
rel="stylesheet"></link> <script
src="https://cdn.rawgit.com/google/code-prettify/master/loader/run_prettify.js"></script>
```
    
### <a name="examples">例</a>
以下は[JSXGraph](http://jsxgraph.uni-bayreuth.de/wp/examples/)を使用してグラフをプロットするために、**neutriNote**のレンダリングコンポーネントをどのように使用するかの例です:

```
<div id="box" class="box" style="width:500px; height:500px;"></div>
<head>
<script type='text/javascript' src='http://cdnjs.cloudflare.com/ajax/libs/jsxgraph/0.98/jsxgraphcore.js'></script>
<script type='text/javascript'>
 var b = JXG.JSXGraph.initBoard('box', {boundingbox: [-10, 10, 10, -10], axis:true});
b.create('functiongraph', [function(x){return Math.sin(x);},-Math.PI,2*Math.PI]);
</script>
</head>
```
以下はシンプルな四角形を描画するために、**neutriNote**のレンダリングコンポーネントをどのように使用するかの例です:
    
```
<canvas id="example" width="200" height="200"> </canvas>

<head> <script> var example = document.getElementById('example'); var
context = example.getContext('2d'); context.fillStyle = 'red';
context.fillRect(30, 30, 50, 50); </script> </head>
```
[yUML](http://yuml.me/diagram/scruffy/class/samples)を使えば、プレーンテキストでシンプルなダイアグラムを描画するのは簡単です。以下を試してみてください(バッククォートで括られていることに注意してください):
    
```
<img src="http://yuml.me/diagram/scruffy/usecase/[Cms Admin]^[User],
[Customer]^[User], [Agent]^[User]" >

<img src="http://yuml.me/diagram/nofunky/class/`[Customer]->[Billing
Address]`">
```

### <a name="automation">オートメーション(自動化)</a>

Taskerを使うことにより、**neutriNote**を簡単に自動化できます。たとえば、([neutriNote Auto Theme](https://play.google.com/store/apps/details?id=com.appmindlab.autotheme))を使って以下のステップを行うことにより、照明レベルに合わせて**neutriNote**のテーマをセットすることができます:

1. Taskerで _新しい_ タスクを作成します。
1. **Select Action Category**から**App**を選択して、 _新しい_ アクションを追加します。
1. アプリ選択画面からダウンロードされた拡張を選択します。
1. タスクが作成されて、これであなたの任意のプロファイルでタスクを使用する準備ができました。たとえばタスクを開始するために、ディスプレイがオンになったことによりトリガーされる新しいプロファイルを作成します(新しいプロファイルを追加して、**State**から**Display**を選択します)。これでスクリーンがオンになるたびに、**neutriNote**は自動的に現在の照明レベルにもとづいたテーマを選択します。

上記のステップは同様に、[neutriNote
Backup+](https://play.google.com/store/apps/details?id=com.appmindlab.backupplus)にも適用できます。

以下は自動化されたバックアップの期限を、より詳細に制御する方法の例です。180日以上保存されたバックアップ、または30を超えた時系列バックアップはパージされます。

```
A1: Send Intent
[Action:com.appmindlab.nano.ACTION_FULL_BACKUP
Cat:None
Mime Type:
Data:
Extra:com.appmindlab.nano.EXTRA_MAX_BACKUP_COUNT:30
Extra:com.appmindlab.nano.EXTRA_MAX_BACKUP_AGE:180
Extra:
Package:
Class:
Target:Broadcast Receiver ]
```

クリップボードの履歴の維持に関心のあるユーザーは、Taskerの`%CLIP`変数をモニターするプロファイルを作成してから、以下のタスクを追加します(パスはあなたの**ローカルリポジトリー**で置き換えてください):
    
``` A1: Variable Set [ Name:%NEWLINE To:Do Maths:Off Append:Off ] A2: Write
File [ File:neutriNote/clipboard_events.txt Text:## %DATE %TIME %NEWLINE
%CLIP %NEWLINE Append:On Add Newline:On ] If [ %clip neq %clip_prev ] A3:
Variable Set [ Name:%clip_prev To:%CLIP Do Maths:Off Append:Off ]
```

### <a name="textexpansion">テキスト展開</a>
**neutriNote**はテキスト展開(text expansion)をサポートします:
ショートカットの単語を単にハイライトして、単語を展開するために**Text Expansion**アイコンをタップしてください。すべてのショートカットは
**~neutrinote_shortcuts**
というファイルに保存されます。ショートカットのは1行ごとに`ショートカットラベル|展開されるテキスト`というフォーマットで定義されます(ファイルを確認できない場合は、**Settings**で非表示ファイル(hidden
files)の表示を有効にしてください)。以下はショートカットの例です:

``` cell|123-456-7890
email|john.smith@test.com

# 使い方: "highlight your_text"を選択して展開すると"<mark>your_text</mark>"をリターンする。
highlight|<mark>???</mark>
```

ショートカットは、文字列置換で頻繁に使用するパターンにたいして定義できます。たとえば:

```
# 使い方: "encode
some_text_string"を選択して展開すると、some_text_stringをすべてスペースに置き換えてリターンする。
encode|neutriNote#replace \s %20
```

以下はテキストの本体から先頭と末尾のスペースを取り除く例です:

```
# 使い方: "trim some_text_string"を選択して展開すると、some_text_stringの先頭と末尾のスペースが削除される。
trim|neutriNote#trim
```

以下は一群のテキストの難読化/復号化(obfuscate/defuscate)を行います:

```
# 使い方: "obfuscate some_text_string"を選択して展開すると、some_text_stringを難読化する。
obfuscate|neutriNote#encode

# 使い方: "defuscate
some_text_string"を選択して展開すると、some_text_stringを復号化する。defuscate|neutriNote#encode
```

"morph"テキストスニペット(text snippets)にたいして、基本的なCスタイルフォーマットを使用することもできます。

```
# 使い方: "addcomma
some_numeric_string"を選択して展開すると、some_numeric_stringはカンマで桁区切りされる。
addcomma|neutriNote#morph %,d
```

以下は行のソートを簡単にするシンプルなショートカットの例です:

```
# 使い方: "sort some_lines"を選択して展開すると、some_linesがソートされる。
sort|neutriNote#sort

# 使い方: "rsort
some_lines"を選択して展開すると、some_linesが逆順にソートされる。rsort|neutriNote#rsort
```

文字列からHTMLを削除することさえできます:

```
# 使い方: "notag some_text_string"を選択して展開すると、some_text_stringからHTMLタグが削除される。
notag|neutriNote#removeHTML
```

同様に、シンプルなシェルコマンドのショートカットを作成することができます。以下のようにコマンドの前にプレフィクス`neutriNote$`を追加してみてください:

```
date|neutriNote$ date
ps|neutriNote$ ps
```

TODOリストの動作をエミュレートするために、チェックボックスのオン/オフのトグルを模倣するショートカットを作成できます。

```
# 使い方: アスタリスクの横にカーソルを配し展開する。チェックボックスをトグルするには、再度展開する。

*|[▪]
[▪]|[✔]
[✖]|[▪]
[✔]|[✖]
```

特にフローティングアプリでは、以下のようなショートカットでマルチタスク化が簡単になります:

```
# 使い方: ショートカットを展開することにより、neutriNoteを離れずに、端末を起動する。

termfloat|neutriNote#launch com.termux.window
```

`shortcut_label param1 , param2 ,
param3`のように、コマンドとなるショートカットの後にスペースとカンマで区切られたパラメーターを続けることにより、コマンドに基本的なパラメーターを含めることができます。出力を貼り付けるには、文字列全体を選択してから、expand(展開)アイコンをタップします。cURLのユーザーは`neutriNote$`のかわりに、`neutriNote?`の後に直接URLを続けることにより、展開定義を簡単にできます。


### <a name="batchselect">バッチ選択</a>
生産性向上のために、特別な選択コマンドが利用できます。

* テキストの一部が選択された状態で*Toolbox*内の`Top`アイコンをタップすると、選択はノートの先頭まで拡張されます。またカーソル位置にアンカーがある場合には、アンカーの先頭まで選択が拡張されます。
* テキストの一部が選択された状態で*Toolbox*内の`Bottom`アイコンをタップすると、選択はノートの終端まで拡張されます。またカーソル位置にアンカーがある場合には、アンカーの終端まで選択が拡張されます。
* ノートタイトルの隣の**editor
  status**(エディター状態)をタップすると、何も選択されていない場合は現在のノートの統計情報、何か選択されている場合には選択されたテキストの情報を収集します(試験的機能)。
* ASCIIアートを編集する場合は、それを選択して**Sketch**アイコンをタップします。
* ノートの一部にたいして暗号化/復号化を行うには、メニューから**Encode/Decode**を選択します。
* テキスト選択がアクティブなときに*Symbol
  Bar*の`(`か`)`をタップすると、選択されたテキストがカッコで括られます。ヒント:他のシンボルペアーも試してみてください。
* 複数パラグラフの編集: 複数のパラグラフを選択して**Markdown Symbol
  Toolbar**のシンボルかアクションを選択します。たとえば、`➡`をタップすると選択されたパラグラフがインデントされ、`*`をタップすると選択されたパラグラフが箇条書きリストになります。
* イメージからテキストを抽出するには、リンクされたイメージのパスを選択して、**OCR**をタップします。

    
### <a name="voicememo">ボイスメモ</a>
**neutriNote**はGoogle Now音声検索と互換性があります。 _Ok Google note to self_
と話し、それをキャプチャーするために**neutriNote**を選択してください。
 

### <a name="externalfonts">外部フォント</a>
**neutriNote**でGoogle Fontsなどにより提供される外部フォントを使用するのは簡単です。(重要:
フォントの使用に際しては、使用条件を慎重に確認してください):

1. ローカルリポジトリー配下に`fonts`というフォルダーを作成しからて、フォントファイル(.ttf)をダウンロードしてそのフォルダーに保存します。外部フォントは**neutriNote**によりバックアップされないことに注意してください。
1. **Settings**で非表示ファイル(hidden
   files)の標準的なを有効にし、まだ作成されていない場合は`~neutrinote_fonts`というノートを新たに作成します。
1. こｎノートにフォントのためのセクションを追加(フォントが複数ある場合は、各セクションを空行で分割)します。セクションの各行には以下を記述します:
    * フォント名(意味のある名前)
    * フォントファイル名(.ttf)
    * リンク情報(Google Fontsの手順参照)
    * CSSスタイル(Google Fontsの手順参照)
1. これで**neutriNote**でそのフォントを使う準備ができました。

たとえばこの[フォント](https://www.google.com/fonts#QuickUsePlace:quickUse/Family:Goudy+Bookletter+1911)を使用する場合は、以下のセクションを`~neutrinote_fonts`に追加します:
        
```
Goudy Bookletter 1911
GoudyBookletter1911.ttf
<link href='https://fonts.googleapis.com/css?family=Goudy+Bookletter+1911' rel='stylesheet' type='text/css'>
font-family: 'Goudy Bookletter 1911', serif;
```        

        
### <a name="ambientglow">アンビエントグロー</a>
**アンビエントグロー**とは、**neutriNote**の色温度を現在の環境レベルに[近似](https://en.wikipedia.org/wiki/Color_temperature#Categorizing_different_lighting)させて調節することで、より
_雰囲気_
に即した編集体験を提供するための、試験的機能です。これは青色光フィルターアプリとは異なります。青色光フィルターアプリは、(バッテリー節約のために)Taskerからの照明センサーのデータだけが使用されており、位置情報にもとづいたものではありません。[neutriNote
Auto
Theme](https://play.google.com/store/apps/details?id=com.appmindlab.autotheme)が正しく機能するためには、この機能が必要です。
注意: **アンビエントグロー**はマークダウンには適用されません。また青色光フィルターのユーザーはこの機能を無効にすることを推奨します。

### <a name="keyboard">キーボード</a>
物理キーボードが接続されている場合は、以下の編集用ショートカットがサポートされます:

| Shortcuts                  | Actions           |
| -------------------------- |:-----------------:|
| `Ctrl-S`                   | Save              |
| `Ctrl-F`                   | Local Find        | 
| `F3`                       | Find Next         | 
| `Ctrl-H`                   | Replace           | 
| `Ctrl-D`                   | Dictionary Lookup |
| `Ctrl-W`                   | Web Search        |  
| `Ctrl-Z`                   | Undo              |  
| `Ctrl-Shift-Z`             | Redo              | 
| `Ctrl-]` or `Ctrl-I`       | Indent            |  
| `Ctrl-[` or `Ctrl-Shift-I` | Un-indent         | 


### <a name="gestures">ジェスチャー</a>
より良い生産性のために、さまざまなインターフェース要素がジェスチャーをサポートします:

* ノートリスト画面:
    * **list status**をタップすると、リストのトップに移動。
    * 任意の青い四角形をロングタップすると、関連するメタデータをもつノートを取得。
    * 任意のスターをロングタップすると、すべてのスター付きノートを取得。
    * 現在のソートメソッドをタップすると、現在のソート順を逆転。
    * **list status**バーを左右にスワイプすると、隣接するフィルター/日時に移動。
    * **list status**をダブルタップすると、デフォルトのフィルター/日時を回復。

* 編集画面:
    * **editor status**(ノートタイトルの右)をタップするとノートの統計情報とクリップボードの内容を閲覧、クリップボードの内容をロングタップするとクリップボードの完全な内容の閲覧、update statusをロングタップすると、現在のノートを離れることなく、他のノートの最近の更新を閲覧。
    * **Shortcut**アイコンをロングタップすると、ユーザー定義ショートカットを閲覧。
    * 検索した直後に、**Search**アイコンをタップすると次のマッチに進む。
    * **editor status**をダブルタップすると、現在のカーソル位置を一時的に保存。
    * **editor status**上で左にスワイプすると、保存したカーソル位置に復帰。
    * 検索した後、**editor status**をダイアルアップ/ダウン(訳注: マッチ番号を上/下にフリック)すると前/次のマッチに移動。
    * Android 6.0以降では、**editor status**上で右にスワイプするとマークダウンプレビューの最後のスクロールバー位置へ編集画面を戻す。

### <a name="hacks">ハック</a>
以降は**neutriNote**の中核機能と競合するかもしれない機能です。使用は自己責任でお願いします。

**~neutrinote_settings_data**(**Settings**の**Show
Hidden**を有効にしてください)内の変数をいろいろ変更することができます。変更を保存したら、その変更を有効にするために、**Restore App
Data**を行ってください。注意: 設定ファイルの変更により、**neutriNote**が不安定になるかもしれません。
    

| 変数名                                            |  値                                                                                                              |
| ------------------------------------------------- |:----------------------------------------------------------------------------------------------------------------:|
| com.appmindlab.nano.pref_open_in_markdown         | `true`: 常にマークダウンビューでノートをオープンする。                                                           |
| com.appmindlab.nano.pref_markdown_trigger         | デフォルトでマークダウンでオープンするノートの、メタデータの部分文字列パターンを指定する。                       |
| com.appmindlab.nano.pref_safe_mode_tag            | 内部マークダウンパーサーを無効にする、メタデータの部分文字列パターンを指定する。                                 |
| com.appmindlab.nano.pref_linkify_trigger          | デフォルトでlinkifyされたノートをオープンするための、メタデータの部分文字列パターンを指定する 。                |
| com.appmindlab.nano.pref_latex_single_dollar      | `true`: 数式を表すために、1つの$記号を使用する。                                                                |
| com.appmindlab.nano.pref_indent_char              | インデントに使用する文字を指定する。デフォルトは4つのスペース。                                                  |
| com.appmindlab.nano.pref_append_custom_style      | `true`: ビルトインスタイルを`~neutrinote_styles.txt`で**拡張**する。 `false`: ビルトインスタイルを`~neutrinote_styles.txt`で**置き換え**る。 |
| com.appmindlab.nano.pref_show_toolbar             | `true`: 常に編集ツールバーを表示する。                                                                      .    |
| com.appmindlab.nano.pref_canvas_strokes           | スケッチツールでサポートされる固定長シンボルをセミコロンで区切って指定する(垂直バーとセミコロンは不可)。         | 
| com.appmindlab.nano.pref_font_size_list           | カスタムフォントサイズのオプションをセミコロンで区切って指定する。デフォルトは`8;10;12;14;16;18;24;32;48`        |
| com.appmindlab.nano.pref_margin_list              | カスタムマージンのオプションをセミコロンで区切って指定する。デフォルトは`8;16;24`                                |
| com.appmindlab.nano.pref_excluded_buttons         | セミコロンで区切られた文字列により、ツールバーのボタンを選択的に非表示にする。たとえば、`location;draw;replace`は、ツールバー上のlocation、draw、replaceボタン。非表示にできるボタンは`markdown`、`time`、`date`、`location`、`expand`、`draw`、`top`、`bottom`、`find`、`replace`、`barcode`、`image`、`ocr`、`define`、`calculate`、`search` |
|com.appmindlab.nano.pref_custom_date_format        | システムの日付スタンプをカスタムの[日付フォーマット](https://developer.android.com/reference/android/icu/text/SimpleDateFormat.html)でオーバーライドする。 |
|com.appmindlab.nano.pref_custom_time_format        | システムの時刻スタンプをカスタムの[時刻フォーマット](https://developer.android.com/reference/android/icu/text/SimpleDateFormat.html)でオーバーライドする。 |
| com.appmindlab.nano.pref_preview_mode             | `start`: プレビューでノートの先頭を表示。 `end`: 最後を表示。 `off`: プレビューを無効にする。                   |
| com.appmindlab.nano.pref_icon_behavior            | 0: アニメーションはオフ。 1: アニメーションはオン。 2: アニメーションを[スヌーズ](#snooze)。                     |
| com.appmindlab.nano.pref_keep_deleted_copies      | `true`: `trash_bin`フォルダー配下に削除されたファイルのコピ＝を保持する。                                       |

| com.appmindlab.nano.pref_max_deleted_copies_age    | 削除されたファイルが保持される最大の日数を指定する(次のバックアップが発生するまでの間に整理する)。デフォルト: -1 (無制限) 
| com.appmindlab.nano.pref_local_priority_tag       | ローカルコピーがリモートからの変更で上書きされることを防ぐ。ノートが複数デバイスから編集される場合は競合が発生するかもしれないことに注意。 |
| com.appmindlab.nano.pref_eval_built_in_variables  | `true`: 検索およびショートカット定義で[ビルトイン変数](#variables)を評価する。                                   |
| com.appmindlab.nano.pref_low_space_mode           | `true`: [storage space saver](#storage)をオンにする。                                                            |
| com.appmindlab.nano.pref_new_note_file_type       |S 新しいノートにたいするファイルタイプを指定する。複数タイプモードが必要(以下参照)。デフォルト: `.txt` | 
             
上級ユーザーは、**neutriNote**で複数のテキストファイルタイプを有効にすると良いかもしれません。これをセットアップする場合は、以下のすべてのステップを慎重に行ってください。

1. アプリのセッティングとノートをすべてバックアップします。
1. **Local Repository**に`~neutrinote_multitype.txt`という名前の空ファイルを追加します。
1. **neutriNote**をアンインストールします(Androidのシステムセッティングのアプリデータをクリアーします)。
1. **neutriNote**を再インストールします。
1. 再スキャンが終了すれば、ファイルの拡張子がノートのタイトルに表示されます。
1. アプリのデータをリストアします。

(複数ファイルタイプのサポートを取り消す場合は、ファイル`~neutrinote_multitype.txt`を削除した後に、**neutriNote**のアンインストールと再インストールが必要になります。)

検索ヒストリーにたいするデバイス間の転送を有効にするには、単に`~neutrinote_search_history.txt`というノートを追加します。すると、他のデバイス上で**Restore App Data**をタップすることによりアプリのデータがリストアされるときに検索ヒストリーもクローンされるようになります。

**neutriNote
Connector**は、拡張子が`.txt`でないファイルを処理しないことに注意してください。拡張子が`.txt`でないファイルをDropboxと同期するには、サードパーティーアプリか[**neutriNote
Connector+**](https://play.google.com/store/apps/details?id=com.appmindlab.connectorplus)をインストールする必要があるでしょう(**neutriNote
Connector**をインストールしていた場合には、 **neutriNote Connector+**
の起動の前にそれを削除する必要があるでしょう)。

### <a name="variables">ビルトイン変数 (v2.3.4) </a>
ビルトイン変数は検索やショートカット定義に使用されることがあります。たとえば明日のタイムスタンプをもつノートを探す場合には、検索ボックスに`@tomorrow`とタイプします。**Custom
Filters**にビルトイン変数を含めることさえできます。たとえば明日のタイムスタンプを含むノートを一覧したり、ビルトイン変数をショートカット定義に含めてオンザフライでテキスト展開の一部を生成できます。

| 変数                 | 説明                                    |                
| ---------------------|-----------------------------------------|
| @title               | 現在のノートのタイトル                  |
| @created             | 現在のノートの作成日時                  |                
| @modified            | 現在のノートの最終修正日時              |
| @accessed            | 現在のノートの最終アクセス日時          |
| @clipboard           | クリップボードの内容                    |
| @yesterday           | 昨日のタイムスタンプ                    |
| @today               | 今日のタイムスタンプ                    |
| @tomorrow            | 明日のタイムスタンプ                    |
| @now                 | 現在のタイムスタンプ                    |

ビルトイン変数の使用を有効にする方法については、[ハック](#hacks)を参照してください。

### <a name="storage">ストレージセーバー</a>
SDカードをもつデバイスでは、内部ストレージの容量を抑えるために、SDカードにバックアップを保存することが可能です。

1. **Backup App Data**をタップする。
1. **~neutrinote_settings_data**に`com.appmindlab.nano.pref_low_space_mode|true`を追加する。
1. **Restore App Data**をタップする。
1. 以降、バックアップはSDカードの`/Android/data/com.appmindlab.nano/files/neutrinote_export`に保存される。

ストレージ容量を回収するために、neutriNoteをアンインストールした場合、バックアップは自動的に削除されることに注目してください。

### <a name="api">API (v2.0.8) </a>
neutriNoteのマークダウンエンジンは完全にモジュラー化されていて交換可能です。あなたがコンパイラースクリプティングに精通していて、自分のパーサーを統合したい場合は、あなたのコードで以下のエントリーポイントを使う必要があるでしょう。

| メソッド             | 説明                                   |
| ---------------------|----------------------------------------|
| init(document)       | フレームワークを初期化                 |
| getData()            | ノートからrawコンテンツを取得          |
| prepare()            | レンダリング処理を準備                 |
| setContent(html)     | レンダリング結果のためにビューをセット |

あなたのスクリプトで、このneutriNote呼び出しのパターンを使用してください:

```
(function (){
  ////////////
  // Set up //
  ////////////
  neutriNote.init(document);

  //////////////////
  // Get raw data //
  //////////////////
  var str = neutriNote.getData();

  ///////////////////////////
  // Prepare for rendering //
  ///////////////////////////
  neutriNote.prepare();

  ///////////
  // Parse //
  ///////////
  
  ... <- Custom conversion logic goes here!

  /////////////////
  // Set content //
  /////////////////
  neutriNote.setContent(str)

})(window, document);
```


説明のために、すべてを斜体で描画したいとします。必要なのは`~neutrinote_script.txt`を作成して、以下のコードを貼り付けることです:

```
(function (){
  ////////////
  // Set up //
  ////////////
  neutriNote.init(document);

  //////////////////
  // Get raw data //
  //////////////////
  var str = neutriNote.getData();

  ///////////////////////////
  // Prepare for rendering //
  ///////////////////////////
  neutriNote.prepare();

  ///////////
  // Parse //
  ///////////
  str = '<i>' + str + '</i>';

  /////////////////
  // Set content //
  /////////////////
  neutriNote.setContent(str)

})(window, document);
```

それではノートを開いてrender(描画)をタップし、あなたのカスタムパーサーで出力を閲覧してみてください。

同じパターンにしたがうことで、より有用なパースを達成できます。neutriNoteに[org-mode](https://raw.githubusercontent.com/appml/nano/master/samples/%7Eneutrinote_script.txt)を統合する例を参照してください。

デフォルトのPHP Markdown構文をリストアするには、`~neutrinote_script.txt`を削除してください。


### <a name="snooze">スヌーズ (試験的)</a>
**neutriNote**の非干渉的なビジュアルリマインダーにより、ノートを一時保留にして後で編集したり、保存したノートをレビューする週間を作るのが簡単になります。`~neutrinote_settings_data`に以下を追加することにより、簡単にスヌーズアニメーションを有効にできます:

```
com.appmindlab.nano.pref_icon_behavior|2
```

それからノートを選択してメタデータに特別な**スヌーズ文字列**(`+1h`は1時間、`+2d`は2時間のスヌーズです)を追加します。これを行うことにより、そのノートがある期間開かれていなければ、非干渉的なアニメーションが、そのノートの閲覧するよう注意を促します。ビジュアルリマインダーは、ノートがオープンされれば解除されます。スヌーズをオフにするには、そのノートのメタデータからスヌーズ文字列を削除するだけです。


| 単位               |  例                                |
|--------------------|:----------------------------------:|
| `m` : 分           | `+30m`: スヌーズ30分               |
| `h` : 時間         | `+8h`: スヌーズ8時間               |
| `d` : 日           | `+3d`: スヌーズ3日間               |
| `w` : 週           | `+2w`: スヌーズ2週間               |
| `M` : 月           | `+3M`: スヌーズ4半期               |
| `y` : 年           | `+10y`: スヌーズ10年間             |

他のデバイスにスヌーズを転送速度するために、確実に**Backup/Restore App
Data**をタップしてください。さらに便利なのは、スヌーズ文字列は標準的なメタデータと同様に機能するので、完全に検索可能であることです!

### <a name="misc">その他</a>
**neutriNote**には、neutriNoteからスイッチすることなくテキストベースのデータをキャプチャーするために、ビルトインのバーコードスキャナーのような豊富な機能が同梱されとぃます。他には[Math.js](http://mathjs.org/docs/expressions/syntax.html)にもとづいた数式を解くためのハンディな計算機があります(ネットワーク接続が必要)。あなたのノートで以下の例を試して、それがどのように機能するか確認してください:

1. 数式を選択する。
1. ツールバーのcalculator(計算機)ボタンをタップする。
1. 解を閲覧する(ノートに解を貼り付けるオプションあり)。

    
```
sin(45 deg) ^ 2

cos(45 deg)

5.08 cm to inch

det([-1, 2; 3, 1])

log(10000, 10)
```
        
### <a name="performance">パフォーマンス</a>
大きなノートを編集する場合は、タイムラグを減らすためにタイトルバーを非表示にしてください。

一般的に、デフォルトのフォントスタイルを使用すると、大きなノートを開く時間が短縮されます。

数式を使用しないユーザーは、**Settings**の**Mathematics**に`.`を入力することにより、数式の描画を無効にできます。数式を無効にすれば、マークダウンの描画が高速になるでしょう。

### <a name="issues">既知の問題</a>
ノートがウィジェットからアクセスされるとき、ノートがすでに編集中の場合は、もともと編集中だったノートは保存されずに終了します。**neutriNote**は、ノートがウィジェットからオープンされたのか、それともノート一覧からオープンされたか区別しないので、新たにオープンされたノートのために、現在オープンされているノートはクローズされます。したがって、重要な変更はただちに保存することを強く推奨します。

ノートのリネームが必要な場合は、**neutriNote**からリネームしてください。ノートタイトルの大文字小文字を変更するクラウド同期も存在します。**neutriNote**は状況に応じて、これらの変更と大文字小文字の非区別を検知するでしょう。しかし**neutriNote**はノートのタイトルが正確にマッチしなければ、ノートを削除しません。したがって**neutriNote**で最後にノートをリネームするのは危険です。

よりローエンドのデバイスにたいする安定性向上のため、**neutriNote**はサイズが1.5MBまでのノートをサポートします。このサイズを超えるノートは、自動的に`import_errors`というフォルダーに移動されます。これを再度**neutriNote**に取り込むには、1.5MB以下のサイズにノートを分割してから、リポジトリーフォルダーに移動する必要があります。

### <a name="faq">FAQ</a>
**フォルダーはサポートしないのですか?**
**neutriNote**はフラットで階層に束縛されない、["low cognitive
load"](http://blog.codinghorror.com/trees-treeviews-and-ui/)(低認知的負荷)なデザインを提供します。これによりタップの回数は最小化されます。フォルダー操作はネストされたUIと、ルートレベルから遠いノートの取得により多くのタップを要求します。階層構造の最上位でのオフライン検索はフォルダーのレベルを横断する必要があり、そのような場合には体感できるほどの遅延が生じるでしょう。メタデータをカスタムフィルターと併用することにより、フォルダーより一般的な組織化が提供されます(ノートは同時に複数のメタデータにマッチすることができます)。

**名前の由来は?** 
乱雑でない何かを伝えようとしたとき、[これ](https://en.wikipedia.org/wiki/Neutrino)が思い浮かびました。

### <a name="privacy">個人情報保護</a>
このアプリは個人情報を収集しません。location
data(位置情報)はSettingsからいつでも無効にできます。メニューオプションでは検索履歴のクリアーも提供されています。

### <a name="todo">TODO</a>
このアプリを可能な限り耐クラッシュに維持することです。

### <a name="about">About</a>
すべてのサードパーティーアプリが正確に評価されることを確実にするために、すべての努力が行われてきました(**About**ダイアログのライセンス情報を確認してください)。不完全または不正確な情報を見つけたときは、いつでも遠慮なく[email](mailto:lightandshadowscamera@gmail.com)で連絡してください。

このアプリの開発版アップデートのために、[プロダクトページ](https://plus.google.com/u/0/communities/117565395761503074053)を訪問することもできます。

さらにneutriNoteの開発をサポートするために、どうか開発者の[Ko-fi](https://ko-fi.com/neutriNote)ページを訪問してください。
