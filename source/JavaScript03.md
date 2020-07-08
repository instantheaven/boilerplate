# JavaScript03
  
jsLesson1.html
```jsLesson1.html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8"/>
<title>jsレッスン</title>
</head>
<body>
<div id="result"></div>
<script>
let x=10;
let y=20;
let z=x+y;
let str="x+y="+z;
console.log(str);
const ele=document.getElementById("result");
ele.textContent=str;
</script>
</body>
</html>
```
  
「x+y=30」と表示される  
  
jsLesson2.html
```jsLesson2.html
<html>
<head>
<meta charset="UTF-8"/>
<title>jsレッスン</title>
</head>
<body>
  <input type="text" id="itAge" value="" placeholder="Enter your age">
  <button onclick="btCheck()">Check!</button>
  <div id="result"></div>
<script>
const btCheck=()=>{
    let age=document.getElementById("itAge").value;
    age=parseInt(age);
    let str;
    if(age >= 20){
        str='おとな';
    }else{
        str='こども';
    }
    document.getElementById("result").textContent=str;
};

</script>
</body>
</html>
```
  
年齢を入力すると「おとな」や「こども」と出力される  
  
jsLesson3.html
```jsLesson3.html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8"/>
<title>jsレッスン</title>
</head>
<body>
  <h1>正の整数を入力してください</h1>
  <input type="number" id="inNum" min="1" value="" placeholder="Enter a Number">
  <button onclick="btCalc()">Calc!</button>
  <div id="result"></div>
<script>
const btCalc=()=>{
    let num=document.getElementById("inNum").value;
    num=parseInt(num);
    let sum=0;
    for(let i=0;i<=num;i++){
        sum+=i;
    }
    let str='1から'+num+'までの和は'+sum+'です。';
    document.getElementById("result").textContent=str;
};
</script>
</body>
</html>
```
  
数値をいれると、１からその数値までの合計が表示される  
  
jsLesson4.html
```jsLesson4.html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8"/>
<title>jsレッスン</title>
</head>
<body>
  <h1>平均の計算</h1>
  <h2 id="data"></h2>
  <button onclick="btCalc()">Calc!</button>
  <div id="result"></div>
<script>
const nums=[10,32,18,20,40];
let str="";
let sum=0;
for(let i=0;i<nums.length;i++){
  str += nums[i]+(i==nums.length-1?"":",");
  sum += nums[i];
}
document.getElementById("data").textContent=str;
const btCalc=()=>{
    let msg="要素の平均は"+sum/nums.length+"です。";
    document.getElementById("result").textContent=msg;
};
</script>
</body>
</html>
```
  
最初に配列の要素が表示され、calcボタンを押すと要素の平均が表示され  
  
jsLesson5.html
```jsLesson5.html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8"/>
<title>jsレッスン</title>
</head>
<body>
  <h1>平均の計算</h1>
  <input type="number" id="num" value="" placeholder="数値を入力"/>
  <button onclick="add()">Add</button>
  <button onclick="btCalc()">Calc!</button>
  <div id="showArray"></div>
  <div id="result"></div>
<script>
const nums=[];
const eleNum=document.getElementById("num");
const eleShowArray=document.getElementById("showArray");
const result=document.getElementById("result");
const add=()=>{
    let num=parseInt(eleNum.value);
    nums.push(num);
    
    eleNum.value="";
    eleShowArray.textContent=nums.join(',');//配列をカンマで結合(カンマは引数省略でも可)
};

const btCalc=()=>{
    
    let sum=0;
    for(let i=0;i<nums.length;i++){
        sum+=nums[i];
    }
    let msg="要素の平均は"+sum/nums.length+"です。";
    result.textContent=msg;
}
</script>
</body>
</html>
```
  
二つの整数を入力し、演算子を選ぶと結果を表示するアプリ
```二つの整数を入力し、演算子を選ぶと結果を表示するアプリ
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
  x:<input type="number" id="num1"><br>
  y:<input type="number" id="num2"><br>
  <button onclick="calc('plus')">+</button>
  <button onclick="calc('minus')">-</button>
  <button onclick="calc('multi')">*</button>
  <button onclick="calc('div')">/</button>
  <button onclick="calc('mod')">%</button>
  <div id="result"></div>
  <script>
      const num1=document.getElementById('num1');
      const num2=document.getElementById('num2');
      const result=document.getElementById('result');
      const calc=(ope)=>{
          let n1=parseInt(num1.value);
          let n2=parseInt(num2.value);
          let str='';
          switch(ope){
              case 'plus':
                str=`${n1}+${n2}=${n1+n2}`;
              break;
              case 'minus':
                str=`${n1}-${n2}=${n1-n2}`;
              break;
              case 'multi':
                str=`${n1}*${n2}=${n1*n2}`;
              break;
              case 'div':
                str=`${n1}/${n2}=${n1/n2}`;
              break;
              case 'mod':
                str=`${n1}%${n2}=${n1%n2}`;
              break;
          }
          result.textContent=str;
      };
  </script>
</body>
</html>
```
