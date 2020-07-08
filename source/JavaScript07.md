jsLesson14.html  
  
```let li=document.createElement('li');```  
メモリ上に作ってる  
```ol.appendChild(li);```  
で、メモリ上にあった**li**をHTMLに書き出す  
  
DOMは簡単にいうとタグのこと  
  
textContentはdivタグの中の中身とかそういうの  
  
href えいちれふ  
  
トグルとは、ある同一の操作をすることで、2つの機能を切り替えられるスイッチ機構のことである。  
ついてたらつけてくれて、ついてたらはずしてくれる挙動(クラスとか)  
トグルスイッチとか言ったりする  

  

panelpazzle.html  

```
td.empty{
    background-color:#eee;
    border-color:#eee;
  }
```
あるんだけど、背景と同じにしているから見えない  
  
td.ok td要素でなおかつクラスokがついてる場合  
  
```#startBt:hover```　idがstartBtでカーソルが乗っかったら  
  
opacityで透明度変えると簡単にボタンっぽい挙動に出来る  
  
tableを空で作っておく  
  
'use strict'; 厳格モード  
普通のJSだとエラーじゃないエラーを教えてくれる  
変数宣言していない変数を使おうとしたときとか  
Javaに近づく挙動  
  
size=4; は、4行4列のテーブル  
  
これは完成状態からシャッフルしてるから、解けないシャッフルにはならない  
出来ない組み合わせはない  
  
```shuffleCount=size*1000;```  
サイズ変えた時に対応できるようにsizeにかけてる  
実際には4000回じゃなくて4分の1ぐらいしかシャッフルされてないような感じになる？  
  
```table.textContent=null;```  
nullを突っ込めばtableの要素が空っぽになる  
  
2重for文は  
最初が行、次が列  
td要素にオリジナルのプロパティindexをつけてやろう  
```var index=i*size+j;```  
０～１５  
  
```td.textContent=index==size*size-1 ? "":index+1;```  
１５なら入れる数字がないから空文字  
  
```td.onclick=click;```  
onclick要素にclickって関数を付けましょう  
  
```tr.appendChild(td);```  
この時点ではまだメモリ上のtr  
```table.appendChild(tr);```  
tableは実際にあるDOMだからtrが追加される  
  
```
function shuffle(shuffleCount){
    for(let i=0;i<shuffleCount;i++){
    click({target:{posId:Math.floor(Math.random()*size*size)}});
    }
    isShuffled=true;
    }
```
  
波カッコはオブジェクト  
targetってラベルを持ったオブジェクト  
floorは床だから切り捨て計算  
  
```function click(e){```  
```var pos=e.target.posId;```  
eはイベント全体  
イベントを元にわかる  
もしくは上のオブジェクト  
targetでどのボタンがクリックされたかDOMが取得されて、posIdでどの番号かがわかる  
  
そのあとのif文は空白と接しているか(動かせるか)  
一番上の場合、上を見る必要がない  
上のtextContentは空きスペースですか  
空きスペースなら今クリックされたものと入れ替え作業をしましょう  
  
一番下の場合、下を見る必要がない  
右を見る場合は右の行じゃないかどうか  
(pos+1)%size  
  

swap 2値の入れ替え  
クリックされた方のp1 textContentを取り出して  
  
クリックしたところは空白になるからadd('empty')  
  
checkは全体がどうなっているかをチェック  
配列のlength文チェック  
okってつけると枠線が緑に  
そうじゃなければ緑の枠を外そう  
```if(isShuffled && okCount===size*size-1){```  
```msgBox.textContent="Complete!";```  
```}```  
isShuffledがあるのは一番最初のシャッフル前にcompleteが出てしまわないように  

