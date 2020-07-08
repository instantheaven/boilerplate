# JavaScriptで九九の作成

  
html
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8"/>
  <title>9*9</title>
  <style>
    table{
      border-collapse:collapse;
    }
    th,td{
      border:1px solid #333;
      width:50px;
      height:50px;
      text-align:center;
    }
    th{
      background:#1cb8ec;
      color:white;
    }
  </style>
</head>
<body>
<table id="table"></table>
<script>
'use strict';
(function(){
  //table要素を取得
  const table=document.getElementById('table');
  //今回は９＊９まで（19なども入れてみよう)
  const MAX=9;
  //2重for文(外側のループは行の制御)
  for(let i=0;i<=MAX;i++){
    //tr(table row)タグを作成
    let tr=document.createElement('tr');
    //内側のループは列の制御
    for(let j=0;j<=MAX;j++){
      //子要素用の変数一つ宣言しておく
      let td;
      //最初の行か？
      if(i===0){
        //見出しにしたいのでth要素を作成する。
        td=document.createElement('th');
        if(j===0){
          //iもjも0は左上隅要素なので'X'
          td.textContent='X';
        }else{
          //最初の行のi==0以外はjを入れればよい、
          td.textContent=j;
        }
      }else{
        //列の最初の要素か?
        if(j===0){
          //最初要素ならばth
          td=document.createElement('th');
          //中身はiを入れる
          td.textContent=i;
        }else{
          //最初の要素でなければtd
          td=document.createElement('td');
          //中身はi*j
          td.textContent=i*j;
        }
      }
      //td要素をtr要素に追加
      tr.appendChild(td);
    }
    //tr要素をtable要素に追加
    table.appendChild(tr);
  }
})();
</script>
</body>
</html>
```
  
  
