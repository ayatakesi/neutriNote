## ユーザーガイド

1. [Getting Started](#started)
1. [Backup and Restore](#backup)
1. [Search Tools](#search)
1. [Advanced Features](#advanced)
    * [Metadata](#metadata)
    * [Markdown](#md)
    * [Automation](#automation)
    * [Text Expansion](#textexpansion)
    * [Batch Select](#batchselect)
    * [Voice Memo](#voicememo)
    * [External Fonts](#externalfonts)
    * [Ambient Glow](#ambientglow)
    * [Keyboard](#keyboard)
    * [Gestures](#gestures)
    * [Hacks](#hacks)
    * [Built-in Variables](#variables)
    * [Storage Saver](#storage)
    * [API](#api)
    * [Snooze](#snooze)
    * [Misc.](#misc)
    * [Examples](#examples) 
1. [Performance](#performance)
1. [Known Issues](#issues)
1. [FAQs](#faq)
1. [Privacy Policy](#privacy)
1. [TODO](#todo)
1. [About](#about)

### <a name="started">Getting Started</a>
**neutriNote**を選んでいただき、ありがとうございます。

インストールが終わったら、画面上の指示にしたがって、**Local Repository**の場所を選択してください。

リポジトリーが空なら、すぐにノートを追加できます。

以前に**neutriNote**をインストールしていた場合には、すでにデバイス上にあるリポジトリーを選択すればよいでしょう。

以前のインストールで設定をバックアップしていた場合には、[Restore App
Data](https://www.dropbox.com/s/nveejx2dn1pdbqi/navigation_drawer.png?dl=0,
"Backup/Restore App Data")を選択して設定をリストアすればよいでしょう。

同期(sync)を有効にするのは簡単です。[Syncthing](https://play.google.com/store/apps/details?id=com.nutomic.syncthingandroid&hl=en)のようなサードパーティーアプリをインストールして、それにリポジトリーを登録するか、**neutriNote**専用にデザインされたDropbox用アダプターの[neutriNote
Connector](https://play.google.com/store/apps/details?id=com.appmindlab.connector)を入手してください。

アドオンなしでも、**neutriNote**をすぐに使うことができます。多くの機能を発見するために、あちこち触ってみてください。それが**neutriNote**をあなたのノート体験の高度に統合された一部とするでしょう(たとえばメタデータラベルをロングタップすれば[同じような](https://www.dropbox.com/s/tqa3h774xrn49zd/metadata_long_click.png?dl=0)ラベルをもつノートを取得できるし、編集画面でローカル検索アイコンをタップすれば次のマッチにジャンプすることができます)。これを個人情報管理ツールに拡張するのは、以降のセクションまで待ってください。新しいユーザーはデータを守るための、同期メカニズム以上の手段として[Backup
and Restore](#backup)も調べてみるとよいでしょう。

**重要** v1.3.1より、**neutriNote**はAndroid Marshmallowデバイスの**実行時権限**をサポートしています。外部ストレージの**Local Repository**が正しく機能するために、**neutriNote**に外部ストレージへのアクセス権限を付与するのを忘れないでください。以前に拒否された権限を有効にするには、Androidの**アプリ情報**から権限を有効にしてからアプリを再起動してください。
#### <a name="backup">Backup and Restore</a> すでに**Local
Repository**をアクティブにしていれば、ノートはリポジトリーにたいしてシームレスに同期されるでしょう。[Syncthing](https://play.google.com/store/apps/details?id=com.nutomic.syncthingandroid&hl=en)のようなサードパーティー製アプリでフォルダーを共有することにより、ノートをリモートに複製できます。**重要**
同期できない可能性があるので、古いリポジトリーは使用しないでください。常に[Getting
Started](#started)セクションの、上記の箇所からリポジトリーの初期化と割り当てで説明している方法を使用してください。
    
**Incremental Backup**とは、煩わしくないやり方でノートをコピーする別の方法です。有効にするには、Settingでそれを単に有効にするだけです。そうすれば、あなたのノートとアプリのセッティングは、少なくとも1日1回は内部ストレージの_neutrinote_export_というフォルダーにインクリメンタルにバックアップされます。注意: エクスポートされたアプリのセッティングデータは、通常のノートにプレフィクス_.neutrinote_をつけて保存されるので、他のノートと同じように同期させることができます。
より複雑なシナリオについては、[neutriNote
Backup+](https://play.google.com/store/apps/details?id=com.appmindlab.backupplus)を調べてみてください。

#### <a name="search">Search Tools</a>
修正日時、アクセス日時、ユーザーインターフェースにより提供されるロケーション(location:
場所)にもとづくノート検索に加えて、**neutriNote**は高精度のテキストベース検索と正規表現([regular
expression](http://en.m.wikipedia.org/wiki/Glob_(programming)))をサポートします。以下の構文も、(セッティングなる)事前定義されたフィルターの一部に含めると、再利用性が高くなります。

**Search by Fields(フィールド検索)**により、指定したフィールドに検索を限定できます。たとえば、ノート一覧の上にあるメイン検索バーでは、プレフィクスに`title:`を使用することにより、検索をタイトルに限定できます。`title:log`のような検索文字列の場合は、タイトルの一部に`log`という文字列が含まれるすべてのノートがリターンされます。
検索文字列内でプレフィクスに_meta:_を使用することにより、検索をメタデータに限定することもできます。_meta:personal_のような検索文字列では、メタデータ内の一部に_personal_という文字列を含むすべてのノートがリターンされます(同様に、_meta:_という検索文字列ではメタデータのないすべてのノートがリターンされます)。検索文字列内で単にプレフィクス_metareg:_を使うことにより、正規表現[regular
expression](http://en.m.wikipedia.org/wiki/Glob_(programming))も使用可能です。

複数単語の検索でメタデータのマッチを確実にするためには、メイン検索バーで以下の構文を使用するとよいでしょう。
`join:term1,term2,term3`,...:
これは検索がヒットしたメタデータ内で、少なくとも1つの単語がマッチしたことを意味します。このような構文は、metadata/tags内で検索をシミュレートするのに使用できます。

複数単語検索を行う一番簡単なのは、**Advanced
Search**を使う方法です。ブーリアン検索を指定することもできます。`and:term1,term2,term3,...,termN`のような構文は、すべての単語を含むノートを検索し、`or:term1,term2,term3,..,termN`は、これらのうち1つを含む単語を検索します。

**Custom Filters** 上記構文の威力は、それを事前定義された検索フィルターに含めることにより、ユーザーが簡単に抽出できることです。カスタムフィルターは、[Settings](https://www.dropbox.com/s/cfve8rfp4yysro8/custom_filters.png?dl=0)でセミコロンで区切って指定することができます。カスタムフィルターのデフォルトは:

``` all;starred;A;B;C;D;E;F;G;H;I;J;K;L;M;N;O;P;Q;R;S;T;U;V;W;X;Y;Z ```

**all**はすべてのノートを取得するために予約されており、**starred**はスター付きのノートを取得するために予約されています。アルファベット1文字は、タイトルがそのアルファベットで始まるノートを取得するために予約されています。

ノート検索では、**neutriNote**は[Perl](http://www.erudil.com/preqr.pdf)スタイルの基本的なパターン(`\d`は数字、`\s`は空白文字、など)を認識します。
 

### <a name="advanced">Advanced Features</a>

### <a name="metadata">Metadata</a>
メタデータとは、ノートの外部に存在する、一般的な用途のためのテキスト文字列です。メタデータは検索することができ、タグとして使用できます。
        
### <a name="md">Markdown</a>
**neutriNote**は[PHP Markdown Extra](
http://michelf.ca/projects/php-markdown/extra/)と、Latexスタイルの数式表現をサポートします。数式表現を入力する一番簡単な方法は、数式を`$$`で囲むことです。インラインで数式を記述するには、次の例のように`\\(...\\)`を使用します:
``` This expression \\(\sqrt{3x-1}+(1+x)^2\\) is an example of an inline
equation.  ```

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

``` [My File](file:///sdcard/neutriNote/my_file.txt)

[My File](./my_file.txt)

[My File](my_file.txt)

[GTD](get%20things%20done.txt)  ```

ローカルリポジトリー配下のイメージにリンクするには、以下のようにします:

``` ![My Image](my_image.jpg)  ```

単にノート名にプレフィクスを`http://neutriNote.io`をつけるだけで、ハイパーリンクをサポートする他のアプリからノートにリンクすることができます。たとえば:

``` http://neutriNote.io/my_diary

http://neutriNote.io/my_diary?search=first%20headquarter%20visit

```

* マークダウンのイタリックシンボルと、Latexの下付きシンボルは、表記が競合します。
  There is a conflict between Markdown italic symbol and LaTeX subscript
  symbol.
  この問題を回避するには、下付きシンボルをエスケープするか、式をスクリプトブロックで囲みます。たとえば、

    `$$k_{n+1} = n^2 + k_n^2 - k_{n-1}$$`

のかわりに
    
    `$$k\_{n+1} = n^2 + k\_n^2 - k\_{n-1}$$`

のように記述するか、以下のように希望するタイプのスクリプトブロックを使用します:
    
``` <script type="math/tex">k_{n+1} = n^2 + k_n^2 - k_{n-1}</script> ```

ポピュラーなインラインCSSで、マークダウンのスタイルを簡単にカスタマイズできます。より高度なスタイルが必要な場合は、`~neutrinote_styles.txt`にあなたのCSSを定義して、ビルトインのスタイルを、"swap
out"
することができます。あなたのスタイルが既存のマークダウンテーマにもとづいたものである場合、このプロセスはとても容易でしょう。たとえば、あなたのマークダウンを**solarize**するには、以下の2行をコピーして、`~neutrinote_styles.txt`に貼り付けてください。

``` <link
href="http://thomasf.github.io/solarized-css/solarized-light.min.css"
rel="stylesheet"></link> <script
src="https://cdn.rawgit.com/google/code-prettify/master/loader/run_prettify.js"></script>
```
    
### <a name="examples">Examples</a>
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
    
``` <canvas id="example" width="200" height="200"> </canvas>

<head> <script> var example = document.getElementById('example'); var
context = example.getContext('2d'); context.fillStyle = 'red';
context.fillRect(30, 30, 50, 50); </script> </head> ``` Draw a simple
diagram in plain text is easy using
[yUML](http://yuml.me/diagram/scruffy/class/samples).  Try this (note the
single ticks):
    
``` <img src="http://yuml.me/diagram/scruffy/usecase/[Cms Admin]^[User],
[Customer]^[User], [Agent]^[User]" >

<img src="http://yuml.me/diagram/nofunky/class/`[Customer]->[Billing
Address]`">
```

### <a name="automation">Automation</a>

Taskerを使うことにより、**neutriNote**を簡単に自動化できます。たとえば、([neutriNote Auto Theme](https://play.google.com/store/apps/details?id=com.appmindlab.autotheme))を使って以下のステップを行うことにより、照明レベルに合わせて**neutriNote**のテーマをセットすることができます:

1. Taskerで_新しい_タスクを作成します。
1. **Select Action Category**から**App**を選択して、_新しい_アクションを追加します。
1. アプリ選択画面からダウンロードされた拡張を選択します。
1. タスクが作成されて、これであなたの任意のプロファイルでタスクを使用する準備ができました。たとえばタスクを開始するために、ディスプレイがオンになったことによりトリガーされる新しいプロファイルを作成します(新しいプロファイルを追加して、**State**から**Display**を選択します)。これでスクリーンがオンになるたびに、**neutriNote**は自動的に現在の照明レベルにもとづいたテーマを選択します。

上記のステップは同様に、[neutriNote
Backup+](https://play.google.com/store/apps/details?id=com.appmindlab.backupplus)にも適用できます。


クリップボードの履歴の維持に関心のあるユーザーは、Taskerの`%CLIP`変数をモニターするプロファイルを作成してから、以下のタスクを追加します(パスはあなたの**ローカルリポジトリー**で置き換えてください):
    
``` A1: Variable Set [ Name:%NEWLINE To:Do Maths:Off Append:Off ] A2: Write
File [ File:neutriNote/clipboard_events.txt Text:## %DATE %TIME %NEWLINE
%CLIP %NEWLINE Append:On Add Newline:On ] If [ %clip neq %clip_prev ] A3:
Variable Set [ Name:%clip_prev To:%CLIP Do Maths:Off Append:Off ] ```

### <a name="textexpansion">Text Expansion</a> **neutriNote** supports text
expansion: simply highlight any shortcut word and tap the **Text Expansion**
icon to expand the word.  All shortcuts are saved in a file called
**~neutrinote_shortcuts**, with one definition per line in the format of
`shortcut label|expanded text` (if you do not see the file, enable hidden
files under **Settings**).  Below are some examples:

``` cell|123-456-7890 email|john.smith@test.com

# Usage: select "highlight your_text" and expand, return
"<mark>your_text</mark>".  highlight|<mark>???</mark> ```

Shortcuts can be defined for frequently used patterns for string
replacements.  For example:

``` # Usage: select "encode some_text_string" and expand, some_text_string
will be returned with all blank spaces encoded.  encode|neutriNote#replace
\s %20 ```

An example to trim leading and trailing spaces from a body of text:

``` # Usage: select "trim some_text_string" and expand, leading and trailing
spaces of some_text_string will be removed.  trim|neutriNote#trim ```

Shortcuts to obfuscate / defuscate a chunk of text:

``` # Usage: select "obfuscate some_text_string" and expand,
some_text_string will be obfuscated.  obfuscate|neutriNote#encode

# Usage: select "defuscate some_text_string" and expand, some_text_string
will be defuscated.  defuscate|neutriNote#decode ```

You can also use basic C style format specifiers to "morph" text snippets.

``` # Usage: select "addcomma some_numeric_string" and expand,
some_numeric_string will be comma separated.  addcomma|neutriNote#morph ℅,d
```

These simple shortcuts make it easy to sort lines:

``` # Usage: select "sort some_lines" and expand, some_lines will be
sorted.  sort|neutriNote#sort

# Usage: select "rsort some_lines" and expand, some_lines will be sorted in
reverse order.  rsort|neutriNote#rsort ```

There is even a way to remove HTML tags from strings:

``` # Usage: select "notag some_text_string" and expand to remove HTML tags
from some_text_string.  notag|neutriNote#removeHTML ```

You can create shortcuts for simple shell commands as well.  Give it a try
by adding the prefix `neutriNote$` to the commands just like below:

``` date|neutriNote$ date ps|neutriNote$ ps ```

To emulate the behavior of to-do list, shortcuts can be defined to mimic
checkbox toggling.

``` # Usage: place cursor next to any asterisk and expand.  To toggle
checkboxes, tap expand again.

*|[▪]
[▪]|[✔]
[✖]|[▪]
[✔]|[✖]
```

Multitasking especially with floating apps is easier with shortcut like
this:

``` # Usage: launch a terminal without leaving neutriNote by expanding the
shortcut.

termfloat|neutriNote#launch com.termux.window ```

You can include basic parameters with the commands, just write them after
the command shortcut and separate each parameter with space+commas like
this: `shortcut_label param1 , param2 , param3`.  Select the whole string
and tap the expand icon to paste the output.  Users of cURL can also
simplify the definitons of their expansions with `neutriNote?` instead of
`neutriNote$` and trail that directly by a URL.


### <a name="batchselect">Batch Select</a> Special selection commands are
available for better productivity.

* Tap `Top` icon in *Toolbox* when a section of text has been selected to
  extend selection all the way to the top, or if an anchor has been
  positioned above current cursor, extend selection up to the anchor.
* Tap `Bottom` icon in *Toolbox* when a section of text has been selected to
  extend selection all the way to the bottom, or if an anchor has been
  positioned below current cursor, extend selection down to the anchor.
* Tap **editor status** next to note title to gather statistics for current
  note when nothing is selected, or just the selected text when a section of
  text has been selected (experimental).
* To edit an ASCII drawing, select it and tap the **Sketch** icon.
* To encode/decode a portion of the note, select the portion and choose
  **Encode/Decode** from menu.
* Tap `(` or `)` from *Symbol Bar* when text selection is active to enclose
  the selected text in brackets.  Hint: also try out other symbol pairs.
* Edit multiple paragraphs: select multiple paragraphs and tap a symbol /
  action from **Markdown Symbol Toolbar**.  For example, you can indent
  selected paragraphs by tapping `➡`, or turn selected paragraphs into a
  bulleted list simply by tapping `*`.

    
### <a name="voicememo">Voice Memo</a> **neutriNote** is compatible with
Google Now dictation.  Simply say _Ok Google note to self_ and pick
**neutriNote** to capture what you say.
 

### <a name="externalfonts">External Fonts</a> It's easy to use external
fonts such as those featured by Google Fonts in **neutriNote** (IMPORTANT:
be sure to read their terms of use carefully):

1. Create a folder called `fonts` under your Local Repository, download and
   save the font file (.ttf) in that folder.  Note that external fonts will
   not be backup by **neutriNote**.
1. Enable hidden files under **Settings**.  Create a new note called
   `~neutrinote_fonts` if one does not exist yet.
1. Add a section in the note for the font (if there are multiple fonts, separate each section by a blank line) with a line dedicated to each of the following: 
    * Font name (any meaningful name)
    * Font file name (.ttf)
    * Link information (see instructions from Google Fonts)
    * CSS style (see instructions from Google Fonts)
1. The font is now ready for use in **neutriNote**.

For example, to use this
[font](https://www.google.com/fonts#QuickUsePlace:quickUse/Family:Goudy+Bookletter+1911),
just add this section to `~neutrinote_fonts`:
        
```
Goudy Bookletter 1911
GoudyBookletter1911.ttf
<link href='https://fonts.googleapis.com/css?family=Goudy+Bookletter+1911' rel='stylesheet' type='text/css'>
font-family: 'Goudy Bookletter 1911', serif;
```        

        
### <a name="ambientglow">Ambient Glow</a> **Ambient Glow** is an
experimental function that adjusts the color temperature of **neutriNote**
to
[approximate](https://en.wikipedia.org/wiki/Color_temperature#Categorizing_different_lighting)
the level of your current environment for a more _atmospheric_ editing
experience.  It differs from blue light filtering apps in that it does not
demand your location information -- instead only light sensor data from
Tasker will be used (to conserve battery).  [neutriNote Auto
Theme](https://play.google.com/store/apps/details?id=com.appmindlab.autotheme)
is required for this function to work properly.  Note that **Ambient Glow**
will not be applied to Markdown and for users of blue light filters it is
recommended that this function be disabled.

### <a name="keyboard">Keyboard</a> The following editor shortcuts are
supported when connected to a physical keyboard:
    
| Shortcuts       | Actions    |
| --------------- |:----------:|
| `Ctrl-S`        | Save       |
| `Ctrl-F`        | Local Find | 
| `F3`            | Find Next  | 
| `Ctrl-H`        | Replace    |  
| `Ctrl-Z`        | Undo       |  
| `Ctrl-Shift-Z`  | Redo       | 
| `Ctrl-]`        | Indent     |  
| `Ctrl-[`        | Un-indent  |  

### <a name="gestures">Gestures</a> Various user interface elements support
gestures for better productivity:

* Note list screen:
    * Tap **list status** to navigate to the top of the list.
    * Long tap any blue rectangle to retrieve notes with related metadata.
    * Long tap any star to retrieve all starred notes.
    * Tap current sort method to reverse current sort order.
    * Swipe left/right on **list status** bar to navigate adjacent filters/days.
    * Double tap **list status** to resume default filter/day.

* Edit screen:
    * Tap **editor status** (to the right of the note title) to view note statistics and clipboard content; long tap clipboard content to view full clipboard content; long tap update status to view recent updates in other notes without leaving the current note.
    * Tap the **Shortcut** icon to view user defined shortcuts.
    * Immediately after conducting a search, tap the **Search** icon to advance to the next match.
    * Double tap **editor status** to temporarily save the current cursor position.  
    * Swipe left on **editor status** to return to saved cursor position.
    * After conducting search, dial up/down **editor status** to go to previous/next hits.
    * For Android 6.0 or higher, swipe right on **editor status** will resume in edit screen the last scroll bar position from Markdown preview.

### <a name="hacks">Hacks</a> What follows are features that may conflict
with the core functions of **neutriNote**.  Use at your own discretion.

You can tinker with the variables found inside of
**~neutrinote_settings_data** (enabled by **Show Hidden** under
**Settings**).  After saving your changes, do **Restore App Data** for the
changes to take effect.  Note: altering the setting file could affect the
stability of **neutriNote**.
    
| Variable Names                                    |  Values                                                                                                          |
| ------------------------------------------------- |:----------------------------------------------------------------------------------------------------------------:|
| com.appmindlab.nano.pref_open_in_markdown         | `true`: always open notes in markdown preview                                                                    |
| com.appmindlab.nano.pref_markdown_trigger         | Specify a metadata substring pattern to open notes in Markdown by default                                        |
| com.appmindlab.nano.pref_safe_mode_tag            | Specify a metadata substring pattern to disable internal Markdown parser                                         |
| com.appmindlab.nano.pref_linkify_trigger          | Specify a metadata substring pattern to open notes linkified by default                                          |
| com.appmindlab.nano.pref_latex_single_dollar      | `true`: use single dollar signs to signify math expressions                                                      |
| com.appmindlab.nano.pref_indent_char              | Specify the character(s) to use for indentation.  Default: 4 spaces                                              |  
| com.appmindlab.nano.pref_append_custom_style    | `true`: **Extend** built-in styles with `~neutrinote_styles.txt`.  `false`: **Replace** built-in styles with `~neutrinote_styles.txt`.                |
| com.appmindlab.nano.pref_show_toolbar             | `true`: always show edit toolbar                                                                                 |
| com.appmindlab.nano.pref_canvas_strokes           | Fixed width symbols supported by sketch tool delimited by semicolons, e.g., `:;\;/;_;-;,;●` (vertical bar and semicolon not allowed) | 
| com.appmindlab.nano.pref_font_size_list           | Specify custom font size options delimited by semicolons.  Default: `8;10;12;14;16;18;24;32;48` |
| com.appmindlab.nano.pref_margin_list              | Specify custom margin options delimited by semicolons.  Default: `8;16;24` |
| com.appmindlab.nano.pref_excluded_buttons         | Selectively hide toolbar buttons via a semicolon delimited string, e.g., `location;draw;replace` will hide the location, draw, and replace buttons on the toolbar.  The following buttons can be hidden: `markdown`, `time`, `date`, `location`, `expand`, `draw`, `top`, `bottom`, `find`, `replace`, `barcode`, `image`, `ocr`, `define`, `calculate`, `search` |
|com.appmindlab.nano.pref_custom_date_format        | Override system date stamp format with custom [date format](https://developer.android.com/reference/android/icu/text/SimpleDateFormat.html) |
|com.appmindlab.nano.pref_custom_time_format        | Override system time stamp format with custom [time format](https://developer.android.com/reference/android/icu/text/SimpleDateFormat.html) |
| com.appmindlab.nano.pref_preview_mode             | `start`: display the beginning of notes in preview, `end`: display the end, `off`: disable preview               |
| com.appmindlab.nano.pref_icon_behavior            | 0: animation off, 1: animation on, 2: [snooze](#snooze) animation                                                |
| com.appmindlab.nano.pref_keep_deleted_copies      | `true`: keep copies of deleted files under `trash_bin` folder                                                        |
| com.appmindlab.nano.pref_local_priority_tag       | Specify a metadata substring pattern to prevent local copy from being overwritten by remote changes.  Note that conflicts may occur if a note is being edited on multiple devices |
| com.appmindlab.nano.pref_eval_built_in_variables  | `true`: evalute [built-in variables](#variables) in search or shortcut definitions            |  
| com.appmindlab.nano.pref_low_space_mode           | `true`: turn on [storage space saver](#storage) |   
             
Advanced users may enable multiple text file types for **neutriNote**.  To
setup, please carefully follow all the steps below:

1. Backup ALL app settings and notes.
1. Add a blank file called `~neutrinote_multitype.txt` to your **Local
   Repository**.
1. Un-install **neutriNote** (or clear the app's data under Android's system
   settings).
1. Re-install **neutriNote**.
1. Once rescan finishes, file extensions will appear in note titles.
1. Restore app data.

(To reverse the support of multiple file types, you would need to remove the
file `~neutrinote_multitype.txt`, then un-install/re-install
**neutriNote**.)

Note that **neutriNote Connector** will not handle files without `.txt`
extension.  To sync files without `.txt` extension with Dropbox you would
have to install a third party app or install [**neutriNote
Connector+**](https://play.google.com/store/apps/details?id=com.appmindlab.connectorplus).
(If you have **neutriNote Connector** installed, you would need to remove it
prior to launching **neutriNote Connector+**.)

### <a name="variables">Built-in Variables (v2.3.4) </a> Built-in variables
may be used in search or shortcut definitions.  For example, to find notes
with tomorrow's time stamp, simply type `@tomorrow` in the search box.  You
can even include built-in variables in **Custom Filters**, say, for listing
notes containing tomorrow's time stamp, or include them in shortcut
definitions to generate text expansion snippets on the fly.

| Variables            | Descriptions                            |                              
| ---------------------|-----------------------------------------|
| @title               | Title of the current note.              |
| @created             | Created time of the current note.       |                     
| @modified            | Last modified time of the current note. |
| @accessed            | Last accessed time of the current note. |
| @clipboard           | Clipboard content.                      |
| @yesterday           | Yesterday's date stamp.                 |
| @today               | Today's date stamp.                     |
| @tomorrow            | Tomorrow's date stamp.                  |
| @now                 | Current time stamp.                     |

See [Hacks](#hacks) for information on how to enable the use of built-in
variables.

### <a name="storage">Storage Saver</a> For devices equipped with SD cards,
it is possible to store backups on SD cards to save space in internal
storage.

1. Tap **Backup App Data**.
1. Add `com.appmindlab.nano.pref_low_space_mode|true` to
   **~neutrinote_settings_data**.
1. Tap **Restore App Data**.
1. Future backups will be stored at
   `/Android/data/com.appmindlab.nano/files/neutrinote_export` under the SD
   card.

Notice that the backups will be automatically removed to reclaim storage
space if neutriNote is uninstalled.

### <a name="api">API (v2.0.8) </a> neutriNote's Markdown engine is fully
modular and swappable.  If you are familar with compiler scripting and would
like to integrate your own parser, you would need to use the following entry
points in your code:

| Methods              | Descriptions           |                              
| ---------------------|----------------------|
| init(document)       | Initialize the framework. |
| getData()            | Get raw content from a note.  |                     
| prepare()            | Prepare for the rendering process. |
| setContent(html)     | Set view to rendering outcome.   |

Adopt this pattern of invoking neurtiNote in your script:

``` (function (){   ////////////   // Set up //   ////////////  
neutriNote.init(document);

  //////////////////   // Get raw data //   //////////////////   var str =
neutriNote.getData();

  ///////////////////////////   // Prepare for rendering //  
///////////////////////////   neutriNote.prepare();

  ///////////   // Parse //   ///////////
  
  ... <- Custom conversion logic goes here!

  /////////////////   // Set content //   /////////////////  
neutriNote.setContent(str)

})(window, document); ```


To illustrate, suppose you simply want to render everything in italics, all
you need is to create `~neutrinote_script.txt` and paste in the following
code:

``` (function (){   ////////////   // Set up //   ////////////  
neutriNote.init(document);

  //////////////////   // Get raw data //   //////////////////   var str =
neutriNote.getData();

  ///////////////////////////   // Prepare for rendering //  
///////////////////////////   neutriNote.prepare();

  ///////////   // Parse //   ///////////   str = '<i>' + str + '</i>';

  /////////////////   // Set content //   /////////////////  
neutriNote.setContent(str)

})(window, document); ```

Now go to your note and tap render to view the output of your custom parser.

More useful parsing can be achieved by following the same pattern.  Take a
look at this example of integrating
[org-mode](https://raw.githubusercontent.com/appml/nano/master/samples/%7Eneutrinote_script.txt)
into neutriNote.

To restore default PHP Markdown syntax, just remove
`~neutrinote_script.txt`.


### <a name="snooze">Snooze (Experimental)</a> With **neutriNote**'s
non-intrusive visual reminders, it is easy to set aside notes for editing
later, or build a habit of reviewing saved notes.  Simply enable snooze
animation by appending the following to `~neutrinote_settings_data`:

``` com.appmindlab.nano.pref_icon_behavior|2 ```

Then add special **snooze strings** such as `+1h` ("snooze for an hour") or
`+2d` ("snooze for two days") to the metadata of selected notes.  By doing
so a non-intrusive animation will remind you to view the notes if they have
not been visited long enough.  The visual reminders would be dismissed as
soon as the notes were opened.  To de-activate the snooze, simply remove the
snooze string from the note's metadata.


| Units              |  Examples                          |
|--------------------|:----------------------------------:|
| `m` for minutes    | `+30m`: snooze for 30 minutes      |
| `h` for hours      | `+8h`: snooze for 8 hours          |
| `d` for days       | `+3d`: snooze for 3 days           |
| `w` for weeks      | `+2w`: snooze for 2 weeks          |
| `M` for months     | `+3M`: snooze for a quarter        |
| `y` for years      | `+10y`: snooze for a decade        |

To transfer snooze to another device, be sure to tap **Backup/Restore App
Data**.  Even more useful is that snooze strings are also fully searchable,
they work just like regular metadata!

### <a name="misc">Miscellaneous</a> **neutriNote** comes with many goodies
for capturing text based data without switching away such as the built-in
barcode scanner.  Another is a handy calculator for solving mathematical
expressions based on
[Math.js](http://mathjs.org/docs/expressions/syntax.html) (network
connection required).  To see how that works, try one of the following
examples in your notes:

1. Select the expression.
1. Tap the calculator button from the toolbar.
1. View the answer with the option to paste it back into your note.

    
``` sin(45 deg) ^ 2

cos(45 deg)

5.08 cm to inch

det([-1, 2; 3, 1])

log(10000, 10)  ```
        
### <a name="performance">Performance</a> When editing a long note, hide the
title bar to reduce lags.

In general, using default font style can help reduce the time in opening
long notes.

For users who do not use mathematics expressions, mathematics rendering can
be disabled by entering a `.` under **Mathematics** in
**Settings**. Markdown rendering should be faster with mathematics disabled.

### <a name="issues">Known Issues</a>
Anytime a note is accessed from widget, if there is a note already being edited, the note originally being edited will exit without saving.  **neutriNote** does not distinguish between opening a note from widget or from the note list, the currently opened note will be closed to make way for the newly opened note.   It is thus highly recommended that important changes be saved right away.

If a note needs to be renamed, do so within **neutriNote**.  Certain cloud
sync would also change the case of note titles.  **neutriNote** would detect
those changes and be case insensitive accordingly.  However, **neutriNote**
would not delete notes unless their titles match exactly.  Therefore it is
so crucial that notes be renamed from the end of **neutriNote**.

To improve app stability in lower-end devices, **neutriNote** supports note
size up to 1.5 MB.  Notes beyond the size will automatically be moved to a
folder called `import_errors`.  To bring them back into **neutriNote**, you
would need to split the notes into files below 1.5 MB and move them into the
repository folder.

### <a name="faq">FAQs</a> **No folder support?** **neutriNote** is designed
to provide a flat, hierarchy-free, ["low cognitive
load"](http://blog.codinghorror.com/trees-treeviews-and-ui/) note taking
experience so that the number of taps can be minimized, folder navigation
would require a nested UI and more taps to get to notes beyond the root
level.  On top of that, offline search would need to traverse levels of
folders in such a way that turnaround time could vary perceivably.  Metadata
used together with custom filters provides more general organization than
folders (a note can match multiple metadata simultaneously).

**Story behind the name?** [This](https://en.wikipedia.org/wiki/Neutrino) came up when trying to conjure up something that conveys unclutterness. 

### <a name="privacy">Privacy Policy</a> This app does not gather personal
information. Location data can always be disabled via Settings.  A menu
option is also provided to clear search history.

### <a name="todo">TODO</a> Keep the app as crash-proof as possible.

### <a name="about">About</a> Every effort has been made to ensure that all
third-party software used be properly acknowledged (see license information
in the **About** dialog).  Please feel free to contact by
[email](mailto:lightandshadowscamera@gmail.com) anytime should such
information be found incomplete or inaccurate.

You can also visit [Product
Page](https://plus.google.com/u/0/communities/117565395761503074053) for
development updates regarding the app.

To further support neutriNote's development, please visit developer's
[Ko-fi](https://ko-fi.com/neutriNote) page.
