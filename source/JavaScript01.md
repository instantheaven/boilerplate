# Site1

```index.html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>site1</title>
		<link rel="stylesheet" href="main.css">
		<script src="main.js"></script>
	</head>
	<body>
		<input type="text" id="name" placeholder="名前"><br>
		<input type="number" id="age" placeholder="年齢"><br>
		<button id="bt">計算</button>
		<p id="result"></p>
	</body>
</html>
```
  
  
```main.js
'use strict';
window.onload=function(){
	const name=document.getElementById('name');
	const age=document.getElementById('age');
	const bt=document.getElementById('bt');
	const result=document.getElementById('result');
	bt.addEventListener('click',()=>{
		let dogName=name.value;
		let dogAge=age.value;
		console.log(typeof dogAge);
		dogAge=Number(dogAge);
		console.log(typeof dogAge);
		result.textContent=`${dogName}(${dogAge}才)は人間の年齢だと${dogAge*7}才です`;
	});
};
```
  
  
# Site2

```index.html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>site2</title>
		<link rel="stylesheet" href="main.css">
		<script src="main.js"></script>
	</head>
	<body>
		<h1>数当てゲーム!!</h1>
		<p>1から100の間の数値を当ててね!</p>
		<input type="number" id="userInput">
		<button id="bt">check</button>
		<ol id="list"></ol>
	</body>
</html>
```
  
```main.cs
h1{
	font-size:30px;
	color:blue;
}
ol{
	list-style-type:none;
}
```
  
```JavaScript
'use strict';
window.onload=function(){
	const ans=Math.floor(Math.random()*100)+1;
	const userInput=document.getElementById('userInput');
	const bt=document.getElementById('bt');
	const list=document.getElementById('list');
	let count=1;
	bt.addEventListener('click',function(){
		let li=document.createElement('li');
		let userAns=userInput.value;
		userAns=Number(userAns);
		if(userAns===ans){
			li.textContent=`${count++}回目:${userAns} 正解!!`;
		}else if(userAns > ans){
			li.textContent=`${count++}回目:${userAns} もっと下だよ`;
		}else{
			li.textContent=`${count++}回目:${userAns} もっと上だよ`;
		}
		list.appendChild(li);
	});
};
```
  
# Site3

```index.html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>site3</title>
		<link rel="stylesheet" href="main.css">
		<script src="main.js"></script>
	</head>
	<body>
		<table id="table"></table>
	</body>
</html>
```
  
```main.css
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
```
  
```main.js
'use strict';
window.onload=function(){
	const table=document.getElementById('table');
	const MAX=9;
	for(let i=0;i<=MAX;i++){
		let tr=document.createElement('tr');
		for(let j=0;j<=MAX;j++){
			let td;
			if(i===0){
				td=document.createElement('th');
				if(j===0){
					td.textContent='X';
				}else{
					td.textContent=j;
				}
			}else{
				if(j===0){
					td=document.createElement('th');
					td.textContent=i;
				}else{
					td=document.createElement('td');
					td.textContent=i*j;
				}
			}
			tr.appendChild(td);
		}
		table.appendChild(tr);
	}
};
```
  
# Site4

```HTML
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>site4</title>
		<link rel="stylesheet" href="main.css">
		<script src="main.js"></script>
	</head>
	<body>
		<h1>赤札メニュー</h1>
		<input type="text" id="name" placeholder="メニュー名"><br>
		<input type="number" id="price" placeholder="値段"><br>
		<input type="number" id="cal" placeholder="カロリー"><br>
		<button id="bt">追加</button>
		<p id="total">全0件</p>
		<table id="table">
			<tr><th>メニュー名</th><th>値段</th><th>カロリー</th></tr>
		</table>
	</body>
</html>
```
  
```main.css
table{
	border-collapse:collapse;
}
th,td{
	border:1px solid #333;
	text-align:center;
	padding:0 10px;
}
th{
	background:#1cb8ec;
	color:white;
}
```
  
```main.js
'use strict';
window.onload=function(){
	class Menu{
		constructor(name,price,cal){
			this.name=name;
			this.price=price;
			this.cal=cal;
		}
	}
	const name=document.getElementById('name');
	const price=document.getElementById('price');
	const cal=document.getElementById('cal');
	const bt=document.getElementById('bt');
	const table=document.getElementById('table');
	const total=document.getElementById('total');
	let ls=[];
	bt.addEventListener('click',()=>{
		let menu=new Menu(name.value,price.value,cal.value);
		ls.push(menu);
		let tr=document.createElement('tr');
		let td=document.createElement('td');
		td.textContent=menu.name;
		tr.appendChild(td);
		td=document.createElement('td');
		td.textContent=menu.price;
		tr.appendChild(td);
		td=document.createElement('td');
		td.textContent=menu.cal;
		tr.appendChild(td);
		table.appendChild(tr);
		total.textContent=`全${ls.length}件`;

	});
};
```
  
```別解
'use strict';
window.onload=function(){
	class Menu{
		constructor(name,price,cal){
			this.name=name;
			this.price=price;
			this.cal=cal;
		}
		showInfo(){
			return `<td>${this.name}</td><td>${this.price}</td><td>${this.cal}</td>`;
		}
	}
	const name=document.getElementById('name');
	const price=document.getElementById('price');
	const cal=document.getElementById('cal');
	const bt=document.getElementById('bt');
	const table=document.getElementById('table');
	const total=document.getElementById('total');
	let ls=[];
	bt.addEventListener('click',()=>{
		let menu=new Menu(name.value,price.value,cal.value);
		ls.push(menu);
		let tr=document.createElement('tr');
		tr.innerHTML=menu.showInfo();
		table.appendChild(tr);
		total.textContent=`全${ls.length}件`;
		//for文を使ったリストの走査(Javaとほぼ同一)
		for (let i=0;i<ls.length;i++){
			console.log(ls[i].name);
		}
		//for of を使った走査(Javaでいう拡張for)
		for (let m of ls){
			console.log(m.showInfo());
		}

	});
};
```
  
  
