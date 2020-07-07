# 関数
ふりがなプログラミングJavaScript  
132P～  
  
関数はしくみ  
  
Javaだとクラスに属してないメソッド(関数)はなくて、  
クラスを持ってる関数をメソッドっていう感じ  
  
書き方  
**アロー関数式**（**ラムダ式**　無名関数？）  
**アロー演算子**  
```=>```  
  
Javaとの一番の違いはここ  
  
Javaは型に厳格な言語  
  
**Javaの場合**  
```public int sum(int x,int y){return x+y;}```  
  
**JavaScriptの場合**  
```let sum=(x,y)=>{};```  
**実行するとき**  
```sum(3,5);```  
  
オーバーロードできない  
同じ関数名は定義できない  
  
変数にメソッドに代入している  
  
Javaでは一度も変数名にメソッドを代入していないはず(今はできる)  
C#もできる  
Javaでは使いづらいから授業で使ってない  
引数にメソッド名を使える  
voidは～～、引数の並びみたいなのが入る型がある  
  
Javaのメソッドの戻り値は少数派  
  
ちょっと前(5年ぐらい前)までは  
```let sum=function(x,y){return x+y};```  
  
letすら使ってなかった  
functionより=>のが短いから使おうみたいな流れ  
  
**()丸括弧　呼び出し演算子**  
  
Javaは宣言文だからセミコロンいらない  
JavaScriptは式だからセミコロンいる  
  
**テンプレート文字列は`(バッククォート)で囲んだ範囲に書いた文字列**のことで、この範囲内  での改行やスペースはプログラムの実行結果に反映されます。  
長い文章を変数に入れたい場合に便利な機能  
  
オブジェクト  
変数={prop1:値a,prop2:値b}  
  
キーとバリュー  
  
配列は[]直カッコ、オブジェクト作るときは{}波カッコ  
  
P145  
超重要　jsonってデータフォーマット(書き方)はほかの言語でも出てくる  
json JavaScript object format  
  
chap4-5-1.js  
これは  
```console.log(data['name']);```  
これでもOK  
```console.log(data.name);```  
  
P146  
配列にオブジェクトを入れる  
chap4-5-2.js  
  
  
JavaScriptでWebページ  
P158  
Windowオブジェクト　はブラウザそのもの  
Documentオブジェクト  
Elementオブジェクト(html＞body＞h1)  
  
DOM(DocumentObjectModel,ドム)  
  
DocumentオブジェクトはWindowオブジェクトのdocumentプロパティに入っているので、  
正式には「window.document.querySelector()」と書かなければいけません。  
しかし、「window」は省略可能なので、「document.querySelector()」と書けます  
  
プロパティはJavaでいうとフィールドみたいなもの  
  
要素の取り方はいろいろある  
今回はquerySelector  
  
htmlに```<script>```に埋め込んで書ける  
```<script>```  
```let elem=document.querySelector('p');```  
```elem.innerText='JavaScriptで書く';```  
```</script``````>```  
  
pタグの中身が書き換わる  
ソースを見ると「結果表示」ってなってるけど、動的に書き換わっている  
レンダリングの時に上から順番に見て行って変わっていく  
一番最初に書くとないからできない  
  
document.querySelector('p');  
```<p>```タグ  
document.querySelector('body p');  
みたいにCSSのような書き方(指定の仕方)ができる  
  
querySelectorは最初に見つけた1件だけ(これは単数形)  
querySelectorAllは全部(これは複数になるから戻り値は配列になるので回す必要がある)  
  
埋め込むのと別ファイルにするのをどっちも書けるようにしておく必要はある  
  
```<html lang="ja" dir="ltr">```  
日本語で左から書く  
  
JavaScriptは全部letでできちゃうから、戻ってくる型とか  
自分で型を知っておく必要がある  
  
Document.getElementById() っていうのもある  
  
## イベント
ユーザーが何かをしたタイミングでプログラムを実行するには、**「イベント」**という仕組みを利用します。  
イベントはWebページ上に置かれたボタンが押された場合などに発生します。  
イベント発生を受けて何かをするようにプログラムすれば、ユーザーの操作に反応するプログラムを作ることができます。  
  
addEventListner(アッドイベントリスナー)  
  
```変数.addEventListner('click',関数);```  
  
```変数.addEventListner('click',()=>{関数内の処理});```  
  
clickされたとき(ボタンを押したとき)に何をするか  
```btn.addEventListener('click',()=>{```  
```elem.innerText=ipt.value;```  
  
処理を止めてるわけではなくclickイベントを待ち続けてる  
  
		let func=()=>{elem.innnerText=ipt.value;};  
		btn.addEventListener('click',func);  
これでうまくうごかない  
  
letは代入できる変数  
constは再代入しないに部品に(定数)  
  
mouseover  
カーソルを乗せたら発火する  
  
```h1.style.transitionDuration='1s';```  
カーソルを乗せたらゆっくり大きくなって小さくなる  
1sって1秒  
  
  
```h1.style.fontSize='50px';```  
styleで書くときfont-sizeみたいなところはfontSizeってキャメルケースにしないといけない  
ハイフンはマイナスになってしまう  
  
基本的にaとtとeで終わるものはtorになる  
selectはselectorみたいな  
