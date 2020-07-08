イベント処理  
  
```jsLesson9.html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8"/>
<title>jsレッスン</title>
</head>
<body>
  <h1 id="msg">Hello</h1>
<div id="box"></div>
<script>
window.onload=function(){
  document.getElementById("msg").textContent="こんにちは、イベント！"
};
</script>
</body>
</html>
```
  
イベントハンドラ
```
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8"/>
<title>jsレッスン</title>
</head>
<body>
<button id="a">A</button>
<button id="b">B</button>
<div id="result"></div>
<script>
window.onload=function(){
  document.getElementById("a").onclick=myHandler;
  document.getElementById("b").onclick=myHandler;
};
function myHandler(e){
  document.getElementById("result").textContent=e.target.textContent + "が選ばれた";
}
</script>
</body>
</html>
```
  
イベントリスナー
```
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8"/>
<title>jsレッスン</title>
</head>
<body>
<button id="bt">click</button>
<div id="result"></div>
<script>
window.onload=function(){
  var ele=document.getElementById("bt");
  var result=document.getElementById("result");
  ele.addEventListener("click",function(){
    result.textContent="Clicked!";
  });
  ele.addEventListener("click",function(){
    window.alert("Clicked!!!");
  });
};
</script>
</body>
</html>
```
  
ファイルの分割  
html
```
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8"/>
<title>僕の猫ちゃん</title>
<link rel="stylesheet" href="css/main.css"/>
</head>
<body>
<div id="container">
<p>画像をクリックしてね</p>
<img  id="mainImage" src="images/cat1.jpg" alt="可愛い猫ちゃん" />
</div>
<script src="js/main.js"></script>
</body>
</html>
```
  
css
```
#container{
  width:80%;
  margin:0 auto;
}
img{
  display: block;
  width:80%;
}
```
  
js
```
window.onload=function(){
  var path="images/";
  var images=["cat1.jpg","cat2.jpg","cat3.jpg"];
  var index=0;
  var ele=document.getElementById("mainImage");
  ele.addEventListener("click",function(){
    this.src=path+images[++index % images.length];
  });
};
```
  
ショッピングアプリ  
数量を変更するとリアルタイムに合計価格が変わる  
  
html
```<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8"/>
<title>フルーツショッピング</title>
</head>
<body>
<table>
<tr><th>りんご(120円)</th><td><input type="number" class="fruits" value="0">個</td></tr>
<tr><th>ばなな(50円)</th><td><input type="number" class="fruits" value="0">個</td></tr>
<tr><th>ぶどう(180円)</th><td><input type="number" class="fruits" value="0">個</td></tr>
</table>
<div id="result"></div>
<script src="js/main.js"></script>
</body>
</html>
```
  
js
```
window.onload=function(){
  var prices=[120,50,180];
  var result=document.getElementById("result");
  var fruits=document.getElementsByClassName("fruits");
  for(var i=0;i<fruits.length;i++){
    fruits[i].addEventListener("change",numberChange);
    /*input type numberは現在バグがあるらしので以下二つも記述しておくとよい*/
    fruits[i].addEventListener("keyup",numberChange);
    fruits[i].addEventListener("mouseup",numberChange);
  }
  function numberChange(){
    var sum=0;
    for(var i=0;i<fruits.length;i++){
      sum+=fruits[i].value*prices[i];
    }
    result.textContent=sum+"円です！";
  }
};
```
  
別解(data属性)  
  
html
```
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8"/>
<title>フルーツショッピング</title>
</head>
<body>
<table>
<tr>
<th>りんご(120円)</th>
<td><input type="number" data-price="120" min="0"></td>
</tr>
<tr>
<th>ばなな(50円)</th>
<td><input type="number" data-price="50" min="0"></td>
</tr>
<tr>
<th>ぶどう(180円)</th>
<td><input type="number" data-price="180"></td>
</tr>
</table>
<div id="result"></div>
<script src="js/main2.js"></script>

</body>
</html>
```
  
js
```
window.onload=function(){
	var result=document.getElementById("result");
	var fruits=document.querySelectorAll('[data-price]');
	for(var i=0;i<fruits.length;i++){
		fruits[i].addEventListener("change",numberChange);
		fruits[i].addEventListener("keyup",numberChange);
    fruits[i].addEventListener("mouseup",numberChange);
	}
	function numberChange(){
		var sum=0;
		for(var i=0;i<fruits.length;i++){
			sum+=parseInt(fruits[i].getAttribute('data-price'))*fruits[i].value;
		}
		result.textContent='合計は'+sum+'円です';
		//console.dir(fruits[0]);
	}
}
```
  
参照及び引用元 [ジョイタスネット](https://joytas.net/programming/website/website09)
