# JavaScript00
### ちょっとしたHTML・CSS・JS
エンジンかかるまで  
**復習**  
JSフォルダ、site1フォルダ作成  
その中にindex.html作成  
htmlを書いていく  
vimの復讐もしつつ  
  
**vim**  
```:tabe main.css```  
でタブで作れる  
G、Tでタブ移動  
  
**CSS**でpタグを装飾  
**HTML**にもmain.cssを読み込む記述を書き加え  
  
上から順じゃなく、開いたら閉じて、中に書いていく  
  
pタグにidを付与  
  
```window.onload=function(){```  
```	const msg=document.getElementById('msg');```  
```	msg.textContent='world';```  
```};```  
  
**関数**  
読み込み終わったら走る  
```const```は定数(Javaなら```final```)  
再代入する予定がないものは定数にすると良い  
```getElementById('msg');```  
で取得して```id```　```msg```をいじれるようになる  
```msg```は住所を持ってる  
worldを書き換えるのは大丈夫  
  
**DOM(ドム)**  
ドキュメントオブジェクトモデル  
  
```<p id="msg">Hello</p>```の```Hello```が```textContent```  
  
  

```<link rel="stylesheet" href="main.css">```  
  
ファイルの読み込みの違いとか  
```<script src="main.js"></script>```  
  
```rel(リレーション)```と```src(ソース)```  
  
```<script>```は閉じタグがいる  
  
```window.onload```は上から読み込み終わったら  
  

クリックしたら変更するように変更  
  
```msg.addEventListener```  
イベントが来るかを聞いてる  
来たらどうするかを第二引数に書ける  
  
```msg.addEventListener('click',()=>{```  
```		msg.textContent='World';```  
ラムダ式、アロー演算子  
クリックしたらWorldに変わる  
  
```var```と```let```の違いはスコープの違い  
変数の有効範囲  
スコープの範囲が少ない方がいい  
  

### わんこの年齢を人間年齢に計算する
  
入力欄2つ  
犬の名前と年齢を入れると  
計算をクリックすると  
人間換算の年齢が計算される  
  
入力欄は```<input>```  
```placeholder```で入力欄に予め文字  
  
```<input>```はインライン要素だから改行しない  
  
  
```const name=document.getElementById('name');```  
```const age=document.getElementById('age');```  
```const bt=document.getElementById('bt');```  
```const result=document.getElementById('result');```  
  
4つの**DOM**を取得  
  
計算ボタンをクリックしたら計算する  
  
```let dogName=name.value;```  
ユーザーがフォームに入れた情報をvalueが知ってる  
valueプロパティ  
  
```console.log()```は```System.out.print()```と同じ  
  
```let dogAge=age.value;```  
```console.log(typeof dogAge);```  
typeofで型がわかる  
この時点ではString型のはず  
```dogAge=Number(dogAge);```  
これで数値に変換  
```parseInt```とは全く同じということではない  
  
テンプレートリテラルを使うためにバックコート  
＄で変数を埋め込める  
**JSP**だったら  
```<%= %>```  
  
```
result.textContent=`  {dogName}(  {dogAge}才)は人間の年齢だと  {dogAge*7}才です`;
```
  
**JS**は文字と数字を掛け算できる  
**python**だと文字に掛け算すると文字が数分並んじゃう  
  

### 数当てゲーム
**ターミナル**  
```cp -r site1 site2```でコピー  
  
**vim**  
```d+i+{```  
デリート　インナー　波かっこ　で波かっこの中を削除  
  
１〜１００の数字  
```const ans=Math.floor(Math.random()*100)+1;```  
そのままだと0.000~99.9999だからfloorで小数点以下落として、0~99になってプラス1で1~100  
  
５〜１０の場合  
5,6,7,8,9,10で６つ  
```const ans=Math.floor(Math.random()*6)+5```  
  
−１０~１０の場合  
21  
  
正解と下と上の３パターンなので  
ifとelse ifとelseで判定  
  
履歴が残るように改良  
```<ol>```で残していく  
  
```let li=document.createElement('li');```  
でリストを作って  
判定抜けた後  
```list.appendChild(li);```  
で子要素を追加していく  
  
**CSS**で  
```ol{```  
```	list-style-type:none;```  
```}```  
  
で、1.　とかが消える  
  
JSでカウント変数を用意する  
  


### [午後のJS（九九表作成)](https://github.com/instantheaven/boilerplate/blob/master/source/JavaScript_kuku.md)

またsite2をコピーしてsite3を作って移動してindex.htmlを開く  
  
**CSS**  
```border-collapse:collapse;```  
二重線にならないように  
th,tdが重なったボーダーが二重線になる  
  
```border:1px solid #333;```  
borderで一括指定してる  
  
スコープを作ってる  
functionでスコープを作るぐらいしかない  
（）は実行演算子  
functionを作ってすぐに実行  
```(function(){```  
```  ここに処理を記述```  
```})();```  
  
**vim**  
Mac  
```:! open ファイル名```  
  
表を作れるようにはしておくこと  
二重for文  

### 赤札のメニュー
赤札のメニューと値段とカロリーを適当に入れてもらって、  
最後にテーブルでリストを表示する  
  
クラス  
クラスを使ってJSでオブジェクトを作る  
骨組みはv
* フィールド
* コンストラクタ
* メソッド
  
```class Menu{```  
```  constructor(name,price,cal){```  
```this.name=name;```  
```this.price=price;```  
```this.cal=cal;```  
	```}```  
```}```  
  
型がなくてもJSなら問題ない  
thisが兼ねてる  
  
空っぽの配列  
```let ls=[];```  
配列(リスト)への追加は  
```push```  
Javaは```add```  
Pythonは```append```  
  
インスタンスを作るのはnewつけてクラス名  
