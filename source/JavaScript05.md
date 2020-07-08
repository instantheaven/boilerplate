## クラス構文
JavaScriptはフィールドの概念がない  
  
jsLesson7.html  
Javaだと引数が2つのコンストラクタがない状態で暗黙のコンストラクタだけで引数が2つのコンストラクタを定義していないとエラーになるけど、  
JavaScriptはコンストラクタも継承できるからコンストラクタなにも書かなくてもエラーにならない  
  
onclickで関数を呼び出せる  
  
グローバルスコープ  
  
console.dir(ele);で見ると上みたいにずらっとあるのが見える  
タグはみんなこんな風に情報をいっぱい持ってる  
この事実を知っておくのはあり  
大事なのはこの中の部分部分をちょこちょこ上書きさせてもらってるってこと  

---


**[Webサイト制作-9日目(JavaScript)](https://github.com/instantheaven/boilerplate/blob/master/source/JavaScript06.md)**  
jsLesson11.html  
  
onloadプロパティ  
文章を全部読み込み終わった後に走る  
最後まで読み込んでいって途中ファンクションあったからあとでやろって感じ  
グローバル空間を汚したくない  
スコープは短いほうがいい  
実際はscriptの中につらつら書かない  
他のファイルに影響を与えないように閉じ込めておく  
  
jsLesson12.html  
ハンドラ  
扱う  
  
イベントハンドラ  
イベント扱うこと  
  
myHandler(event)  
eは仮引数  
サーブレットの時のrequestとかresponceにデータが入ってきたのと同じ  
ここで発生したイベントを全部知っているイベントオブジェクトが入ってくる  
  
function(ファンクション)は関数  
  

Lesson12フォルダ  
functionとアロー関数は完全に一致ではない  
thisが指す先が違う  
  
src(ソース)属性を書き換える  
  
++index % images.length  
循環する仕組み  
最初indexは0  
  
クラスとるなら  
getElementsByClassName  
